---
layout: archive
title: "Research"
permalink: /research/
author_profile: true
---

<style>
.research-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
  margin: 1.25rem 0;
}
.research-card {
  border: 1px solid #d8dee4;
  border-radius: 8px;
  background: #fff;
  overflow: hidden;
}
.research-card a {
  text-decoration: none;
}
.research-card img {
  width: 100%;
  height: 165px;
  object-fit: contain;
  display: block;
  background: #f6f8fa;
}
.research-card__body {
  padding: 0.9rem;
}
.research-card__body h2 {
  font-size: 1.05rem;
  line-height: 1.25;
  margin: 0 0 0.4rem;
}
.research-card__body p {
  color: #57606a;
  font-size: 0.88rem;
  line-height: 1.45;
  margin: 0 0 0.75rem;
}
.research-card__meta {
  color: #6e7781;
  font-size: 0.78rem;
  margin-bottom: 0.45rem;
}
.research-card__link {
  font-weight: 600;
}
</style>

<div class="research-grid">
  <article class="research-card">
    <a href="{{ '/research/near-horizon-kerr-perturbations/' | relative_url }}">
      <img src="{{ '/images/Waveform_horizon.pdf' | relative_url }}" alt="Near-horizon Kerr perturbation waveform">
    </a>
    <div class="research-card__body">
      <div class="research-card__meta">Kerr perturbation theory</div>
      <h2><a href="{{ '/research/near-horizon-kerr-perturbations/' | relative_url }}">Near-Horizon Kerr Perturbations</a></h2>
      <p>Convergent source terms for spin-weight +2 gravitational perturbations near rotating black-hole horizons.</p>
      <a class="research-card__link" href="https://arxiv.org/abs/2512.07937">Read article</a>
    </div>
  </article>

  <article class="research-card">
    <a href="{{ '/research/sasaki-nakamura-waveforms/' | relative_url }}">
      <img src="{{ '/images/waveform_bound.pdf' | relative_url }}" alt="Bound-orbit waveform computed with Sasaki-Nakamura formalism">
    </a>
    <div class="research-card__body">
      <div class="research-card__meta">EMRI waveforms</div>
      <h2><a href="{{ '/research/sasaki-nakamura-waveforms/' | relative_url }}">Sasaki-Nakamura Waveforms</a></h2>
      <p>Frequency-domain waveform and flux calculations using the short-range Sasaki-Nakamura equation.</p>
      <a class="research-card__link" href="https://arxiv.org/abs/2511.08673">Read article</a>
    </div>
  </article>

  <article class="research-card">
    <a href="{{ '/research/binary-emri-waveform-modeling/' | relative_url }}">
      <img src="{{ '/images/b-EMRI.png' | relative_url }}" alt="Binary extreme-mass-ratio inspiral system">
    </a>
    <div class="research-card__body">
      <div class="research-card__meta">Relativistic triple systems</div>
      <h2><a href="{{ '/research/binary-emri-waveform-modeling/' | relative_url }}">Binary EMRI Waveform Modeling</a></h2>
      <p>Relativistic three-body dynamics and black-hole perturbation theory for compact binaries around SMBHs.</p>
      <a class="research-card__link" href="https://arxiv.org/abs/2410.09796">Read article</a>
    </div>
  </article>
</div>
