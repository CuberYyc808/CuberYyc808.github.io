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
<p class="isem-note"><strong>This note introduces a practical workflow for large scale 0PA flux generation: a reusable radial solver layer, a tail aware mode summation order, and Adaptive Levin integration for difficult source integrals in generic EMRI calculations.</strong></p>

In EMRI waveform work, a flux calculation is rarely a one time exercise. One quickly ends up with many parameter points, many modes, and orbits that may be eccentric, inclined, or close to difficult regions of Kerr parameter space. The useful question is therefore not only "can I compute this mode?" It is: can I compute many modes, see where the truncation really happens, reuse the expensive pieces, and avoid wasting samples on oscillations that the integrator should understand analytically?

The workflow has three parts. First, the radial equation is handled by an iterative series expansion matching method, ISEM for short. Second, the mode sum is organized so that the radial harmonic $n$ remains visible as the final tail direction rather than being hidden inside a rectangular grid. Third, Adaptive Levin integration is used where source integrals become strongly oscillatory.

<div class="isem-links">
  <a href="{{ '/tools/#generalized-sasaki-nakamura' | relative_url }}">GSN tool card</a>
  <a href="{{ '/tools/#kerr-geodesics' | relative_url }}">KerrGeodesics card</a>
  <a href="{{ '/tools/#adaptive-levin' | relative_url }}">AdaptiveLevin card</a>
  <a href="{{ '/research/sasaki-nakamura-waveforms/' | relative_url }}">Sasaki-Nakamura waveform work</a>
  <a href="https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/ISEM">GSN ISEM branch</a>
</div>

<div class="isem-diagram">
  <div class="isem-diagram__title">Workflow in one line</div>
  <div class="isem-flow">
    <div class="isem-flow__box"><strong>Kerr orbit</strong><span>trajectory, velocity, phases</span></div>
    <div class="isem-flow__box"><strong>Radial solver</strong><span>ISEM, Teukolsky and GSN homogeneous solutions</span></div>
    <div class="isem-flow__box"><strong>Source integral</strong><span>trapezoidal or Adaptive Levin depending on the tail</span></div>
    <div class="isem-flow__box"><strong>Mode shells</strong><span>$\ell$, $m$, $k$ grouped outside; $n$ monitored as radial tail</span></div>
    <div class="isem-flow__box"><strong>Flux dataset</strong><span>infinity and horizon branches with recorded convergence metadata</span></div>
  </div>
</div>

## Motivation: why this is worth doing

LISA, Taiji, and TianQin are space based gravitational wave detector projects. One important class of sources for these missions is EMRIs, where 0PA flux generation becomes a production scale numerical task rather than a small script. Frequency domain Teukolsky calculations are accurate and modular, but the cost grows sharply when the orbit becomes highly eccentric, inclined, and precessing. In the fully generic case, the signal power is spread across a large set of $(\ell,m,k,n)$ modes. If the time for a single mode cannot be reduced effectively, the full flux calculation becomes a large computational expense.

The goal is not only to compute one mode quickly. The goal is to know which part of the spectrum is still active, which part has become tail, and which numerical method should be used for each region. That is where the current implementation differs from a plain rectangular mode loop: it treats the mode sum as something to diagnose, not just something to force through a larger grid.

## The radial solver layer

The first piece is the radial solver. Here the radial Teukolsky equation is handled by iterative series expansion matching, abbreviated as ISEM below. The idea is to use the transformed form of the Teukolsky equation, build series expansions from the horizon and from infinity, and then propagate the two physical branches toward an intermediate matching point. At that point, the solution and its radial derivative are matched to determine the matching coefficients, which are also the asymptotic amplitudes needed for flux evaluation. The full radial solution is then reconstructed from the matched branches.

