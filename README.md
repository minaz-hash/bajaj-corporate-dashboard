# Bajaj Corporate — Dashboard (Overview)

A React + Tailwind rebuild of the L&T / Bajaj Allianz corporate insurance overview
screen, restyled against the Bajaj design system (`design.md`).

## Run it

**No build step required.** Just open `index.html` in any modern browser — it loads
React, Tailwind and the fonts from CDNs and renders immediately.

To serve it over `http://localhost` (e.g. for the in-IDE preview), a tiny dependency-free
static server is included (no Node/Python needed):

```powershell
powershell -ExecutionPolicy Bypass -File serve.ps1   # → http://localhost:8080
```

## What changed vs. the Figma screen (the client's "it's cluttered" note)

The brief: **keep the visual treatment, lose the clutter.** What was kept and what was calmed:

**Kept (the visual DNA):** Bajaj blue brand bar, soft blue page wash, rounded card system,
the isometric 3D building motif, the floating policy/shield chips, the Bajaj AI assistant.

**Decluttered:**
| Original | Change |
|---|---|
| Two overlapping stat layers (4 top KPIs **and** 4 property stats competing for attention) | Top KPIs = **portfolio-wide**; the in-card tiles = **per-line-of-business**. Clear, non-duplicating hierarchy. |
| Giant 3D illustration as the page hero, pushing data to the margins | Shrunk to a **supporting accent** in its own band. Data leads; illustration supports. |
| Free-floating callout tags ("Fire Insurance", "Property Insurance") over the art | Removed; replaced by one inline **"Fully insured"** badge + a slim expiry banner. |
| Left icon rail + heavy gradients + many focal points | Single clean **F-pattern**: nav → greeting/search → KPI row → portfolio (primary) + actions/AI (secondary). More whitespace, one accent. |
| Mixed search bars / dense header | One calm search, generous spacing on the `00–17` token scale. |

## Design-system fidelity (`design.md`)

- **Colors** — CSS variables in `<style>` are a 1:1 transliteration of the Figma tokens
  (§13). Tailwind maps to them (§12): `bg-brand`, `text-fg-subtle`, `border-line`, etc.
- **Type** — Familjen Grotesk for titles/KPI numbers (`font-title`), Rubik for UI
  (`font-sans`); scale `t1…b3` per §9. Default UI text = Body 2 (14/20).
- **Spacing** — the `00–17` 4px scale (§8). **Radius** uses the assumed scale (§11,
  no DS token): cards `2xl/xl`, inputs/buttons `lg/md`, chips `full`.
- **Shadows** — `xs/sm/md` and the `focus` ring from §10. Focus outlines are preserved.
- **Status/accents** — badges always pair colour **+ text + icon** (a11y, §7).

## Structure

Single-file app (`index.html`) organised into clear components:
`TopNav · PageHeader · ExpiryBanner · KpiCard · PortfolioCard (Donut + StatTile + BuildingArt) · QuickActions · Assistant`.
Mock data lives at the top of the script (`KPIS`, `LOBS`, `PORTFOLIO`, `AI_PROMPTS`).

### Porting to a Vite project (when Node is available)

1. `npm create vite@latest bajaj-dashboard -- --template react-ts`
2. Install Tailwind v3; drop the `<style>` token block into `src/styles/tokens.css`
   and the inline `tailwind.config` object into `tailwind.config.js` (both already
   match `design.md` §12–13).
3. Move each component into `src/components/*.tsx`; the JSX transfers as-is.

## Notes
- `[ASSUMPTION]` — corner radii (no DS radius token, §11) and the claim-status→accent
  mapping (§7) follow `design.md`'s suggested values; confirm with Bajaj.
- All figures are demo data.
