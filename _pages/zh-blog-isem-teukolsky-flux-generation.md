---
layout: single
title: "面向偏心 EMRI 的 adiabatic (0PA) 能流生成流程"
permalink: /zh/blog/isem-teukolsky-flux-generation/
author_profile: true
lang: zh
lang_switch_url: /blog/isem-teukolsky-flux-generation/
---

<style>
:root {
  --isem-surface: #ffffff;
  --isem-surface-alt: #f8fafc;
  --isem-text: #17202a;
  --isem-muted: #475569;
  --isem-border: #d8dee4;
}
html[data-theme="dark"] {
  --isem-surface: #ffffff;
  --isem-surface-alt: #f8fafc;
  --isem-text: #111827;
  --isem-muted: #334155;
  --isem-border: #cbd5e1;
}
.isem-note {
  color: var(--global-text-color-light);
  font-size: 1rem;
  line-height: 1.55;
  margin: -0.3rem 0 1.2rem;
}
.isem-kicker {
  color: var(--global-text-color-light);
  font-size: 0.86rem;
  font-weight: 700;
  letter-spacing: 0;
  text-transform: uppercase;
  margin-bottom: 0.35rem;
}
.isem-links {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 210px), 1fr));
  gap: 0.8rem;
  margin: 1.1rem 0 1.4rem;
}
.isem-links a {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  color: var(--isem-text);
  padding: 0.75rem 0.85rem;
  text-decoration: none;
  font-weight: 600;
  background: var(--isem-surface);
  transition: border-color 160ms ease, box-shadow 160ms ease, transform 160ms ease;
}
.isem-links a:hover,
.isem-links a:focus {
  border-color: #52adc8;
  box-shadow: 0 8px 22px rgba(15, 23, 42, 0.08);
  transform: translateY(-2px);
}
.isem-diagram {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface);
  color: var(--isem-text);
  padding: 1rem;
  margin: 1.2rem 0 1.4rem;
}
.isem-figure {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface);
  color: var(--isem-text);
  margin: 1.2rem 0 1.5rem;
  overflow: hidden;
}
.isem-figure img {
  display: block;
  width: 100%;
  height: auto;
}
.isem-figure figcaption {
  color: var(--isem-muted);
  font-size: 0.84rem;
  line-height: 1.45;
  padding: 0.65rem 0.85rem 0.8rem;
}
.isem-diagram__title {
  font-weight: 700;
  margin-bottom: 0.75rem;
}
.isem-flow {
  display: grid;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  gap: 0.45rem;
  align-items: stretch;
}
.isem-flow__box {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface-alt);
  color: var(--isem-text);
  padding: 0.58rem 0.62rem;
}
.isem-flow__box strong {
  display: block;
  font-size: 0.82rem;
  margin-bottom: 0.25rem;
}
.isem-flow__box span {
  color: var(--isem-muted);
  display: block;
  font-size: 0.73rem;
  line-height: 1.32;
}
@media (max-width: 900px) {
  .isem-flow {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
@media (max-width: 560px) {
  .isem-flow {
    grid-template-columns: 1fr;
  }
}
.isem-compare {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 260px), 1fr));
  gap: 0.9rem;
  margin: 1.2rem 0 1.4rem;
}
.isem-compare__panel {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface);
  color: var(--isem-text);
  padding: 0.95rem;
}
.isem-compare__panel h3 {
  font-size: 1rem;
  margin: 0 0 0.55rem;
}
.isem-compare__panel p,
.isem-compare__panel li {
  color: var(--isem-muted);
  font-size: 0.9rem;
  line-height: 1.5;
}
.isem-callout {
  border-left: 4px solid var(--isem-muted);
  background: var(--isem-surface-alt);
  color: var(--isem-text);
  padding: 0.85rem 1rem;
  margin: 1.2rem 0;
}
.isem-steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 230px), 1fr));
  gap: 0.8rem;
  margin: 1.1rem 0 1.4rem;
}
.isem-step {
  border-top: 3px solid var(--isem-muted);
  background: var(--isem-surface);
  color: var(--isem-text);
  padding: 0.8rem 0.9rem;
}
.isem-step strong {
  display: block;
  margin-bottom: 0.3rem;
}
.isem-step p {
  margin: 0;
  color: var(--isem-muted);
  font-size: 0.92rem;
  line-height: 1.5;
}
.isem-metric {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 170px), 1fr));
  gap: 0.75rem;
  margin: 1rem 0 1.4rem;
}
.isem-metric__item {
  border: 1px solid var(--isem-border);
  border-radius: 8px;
  background: var(--isem-surface-alt);
  color: var(--isem-text);
  padding: 0.85rem;
}
.isem-metric__value {
  display: block;
  font-size: 1.35rem;
  font-weight: 700;
  line-height: 1.1;
}
.isem-metric__label {
  color: var(--isem-muted);
  display: block;
  font-size: 0.82rem;
  line-height: 1.35;
  margin-top: 0.35rem;
}
</style>

