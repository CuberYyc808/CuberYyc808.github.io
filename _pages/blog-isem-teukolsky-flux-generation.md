---
layout: single
title: "A practical Teukolsky flux workflow for high-eccentricity EMRIs"
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
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 150px), 1fr));
  gap: 0.65rem;
  align-items: stretch;
}
.isem-flow__box {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface-alt);
  color: var(--isem-text);
  padding: 0.7rem 0.8rem;
}
.isem-flow__box strong {
  display: block;
  font-size: 0.92rem;
  margin-bottom: 0.25rem;
}
.isem-flow__box span {
  color: var(--isem-muted);
  display: block;
  font-size: 0.82rem;
  line-height: 1.4;
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
<p class="isem-note"><strong>This note introduces a practical workflow for large-scale frequency-domain Teukolsky flux generation: a reusable radial-solver layer, a tail-aware mode-summation order, and Adaptive Levin integration for difficult high-eccentricity modes.</strong></p>

In EMRI waveform work, a flux calculation is rarely a one-off exercise. One quickly ends up with many parameter points, many modes, and orbits that may be eccentric, inclined, or close to difficult regions of Kerr parameter space. The useful question is therefore not only "can I compute this mode?" It is: can I compute many modes, see where the truncation really happens, reuse the expensive pieces, and avoid wasting samples on oscillations that the integrator should understand analytically?

The workflow has three parts. First, the radial equation is handled by an iterative series expansion matching method, ISEM for short. Second, the mode sum is organized so that the radial harmonic $n$ remains visible as the final tail direction rather than being hidden inside a rectangular grid. Third, Adaptive Levin integration is used where high-eccentricity source integrals become strongly oscillatory.

<div class="isem-links">
  <a href="{{ '/tools/' | relative_url }}">Tools overview</a>
  <a href="{{ '/research/sasaki-nakamura-waveforms/' | relative_url }}">Sasaki-Nakamura waveform work</a>
  <a href="https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/ISEM">GSN ISEM branch</a>
  <a href="https://github.com/CuberYyc808/AdaptiveLevin.jl">AdaptiveLevin.jl</a>
</div>

<div class="isem-diagram">
  <div class="isem-diagram__title">Workflow in one line</div>
  <div class="isem-flow">
    <div class="isem-flow__box"><strong>Kerr orbit</strong><span>frequencies, phases, turning points</span></div>
    <div class="isem-flow__box"><strong>Radial solver</strong><span>ISEM, Teukolsky and GSN homogeneous solutions</span></div>
    <div class="isem-flow__box"><strong>Source integral</strong><span>trapezoidal or Adaptive Levin depending on the tail</span></div>
    <div class="isem-flow__box"><strong>Mode shells</strong><span>$\ell$, $m$, $k$ grouped outside; $n$ monitored as radial tail</span></div>
    <div class="isem-flow__box"><strong>Flux dataset</strong><span>infinity and horizon branches with recorded convergence metadata</span></div>
  </div>
</div>

## Motivation: why this is worth doing

For LISA, Taiji, TianQin and other EMRI programs, zero-PA flux generation is a production problem. Frequency-domain Teukolsky calculations are accurate and modular, but high-eccentricity and generic Kerr orbits spread power across many harmonics. Once the mode sum becomes large, a naive "just make the rectangular grid bigger" approach is not a satisfying workflow.

The goal is not only to compute one mode quickly. The goal is to know which part of the spectrum is still active, which part has become tail, and which numerical method should be used for each region. That is where the current implementation differs from a plain rectangular mode loop: it treats the mode sum as something to diagnose, not just something to brute-force.

## The radial-solver layer

The radial part uses iterative series expansion matching, abbreviated as ISEM below. It is the radial-solver part of the workflow, separate from the mode-summation order and separate from the source-integral method. It provides a first-class radial construction path for Teukolsky/GSN calculations, with matching, transformations, and the `Y` radial interface organized so the source side can call the same conventions repeatedly.

This matters because the radial solve sits inside every mode calculation. If the radial layer is unstable, the rest of the pipeline is fragile. If the radial layer is reusable, source construction and flux summation can be written as a production workflow rather than as a collection of one-off scripts.

<figure class="isem-figure">
  <img src="{{ '/images/isem_matching_original_30fps.gif' | relative_url }}" alt="Animated illustration of iterative series expansion matching for radial Teukolsky solutions">
  <figcaption>ISEM as a radial construction idea: local series information is propagated and matched so the physical radial branches can be built with consistent horizon and infinity behavior. This is the radial layer that the flux workflow calls repeatedly.</figcaption>
</figure>

<div class="isem-steps">
  <div class="isem-step">
    <strong>Homogeneous solutions</strong>
    <p>Construct radial Teukolsky/GSN solutions with consistent boundary and normalization conventions.</p>
  </div>
  <div class="isem-step">
    <strong>Y interface</strong>
    <p>Expose a shared radial variable convention for source construction and flux evaluation.</p>
  </div>
  <div class="isem-step">
    <strong>Fallback behavior</strong>
    <p>Keep automatic fallback paths for cases where a specific radial construction is not the best choice.</p>
  </div>
</div>

## The important change: how the mode sum is ordered

For eccentric equatorial orbits the radial index $n$ is the natural tail coordinate. For generic orbits there is also a polar index $k$, but the same lesson remains: high eccentricity shows up very clearly in the radial harmonic tail. If $n$ is buried inside a rectangular grid, truncation is harder to interpret.

The older mental model is:

<div class="isem-compare">
  <div class="isem-compare__panel">
    <h3>Rectangular-grid mindset</h3>
    <ul>
      <li>First enlarge the radial/polar block: $n$, then $k$.</li>
      <li>Then enlarge azimuthal and angular content: $m$, then $\ell$.</li>
      <li>Easy to implement, but the radial tail is mixed into the whole rectangle.</li>
    </ul>
  </div>
  <div class="isem-compare__panel">
    <h3>Production workflow mindset</h3>
    <ul>
      <li>Reverse the practical control order: $\ell$, then $m$, then $k$.</li>
      <li>Leave $n$ last, as the radial tail direction to monitor.</li>
      <li>For high eccentricity, the stopping point becomes visible as an $n$-shell decision.</li>
    </ul>
  </div>
</div>

This is not really an ISEM claim. It is a mode-summation claim. The benefit is conceptual and practical: once $n$ is treated as the radial tail coordinate, the code can report where the infinity and horizon branches reached, what the last shell contributed, and whether the user should increase $n_\mathrm{max}$. In a high-eccentricity run, that is exactly the diagnostic you want. You can literally see whether the radial tail is dead or still alive.

<div class="isem-diagram">
  <div class="isem-diagram__title">Mode-summation flow</div>
  <div class="isem-flow">
    <div class="isem-flow__box"><strong>Select $\ell$ shell</strong><span>angular resolution layer</span></div>
    <div class="isem-flow__box"><strong>Select $m$ branch</strong><span>azimuthal structure and frequency sign</span></div>
    <div class="isem-flow__box"><strong>Select $k$ shell</strong><span>polar harmonic structure for generic orbits</span></div>
    <div class="isem-flow__box"><strong>Scan $n$ tail</strong><span>radial harmonic tail; high-eccentricity truncation is visible here</span></div>
    <div class="isem-flow__box"><strong>Latch method</strong><span>switch tail modes to Adaptive Levin when oscillations dominate</span></div>
  </div>
</div>

In local benchmark notes, a grouped mode ordering was the fastest tested trapezoidal-SIMD path for one 10,000-mode generic high-e manifest. The blog-level takeaway is broader than that exact file name: group slow-changing structure, keep tail diagnostics explicit, and do not let a four-dimensional rectangle hide convergence. The user-facing workflow is therefore $\ell \to m \to k \to n$: angular structure first, radial tail last.

## Adaptive Levin: use the right tool for the tail

The second piece is Adaptive Levin integration. For high-eccentricity modes, especially large $n$, the source integral can oscillate rapidly. A plain quadrature rule then pays for many samples whose job is just to chase phase.

Adaptive Levin changes the problem. Instead of sampling the oscillation blindly, it builds the oscillatory phase into the integration strategy. That is why it is a natural tail method: use simpler rules when the mode is easy; switch when the high-frequency source structure appears. In large batches, the other important point is reuse: orbit samples, phase data, workspaces, and branch metadata should not be rebuilt from scratch for every single mode.

<div class="isem-diagram">
  <div class="isem-diagram__title">Adaptive Levin flow</div>
  <div class="isem-flow">
    <div class="isem-flow__box"><strong>Precompute orbit data</strong><span>reuse geodesic samples and phase information across batches</span></div>
    <div class="isem-flow__box"><strong>Detect tail mode</strong><span>large radial harmonic or difficult generic $(n,k)$ row</span></div>
    <div class="isem-flow__box"><strong>Refine radially</strong><span>the high-$n$ oscillation is mainly radial</span></div>
    <div class="isem-flow__box"><strong>Use theta CC</strong><span>fixed polar Clenshaw-Curtis nodes for generic 2D integrals</span></div>
    <div class="isem-flow__box"><strong>Record metadata</strong><span>segments, depth, stop reason, and effective intervals</span></div>
  </div>
</div>

The current generic high-e recommendation from local tests is radial adaptive Levin plus fixed theta Clenshaw-Curtis. With a conservative $17\times17$ local grid, the benchmark summary reports a post-warm median of 8.925 ms on a stratified 1000-row sample; focused low/high-$n$ 100-row checks are around the same scale, with high-$n$ p95 reported at 16.531 ms. For representative eccentric single-mode checks, warmed low-mode timings are already well below the 5 ms scale; for harder eccentric tail batches, repeated-run timings in the cache-reuse benchmark are several-to-tens of milliseconds per mode across sampled orbits.

Those numbers are engineering benchmarks, not a universal performance guarantee for the current open-source path. They explain why this workflow is worth trying. For the cases it is designed for, the single-mode source integral is no longer the hopeless bottleneck it used to look like, and the generic 2D path is already operating around the 10 ms scale in the best current route.

<div class="isem-metric">
  <div class="isem-metric__item">
    <span class="isem-metric__value">8.925 ms</span>
    <span class="isem-metric__label">post-warm median for generic 2D non-Y convolution, stratified 1000-row benchmark</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">16.531 ms</span>
    <span class="isem-metric__label">reported high-$n$ p95 in focused 100-row generic check</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">&lt;5 ms</span>
    <span class="isem-metric__label">representative warmed eccentric single-mode checks can fall below this scale</span>
  </div>
</div>

## Related software and modules

- [GeneralizedSasakiNakamura.jl](https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/ISEM): current ISEM development branch.
- [KerrGeodesics.jl](https://github.com/CuberYyc808/KerrGeodesics.jl): bound Kerr geodesic infrastructure for orbital frequencies, phases, and trajectories.
- [AdaptiveLevin.jl](https://github.com/CuberYyc808/AdaptiveLevin.jl): adaptive methods for highly oscillatory integrals.
- [Tools overview]({{ '/tools/' | relative_url }}): homepage entry point for the software modules.

<div class="isem-callout">
  <strong>Try it and send feedback.</strong> The code and related modules are open for testing and use.
</div>
