---
layout: archive
title: "Sasaki-Nakamura Waveforms"
permalink: /research/sasaki-nakamura-waveforms/
author_profile: true
lang: en
lang_switch_url: /zh/research/sasaki-nakamura-waveforms/
---

<style>
.research-note {
  color: var(--global-text-color-light);
  font-size: 0.95rem;
  line-height: 1.55;
}
.research-points {
  margin: 1rem 0 1.2rem;
}
.research-points li {
  margin-bottom: 0.45rem;
}
</style>

<div class="research-note" style="margin-bottom:1rem;">
Waveforms and fluxes at infinity · <a href="https://arxiv.org/abs/2511.08673">arXiv:2511.08673</a>
</div>

<img src="{{ '/images/waveform_bound.png' | relative_url }}" alt="Bound-orbit waveform from Sasaki-Nakamura formalism" width="760"/>

This work turns the Sasaki-Nakamura formalism into a usable frequency-domain pipeline for gravitational radiation from Kerr black holes. The formalism is attractive because it replaces the long-range Teukolsky radial equation with a short-range equation, but source-driven waveform calculations still require careful treatment of inhomogeneous terms and Green-function integrals.

The main ingredients are:

- a source treatment based on integration by parts, avoiding unstable direct evaluations of the distributional source;
- frequency-domain waveforms and fluxes at infinity for particles on Kerr geodesics;
- a consistent connection between the Sasaki-Nakamura variable, the Teukolsky radiation field, and the `Y` convention used in the broader GSN code.

The result is a stable way to compute infinity-side radiation with the Sasaki-Nakamura equation. It also gives one half of the validation picture for ISEM: the infinity flux here can be compared against the horizon-side quantities in the near-horizon work.

The implementation is part of [GeneralizedSasakiNakamura.jl](https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl).

[Back to Research]({{ '/research/' | relative_url }})
