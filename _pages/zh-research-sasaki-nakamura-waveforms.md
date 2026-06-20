---
layout: archive
title: "Sasaki-Nakamura 波形"
permalink: /zh/research/sasaki-nakamura-waveforms/
author_profile: true
lang: zh
lang_switch_url: /research/sasaki-nakamura-waveforms/
---

<div style="color:#57606a;font-size:0.9rem;margin-bottom:1rem;">
无穷远处的波形与能流 · <a href="https://arxiv.org/abs/2511.08673">arXiv:2511.08673</a>
</div>

<img src="{{ '/images/waveform_bound.png' | relative_url }}" alt="Sasaki-Nakamura 形式下的束缚轨道波形" width="760"/>

Sasaki-Nakamura 形式将 Kerr 微扰问题改写为短程波动方程，因此特别适合波形计算，尤其是研究沿束缚或非束缚 Kerr 测地线运动的粒子所产生的辐射。

实际计算中的主要困难来自非齐次源项以及相应的 Green 函数积分。在这项工作中，我们使用分部积分方法绕开不稳定的源项直接求值，从而稳定地产生无穷远处的波形和能流。

这一方向连接了解析结构与数值波形生成：形式理论提供条件更好的方程，数值方法则将其转化为可用于 EMRI 辐射计算的流程。

相关实现属于 [GeneralizedSasakiNakamura.jl](https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl)。

[返回研究主页]({{ '/zh/research/' | relative_url }})
