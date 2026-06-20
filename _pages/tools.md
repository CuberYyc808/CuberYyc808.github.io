---
layout: archive
title: "Tools"
permalink: /tools/
author_profile: true
lang: en
lang_switch_url: /zh/tools/
---

<style>
.tools-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 320px), 1fr));
  gap: 1.15rem;
  margin: 1.25rem 0;
}
@media (min-width: 900px) {
  .tools-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
.tool-card {
  border: 1px solid #d8dee4;
  border-radius: 8px;
  background: var(--global-bg-color);
  padding: 1.15rem;
  display: flex;
  flex-direction: column;
  min-height: 245px;
  overflow: hidden;
}
.tool-card__head {
  display: grid;
  grid-template-columns: 68px 1fr;
  gap: 0.9rem;
  align-items: center;
  margin-bottom: 0.85rem;
}
.tool-card__head > div {
  min-width: 0;
}
.tool-card__thumb {
  width: 68px;
  height: 68px;
  object-fit: contain;
  border: 1px solid #d8dee4;
  border-radius: 8px;
  background: var(--global-thead-color);
}
.tool-card h2 {
  font-size: 1.12rem;
  line-height: 1.2;
  margin: 0;
  overflow-wrap: anywhere;
}
.tool-card__tag {
  color: var(--global-text-color-light);
  font-size: 0.8rem;
  margin-top: 0.2rem;
}
.tool-card p {
  color: var(--global-text-color-light);
  font-size: 0.92rem;
  line-height: 1.45;
  margin: 0 0 0.75rem;
}
.tool-card__links {
  display: flex;
  flex-wrap: wrap;
  gap: 0.85rem;
  margin-top: auto;
}
.tool-card__links a {
  display: inline-block;
  font-weight: 600;
}
</style>

<div class="tools-grid">
  <article class="tool-card">
    <div class="tool-card__head">
      <img class="tool-card__thumb" src="{{ '/images/waveform_bound.png' | relative_url }}" alt="Teukolsky flux thumbnail">
      <div>
        <h2>ISEM Teukolsky Flux Workflow</h2>
        <div class="tool-card__tag">EMRI flux generation</div>
      </div>
    </div>
    <p>Technical infrastructure for repeated frequency-domain Teukolsky flux calculations, combining radial solves, shell-aware mode summation, and oscillatory source integration for high-eccentricity and generic EMRI orbits.</p>
    <div class="tool-card__links">
      <a href="{{ '/blog/isem-teukolsky-flux-generation/' | relative_url }}">Technical blog</a>
      <a href="{{ '/research/sasaki-nakamura-waveforms/' | relative_url }}">Related research</a>
    </div>
  </article>

  <article class="tool-card">
    <div class="tool-card__head">
      <img class="tool-card__thumb" src="{{ '/images/waveform_bound.png' | relative_url }}" alt="Waveform thumbnail">
      <div>
        <h2>GeneralizedSasakiNakamura.jl</h2>
        <div class="tool-card__tag">Black-hole perturbation theory</div>
      </div>
    </div>
    <p>Julia tools for Kerr perturbation calculations, including homogeneous solutions and source-driven inhomogeneous workflows connected to frequency-domain waveform and flux production.</p>
    <div class="tool-card__links">
      <a href="https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl">GitHub</a>
      <a href="{{ '/blog/isem-teukolsky-flux-generation/' | relative_url }}">ISEM note</a>
    </div>
  </article>

  <article class="tool-card">
    <div class="tool-card__head">
      <img class="tool-card__thumb" src="{{ '/files/Trajectory_generic.gif' | relative_url }}" alt="Kerr trajectory thumbnail">
      <div>
        <h2>KerrGeodesics.jl</h2>
        <div class="tool-card__tag">Relativistic orbital dynamics</div>
      </div>
    </div>
    <p>Bound timelike Kerr geodesics parameterized by orbital elements, supplying orbital frequencies, phases, and trajectories for EMRI and b-EMRI waveform pipelines.</p>
    <div class="tool-card__links">
      <a href="https://github.com/CuberYyc808/KerrGeodesics.jl">GitHub</a>
      <a href="{{ '/blog/isem-teukolsky-flux-generation/' | relative_url }}">Flux workflow</a>
    </div>
  </article>

  <article class="tool-card">
    <div class="tool-card__head">
      <img class="tool-card__thumb" src="{{ '/images/Waveform_horizon.png' | relative_url }}" alt="Oscillatory signal thumbnail">
      <div>
        <h2>AdaptiveLevin.jl</h2>
        <div class="tool-card__tag">Numerical algorithms</div>
      </div>
    </div>
    <p>Adaptive Levin methods for one- and two-dimensional highly oscillatory integrals, useful when high-eccentricity source terms develop rapidly oscillating high-frequency structure.</p>
    <div class="tool-card__links">
      <a href="https://github.com/CuberYyc808/AdaptiveLevin.jl">GitHub</a>
      <a href="{{ '/blog/isem-teukolsky-flux-generation/' | relative_url }}">Method context</a>
    </div>
  </article>
</div>
