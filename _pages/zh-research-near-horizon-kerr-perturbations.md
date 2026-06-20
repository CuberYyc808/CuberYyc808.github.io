---
layout: archive
title: "近视界 Kerr 微扰"
permalink: /zh/research/near-horizon-kerr-perturbations/
author_profile: true
lang: zh
lang_switch_url: /research/near-horizon-kerr-perturbations/
---

<div style="color:var(--global-text-color-light);font-size:0.9rem;margin-bottom:1rem;">
旋转黑洞的线性引力微扰 · <a href="https://arxiv.org/abs/2512.07937">arXiv:2512.07937</a>
</div>

<img src="{{ '/images/Waveform_horizon.png' | relative_url }}" alt="近视界剪切微扰波形" width="760"/>

这一项目研究 Kerr 时空中引力微扰在黑洞视界附近的行为。核心技术问题是为自旋权重 \(s=+2\) 的微扰构造收敛的源项；直接的源项表达在接近视界时可能难以稳定计算。

我们通过比较一般 EMRI 轨道的剪切微扰和能流，并与 Teukolsky 形式下得到的结果对照，验证了计算的正确性。这一符合性直接检验了视界侧形式和数值实现是否描述同一个物理微扰。

相关实现属于 [GeneralizedSasakiNakamura.jl](https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl)。

[返回研究主页]({{ '/zh/research/' | relative_url }})
