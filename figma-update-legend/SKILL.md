# figma-update-legend

Update the status of an existing Figma annotation legend. Use when the user says "update the annotation legend", "update legend status", provides a Figma URL to mark findings as done, decided, open, or deferred, or runs `/figma-update-legend`.

**Statuses:** 🔴 OPEN HIGH · 🟡 OPEN MED · ⚪ OPEN LOW · ✅ DONE · 🔘 DECIDED · ⏳ DEFERRED

---

## Workflow

### Step 1 — Load the figma-use skill

Before any `use_figma` call, load the `figma:figma-use` skill and follow its rules.

Parse `fileKey` and `nodeId` from the Figma URL:
- `fileKey` — segment between `/design/` and the next `/`
- `nodeId` — value of the `node-id` query param, replacing `-` with `:`

---

### Step 2 — Get current state (two calls in parallel)

**Call A — screenshot:** Call `get_screenshot` on the `nodeId` to see the current design.

**Call B — read legend text:**
```js
for (const pg of figma.root.children) {
  await figma.setCurrentPageAsync(pg);
  const target = figma.currentPage.findOne(n => n.id === "NODE_ID_HERE");
  if (!target) continue;
  const legend = target.parent.findOne(n => n.name === "🔍 Annotation Legend");
  if (legend) {
    const textNode = legend.type === "TEXT" ? legend : legend.findOne(n => n.type === "TEXT");
    if (textNode) return { legendText: textNode.characters, legendId: legend.id };
  }
  break;
}
return { legendText: null };
```

---

### Step 3 — Parse findings and present to user

Extract each numbered finding from the legend text. Original format:
```
N  Finding label — detail sentence
   → Principle Name
   ✦ Suggestion sentence
```

Also read the original priority of each finding (HIGH/MEDIUM/LOW) from the legend's section headers if present, or infer from the marker colour.

Show a compact list to the user and suggest statuses based on what you see in the screenshot. Mark uncertain ones as OPEN with current priority. Wait for confirmation before rebuilding.

---

### Step 4 — Rebuild the legend

Delete the old `🔍 Annotation Legend` node and create a new one.

**Legend structure — findings grouped by priority, in original finding-number order within each group:**
```
Design Review — [frame title]
N findings · N done · N decided · N open high · N open med · N open low · N deferred

HIGH

🔘  [DECIDED]  1  Finding label — detail
   → Principle
   ✦ Suggestion

✅  [DONE]  2  Finding label — detail
   → Principle
   ✦ Suggestion

🔴  [OPEN HIGH]  3  Finding label — detail
   → Principle
   ✦ Suggestion

MEDIUM

🟡  [OPEN MED]  4  Finding label — detail
   → Principle
   ✦ Suggestion

⏳  [DEFERRED]  5  Finding label — detail
   → Principle
   ✦ Suggestion
   ↳ Note in amber gold

LOW

⚪  [OPEN LOW]  6  Finding label — detail
   → Principle
   ✦ Suggestion
```

**Code pattern — range tracking:**
```js
const badgeRanges    = []; // [s, e, status] — icon + [STATUS] + spaces
const titleRanges    = []; // [s, e, status] — num + label + detail
const principleRanges = []; // [s, e, status]
const suggestionRanges = []; // [s, e, status]
const noteRanges     = []; // [s, e] — DEFERRED ↳ note lines

// Per finding:
const badgeText = `${icon}  [${statusLabel}]  `;
const bStart = content.length; content += badgeText;
badgeRanges.push([bStart, content.length, f.status]);

const tStart = content.length;
content += `${f.num}  ${f.label} — ${f.detail}\n`;
titleRanges.push([tStart, content.length, f.status]);

const pStart = content.length;
content += `   → ${f.principle}\n`;
principleRanges.push([pStart, content.length, f.status]);

const sStart = content.length;
content += `   ✦ ${f.suggestion}\n`;
suggestionRanges.push([sStart, content.length, f.status]);

if (f.status === "DEFERRED" && f.note) {
  const nStart = content.length;
  content += `   ↳ ${f.note}\n`;
  noteRanges.push([nStart, content.length]);
}
```

**Styling rules:**

| Part | OPEN | DONE | DECIDED | DEFERRED |
|------|------|------|---------|----------|
| Badge `icon [STATUS]` | status colour + bold | green + bold | slate blue + bold | purple + bold |
| Title `num  label` | lavender (base) | muted grey + strikethrough | muted grey + strikethrough | lavender (base) |
| `→ Principle` | muted blue | muted grey + strikethrough | muted grey + strikethrough | muted blue |
| `✦ Suggestion` | warm amber | muted grey + strikethrough | muted grey + strikethrough | warm amber |
| `↳ Note` | — | — | — | amber gold |

**Key rule: badge only gets the status colour. The title text (num + label + detail) stays at the base lavender colour for all OPEN and DEFERRED items.**

