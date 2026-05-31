---
layout: archive
title: "Sasaki-Nakamura Waveforms"
permalink: /research/sasaki-nakamura-waveforms/
author_profile: true
---

<div style="color:#57606a;font-size:0.9rem;margin-bottom:1rem;">
Waveforms and fluxes at infinity · <a href="https://arxiv.org/abs/2511.08673">arXiv:2511.08673</a>
</div>

<img src="{{ '/images/waveform_bound.pdf' | relative_url }}" alt="Bound-orbit waveform from Sasaki-Nakamura formalism" width="760"/>

The Sasaki-Nakamura formalism rewrites the Kerr perturbation problem into a short-range wave equation. This makes it useful for waveform calculations, especially when one wants to evaluate radiation sourced by particles moving on bound or unbound Kerr geodesics.

The practical obstacle is the inhomogeneous source term and the associated Green's-function integral. In this work, the integration-by-parts method is used to avoid problematic source evaluations and produce stable waveforms and fluxes at infinity.

This direction connects analytic structure and numerical waveform generation: the formalism supplies a better-conditioned equation, while the numerical method turns it into a usable pipeline for EMRI radiation.

The implementation is part of [GeneralizedSasakiNakamura.jl](https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl).

[Back to Research]({{ '/research/' | relative_url }})
