---
layout: archive
title: "Tools"
permalink: /tools/
author_profile: true
---

<style>
.tools-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(235px, 1fr));
  gap: 1rem;
  margin: 1.25rem 0;
}
.tool-card {
  border: 1px solid #d8dee4;
  border-radius: 8px;
  background: #fff;
  padding: 0.95rem;
  display: flex;
  flex-direction: column;
  min-height: 210px;
}
.tool-card__head {
  display: grid;
  grid-template-columns: 52px 1fr;
  gap: 0.75rem;
  align-items: center;
  margin-bottom: 0.65rem;
}
.tool-card__thumb {
  width: 52px;
  height: 52px;
  object-fit: contain;
  border: 1px solid #d8dee4;
  border-radius: 8px;
  background: #f6f8fa;
}
.tool-card h2 {
  font-size: 1.02rem;
  line-height: 1.2;
  margin: 0;
}
.tool-card__tag {
  color: #6e7781;
  font-size: 0.78rem;
  margin-top: 0.2rem;
}
.tool-card p {
  color: #57606a;
  font-size: 0.88rem;
  line-height: 1.45;
  margin: 0 0 0.75rem;
}
.tool-card__links a {
  display: inline-block;
  font-weight: 600;
  margin-top: auto;
}
</style>

<div class="tools-grid">
  <article class="tool-card">
    <div class="tool-card__head">
      <img class="tool-card__thumb" src="{{ '/images/waveform_bound.png' | relative_url }}" alt="Waveform thumbnail">
      <div>
        <h2>GeneralizedSasakiNakamura.jl</h2>
        <div class="tool-card__tag">Black-hole perturbation theory</div>
      </div>
    </div>
    <p>Julia tools for metric and curvature perturbations in Kerr spacetime, including source-driven inhomogeneous calculations.</p>
    <div class="tool-card__links"><a href="https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl">GitHub</a></div>
  </article>

  <article class="tool-card">
    <div class="tool-card__head">
      <img class="tool-card__thumb" src="{{ '/files/Trajectory_generic.gif' | relative_url }}" alt="Kerr trajectory thumbnail">
      <div>
        <h2>KerrGeodesics.jl</h2>
        <div class="tool-card__tag">Relativistic orbital dynamics</div>
      </div>
    </div>
    <p>Bound timelike Kerr geodesics parameterized by orbital elements, useful for EMRI and b-EMRI waveform pipelines.</p>
    <div class="tool-card__links"><a href="https://github.com/CuberYyc808/KerrGeodesics.jl">GitHub</a></div>
  </article>

  <article class="tool-card">
    <div class="tool-card__head">
      <img class="tool-card__thumb" src="{{ '/images/Waveform_horizon.png' | relative_url }}" alt="Oscillatory signal thumbnail">
      <div>
        <h2>AdaptiveLevin.jl</h2>
        <div class="tool-card__tag">Numerical algorithms</div>
      </div>
    </div>
    <p>Adaptive Levin methods for one- and two-dimensional highly oscillatory integrals.</p>
    <div class="tool-card__links"><a href="https://github.com/CuberYyc808/AdaptiveLevin.jl">GitHub</a></div>
  </article>
</div>
