# MineShield — Open-Pit Slope Stability Digital Twin

A live **digital twin** of an open-pit mine paired with a **risk dashboard**. Move any
slider — rainfall, dewatering, blasting, slope angle, rock strength — and the 3D pit
responds instantly: the water table rises or drops, each pit sector recolours by risk,
and the assessment panel recomputes a per-sector **Factor of Safety** with a recommended
remediation action and early-warning horizon.

Built for the **MineShield** concept: turning borehole, groundwater, rainfall and
geotechnical data into one early warning — *which zone is at risk, and what to do about it.*

> Developed by **Purity Kampamba**, Environmental Engineer

## View it locally

No build step, no server. Just open the file:

1. Double-click **`index.html`**, or right-click → *Open with* → Chrome.
2. The 3D twin loads from CDN (Three.js), so you need an internet connection the first time.

If you're offline, the dashboard and risk calculations still work — only the 3D view needs the CDN.

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
