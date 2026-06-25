# MineShield — Open-Pit Slope Stability Digital Twin

A live **digital twin** of an open-pit mine paired with a **risk dashboard**. Move any
slider — rainfall, dewatering, blasting, slope angle, rock strength — and the 3D pit
responds instantly: the water table rises or drops, each pit sector recolours by risk,
and the assessment panel recomputes a per-sector **Factor of Safety** with a recommended
remediation action and early-warning horizon.

Built for the **MineShield** concept: turning borehole, groundwater, rainfall and
geotechnical data into one early warning — *which zone is at risk, and what to do about it.*

> Developed by **Purity Kampamba**, Environmental Engineer

## What's inside

Scroll through three linked views, all driven by the same live inputs:

1. **Live 3D twin** — a terraced open-pit you can orbit, with per-sector risk colouring and a rising/falling water table.
2. **Slope cross-section** — an annotated, animated section (β, water table, pore pressure `u`, depth-to-failure-plane `z`, failure plane, borehole, piezometer, rain gauge) with groundwater that **seeps toward the slope face** in real time.
3. **Failure scenario** — press *Run* to watch the slope collapse along the failure plane and run out into the working pit, with a runout / casualty readout. Severity scales with the live Factor of Safety.

## View it locally — fully offline

No build step, no server, **no internet required**. Just open the file:

1. Double-click **`index.html`**, or right-click → *Open with* → Chrome.
2. Everything works offline — Three.js is vendored in [`lib/`](lib/), and the two new sections are pure HTML5 canvas with no dependencies.

*(Fonts come from Google Fonts when online; offline they fall back to system serif/sans and remain perfectly readable.)*

## Deploy online (Netlify)

**Option A — drag & drop:** go to [app.netlify.com/drop](https://app.netlify.com/drop) and
drag this whole folder onto the page. Done.

**Option B — from GitHub:** in Netlify, *Add new site → Import from Git*, pick this repo.
No build command is needed; `netlify.toml` already points the publish directory at the repo root.

## How the risk is modelled

Each of the four pit sectors is scored with an infinite-slope **limit-equilibrium** model:

```
FoS = ( c' + (σ − u)·tanφ )  /  ( γ·z·sinβ·cosβ  +  k_h·γ·z·cos²β )
```

- `c'` rock cohesion, `φ` friction angle, `β` slope angle, `γ` unit weight, `z` slip depth
- `u` pore-water pressure — driven up by **rainfall**, down by **dewatering**
- `k_h` pseudo-static seismic coefficient — driven by **blasting**

Sectors differ in depth, drainage and rock strength, so risk is **spatial** — typically the
East wall (Sector B) reaches the limit first. `FoS < 1.0` means failure conditions.

*This is a decision-support demonstration, not a substitute for a site-specific geotechnical study.*

## Repository

https://github.com/mulengachilufya/open-pit-mine-slope-instability-innovation