<script>
window.MathJax = {
  tex: { inlineMath: [['$', '$'], ['\\(', '\\)']], processEscapes: true },
  svg: { fontCache: 'global' }
};
</script>
<script defer src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js"></script>

<div class="isem-kicker">技术博客</div>
<p class="isem-note"><strong>这篇 note 介绍一个面向大规模频域 0PA flux generation 的实用 workflow：可复用的径向求解层、能看清尾部截断的 mode summation 顺序，以及用于高偏心率困难 mode 的 Adaptive Levin 积分。</strong></p>

做 EMRI waveform 的时候，flux 往往不是“算一次就结束”的东西。真正麻烦的是：参数点很多，mode 很多，轨道还可能高偏心、非赤道，甚至接近 Kerr 参数空间里比较难的区域。所以真正有用的问题不只是“这一个 mode 能不能算”，而是：能不能批量算很多 mode？能不能看清截断到底发生在哪里？能不能复用昂贵的数据？能不能不要把采样点浪费在追着相位振荡跑上？

这个 workflow 有三个部分。第一，径向方程用 iterative series expansion matching 方法来处理，后面简称 ISEM。第二，mode sum 的组织方式要让径向谐波 $n$ 保持为最后的 tail direction，而不是被藏在一个 rectangular grid 里。第三，对高偏心率下强振荡的 source integral，使用 Adaptive Levin 积分。

<div class="isem-links">
  <a href="{{ '/zh/tools/#generalized-sasaki-nakamura' | relative_url }}">GSN 工具卡片</a>
  <a href="{{ '/zh/tools/#kerr-geodesics' | relative_url }}">KerrGeodesics 卡片</a>
  <a href="{{ '/zh/tools/#adaptive-levin' | relative_url }}">AdaptiveLevin 卡片</a>
  <a href="{{ '/zh/research/sasaki-nakamura-waveforms/' | relative_url }}">Sasaki-Nakamura 波形工作</a>
  <a href="https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/ISEM">GSN ISEM branch</a>
</div>

<div class="isem-diagram">
  <div class="isem-diagram__title">一句话流程图</div>
  <div class="isem-flow">
    <div class="isem-flow__box"><strong>Kerr 轨道</strong><span>轨道、速度、相位</span></div>
    <div class="isem-flow__box"><strong>径向求解</strong><span>ISEM、Teukolsky 和 GSN 齐次解</span></div>
    <div class="isem-flow__box"><strong>源项积分</strong><span>普通积分或尾部 Adaptive Levin</span></div>
    <div class="isem-flow__box"><strong>Mode shells</strong><span>外层按 $\ell$、$m$、$k$ 组织；$n$ 作为径向尾部监控</span></div>
    <div class="isem-flow__box"><strong>Flux dataset</strong><span>无穷远与视界分支，并记录收敛信息</span></div>
  </div>
</div>

## Motivation：为什么要这么做

LISA、太极、天琴是空间引力波探测项目。对这些任务来说，EMRI 是一类重要的源，而 EMRI 的 0PA flux generation 不是一个小脚本问题，而是一个生产规模的数值计算问题。频域 Teukolsky 计算的优点是精确、模块化；问题是当轨道偏心率变高，并且出现进动、倾斜和 generic Kerr 轨道结构时，能量会铺到大量 $(\ell,m,k,n)$ mode 上。如果单个 mode 的计算时间不能有效降下来，完整的 flux 计算就会变成很大的计算资源开销。

我们真正关心的不只是“某一个 mode 算得快不快”，而是：哪些区域还在贡献？哪些区域已经是 tail？哪个区域该换成更适合高振荡的积分器？这就是当前实现和普通矩形循环的区别：mode sum 不是一个盲目放大的循环，而是一个需要被诊断、被记录、被控制的对象。

## 径向求解层

第一块是径向求解。这里对 radial Teukolsky equation 使用 iterative series expansion matching，后面简称 ISEM。基本思路是先处理 Teukolsky 方程的变式，然后分别从 horizon 和 infinity 做级数展开，把两个物理解分支向中间的匹配点推进。在匹配点处，通过解和径向导数的 matching 求出 matching coefficients；这些系数也就是 flux evaluation 需要的渐近振幅。最后再由匹配后的两个分支重构出整个径向解。

