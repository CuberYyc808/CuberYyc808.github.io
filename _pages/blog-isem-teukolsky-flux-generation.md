---
layout: single
title: "A practical adiabatic (0PA) flux workflow for generic EMRIs"
permalink: /blog/isem-teukolsky-flux-generation/
author_profile: true
lang: en
lang_switch_url: /zh/blog/isem-teukolsky-flux-generation/
---

<style>
:root {
  --isem-surface: #ffffff;
  --isem-surface-alt: #f8fafc;
  --isem-text: #17202a;
  --isem-muted: #475569;
  --isem-border: #d8dee4;
}
html[data-theme="dark"] {
  --isem-surface: #ffffff;
  --isem-surface-alt: #f8fafc;
  --isem-text: #111827;
  --isem-muted: #334155;
  --isem-border: #cbd5e1;
}
.isem-note {
  color: var(--global-text-color-light);
  font-size: 1rem;
  line-height: 1.55;
  margin: -0.3rem 0 1.2rem;
}
.isem-kicker {
  color: var(--global-text-color-light);
  font-size: 0.86rem;
  font-weight: 700;
  letter-spacing: 0;
  text-transform: uppercase;
  margin-bottom: 0.35rem;
}
.isem-links {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 210px), 1fr));
  gap: 0.8rem;
  margin: 1.1rem 0 1.4rem;
}
.isem-links a {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  color: var(--isem-text);
  padding: 0.75rem 0.85rem;
  text-decoration: none;
  font-weight: 600;
  background: var(--isem-surface);
  transition: border-color 160ms ease, box-shadow 160ms ease, transform 160ms ease;
}
.isem-links a:hover,
.isem-links a:focus {
  border-color: #52adc8;
  box-shadow: 0 8px 22px rgba(15, 23, 42, 0.08);
  transform: translateY(-2px);
}
.isem-diagram {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface);
  color: var(--isem-text);
  padding: 1rem;
  margin: 1.2rem 0 1.4rem;
}
.isem-figure {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface);
  color: var(--isem-text);
  margin: 1.2rem 0 1.5rem;
  overflow: hidden;
}
.isem-figure img {
  display: block;
  width: 100%;
  height: auto;
}
.isem-figure figcaption {
  color: var(--isem-muted);
  font-size: 0.84rem;
  line-height: 1.45;
  padding: 0.65rem 0.85rem 0.8rem;
}
.isem-diagram__title {
  font-weight: 700;
  margin-bottom: 0.75rem;
}
.isem-flow {
  display: grid;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  gap: 0.45rem;
  align-items: stretch;
}
.isem-flow__box {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface-alt);
  color: var(--isem-text);
  padding: 0.58rem 0.62rem;
}
.isem-flow__box strong {
  display: block;
  font-size: 0.82rem;
  margin-bottom: 0.25rem;
}
.isem-flow__box span {
  color: var(--isem-muted);
  display: block;
  font-size: 0.73rem;
  line-height: 1.32;
}
@media (max-width: 900px) {
  .isem-flow {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
@media (max-width: 560px) {
  .isem-flow {
    grid-template-columns: 1fr;
  }
}
.isem-compare {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 260px), 1fr));
  gap: 0.9rem;
  margin: 1.2rem 0 1.4rem;
}
.isem-compare__panel {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface);
  color: var(--isem-text);
  padding: 0.95rem;
}
.isem-compare__panel h3 {
  font-size: 1rem;
  margin: 0 0 0.55rem;
}
.isem-compare__panel p,
.isem-compare__panel li {
  color: var(--isem-muted);
  font-size: 0.9rem;
  line-height: 1.5;
}
.isem-callout {
  border-left: 4px solid var(--isem-muted);
  background: var(--isem-surface-alt);
  color: var(--isem-text);
  padding: 0.85rem 1rem;
  margin: 1.2rem 0;
}
.isem-steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 230px), 1fr));
  gap: 0.8rem;
  margin: 1.1rem 0 1.4rem;
}
.isem-step {
  border-top: 3px solid var(--isem-muted);
  background: var(--isem-surface);
  color: var(--isem-text);
  padding: 0.8rem 0.9rem;
}
.isem-step strong {
  display: block;
  margin-bottom: 0.3rem;
}
.isem-step p {
  margin: 0;
  color: var(--isem-muted);
  font-size: 0.92rem;
  line-height: 1.5;
}
.isem-metric {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 170px), 1fr));
  gap: 0.75rem;
  margin: 1rem 0 1.4rem;
}
.isem-metric__item {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface-alt);
  color: var(--isem-text);
  padding: 0.85rem;
}
.isem-metric__value {
  display: block;
  font-size: 1.35rem;
  font-weight: 700;
  line-height: 1.1;
}
.isem-metric__label {
  color: var(--isem-muted);
  display: block;
  font-size: 0.82rem;
  line-height: 1.35;
  margin-top: 0.35rem;
}
</style>

