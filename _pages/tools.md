---
layout: archive
title: "Tools"
permalink: /tools/
author_profile: true
---

<style>
.tool-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1rem;
  margin: 1.5rem 0 2rem;
}
.tool-card {
  border: 1px solid #d8dee4;
  border-radius: 8px;
  background: #fff;
  overflow: hidden;
}
.tool-card img {
  width: 100%;
  height: 170px;
  object-fit: contain;
  background: #f6f8fa;
  display: block;
}
.tool-card__body {
  padding: 0.9rem;
}
.tool-card__body h2 {
  font-size: 1.05rem;
  margin: 0 0 0.35rem;
}
.tool-card__body p {
  font-size: 0.88rem;
  margin: 0 0 0.7rem;
}
.tool-section {
  margin: 2.2rem 0;
}
.tool-meta {
  color: #57606a;
  font-size: 0.9rem;
  margin-bottom: 0.8rem;
}
.tool-example {
  font-size: 0.82rem;
}
</style>

<div class="tool-grid">
  <article class="tool-card">
    <a href="#generalized-sasaki-nakamura"><img src="{{ '/images/waveform_bound.pdf' | relative_url }}" alt="Waveform generated from black-hole perturbation equations"></a>
    <div class="tool-card__body">
      <h2>GeneralizedSasakiNakamura.jl</h2>
      <p>Numerical toolkit for metric and curvature perturbations in Kerr spacetime.</p>
      <a href="#generalized-sasaki-nakamura">Usage notes</a>
    </div>
  </article>

  <article class="tool-card">
    <a href="#kerr-geodesics"><img src="{{ '/files/Trajectory_generic.gif' | relative_url }}" alt="Generic Kerr geodesic trajectory"></a>
    <div class="tool-card__body">
      <h2>KerrGeodesics.jl</h2>
      <p>Bound timelike Kerr geodesics parameterized by orbital elements.</p>
      <a href="#kerr-geodesics">Usage notes</a>
    </div>
  </article>

  <article class="tool-card">
    <a href="#adaptive-levin"><img src="{{ '/images/Waveform_horizon.pdf' | relative_url }}" alt="Oscillatory numerical signal"></a>
    <div class="tool-card__body">
      <h2>AdaptiveLevin.jl</h2>
      <p>Adaptive Levin algorithms for one- and two-dimensional oscillatory integrals.</p>
      <a href="#adaptive-levin">Usage notes</a>
    </div>
  </article>
</div>

## Black-Hole Perturbation Theory

### GeneralizedSasakiNakamura.jl
{: #generalized-sasaki-nakamura .tool-section}

<div class="tool-meta"><a href="https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl">GitHub repository</a> · Julia · Kerr perturbation equations</div>

[GeneralizedSasakiNakamura.jl](https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl) solves linear metric and curvature perturbations in Kerr spacetime. I developed the inhomogeneous module used for source-driven perturbations. The project was founded by [Rico K. L. Lo](https://ricokaloklo.github.io).

Typical use cases include:

- homogeneous and inhomogeneous radial solutions;
- waveform and flux calculations for point-particle sources;
- checks between Sasaki-Nakamura and Teukolsky-based calculations.

```julia
using GeneralizedSasakiNakamura

# Sketch of the workflow:
# 1. choose orbital parameters and mode labels
# 2. build the source term
# 3. solve the radial equation
# 4. evaluate waveform amplitudes and fluxes
```

### KerrGeodesics.jl
{: #kerr-geodesics .tool-section}

<div class="tool-meta"><a href="https://github.com/CuberYyc808/KerrGeodesics.jl">GitHub repository</a> · Julia · relativistic orbital dynamics</div>

[KerrGeodesics.jl](https://github.com/CuberYyc808/KerrGeodesics.jl) computes timelike bound geodesic motion around a Kerr black hole. The package is designed around orbital-element parameterizations and elliptic-function structure, which makes it useful for EMRI and b-EMRI waveform pipelines.

<img src="{{ '/files/Trajectory_generic.gif' | relative_url }}" alt="Generic bound Kerr geodesic trajectory" width="700"/>

Example workflow:

```julia
using KerrGeodesics

# Sketch of the workflow:
# orbit = KerrOrbit(a, p, e, x)
# trajectory = sample_trajectory(orbit, time_grid)
# constants = constants_of_motion(orbit)
```

## Numerical Algorithms

### AdaptiveLevin.jl
{: #adaptive-levin .tool-section}

<div class="tool-meta"><a href="https://github.com/CuberYyc808/AdaptiveLevin.jl">GitHub repository</a> · Julia · oscillatory quadrature</div>

[AdaptiveLevin.jl](https://github.com/CuberYyc808/AdaptiveLevin.jl) implements adaptive Levin methods for highly oscillatory one- and two-dimensional integrals. This is an algorithmic tool rather than a high-performance-computing platform: the focus is stable and efficient numerical quadrature for integrands where standard adaptive integration can waste many samples resolving rapid phase oscillations.

Example workflow:

```julia
using AdaptiveLevin

# Sketch of the workflow:
# f(x) is a slowly varying amplitude
# phi(x) is a rapidly varying phase
# integral = levin_integrate(f, phi, domain)
```

In gravitational-wave calculations, this kind of algorithm is useful when Green's-function integrals or source terms contain rapidly oscillating phases. The goal is to exploit the phase structure directly instead of brute-force sampling every oscillation.