这一层很重要，因为每一个 mode 都要碰到 radial solve，而径向方程求解一直是 source integral calculation 里的一个 bottleneck。在当前实现里，这个构造对重复 mode production 来说大约比传统直接数值求解 GSN 方程和 MST 路径快两个数量级左右。把单个 mode 的径向求解时间降下来，是整个 0PA flux workflow 能真正跑起来的关键。

<figure class="isem-figure">
  <img src="{{ '/images/isem_matching_original_30fps.gif' | relative_url }}" alt="Iterative series expansion matching for radial Teukolsky solutions">
  <figcaption>ISEM 的径向构造思想：从 horizon 和 infinity 分别生成级数解，推进到中间匹配点，并通过函数值和径向导数进行 matching。由此得到的渐近振幅会直接进入 flux calculation。</figcaption>
</figure>

<div class="isem-steps">
  <div class="isem-step">
    <strong>齐次解</strong>
    <p>从受控的级数展开构造 horizon side 和 infinity side homogeneous radial Teukolsky solutions。</p>
  </div>
  <div class="isem-step">
    <strong>Matching coefficients</strong>
    <p>在中间点匹配解和导数，得到 flux 计算需要的渐近振幅。</p>
  </div>
  <div class="isem-step">
    <strong>Source interface</strong>
    <p>把重构后的径向解和振幅复用于 source integral 与 flux evaluation。</p>
  </div>
</div>

## Mode 怎么加在一起

接下来是 mode summation 的顺序。一个很有用的经验结构是，贡献更大的 mode 往往在角向空间里接近对角线：对固定的 $\ell$ 来说，$m=\pm \ell$ 的分支通常是比较重要的贡献。直接做 rectangular loop 并没有利用这个结构。如果固定 $\ell$，再从 $-\ell$ 到 $\ell$ 扫完整个 $m$，然后再套进很大的 $k$ 和 $n$ 范围，程序会算很多 mode 之后才看得清真正的收敛结构。

更自然的顺序是固定 $m$，然后让 $\ell$ 从 $\max(\mathrm{abs}(m),2)$ 开始往上加。这样角向收敛更容易判断。同样的想法也可以推广到 $k$ 和 $n$。$k$ 方向通常收敛更快，在这里考虑的情形里一般十个 shell 左右就可以降到很小；而径向谐波 $n$ 收敛更慢，承载高偏心率带来的长尾。因此把 $n$ 放在最后，是为了把最慢的 radial tail 暴露出来。

以前很自然的想法是：

<div class="isem-compare">
  <div class="isem-compare__panel">
    <h3>Rectangular grid 思路</h3>
    <ul>
      <li>先选一个很大的 (&ell;, m, k, n) box。</li>
      <li>即使很多条目已经很小，也会在整个 block 里继续扫。</li>
      <li>最慢的 radial tail 被混进四维矩形里，不容易判断截断。</li>
    </ul>
  </div>
  <div class="isem-compare__panel">
    <h3>Production workflow 思路</h3>
    <ul>
      <li>对每个 m，让 &ell; 从 max(abs(m), 2) 开始往上加。</li>
      <li>先处理收敛更快的 k shell。</li>
      <li>把 n 留在最后，让高偏心率截断直接可见。</li>
    </ul>
  </div>
</div>

这个顺序的实际好处是收敛更容易诊断。程序不再只是问“这个 rectangular block 够不够大”，而是可以直接报告无穷远分支和视界分支分别跑到了哪个 $n$，最后一个 shell 贡献多大，是否应该增大 $n_\mathrm{max}$。当前代码里最大的径向截断设置为 $n_\mathrm{max}=500$，对目标范围里 $e<0.9$ 的情形基本稳定。和 rectangular ordering 相比，这种按 shell 暴露尾部的顺序通常可以少算约 50% 的 mode，同时更方便判断 truncation。

<div class="isem-diagram">
  <div class="isem-diagram__title">Mode summation 流程</div>
  <div class="isem-flow">
    <div class="isem-flow__box"><strong>选 &ell; shell</strong><span>角向分辨率层</span></div>
    <div class="isem-flow__box"><strong>选 m branch</strong><span>方位角结构和频率符号</span></div>
    <div class="isem-flow__box"><strong>选 k shell</strong><span>generic 轨道的极向谐波结构</span></div>
    <div class="isem-flow__box"><strong>扫描 n tail</strong><span>径向谐波尾部；偏心率截断在这里最清楚</span></div>
    <div class="isem-flow__box"><strong>切换方法</strong><span>尾部强振荡 mode 切到 Adaptive Levin</span></div>
  </div>
