---
layout: single
title: "Introducing ISEM: scalable Teukolsky flux generation for high-eccentricity EMRIs"
permalink: /blog/isem-teukolsky-flux-generation/
author_profile: true
lang: en
lang_switch_url: /zh/blog/isem-teukolsky-flux-generation/
---

<style>
.isem-note {
  color: #57606a;
  font-size: 0.95rem;
  line-height: 1.55;
  margin: -0.3rem 0 1.2rem;
}
.isem-links {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 210px), 1fr));
  gap: 0.8rem;
  margin: 1.1rem 0 1.4rem;
}
.isem-links a {
  border: 1px solid #d8dee4;
  border-radius: 8px;
  padding: 0.75rem 0.85rem;
  text-decoration: none;
  font-weight: 600;
  background: #fff;
}
.isem-callout {
  border-left: 4px solid #57606a;
  background: #f6f8fa;
  padding: 0.85rem 1rem;
  margin: 1.2rem 0;
}
</style>

<p class="isem-note"><strong>A technical infrastructure note for large-scale frequency-domain EMRI flux production.</strong></p>

ISEM is a workflow for producing Teukolsky-based gravitational-wave fluxes for extreme-mass-ratio inspirals (EMRIs), especially when the orbit is highly eccentric or generic. The emphasis is practical: many waveform studies need repeated, reliable flux calculations across a large orbital parameter space, and the bottleneck is often not one spectacular calculation but the accumulation of many expensive mode computations.

This note introduces ISEM as technical infrastructure and method development. It is not being presented here as an independent paper. The current purpose is to make the work visible, explain the computational strategy, and keep the method available for broader LISA waveform infrastructure and related consortium workflows.

<div class="isem-links">
  <a href="{{ '/tools/' | relative_url }}">Tools overview</a>
  <a href="{{ '/research/sasaki-nakamura-waveforms/' | relative_url }}">Sasaki-Nakamura waveform work</a>
  <a href="https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl">GeneralizedSasakiNakamura.jl</a>
  <a href="https://github.com/CuberYyc808/AdaptiveLevin.jl">AdaptiveLevin.jl</a>
</div>

## Why flux generation matters

Future space-based gravitational-wave missions such as LISA, Taiji, and TianQin will target long-duration signals from compact objects orbiting massive black holes. For EMRI modeling, fluxes are a basic ingredient: they control the slow inspiral of orbital constants and connect local orbital dynamics to observable gravitational radiation.

Frequency-domain black-hole perturbation theory is attractive because it can deliver accurate fluxes mode by mode. In practice, however, waveform production requires these calculations to be repeated many times. A useful infrastructure layer must therefore be accurate, stable, and scalable enough for large batches rather than only individual benchmark orbits.

## Why high-eccentricity and generic orbits are hard

For circular or mildly eccentric equatorial orbits, the mode content is relatively compact. High-eccentricity and generic Kerr orbits are different. Their radial and polar motion generates a much broader frequency spectrum, and the flux becomes a large sum over angular, azimuthal, radial, and polar mode labels.

The naive approach is to view the flux as a rectangular sum over all mode indices up to fixed cutoffs. That is simple, but it can waste work and obscure convergence. The physically important question is not only whether each individual mode can be computed, but how the global mode sum is organized, monitored, and truncated.

## The ISEM radial-solver layer

ISEM treats the radial Teukolsky calculation as a reusable solver layer. The goal is to produce stable homogeneous radial solutions, perform matching and transformations consistently, and construct source terms in a form suitable for repeated mode calculations.

This layer is where much of the per-mode cost lives. Improving it matters because every point in parameter space can require many radial solves. A robust radial-solver interface also makes it easier to compare related formulations, connect to Sasaki-Nakamura style methods, and separate solver accuracy from higher-level summation logic.

## Shell-aware mode summation

For eccentric and generic orbits, ISEM organizes the mode sum using shell-aware structure rather than treating every index combination as an undifferentiated rectangular grid. The idea is to group and monitor physically meaningful shells of modes, so the computation can track how different parts of the spectrum contribute to the total flux.

This does not remove the need for convergence checks. It changes the bookkeeping so convergence can be assessed at the level where high-frequency tails and truncation errors become visible. That is especially useful when different orbital regions excite very different mode distributions.

## Adaptive Levin integration for oscillatory source integrals

High-eccentricity orbits can produce source integrals with strong oscillatory behavior, particularly at high radial harmonics. Standard quadrature can then spend a large amount of work resolving oscillations directly.

ISEM connects this part of the workflow to adaptive Levin integration. The point is not to use a specialized method everywhere, but to switch to an oscillatory integration strategy where the source structure calls for it. In difficult high-frequency regimes, this can reduce wasted work while keeping the integral evaluation controlled.

## How this fits into LISA waveform infrastructure

The combined workflow has three layers. ISEM reduces the cost and fragility of each radial Teukolsky solve. Shell-aware summation controls the global cost of the mode sum. Adaptive Levin integration accelerates difficult individual source integrals. Together, these components form a practical route toward high-eccentricity and generic EMRI flux production.

The current framing is intentionally infrastructural. The method is useful as part of a larger waveform-production stack, where flux generation, geodesic dynamics, source construction, and validation need to work together. Keeping this work in that context leaves room for it to support broader LISA Consortium Waveform Working Group efforts.

## Related software and modules

- [GeneralizedSasakiNakamura.jl](https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl): Kerr perturbation tools connected to homogeneous solutions and source-driven waveform calculations.
- [KerrGeodesics.jl](https://github.com/CuberYyc808/KerrGeodesics.jl): bound Kerr geodesic infrastructure for orbital frequencies, phases, and trajectories.
- [AdaptiveLevin.jl](https://github.com/CuberYyc808/AdaptiveLevin.jl): adaptive methods for highly oscillatory integrals.
- [Tools overview]({{ '/tools/' | relative_url }}): homepage entry point for the software modules.

<div class="isem-callout">
  <strong>Status.</strong> ISEM is presented here as technical infrastructure and method development, not as an independently published paper.
</div>

