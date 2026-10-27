# Li-ion cell test calculator (18650 / 21700)

<p>
  <a href="https://technikweber.github.io/liion-cell-calculator/"><img alt="Live demo" src="https://img.shields.io/badge/live%20demo-open-brightgreen"></a>
  <img alt="Single HTML file, offline" src="https://img.shields.io/badge/single%20HTML%20file-offline-blue">
  <img alt="UI language: German" src="https://img.shields.io/badge/UI-Deutsch-informational">
  <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-green"></a>
</p>

A self-contained HTML tool for planning, evaluating and sanity-checking tests on
cylindrical lithium-ion cells (18650, 21700) of the common chemistries NMC, NCA and LFP.
One file, nothing to install, runs offline in any modern browser.

👉 **[Open the calculator](https://technikweber.github.io/liion-cell-calculator/)**

## Background

Lithium-ion cells age fundamentally differently from lead-acid batteries:

- Life roughly halves for every **10 °C** above 25 °C (Battery University), not every 7 °C
  as with lead-acid.
- In the **cold**, Li-ion cells age *faster* through lithium plating, not slower — the rule
  of thumb only applies to elevated temperatures.
- Instead of plain depth of discharge (DoD), the **SoC window** used determines the life
  (10–90 % is much gentler than 0–100 %).
- Charging uses **CC-CV** to a fixed end voltage (4.2 V NMC/NCA, 3.65 V LFP) — *without*
  temperature compensation as with lead-acid.

So whoever tests Li-ion cells cannot take over the tools of a lead-acid calculator one to
one. This tool is tailored to the Li-ion reality.

## What it does

Seven modules; choose the chemistry at the top (it sets the voltage window and defaults):

- **▶ Temp → cycles** — convert cycles at 25 °C to another temperature (with a cold warning
  below ~15 °C).
- **◀ Backward** — convert test cycles at elevated temperature back to the 25 °C equivalent.
- **▭ SoC window** — effect of a narrower charge window (window width + upper limit).
- **⏱ Test duration** — cycles × time per cycle + utilisation → test duration; with the time
  saved by the test temperature. Warns above 45 °C, where ageing mechanisms shift.
- **⚡ CC-CV charging** — charge current and rough charge time from capacity (mAh) and
  C-rate; end voltage per chemistry.
- **↻ C-rate** — conversion between mAh, C-rate, current and duration in Li-ion convention.
- **▤ Limits** — reference table: end, nominal and cut-off voltage, storage SoC, charge rate
  per chemistry.

## How to use it

Open the [live version](https://technikweber.github.io/liion-cell-calculator/), or download
`index.html` and open it in a browser (double-click is enough). Choose the chemistry at the
top, open a tab, calculate.

All inputs are evaluated live. Every module shows the calculation and a range, so that it
stays visible that these are approximations. The interface is in German.

## Formula sources

| Module | Source / constant |
|---|---|
| Temperature rule of thumb | `0.5^((T−25)/10)` — Battery University, Arrhenius simplification for Li-ion |
| CC-CV charging | Standard Li-ion charging method; end voltage 4.2 V (NMC/NCA) or 3.65 V (LFP) |
| C-rate | current = C-rate × capacity, duration = 1/C-rate |
| SoC window model | Heuristic: window width and upper limit as separate factors — rough order of magnitude |
| Limits | Typical data sheet values of cylindrical cells (vary slightly by manufacturer) |

## Safety notes

- **Overcharging** beyond the end voltage or **deep discharge** below the cut-off damages
  cells irreversibly and can lead to thermal runaway.
- Avoid charging **below 0 °C** — risk of lithium plating.
- Cells keep best when stored at **~40–50 % SoC** (≈ 3.7 V for NMC).
- Accelerated ageing above **~45 °C** is no longer representative of real operation —
  ageing mechanisms shift.

## Limitations

- Rules of thumb and approximations — not suitable for safety or certification statements.
- Values apply to cylindrical Li-ion cells (NMC/NCA/LFP) and vary considerably by
  manufacturer.
- Pouch and prismatic cells are not covered explicitly, but most formulas carry over.
- For a relative comparison of several cells under identical conditions, no conversion is
  needed — the tool does not replace a test, it puts results into context.
- For lead-acid batteries see the sister tool
  [lead-battery-calculator](https://github.com/TechnikWeber/lead-battery-calculator).

## Technology

- One HTML file (~20 KB)
- Vanilla JavaScript, no build, no dependencies
- No tracking, no external calls — runs fully offline

## License

[MIT](LICENSE). Use at your own risk; the tool does not replace a professional review.
