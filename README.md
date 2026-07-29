# DLS Explainer Suite

Built by **Daniel P. Seeman, Ph.D.** — [about.me/danielseeman](https://about.me/danielseeman)

A set of self-contained, interactive web pages that illustrate the physics of
**Dynamic Light Scattering (DLS)**. Each page isolates a single variable and
shows, in real time, how that variable affects the scattered-light intensity
history and the resulting intensity autocorrelation function (ACF).

Every file is a single HTML document with no build step, no external
dependencies, and no network calls — open it in a browser and it runs.

## The pages

| File | Variable demonstrated |
|------|----------------------|
| `dls-explainer-big-small-particles.html` | Particle hydrodynamic diameter (0.5 nm – 1 µm) |
| `dls-explainer-delay-times.html` | Correlator layout: first and last delay times (particle diameter also editable) |
| `dls-explainer-angle-goniometer.html` | Scattering angle, swept continuously 8° – 155° |
| `dls-explainer-angle-benchtop.html` | Fixed detection angles: forward (15°), right-angle (90°), backscatter (173°) |
| `dls-explainer-wavelength.html` | Laser wavelength (410 – 680 nm); the intensity trace is colored to match the beam |
| `dls-explainer-template.html` | Blank scaffold for building a new page |

## What each page shows

- **Control panel** — the single variable for that page (slider, text inputs, or
  selectable options), plus the quantities held fixed.
- **Derived quantities** — diffusion coefficient *D*, decay rate Γ, correlation
  time 1/Γ, and scattering vector *q*, all recomputed live.
- **Intensity vs. time** — a simulated count-rate history. The fluctuation
  timescale tracks the correlation time, and both the mean count rate and the
  fluctuation depth scale with particle size: larger particles scatter more
  light and diffuse more slowly.
- **Autocorrelation function** — the ideal g²(τ) − 1 = β·exp(−2Γτ) curve on a
  logarithmic τ axis spanning the correlator window, with a cosmetic
  measurement-noise overlay that is larger at long delays and settles as the
  configuration is held fixed.

## The physics

All pages use the same model:

- **Stokes–Einstein:** D = k_B·T / (3πηd), with η = 0.890 mPa·s and n = 1.330
  for water at 25 °C.
- **Scattering vector:** q = (4πn/λ₀)·sin(θ/2).
- **Decay rate:** Γ = D·q², with field correlation time 1/Γ.
- **ACF:** g²(τ) − 1 = β·exp(−2Γτ).

The intensity time series is a simplified, illustrative signal (a sum of
detuned sinusoids centered on the mean), not a literal speckle simulation. It
conveys the correct timescale and amplitude behavior rather than reproducing
true photon statistics. The ACF curve is the analytic single-exponential decay;
the overlaid "measurement" noise is cosmetic.

Reasonable input bounds are enforced on each page (for example, particle
diameter 0.5 nm – 1 µm, delay times 100 ns – 10 s, angle 8° – 155°, wavelength
410 – 680 nm).

## Usage

Each HTML file is fully self-contained. Open any file directly in a desktop
browser, or host the folder as static files on any web server (GitHub Pages,
Netlify, S3, etc.) — no configuration required.

```bash
# clone and open locally
git clone <your-repo-url>.git
cd <repo>
open dls-explainer-wavelength.html      # macOS
# or: xdg-open dls-explainer-wavelength.html   (Linux)
# or just double-click the file
```

To build a new explainer, copy `dls-explainer-template.html` and add your
control and drawing logic; the layout, styling, and shared physics helpers are
already scaffolded.

## Notes

These pages are educational/illustrative tools. The simulations are designed to
build intuition for how each DLS variable shapes the measurement, not to serve
as a quantitative instrument model.

## License

Released under the MIT License — free to use, modify, and distribute, including
commercially, provided the copyright and license notice are retained. See
[`LICENSE`](LICENSE) for the full text.

Copyright (c) 2026 Daniel Seeman.