This is the right place to spend effort because the radial solve sits inside every mode calculation and has long been a bottleneck in the source integral calculation. In the current implementation, this construction is roughly two orders of magnitude faster than the traditional direct numerical GSN solve and MST based routes for the same repeated mode production use case. Reducing this cost for each mode is what makes the larger 0PA flux workflow practical.

<figure class="isem-figure">
  <img src="{{ '/images/isem_matching_original_30fps.gif' | relative_url }}" alt="Animated illustration of iterative series expansion matching for radial Teukolsky solutions">
  <figcaption>ISEM as a radial construction idea: series solutions are generated from the horizon and infinity, propagated to an intermediate point, and matched through the value and radial derivative. The resulting asymptotic amplitudes feed directly into the flux calculation.</figcaption>
</figure>

<div class="isem-steps">
  <div class="isem-step">
    <strong>Homogeneous solutions</strong>
    <p>Build horizon side and infinity side homogeneous radial Teukolsky solutions from controlled series expansions.</p>
  </div>
  <div class="isem-step">
    <strong>Matching coefficients</strong>
    <p>Match the solution and derivative at an intermediate point to obtain the asymptotic amplitudes.</p>
  </div>
  <div class="isem-step">
    <strong>Source interface</strong>
    <p>Reuse the reconstructed radial solution and amplitudes in the source integral and flux evaluation.</p>
  </div>
</div>

## How modes are added together

Next comes the mode summation order. The useful empirical structure is that the largest contributions usually sit close to the diagonal in angular space: for a fixed $\ell$, modes with $m=\pm \ell$ are often among the dominant branches. A direct rectangular loop does not exploit this structure. If one fixes $\ell$ and then scans all $m$ from $-\ell$ to $\ell$, and then repeats this inside large $k$ and $n$ ranges, the calculation can spend many modes before the relevant convergence pattern becomes clear.

A more useful order is to fix $m$ and grow $\ell$ from $\max(\mathrm{abs}(m),2)$ upward. This makes the angular convergence easier to see. The same idea can then be extended to the polar and radial harmonics. The $k$ direction often converges quickly, usually within about ten shells for the cases considered here, while the radial harmonic $n$ is slower and carries the long eccentricity tail. For that reason, $n$ is left as the final summation direction.

The older mental model is:

<div class="isem-compare">
  <div class="isem-compare__panel">
    <h3>Rectangular grid mindset</h3>
    <ul>
      <li>Choose a large box in (&ell;, m, k, n).</li>
      <li>Loop through the full block even when many entries are already negligible.</li>
      <li>The slow radial tail is mixed into the whole four dimensional rectangle.</li>
    </ul>
  </div>
  <div class="isem-compare__panel">
    <h3>Production workflow mindset</h3>
    <ul>
      <li>For each m, grow &ell; from max(abs(m), 2) upward.</li>
      <li>Add the faster k shells before the slow radial direction.</li>
      <li>Leave n last, so the eccentric tail truncation is visible.</li>
    </ul>
  </div>
</div>

The practical advantage is that convergence becomes easier to diagnose. Instead of asking whether a whole rectangular block is large enough, the code can report where the infinity and horizon branches reached in $n$, how large the final shell contribution is, and whether $n_\mathrm{max}$ should be increased. In this ordering, the maximum radial truncation used in the code is $n_\mathrm{max}=500$, which is stable for the target cases with $e<0.9$. Compared with the rectangular ordering, this shell aware order typically reduces the number of modes that need to be evaluated by about 50%, while making the truncation decision more transparent.

<div class="isem-diagram">
  <div class="isem-diagram__title">Mode summation flow</div>
  <div class="isem-flow">
    <div class="isem-flow__box"><strong>Select &ell; shell</strong><span>angular resolution layer</span></div>
    <div class="isem-flow__box"><strong>Select m branch</strong><span>azimuthal structure and frequency sign</span></div>
    <div class="isem-flow__box"><strong>Select k shell</strong><span>polar harmonic structure for generic orbits</span></div>
    <div class="isem-flow__box"><strong>Scan n tail</strong><span>radial harmonic tail; eccentric truncation is visible here</span></div>
    <div class="isem-flow__box"><strong>Latch method</strong><span>switch tail modes to Adaptive Levin when oscillations dominate</span></div>
  </div>
