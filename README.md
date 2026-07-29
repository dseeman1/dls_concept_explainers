# DLS Explainer Suite

Built by **Daniel P. Seeman, Ph.D.** — [about.me/danielseeman](https://about.me/danielseeman)

A set of self-contained, interactive web pages that illustrate the physics of
Dynamic Light Scattering (DLS). Each page isolates a single variable and shows,
in real time, how that variable affects the scattered-light intensity history
and the resulting intensity autocorrelation function (ACF).

The suite is styled in Brookhaven Instruments branding and is intended as an
educational / explanatory tool.

## The pages

| File | Variable demonstrated |
|------|----------------------|
| `dls-explainer-big-small-particles.html` | Particle hydrodynamic diameter (0.5 nm to 1 um) |
| `dls-explainer-delay-times.html` | Correlator layout: first and last delay times; particle diameter is also editable |
| `dls-explainer-angle-bi200sm.html` | Scattering angle, swept continuously 8 deg to 155 deg (BI-200SM Continuous Multi-Angle DLS) |
| `dls-explainer-angle-nanobrook.html` | Fixed detection angles: forward (15 deg), right-angle (90 deg), backscatter (173 deg) (NanoBrook family) |
| `dls-explainer-wavelength.html` | Laser wavelength (410 to 680 nm); the intensity trace is colored to match the beam |
| `dls-explainer-template.html` | Blank scaffold for building a new page |

## What each page shows

- **Control panel** — the single variable for that page (slider, text inputs, or
  selectable options), plus any quantities held fixed.
- **Derived quantities** — diffusion coefficient D, decay rate Gamma, correlation
  time 1/Gamma, and scattering vector q, all recomputed live.
- **Intensity vs. time** — a simulated count-rate history. The fluctuation
  timescale tracks the correlation time, and both the mean count rate and the
  fluctuation depth scale with particle size (larger particles scatter more light
  and diffuse more slowly).
- **Autocorrelation function** — the ideal g²(τ) − 1 = β·exp(−2Γτ) curve plotted
  on a logarithmic τ axis spanning the correlator window, with a cosmetic
  measurement-noise overlay that is larger at long delays and settles as the
  configuration is held fixed.

## The physics

All pages use the same model:

- **Stokes–Einstein:** D = kᵦT / (3πηd), with η = 0.890 mPa·s and n = 1.330 for
  water at 25 °C.
- **Scattering vector:** q = (4πn/λ₀)·sin(θ/2).
- **Decay rate:** Γ = D·q², with field correlation time 1/Γ.
- **ACF:** g²(τ) − 1 = β·exp(−2Γτ).

The intensity time series is a simplified, illustrative signal (a sum of detuned
sinusoids centered on the mean), not a literal speckle simulation. It is intended
to convey the correct timescale and amplitude behavior rather than to reproduce
true photon statistics. The ACF curve is the analytic single-exponential decay;
the overlaid "measurement" noise is cosmetic.

Reasonable input bounds are enforced on each page (for example, particle diameter
0.5 nm to 1 um or 10 um, delay times 100 ns to 10 s, angle 8 deg to 155 deg,
wavelength 410 to 680 nm).

## Usage

Each HTML file is fully self-contained: no build step, no external dependencies,
no network calls. Open any file directly in a desktop browser, or host it as a
static page.

- The two plots are placed side by side on screens 760 px wide or wider, and
  stack vertically on narrower screens.
- The Brookhaven logo links to brookhaveninstruments.com (new tab), and a Back
  button returns to the previous page. These navigation actions may be sandboxed
  inside an embedded preview but work normally when the file is opened or hosted
  as an ordinary web page.

## Building a new page from the template

1. Copy `dls-explainer-template.html` to a new filename.
2. Set the page `<title>`, the brand-bar tag, and the intro heading / text.
3. Replace the contents of the control card with your input(s).
4. In the script, find the **VARIANT WIRING** stub near the bottom and set the
   fixed conditions, then wire your control to the relevant mutable globals:
   `diam` (m), `lambda0` (m), `thetaRad` (rad), `TAU_MIN` / `TAU_MAX` (s), and
   `traceColor` (any CSS color). After changing any of them, call `drawStats()`.
   The animation loop reads these globals every frame, so the plots update
   automatically.

## Instruments referenced

- **BI-200SM** Continuous Multi-Angle DLS goniometer (continuous-angle page)
- **NanoBrook** family of instruments (fixed-angle page)
- **BI-TurboCorr** USB correlator card (correlator-layout page)

## Notes and caveats

- The time-series and the ACF measurement noise are illustrative, not a
  rigorous photon-correlation simulation.
- Solvent properties are fixed to water at 25 °C.
- The model assumes a single, monodisperse particle population.

