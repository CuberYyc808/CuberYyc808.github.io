---
layout: archive
title: "Near-Horizon Kerr Perturbations"
permalink: /research/near-horizon-kerr-perturbations/
author_profile: true
---

<div style="color:#57606a;font-size:0.9rem;margin-bottom:1rem;">
Linear gravitational perturbations of rotating black holes · <a href="https://arxiv.org/abs/2512.07937">arXiv:2512.07937</a>
</div>

<img src="{{ '/images/Waveform_horizon.png' | relative_url }}" alt="Near-horizon shear perturbation waveform" width="760"/>

This project studies the near-horizon behavior of gravitational perturbations in Kerr spacetime. The main technical point is to construct a convergent source term for the spin-weight \(s=+2\) perturbation, where the naive source representation can become difficult to evaluate stably close to the horizon.

The calculation is validated by comparing shear perturbations and fluxes for generic EMRI orbits against results obtained in the Teukolsky formalism. The agreement provides a direct check that the horizon-side formulation and the numerical implementation describe the same physical perturbation.

The implementation is part of [GeneralizedSasakiNakamura.jl](https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl).

[Back to Research]({{ '/research/' | relative_url }})