</div>

The resulting workflow is therefore $\ell \to m \to k \to n$: angular structure first, the fast polar direction next, and the slow radial tail last. This is not just a different loop order; it is a way to expose the convergence information that is otherwise hidden inside a large rectangular sum.

## Adaptive Levin: use the right tool for the tail

The third piece is Adaptive Levin integration. In generic 0PA flux calculations, source integrals with large $n$ can oscillate rapidly. A plain quadrature rule then pays for many samples whose job is just to chase phase. In representative one dimensional radial integrations, a standard sampling route may need about $2^{14}=16384$ radial samples to reach the desired convergence, while the Adaptive Levin route can reach the same convergence with an effective scale closer to $2048$.

The Levin method treats a highly oscillatory integral by rewriting it as an auxiliary ODE system; after discretization, that system becomes a small matrix solve. The adaptive part is the interval refinement around it: easy regions stay coarse, while difficult oscillatory regions are cut into smaller segments. On each local segment, the working grid is small, typically $17\times17$ in the two dimensional setup. The dense local solve scales like $O(q^3)$ with $q=17$, and the total cost follows the number of accepted segments rather than one globally inflated sampling grid. For generic two dimensional integrals, the current route uses Adaptive Levin in the radial direction and Clenshaw Curtis quadrature in the $\theta$ direction.

<div class="isem-diagram">
  <div class="isem-diagram__title">Adaptive Levin flow</div>
  <div class="isem-flow">
    <div class="isem-flow__box"><strong>Precompute orbit data</strong><span>reuse geodesic samples and phase information across batches</span></div>
    <div class="isem-flow__box"><strong>Detect tail mode</strong><span>large radial harmonic or difficult generic $(n,k)$ row</span></div>
    <div class="isem-flow__box"><strong>Refine radially</strong><span>the high-$n$ oscillation is mainly radial</span></div>
    <div class="isem-flow__box"><strong>Use theta CC</strong><span>fixed polar Clenshaw Curtis nodes for generic 2D integrals</span></div>
    <div class="isem-flow__box"><strong>Record metadata</strong><span>segments, depth, stop reason, and effective intervals</span></div>
  </div>
</div>

The effect is simple: the difficult high $n$ integrals no longer require the same brute force sampling strategy as the easy modes. Radial Adaptive Levin plus fixed $\theta$ direction Clenshaw Curtis keeps the high frequency radial direction under control, while still using a stable tensor product structure for generic orbits.

<div class="isem-metric">
  <div class="isem-metric__item">
    <span class="isem-metric__value">8.925 ms</span>
    <span class="isem-metric__label">typical post warm time for generic case 2D convolution integral evaluation</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">16.531 ms</span>
    <span class="isem-metric__label">95% of high $n$ modes in generic case 2D convolution integrals finish within this time</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">5 ms</span>
    <span class="isem-metric__label">95% of eccentric case 1D integral tests finish below this scale</span>
  </div>
</div>

## Related software and modules

- [GeneralizedSasakiNakamura.jl](https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/ISEM): current ISEM development branch.
- [KerrGeodesics.jl](https://github.com/CuberYyc808/KerrGeodesics.jl): bound Kerr geodesic infrastructure for orbital frequencies, phases, and trajectories.
- [AdaptiveLevin.jl](https://github.com/CuberYyc808/AdaptiveLevin.jl): adaptive methods for highly oscillatory integrals.
- [Tools overview]({{ '/tools/#generalized-sasaki-nakamura' | relative_url }}): homepage entry point for the software modules.

<div class="isem-callout">
  <strong>Try it and send feedback.</strong> The code and related modules are open for testing and use.
</div>
