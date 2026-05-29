---
layout: archive
title: "Research"
permalink: /research/
author_profile: true
---

<style>
.research-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1rem;
  margin: 1.5rem 0 2rem;
}
.research-card {
  border: 1px solid #d8dee4;
  border-radius: 8px;
  overflow: hidden;
  background: #fff;
}
.research-card img {
  width: 100%;
  height: 170px;
  object-fit: contain;
  background: #f6f8fa;
  display: block;
}
.research-card__body {
  padding: 0.9rem;
}
.research-card__body h2 {
  font-size: 1.05rem;
  margin: 0 0 0.35rem;
}
.research-card__body p {
  font-size: 0.88rem;
  margin: 0 0 0.7rem;
}
.research-link {
  font-weight: 600;
}
.research-article {
  margin: 2.2rem 0;
}
.research-article img {
  max-width: 100%;
  border: 1px solid #d8dee4;
  border-radius: 8px;
  background: #f6f8fa;
}
.research-meta {
  color: #57606a;
  font-size: 0.9rem;
  margin-bottom: 0.8rem;
}
</style>

<div class="research-grid">
  <article class="research-card">
    <a href="#near-horizon-kerr-perturbations"><img src="{{ '/images/Waveform_horizon.pdf' | relative_url }}" alt="Near-horizon Kerr perturbation waveform"></a>
    <div class="research-card__body">
      <h2>Near-horizon Kerr perturbations</h2>
      <p>Convergent source terms for spin-weight +2 gravitational perturbations near rotating black-hole horizons.</p>
      <a class="research-link" href="#near-horizon-kerr-perturbations">Read notes</a>
    </div>
  </article>

  <article class="research-card">
    <a href="#sasaki-nakamura-waveforms"><img src="{{ '/images/waveform_bound.pdf' | relative_url }}" alt="Bound-orbit waveform computed with Sasaki-Nakamura formalism"></a>
    <div class="research-card__body">
      <h2>Sasaki-Nakamura waveforms</h2>
      <p>Frequency-domain waveform and flux calculations for Kerr black holes using short-range SN equations.</p>
      <a class="research-link" href="#sasaki-nakamura-waveforms">Read notes</a>
    </div>
  </article>

  <article class="research-card">
    <a href="#binary-emri-waveform-modeling"><img src="{{ '/images/b-EMRI.png' | relative_url }}" alt="Binary extreme-mass-ratio inspiral system"></a>
    <div class="research-card__body">
      <h2>Binary EMRI modeling</h2>
      <p>Relativistic three-body dynamics and black-hole perturbation theory for b-EMRI gravitational radiation.</p>
      <a class="research-link" href="#binary-emri-waveform-modeling">Read notes</a>
    </div>
  </article>
</div>

## Near-Horizon Kerr Perturbations
{: #near-horizon-kerr-perturbations .research-article}

<div class="research-meta">Linear gravitational perturbations of rotating black holes · <a href="https://arxiv.org/abs/2512.07937">arXiv:2512.07937</a></div>

<img src="{{ '/images/Waveform_horizon.pdf' | relative_url }}" alt="Near-horizon shear perturbation waveform" width="700"/>

This project studies the near-horizon behavior of gravitational perturbations in Kerr spacetime. The main technical point is to construct a convergent source term for the spin-weight \(s=+2\) perturbation, where the naive source representation can become difficult to evaluate stably close to the horizon.

The calculation is validated by comparing shear perturbations and fluxes for generic EMRI orbits against results obtained in the Teukolsky formalism. The agreement provides a direct check that the horizon-side formulation and the numerical implementation are describing the same physical perturbation.

Code implementation: [GeneralizedSasakiNakamura.jl](https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl).

## Sasaki-Nakamura Waveforms
{: #sasaki-nakamura-waveforms .research-article}

<div class="research-meta">Waveforms and fluxes at infinity · <a href="https://arxiv.org/abs/2511.08673">arXiv:2511.08673</a></div>

<img src="{{ '/images/waveform_bound.pdf' | relative_url }}" alt="Bound-orbit waveform from Sasaki-Nakamura formalism" width="700"/>

The Sasaki-Nakamura formalism rewrites the Kerr perturbation problem into a short-range wave equation. This makes it useful for waveform calculations, especially when one wants to evaluate radiation sourced by particles moving on bound or unbound Kerr geodesics.

The practical obstacle is the inhomogeneous source term and the associated Green's-function integral. In this work, the integration-by-parts method is used to avoid problematic source evaluations and produce stable waveforms and fluxes at infinity.

This direction connects analytic structure and numerical waveform generation: the formalism supplies a better-conditioned equation, while the numerical method turns it into a usable pipeline for EMRI radiation.

Code implementation: [GeneralizedSasakiNakamura.jl](https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl).

## Binary EMRI Waveform Modeling
{: #binary-emri-waveform-modeling .research-article}

<div class="research-meta">Relativistic triple systems and black-hole perturbation theory · <a href="https://arxiv.org/abs/2410.09796">arXiv:2410.09796</a></div>

<img src="{{ '/images/b-EMRI.png' | relative_url }}" alt="Binary extreme-mass-ratio inspiral diagram" width="700"/>

Binary extreme-mass-ratio inspirals are hierarchical triple systems: a supermassive black hole is orbited by a compact binary whose total mass is much smaller than the central object. Their radiation carries signatures from both the relativistic motion around the massive black hole and the internal motion of the small binary.

The waveform model combines relativistic three-body dynamics with black-hole perturbation theory. One interesting feature is that the small binary can resonantly excite quasi-normal modes of the central black hole, producing structure that is not present in ordinary single-body EMRIs.

<img src="{{ '/images/QNM_excitation_bEMRI.png' | relative_url }}" alt="Quasi-normal mode excitation in binary EMRI waveform" width="700"/>