```js
// Base text colour = lavender {r:0.85, g:0.85, b:0.95}
// Set this as the default fill on the text node before applying ranges.

// ALL badges — status colour + Bold (badge range only, not the title)
for (let i = 0; i < badgeRanges.length; i++) {
  const [bs, be, status] = badgeRanges[i];
  t.setRangeFills(bs, be, [{ type: "SOLID", color: statusColor[status] }]);
  t.setRangeFontName(bs, be, { family: "Inter", style: "Bold" });
}

// Principle lines — muted blue (OPEN and DEFERRED)
for (const [s, e, status] of principleRanges) {
  if (status !== "DONE" && status !== "DECIDED") {
    t.setRangeFills(s, e, [{ type: "SOLID", color: { r:0.45, g:0.62, b:0.88 } }]);
  }
}

// Suggestion lines — warm amber (OPEN and DEFERRED)
for (const [s, e, status] of suggestionRanges) {
  if (status !== "DONE" && status !== "DECIDED") {
    t.setRangeFills(s, e, [{ type: "SOLID", color: { r:1.00, g:0.88, b:0.60 } }]);
  }
}

// DEFERRED note — amber gold
for (const [s, e] of noteRanges) {
  t.setRangeFills(s, e, [{ type: "SOLID", color: { r:0.85, g:0.70, b:0.40 } }]);
}

// DONE + DECIDED — content becomes muted grey + strikethrough
// (Badges already coloured correctly above)
const muted = [{ type: "SOLID", color: { r:0.40, g:0.40, b:0.50 } }];
for (let i = 0; i < badgeRanges.length; i++) {
  const [bs, be, status] = badgeRanges[i];
  const [ts, te] = titleRanges[i];
  const [ps, pe] = principleRanges[i];
  const [sgs, sge] = suggestionRanges[i];
  if (status === "DONE" || status === "DECIDED") {
    t.setRangeFills(ts, te, muted); t.setRangeTextDecoration(ts, te, "STRIKETHROUGH");
    t.setRangeFills(ps, pe, muted); t.setRangeTextDecoration(ps, pe, "STRIKETHROUGH");
    t.setRangeFills(sgs, sge, muted); t.setRangeTextDecoration(sgs, sge, "STRIKETHROUGH");
  }
}
```

**Updated subtitle counts:**
```js
let subtitle = `${total} findings`;
if (nDone)     subtitle += ` · ${nDone} done`;
if (nDecided)  subtitle += ` · ${nDecided} decided`;
if (nHigh)     subtitle += ` · ${nHigh} open high`;
if (nMed)      subtitle += ` · ${nMed} open med`;
if (nLow)      subtitle += ` · ${nLow} open low`;
if (nDeferred) subtitle += ` · ${nDeferred} deferred`;
```

---

### Colour reference (exact values from reference design)

**Frame:**
| Element | Colour |
|---------|--------|
| Background | `{r:0.07, g:0.07, b:0.12}` dark navy |
| Title "Design Review —" | `{r:1.00, g:1.00, b:1.00}` white + Bold |
| Subtitle + base text | `{r:0.85, g:0.85, b:0.95}` lavender |
| Section headers HIGH/MEDIUM/LOW | `{r:1.00, g:1.00, b:1.00}` white + Bold |

**Badge colours (icon + [STATUS] only):**
| Status    | Icon | Badge colour |
|-----------|------|-------------|
| DONE      | ✅   | `{r:0.38, g:0.66, b:0.46}` green |
| DECIDED   | 🔘   | `{r:0.52, g:0.56, b:0.72}` slate blue |
| OPEN HIGH | 🔴   | `{r:0.76, g:0.36, b:0.36}` muted red |
| OPEN MED  | 🟡   | `{r:0.80, g:0.58, b:0.34}` warm brown |
| OPEN LOW  | ⚪   | `{r:0.52, g:0.52, b:0.62}` slate grey-blue |
| DEFERRED  | ⏳   | `{r:0.62, g:0.48, b:0.80}` purple |

**Content colours:**
| Part | Colour | Strikethrough |
|------|--------|---------------|
| Title `num  label — detail` (all statuses) | `{r:0.85, g:0.85, b:0.95}` lavender | If DONE/DECIDED → muted grey |
| `→ Principle` | `{r:0.45, g:0.62, b:0.88}` muted blue | If DONE/DECIDED → muted grey |
| `✦ Suggestion` | `{r:1.00, g:0.88, b:0.60}` warm amber | If DONE/DECIDED → muted grey |
| `↳ Note` (DEFERRED) | `{r:0.85, g:0.70, b:0.40}` amber gold | No |
| DONE/DECIDED content | `{r:0.40, g:0.40, b:0.50}` muted grey | Yes |

**Font:** Inter, 13px, line-height 20px. All text base Regular; badges Bold; section headers and title header Bold.

---

### Step 5 — Verify

Call `get_screenshot` on the legend node ID. Confirm:
- Title "Design Review —" is white Bold; subtitle is lavender
- Section headers (HIGH/MEDIUM/LOW) white Bold
- DONE badges green, DECIDED badges slate blue — neither has strikethrough on the badge
- DONE/DECIDED content (title, principle, suggestion) is muted grey with strikethrough
- OPEN item badges in their status colour (muted red/brown/slate); title text is lavender
- Principles muted blue, suggestions warm amber
- Amber gold `↳` note for DEFERRED items
- Subtitle counts are correct