</div>

最后得到的 workflow 是 $\ell \to m \to k \to n$：先角向结构，再处理较快的极向方向，最后处理最慢的径向尾部。这不只是换一个 loop order，而是把原来被四维矩形藏起来的收敛信息显式暴露出来。

## Adaptive Levin：尾部 mode 要用对积分器

第三块是 Adaptive Levin。高偏心率 mode，尤其是大的 $n$，源项积分会出现很强的振荡。普通求积方法在这种情况下会把大量采样点花在“追相位”上。以一维径向积分为例，普通采样型方法可能需要约 $2^{14}=16384$ 个径向采样点才能达到需要的收敛；Adaptive Levin 路径有效上大约到 $2048$ 这个量级就可以达到类似的收敛效果。

这个名字其实是两个部分。Adaptive 指的是区间切分是自适应的：简单区域保持较粗的切分，真正振荡困难的区域再切成更小的片段。Levin 指的是 Levin method，它处理高频振荡积分的方式不是盲目加密采样，而是把积分问题改写成一个辅助 ODE 系统；离散以后，这个 ODE 系统就变成每个小区间上的矩阵求解问题。把这两件事合在一起，代码就可以一边自动决定哪里需要细分，一边在局部使用 Levin 形式来处理振荡。

Adaptive Levin 的思路是不盲目采样振荡，而是把振荡相位放进积分策略里，并且把积分区间自适应地切成更小的片段。每个小区间上使用很小的 local grid，二维设置里通常是 $17\times17$。局部 Levin 系统的 dense solve 对每个 segment 大约按 $O(q^3)$ 缩放，这里 $q=17$；总成本随被接受的小区间数增长，而不是随一个全局膨胀的采样网格增长。对 generic 2D 积分，当前做法是在 radial 方向用 Adaptive Levin，在 $\theta$ 方向用 Clenshaw Curtis。

<div class="isem-diagram">
  <div class="isem-diagram__title">Adaptive Levin 流程</div>
  <div class="isem-flow">
    <div class="isem-flow__box"><strong>预计算轨道数据</strong><span>批量复用 geodesic sample 和相位信息</span></div>
    <div class="isem-flow__box"><strong>识别 tail mode</strong><span>大的径向谐波或困难的 generic $(n,k)$ 行</span></div>
    <div class="isem-flow__box"><strong>径向自适应</strong><span>高 $n$ 振荡主要在 radial 方向</span></div>
    <div class="isem-flow__box"><strong>theta CC</strong><span>generic 2D 积分中使用固定 polar Clenshaw Curtis 节点</span></div>
    <div class="isem-flow__box"><strong>记录元数据</strong><span>segments、depth、stop reason 和 effective intervals</span></div>
  </div>
</div>

效果很直接：困难的高 $n$ 积分不再需要和简单 mode 使用同一套强行加密采样。Radial Adaptive Levin 加固定 $\theta$ 方向的 Clenshaw Curtis，可以控制高频径向振荡，同时在 generic orbit 的二维积分里保留稳定的张量积结构。

<div class="isem-metric">
  <div class="isem-metric__item">
    <span class="isem-metric__value">8.925 ms</span>
    <span class="isem-metric__label">generic 情形下 2D convolution integral evaluation 的典型 post warm 时间</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">16.531 ms</span>
    <span class="isem-metric__label">generic 情形下 2D convolution integral 的 high $n$ modes 中，95% 可以在这个时间以内完成</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">5 ms</span>
    <span class="isem-metric__label">eccentric 情形下的 1D integral 测试中，95% 可以低于这个量级</span>
  </div>
</div>

## 相关软件与模块

- [GeneralizedSasakiNakamura.jl](https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/ISEM)：当前 ISEM 开发分支。
- [KerrGeodesics.jl](https://github.com/CuberYyc808/KerrGeodesics.jl)：用于轨道频率、相位和轨迹的束缚 Kerr 测地线基础设施。
- [AdaptiveLevin.jl](https://github.com/CuberYyc808/AdaptiveLevin.jl)：用于高振荡积分的自适应数值方法。
- [工具总览]({{ '/zh/tools/#generalized-sasaki-nakamura' | relative_url }})：主页上的相关软件入口。

<div class="isem-callout">
  <strong>欢迎试用，也欢迎反馈。</strong> 相关代码和模块已经开放，欢迎测试和使用。
</div>
