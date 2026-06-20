---
layout: archive
title: "Near-Horizon Kerr Perturbations"
permalink: /research/near-horizon-kerr-perturbations/
author_profile: true
lang: en
lang_switch_url: /zh/research/near-horizon-kerr-perturbations/
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
Linear gravitational perturbations of rotating black holes · <a href="https://arxiv.org/abs/2512.07937">arXiv:2512.07937</a>
</div>

<img src="{{ '/images/Waveform_horizon.png' | relative_url }}" alt="Near-horizon shear perturbation waveform" width="760"/>

This work builds a horizon-side formulation for gravitational perturbations of rotating black holes. The key problem is practical as much as formal: the spin-weight \(s=+2\) source term is the natural object near the horizon, but its direct expression is hard to evaluate stably for generic EMRI orbits. We reorganize the source into a convergent form and use it to compute shear perturbations and horizon fluxes.

In short, the project does three things:

- constructs a numerically stable source for near-horizon \(s=+2\) Kerr perturbations;
- computes the corresponding shear perturbation and flux for generic orbits;
- checks the result against the Teukolsky calculation, so the horizon-side and infinity-side descriptions are tied to the same physical perturbation.

The conclusion is that the near-horizon formulation is not just a formal rewriting. It gives a stable numerical route to horizon observables, and it also fixes conventions that are useful for the shared `Y` variable used in the Generalized Sasaki-Nakamura infrastructure.

The implementation is part of [GeneralizedSasakiNakamura.jl](https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl).

[Back to Research]({{ '/research/' | relative_url }})