<script>
window.MathJax = {
  tex: { inlineMath: [['$', '$'], ['\\(', '\\)']], processEscapes: true },
  svg: { fontCache: 'global' }
};
</script>
<script defer src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js"></script>

<div class="isem-kicker">Technical blog</div>
<p class="isem-note"><strong>How GeneralizedSasakiNakamura.jl turns a Kerr geodesic into total Teukolsky fluxes, and where the speed comes from.</strong></p>

For a Kerr orbit, compute the fluxes with:

```julia
using GeneralizedSasakiNakamura
flux = Teukolsky_pointparticle_flux(a, p, e, x; tol = 1e-8)
```

It returns the energy, angular momentum and Carter-constant fluxes, separately at infinity and at the horizon.

### Motivation

Space-based detectors such as LISA, Taiji and TianQin will observe extreme mass-ratio inspirals for months to years. Modelling them at adiabatic order needs the orbit-averaged fluxes on a dense grid in (a, p, e, x), and each flux is a sum over Teukolsky modes labelled by (ℓ, m, k, n). For a generic, eccentric and inclined orbit that sum easily runs to a million modes. Two numbers therefore decide whether a flux grid is practical: the cost of one mode, and how many modes you actually have to compute. The rest of this post goes through both.

### Sampling the orbit

The geodesic comes from KerrGeodesics.jl and is computed once per orbit. We sample it in Mino time, using the radial phase $q_r = \Upsilon_r \lambda + q_{r,0}$ and the polar phase $q_\theta = \Upsilon_\theta \lambda + q_{\theta,0}$. At each node we store $r$, $r_*$, $\theta$, the oscillating parts of $t$ and $\phi$, and the velocities $\Sigma u^r$ and $\Sigma u^\theta$.

Two details keep this cheap.

- **Half periods.** Each phase only needs $[0, \pi]$. The return half of a libration is the same path with $u^r \to -u^r$ (or $u^\theta \to -u^\theta$), so it enters the integrand as a sign flip rather than as new samples.
- **One dense master grid.** For each orbit we build a single uniform grid at the finest resolution we allow: $2^{14}+1$ radial and $2^{12}+1$ polar points. Every coarser grid is a strided view of it. The nodes are nested, so refining a mode never re-evaluates the trajectory, it just reads more of the master.

### The radial solver

Every mode has its own frequency $\omega = (m\Upsilon_\phi + n\Upsilon_r + k\Upsilon_\theta)/\Gamma$, so every mode needs a fresh homogeneous radial solution. This is where most codes spend their time, and where GSN-ISEM comes in.

GSN-ISEM solves the generalized Sasaki–Nakamura equation directly instead of the Teukolsky equation. It works in the compact coordinate $x = (r - r_+)/(r - r_-) \in (0, 1)$:

- **Seeds at the boundaries.** A Frobenius series at the horizon and an asymptotic series at infinity give the IN and UP solutions with the right boundary behaviour.
- **Continuation.** Each seed is carried inward by Taylor patches about ordinary points. The recurrence coefficients are generated ahead of time as rational tables, so building a patch is a short, fixed recursion.
- **Matching.** The two sides meet at an interior point. Matching the values and derivatives there gives the incidence and reflection amplitudes, which fix the normalisation of the mode.

