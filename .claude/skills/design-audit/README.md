# Design Implementation Audit Skill

A Claude Code skill that compares an approved UI/UX design screenshot against an implemented application screenshot, identifies all meaningful mismatches, and produces a structured QA audit report with ready-to-log bug reports.

---

## How to Activate

Use any of the following:

```
/design-audit
Run DESIGN_IMPLEMENTATION_AUDIT
design audit
compare design with implementation
review UI against Figma
audit implemented screen
check screen against design
```

---

## Required Inputs

| # | Input | Description |
|---|-------|-------------|
| 1 | `design_screenshot` | Approved design image from Figma, Adobe XD, Zeplin, or any design tool |
| 2 | `implementation_screenshot` | Actual screenshot of the implemented screen |
| 3 | `screen_name` | Human-readable name for the screen (e.g., "Create Committee Form") |
| 4 | `platform` | Web / Mobile / Tablet |
| 5 | `ui_state` | Optional — Default, Error, Loading, Empty, Disabled, etc. |

### Example Prompt

```
/design-audit

Screen name: Create Committee Form
Design screenshot: [attach design.png]
Implementation screenshot: [attach implementation.png]
Platform: Web
State: Default
```

---

## What Gets Checked

- Layout & structure
- Spacing & alignment
- Missing or extra elements
- Text & labels (wording, casing, placeholders)
- Colors (backgrounds, text, borders, state colors)
- Typography (size, weight, casing)
- Icons (presence, size, color)
- Interactive components (buttons, inputs, dropdowns, checkboxes, tabs)
- Data display components (tables, cards, lists)
- Modals & overlays
- UI states (default, error, loading, empty, disabled, success)
- Responsive behavior
- Accessibility indicators

---

## Severity Scale

| Severity | Description |
|----------|-------------|
| **Critical** | Blocks the user from completing the flow |
| **High** | Important element missing, misleading, or affects business logic |
| **Medium** | Noticeable mismatch affecting usability — user can still complete task |
| **Low** | Minor cosmetic mismatch |
| **Info** | Recommendation or needs designer confirmation |

---

## Match Score

| Score | Rating |
|-------|--------|
| 90–100% | Excellent |
| 75–89% | Good |
| 60–74% | Fair |
| < 60% | Poor |

Deductions: Critical −15 · High −8 · Medium −4 · Low −1 · Info 0

---

## Report Output

Every audit produces:

1. **Audit Summary** — screen name, platform, score, and overall recommendation
2. **Findings by Severity** — count table
3. **Detailed Findings** — full findings table with Expected vs Actual for every issue
4. **Ready-to-Log Bug Reports** — one structured bug report per Critical/High finding
5. **Final QA Recommendation** — Pass / Pass with Minor Issues / Needs Fixes / Blocked

---

## Verdict Legend

| Verdict | Meaning |
|---------|---------|
| ✅ Pass | No meaningful mismatches |
| ⚠️ Pass with Minor Issues | Only Low/Info findings — safe to ship |
| 🔶 Needs Fixes | Medium or High findings — fix before release |
| 🚫 Blocked | Critical findings — must resolve before any release |
