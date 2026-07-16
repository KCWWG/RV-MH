# MH & RV Park Buy Box

An interactive, single-file investment-screening dashboard for **manufactured-housing communities (MHC) and RV parks**, calibrated to the *Texas-Focused MHC & RV Park Investment Thesis* (Chandler, Jul 2026). Every deal in the pipeline is scored on a deterministic engine, mapped to Texas, and linked to its source Offering Memorandum — click a deal and the OM opens.

## Structure

```
mh-rv-buybox/
├── index.html                                    the dashboard (open this)
├── README.md
└── OM/                                           Offering Memoranda, loaded by relative path
    ├── Offering Memorandum - Texas Portfolio (1) (1).pdf
    ├── South Texas - Two Park Portfolio - OM.pdf
    ├── Water Tower RV Park - OM.pdf
    ├── Copper Ridge RV Park OM.pdf
    ├── Sugar Hill RV Resort  OM.pdf
    └── Village RV Park - OM.pdf
```

The **investment thesis PDF is embedded inside `index.html`**, so the *View Full Investment Thesis* button works even though the thesis is not a file in `OM/`.

`index.html` is self-contained (fonts, styles, scoring engine, and map are all inline). The only external references are the PDFs in `OM/`, which it loads by relative path (the thesis is embedded).

## Opening a deal's OM

Each deal is clickable in three places — the pipeline map pins, the priority cards, and the full ranking table. Clicking opens a scorecard modal with two buttons:

- **View Full OM** embeds the document inline in the modal (toggles open/closed).
- **Open in new tab** opens the PDF in its own browser tab.

The **Governing Thesis** section (and the Sources footnotes) also carry a **View Full Investment Thesis** button that opens the embedded thesis the same way.

## Running it

**GitHub Pages (recommended).** Push the repo, then enable Pages (Settings → Pages → deploy from branch, root). Both the inline OM viewer and the new-tab button work over `https://`.

**Locally.** Open `index.html` in a browser. The **Open in new tab** button is the most reliable way to view an OM under the `file://` protocol; some browsers restrict inline PDF iframes locally, so if the embedded viewer is blank, use that button. Serving the folder (e.g. `python3 -m http.server`) makes the inline viewer work locally too.

## About the OM files

`index.html` points at the `OM/` folder using each document's **exact filename** (see `OM_FILE` near the top of the script). Filenames with spaces and parentheses are fine — they're URL-encoded automatically. If your folder is named something other than `OM/`, change the single `OM_DIR` line at the top of that block.

The PDFs shipped in this zip are **compressed copies** (rasterized ~105 DPI, ~2.5–5 MB each) so the repo stays light. To use full-resolution originals, drop them into `OM/` **using the same filenames** — no code changes needed. Brokers: Marcus & Millichap (five single-asset deals) and Sunstone Real Estate Advisors (the RGV portfolio).

## Scoring & thesis calibration

Each park carries two 1–10 scores — **Asset** (utilities, market, scale, land) and **Operations** (home mix, occupancy, rent-to-market, expense, bill-back) — blended 60/40 into a composite that drives a tier, a recommended cap band, and a GO / CAUTION / NO-GO call. Hard structural gates (unverifiable wastewater with no city path, floodway, non-conforming zoning, predominantly park-owned inventory, sub-scale, extraction-dependent underwriting in rent-capped markets) kill a deal regardless of price.

Calibrated to the thesis, the engine also applies:

- **Size bands** — MHC 75–300 pads, RV 80–250 sites.
- **DSCR floors** — 1.35× MHC, 1.40× RV (shown against broker going-in DSCR where disclosed).
- A non-gating **Thesis Fit** read per deal — flags sub-scale, RV occupancy below the 60% floor, park-owned share over 25%, large rent gaps, private-wastewater verification, and single-driver RV demand.
- A live **70/30 allocation tracker** measuring the pipeline (MHC vs RV by committed equity) against the mandate.

Use the **Live Thesis Controls** to change the blend and factor weights (or pick a preset); every score, decision, map pin, and the allocation tracker recompute instantly.

## Notes

Figures are transcribed from the OMs; assumed inputs (rent gaps, undisclosed expense ratios) are flagged in each deal's notes and must be confirmed against the actual rent roll and T12 in diligence. Not investment advice — verify every input independently.