There is no adaptive ODE integration anywhere in this. A full solve is a fixed amount of polynomial arithmetic and takes about a millisecond. After that, evaluating the solution at any radius is just evaluating one of the patches. The same solver handles complex frequencies (it rotates the contour into the complex plane), which is what the `qnm` solver in the package is built on.

The animation below shows how the boundary series are continued and matched to construct the GSN radial function:

<p align="center"><img src="{{ '/images/isem_matching_gsn_0_10_0.gif' | relative_url }}" width="80%" alt="GSN-ISEM series continuation from the horizon and infinity, matching, and reconstruction of the radial function X"></p>

*GSN-ISEM: continuation of the horizon and infinity series, matching at an interior point, and reconstruction of the radial function $X$.*

### The polar part

The angular functions come from [SpinWeightedSpheroidalHarmonics.jl](https://github.com/ricokaloklo/SpinWeightedSpheroidalHarmonics.jl), one harmonic object per mode. At each polar node we need $S$ and $S^\prime$; the second derivative $S^{\prime\prime}$ is taken from the spheroidal equation instead of being evaluated separately. Equatorial orbits only need the harmonic at $\theta = \pi/2$, which is one reason they are cheaper per mode.

### Putting the two together

For each mode the amplitude $Z$ is a source integral over the orbit, normalised by the incidence amplitude of the radial solution. The integrand combines the radial solution, the spheroidal harmonic, the orbit velocities and the phase $e^{i(\omega \Delta t - m \Delta \phi + \dots)}$.

- **Circular equatorial orbits** need no integral at all.
- **Circular inclined orbits** need the radial solution at one radius, $r = p$, and a 1-D integral over $q_\theta$.
- **Eccentric equatorial orbits** need a 1-D integral over $q_r$, with the harmonic at a single angle.
- **Generic orbits** need a 2-D integral over $(q_r, q_\theta)$.

The 2-D integral does not factor into a radial piece times a polar piece, because $\rho = -1/(r - ia\cos\theta)$ couples $r$ and $\theta$. So the sum runs over all $N \times K$ nodes, but everything that can be precomputed is precomputed:

- the $\rho$-dependent tables are built once per grid size and shared by every mode of the orbit;
- radial-only factors are computed once per row and polar-only factors once per column;
- the phase is an outer product of a radial vector and a polar vector.

All integrals are trapezoid sums on the uniform phase grids. For periodic smooth integrands this converges very quickly, and it lets each mode refine adaptively on nested grids:

1. Start at $N = 64$ radial intervals. The polar resolution starts at $K = 16$, raised to cover $\ell + \lvert k\rvert$.
2. Double $N$. Only the new nodes are evaluated, and the old partial sum is reused as half of the new one.
3. Stop when the relative change is below about $3\times 10^{-4}$ at the default tolerance, after a minimum grid that grows with $\lvert n\rvert$. $K$ only doubles when the result looks suspicious.

On large grids, evaluating the radial solution at every new node becomes the cost. Once that happens the code builds a Chebyshev table of the solution (a few hundred points, checked against direct evaluations to $10^{-10}$) and interpolates from it.

From $Z$ the fluxes follow directly. At infinity, $\dot E = \lvert Z\rvert^2/(4\pi\omega^2)$ and $\dot L = m\lvert Z\rvert^2/(4\pi\omega^3)$. At the horizon the same $\lvert Z\rvert^2$ gets the horizon factor. The Carter flux uses an extra polar average.

### How the modes are added together

A rectangular box in (ℓ, m, k, n) is the obvious choice and a wasteful one. Most of the box contributes nothing at the tolerance we care about. The summation instead walks outward from where the flux actually is.

- **Symmetry first.** A mode and its $(\ell, -m, -n, -k)$ partner contribute equally, so only half of the index space is computed and each mode counts twice.
- **Nesting.** For each radial shell $n$, we loop over $k$, then over $m$, and inside that walk in $\ell$.
- **Start at the peak.** For $k \neq 0$ the $\ell$ walk starts near $\lvert m \pm k\rvert$, where the mode is largest, and goes up and down from there.
- **Stop when it is small.** An $\ell$ walk stops after a few consecutive modes below the threshold, or immediately when one mode is far below it. An $m$ shell that is still growing does not count towards stopping. The $n$ tail stops after a few shells below `tol` times the running total; a fit of the shell sizes tells the code roughly where that will happen.
- **Two branches.** Infinity and the horizon keep separate totals and separate thresholds, so the much smaller horizon flux is still resolved to relative accuracy.

For the high-$n$ tails of very eccentric orbits the code also has an adaptive Levin rule for the radial integral, switched on with `tail_levin = true`. All the examples below use the trapezoid rule throughout.

### What it costs

All four cases use $a = 0.9$, $p = 6$ and `tol = 1e-8`, on a single thread with a warm session.

| orbit | e | x | modes | time | per mode |
|---|---|---|---:|---:|---:|
| circular equatorial | 0 | 1 | 378 | 0.34 s | 0.89 ms |
| circular inclined | 0 | 0.5 | 11 466 | 10.3 s | 0.90 ms |
| eccentric equatorial | 0.7 | 1 | 45 204 | 26.1 s | 0.58 ms |
| generic | 0.7 | 0.5 | 1 319 722 | 21.8 min | 0.99 ms |

In every case the cost per mode stays close to the cost of one radial solve. The integration and summation add little on top of it. That comes from the nested grids, the shared per-orbit tables and the radial interpolation table. The eccentric case is the cheapest per mode because it only needs the harmonic at one angle and a 1-D integral.

<div class="isem-metric">
  <div class="isem-metric__item">
    <span class="isem-metric__value">~1 ms</span>
    <span class="isem-metric__label">one GSN-ISEM radial solve</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">0.58 ms</span>
    <span class="isem-metric__label">per mode, eccentric equatorial (e = 0.7)</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">0.99 ms</span>
    <span class="isem-metric__label">per mode, generic orbit (e = 0.7, x = 0.5)</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">1.32 M modes in 21.8 min</span>
    <span class="isem-metric__label">full generic flux, single thread</span>
  </div>
</div>

### Running many orbits

Radial solves, mode calls and flux calls are thread-safe, and they give the same numbers in serial and threaded runs. A flux grid can therefore be spread over threads directly. Start Julia with `--threads=auto` and set `BLAS.set_num_threads(1)`.

When several calls work on the same orbit, a submission lets them share the trajectory, the master grid and the precomputed tables:

```julia
modes = with_pointparticle_submission(0.9, 10.0, 0.2, 0.3) do submission
    tasks = [spawn_pointparticle_submission!(submission) do
                 Teukolsky_pointparticle_mode(-2, 2, 2, n, 0, 0.9, 10.0, 0.2, 0.3; submission)
             end for n in 0:2]
    fetch.(tasks)
end
```

### Related software and modules

<div class="isem-links isem-compare">
  <a href="https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/claude/project-thread-s9q61h">GSN code</a>
  <a href="{{ '/tools/#generalized-sasaki-nakamura' | relative_url }}">GSN tool card</a>
  <a href="{{ '/tools/#kerr-geodesics' | relative_url }}">KerrGeodesics card</a>
  <a href="{{ '/research/sasaki-nakamura-waveforms/' | relative_url }}">Sasaki-Nakamura waveform work</a>
</div>

- [GeneralizedSasakiNakamura.jl](https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/claude/project-thread-s9q61h), the radial solver and the flux pipeline.
- [KerrGeodesics.jl](https://github.com/CuberYyc808/KerrGeodesics.jl), for the orbits.
- [SpinWeightedSpheroidalHarmonics.jl](https://github.com/ricokaloklo/SpinWeightedSpheroidalHarmonics.jl), for the angular functions.
