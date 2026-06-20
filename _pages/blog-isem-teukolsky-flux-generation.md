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
.isem-steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 230px), 1fr));
  gap: 0.8rem;
  margin: 1.1rem 0 1.4rem;
}
.isem-step {
  border-top: 3px solid #57606a;
  background: #fff;
  padding: 0.8rem 0.9rem;
}
.isem-step strong {
  display: block;
  margin-bottom: 0.3rem;
}
.isem-step p {
  margin: 0;
  color: #57606a;
  font-size: 0.92rem;
  line-height: 1.5;
}
</style>

<p class="isem-note"><strong>A technical note on ISEM: not a paper by itself, but the machinery that makes large batches of Teukolsky flux calculations practical.</strong></p>

In EMRI waveform work, a flux calculation is rarely a one-off exercise. One quickly ends up with many parameter points, many modes, and orbits that may be eccentric, inclined, or close to difficult regions of Kerr parameter space. ISEM is meant for that less glamorous but very real problem: making frequency-domain Teukolsky flux production stable enough to run repeatedly.

The right way to think about it is as an infrastructure layer. It sits between radial equation solvers and the higher-level flux dataset machinery: below it are radial Teukolsky and generalized Sasaki-Nakamura solves; above it are mode summation, convergence checks, and waveform-infrastructure use cases. The current development branch is in [GeneralizedSasakiNakamura.jl](https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/ISEM).

<div class="isem-links">
  <a href="{{ '/tools/' | relative_url }}">Tools overview</a>
  <a href="{{ '/research/sasaki-nakamura-waveforms/' | relative_url }}">Sasaki-Nakamura waveform work</a>
  <a href="https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/ISEM">GSN ISEM branch</a>
  <a href="https://github.com/CuberYyc808/AdaptiveLevin.jl">AdaptiveLevin.jl</a>
</div>

## What ISEM handles

In the frequency domain, Teukolsky fluxes are built mode by mode. One mode is manageable. A dataset is not. ISEM is mainly about organizing three pieces:

<div class="isem-steps">
  <div class="isem-step">
    <strong>Radial solves</strong>
    <p>Common handling for the radial Teukolsky equation and the generalized Sasaki-Nakamura equation, including homogeneous solutions, matching, and transformations.</p>
  </div>
  <div class="isem-step">
    <strong>Source integrals</strong>
    <p>Point-particle sources in a form that can be called repeatedly, with Adaptive Levin integration available for strongly oscillatory cases.</p>
  </div>
  <div class="isem-step">
    <strong>Mode summation</strong>
    <p>Shell-aware bookkeeping, so convergence is monitored by structure rather than by a single rectangular cutoff.</p>
  </div>
</div>

## Why the `Y` function matters

One useful cleanup in the ISEM branch is to make the new `Y` function an explicit interface. The point is not notation for its own sake. It gives the radial Teukolsky side, the GSN side, and the source/flux side a common variable convention.

The definition and normalization of `Y` should be read together with two related PRD projects:

- [Sasaki-Nakamura waveforms]({{ '/research/sasaki-nakamura-waveforms/' | relative_url }}), where the focus is the infinity-side waveform and flux.
- [Near-horizon Kerr perturbations]({{ '/research/near-horizon-kerr-perturbations/' | relative_url }}), where the focus is the horizon-side shear perturbation and flux.

Putting these conventions into one implementation should make later validation much less painful.

## Why not just sum everything

For high-eccentricity or generic Kerr orbits, the mode spectrum spreads out. A rectangular cutoff is easy to write down, but it often hides what is actually happening: some parts of the spectrum matter, many do not, and the tail behavior is what determines whether the final flux is trustworthy.

ISEM is organized around shell-aware summation. That makes it easier to see how contributions fall off and where truncation error is coming from. For production runs, this is just as important as being able to compute any single mode.

## Current status

Version `0.9.0` is not the finish line. It is the point where the skeleton is useful: radial solvers, source integrals, and mode bookkeeping are beginning to live in one workflow.

The next important step is validation: comparing against existing Teukolsky and Sasaki-Nakamura calculations, checking infinity and horizon fluxes, and understanding convergence across different orbit families.

## Related software and modules

- [GeneralizedSasakiNakamura.jl](https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/ISEM): current ISEM development branch.
- [KerrGeodesics.jl](https://github.com/CuberYyc808/KerrGeodesics.jl): bound Kerr geodesic infrastructure for orbital frequencies, phases, and trajectories.
- [AdaptiveLevin.jl](https://github.com/CuberYyc808/AdaptiveLevin.jl): adaptive methods for highly oscillatory integrals.
- [Tools overview]({{ '/tools/' | relative_url }}): homepage entry point for the software modules.

<div class="isem-callout">
  <strong>Short version.</strong> ISEM is a workflow for connecting radial solves, source integrals, and mode summation into Teukolsky flux production.
</div>
