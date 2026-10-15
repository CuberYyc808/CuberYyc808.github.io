---
layout: single
title: "通用 EMRI 的绝热阶（0PA）通量计算流程"
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
<p class="isem-note"><strong>GeneralizedSasakiNakamura.jl 怎样把一条 Kerr 测地线变成 Teukolsky 总通量，以及速度从哪里来。</strong></p>

### 一句话流程

<div class="isem-diagram">
  <div class="isem-flow">
    <div class="isem-flow__box"><strong>轨道与采样</strong><span>$(a, p, e, x)$ → 测地线采样</span></div>
    <div class="isem-flow__box"><strong>每个模式</strong><span>一次 GSN-ISEM 径向求解 + 一个球状谐函数</span></div>
    <div class="isem-flow__box"><strong>源积分</strong><span>振幅 $Z$ → $\lvert Z\rvert^2$</span></div>
    <div class="isem-flow__box"><strong>模式求和</strong><span>$\ell \to m \to k \to n$</span></div>
    <div class="isem-flow__box"><strong>通量</strong><span>无穷远和视界处</span></div>
  </div>
</div>

这些都包在一个函数里：

```julia
using GeneralizedSasakiNakamura
flux = Teukolsky_pointparticle_flux(a, p, e, x; tol = 1e-8)
```

它返回能量、角动量和 Carter 常数三种通量，无穷远和视界分开给出。

### 动机

LISA、太极、天琴这类空间探测器会对极端质量比旋近（EMRI）连续观测数月到数年。要在绝热阶建模，需要在 (a, p, e, x) 的密集网格上算轨道平均通量，而每个通量都是对 (ℓ, m, k, n) 标记的 Teukolsky 模式求和。一条既偏心又倾斜的通用轨道，模式数很容易上百万。所以通量网格算不算得动，取决于两件事：一个模式要多少时间，以及实际需要算多少个模式。下面分别讲。

### 轨道采样

测地线由 KerrGeodesics.jl 给出，每条轨道只算一次。采样用的是 Mino 时间下的径向相位 $q_r = \Upsilon_r \lambda + q_{r,0}$ 和极向相位 $q_\theta = \Upsilon_\theta \lambda + q_{\theta,0}$。每个节点上存 $r$、$r_*$、$\theta$、$t$ 和 $\phi$ 的振荡部分，以及速度 $\Sigma u^r$、$\Sigma u^\theta$。

有两处设计让采样很便宜。

- **只取半个周期。** 每个相位只需要 $[0, \pi]$。往返运动的另一半是同一条路径，只是 $u^r \to -u^r$（或 $u^\theta \to -u^\theta$），在被积函数里体现为符号翻转，不需要新的采样点。
- **一张稠密的母网格。** 每条轨道只建一张均匀网格，取允许的最高分辨率：径向 $2^{14}+1$ 个点，极向 $2^{12}+1$ 个点。所有更粗的网格都是它的等间隔抽取。网格是嵌套的，所以某个模式加密时不用重新计算轨迹，只是多读一部分母网格。

### 径向求解器

每个模式都有自己的频率 $\omega = (m\Upsilon_\phi + n\Upsilon_r + k\Upsilon_\theta)/\Gamma$，所以每个模式都要重新求一次齐次径向解。多数代码的时间都花在这里，GSN-ISEM 解决的正是这一步。

GSN-ISEM 不解 Teukolsky 方程，而是直接解广义 Sasaki–Nakamura 方程，在紧致坐标 $x = (r - r_+)/(r - r_-) \in (0, 1)$ 上工作：

- **边界处起步。** 视界处用 Frobenius 级数，无穷远处用渐近级数，分别给出边界行为正确的 IN 解和 UP 解。
- **向内延拓。** 两边的解各自通过常点处的 Taylor 展开片段往里推。递推系数事先生成为有理系数表，所以构造一个片段只是一段固定长度的递推。
- **匹配。** 两边在内部某一点相遇，在那里匹配函数值和导数，得到入射和反射振幅，也就确定了这个模式的归一化。

整个过程里没有自适应的 ODE 积分。一次完整求解是固定量的多项式运算，大约一毫秒。之后在任意半径上求值，就是对某个片段做一次多项式求值。同一个求解器也能处理复频率（把积分路径转到复平面上），程序包里的 `qnm` 就建立在这上面。

下面的演示是求解器实时运行的样子，每一帧都是一次新的求解加上求值：

<p align="center"><img src="{{ '/images/isem_realtime_demo_30s.gif' | relative_url }}" width="80%" alt="每一帧重新求解并求值的 GSN-ISEM 径向函数"></p>

*图注：GSN-ISEM 现场求解并计算径向函数。*

### 极向部分

角向函数来自 SpinWeightedSpheroidalHarmonics.jl，每个模式一个谐函数对象。每个极向节点上需要 $S$ 和 $S^\prime$，二阶导 $S^{\prime\prime}$ 直接由球状方程得到，不单独求值。赤道轨道只需要 $\theta = \pi/2$ 一处的谐函数值，这也是它每个模式更便宜的原因之一。

### 两部分怎么组合

每个模式的振幅 $Z$ 是沿轨道的源积分，再除以径向解的入射振幅做归一化。被积函数由径向解、球状谐函数、轨道速度和相位因子 $e^{i(\omega \Delta t - m \Delta \phi + \dots)}$ 组成。

- **赤道圆轨道**不需要积分。
- **倾斜圆轨道**只需要 $r = p$ 一处的径向解，加上对 $q_\theta$ 的一维积分。
- **赤道偏心轨道**是对 $q_r$ 的一维积分，谐函数只取一个角度。
- **通用轨道**是对 $(q_r, q_\theta)$ 的二维积分。

二维积分不能拆成径向乘极向，因为 $\rho = -1/(r - ia\cos\theta)$ 把 $r$ 和 $\theta$ 耦合在一起。所以求和要遍历全部 $N \times K$ 个节点，但能预先算的都预先算好：

- 和 $\rho$ 有关的表按网格尺寸只建一次，这条轨道的所有模式共用；
- 只依赖 $r$ 的因子每行算一次，只依赖 $\theta$ 的因子每列算一次；
- 相位因子是一个径向向量和一个极向向量的外积。

所有积分都是均匀相位网格上的梯形求和。对光滑周期函数，梯形法收敛非常快，而且每个模式可以在嵌套网格上自适应加密：

1. 径向从 $N = 64$ 个区间开始。极向从 $K = 16$ 开始，并提高到足以分辨 $\ell + \lvert k\rvert$。
2. 把 $N$ 加倍。只在新节点上求值，旧的部分和直接作为新和的一半。
3. 默认容差下，相对变化低于约 $3\times 10^{-4}$ 就停，但网格不能小于一个随 $\lvert n\rvert$ 增大的下限。只有结果看起来可疑时 $K$ 才加倍。

网格很大时，在每个新节点上求径向解会成为主要开销。这时代码改为先建一张径向解的 Chebyshev 表（几百个点，用直接求值核对到 $10^{-10}$），再从表里插值。

有了 $Z$，通量就直接得到。无穷远处 $\dot E = \lvert Z\rvert^2/(4\pi\omega^2)$，$\dot L = m\lvert Z\rvert^2/(4\pi\omega^3)$；视界处同一个 $\lvert Z\rvert^2$ 乘上视界因子。Carter 通量还要额外做一次极向平均。

### 模式怎么加起来

在 (ℓ, m, k, n) 上铺长方体网格是最直接的做法，也最浪费：在我们关心的容差下，盒子里大部分模式没有贡献。实际的求和从通量真正集中的地方往外走。

- **先用对称性。** 一个模式和它的 $(\ell, -m, -n, -k)$ 伙伴贡献相同，所以只算一半的指标空间，每个模式计两次。
- **嵌套顺序。** 对每个径向壳层 $n$，循环 $k$，再循环 $m$，最内层沿 $\ell$ 走。
- **从峰值出发。** $k \neq 0$ 时，$\ell$ 从 $\lvert m \pm k\rvert$ 附近开始，那里模式最大，然后往上和往下走。
- **小了就停。** $\ell$ 方向连续几个模式低于阈值就停；某个模式远低于阈值时立刻停。仍在增长的 $m$ 壳层不计入停止条件。$n$ 的尾巴在连续几个壳层都低于 `tol` 乘当前总和时停止，代码会拟合壳层大小，预估大致在哪里停。
- **两个分支。** 无穷远和视界各自维护总和和阈值，所以小得多的视界通量也能达到同样的相对精度。

对偏心率很高的轨道，代码在高 $n$ 尾部还提供径向的自适应 Levin 积分，用 `tail_levin = true` 打开。下面的例子全程用的是梯形法。

### 耗时

四个例子都取 $a = 0.9$、$p = 6$、`tol = 1e-8`，单线程，预热后计时。

| 轨道 | e | x | 模式数 | 耗时 | 每个模式 |
|---|---|---|---:|---:|---:|
| 赤道圆轨道 | 0 | 1 | 378 | 0.34 s | 0.89 ms |
| 倾斜圆轨道 | 0 | 0.5 | 11 466 | 10.3 s | 0.90 ms |
| 赤道偏心 | 0.7 | 1 | 45 204 | 26.1 s | 0.58 ms |
| 通用 | 0.7 | 0.5 | 1 319 722 | 21.8 min | 0.99 ms |

所有情况下，每个模式的耗时都接近一次径向求解的耗时，积分和求和带来的额外开销很小。这来自嵌套网格、按轨道共享的预计算表和径向插值表。赤道偏心轨道每个模式最便宜，因为谐函数只取一个角度，积分也是一维的。

<div class="isem-metric">
  <div class="isem-metric__item">
    <span class="isem-metric__value">~1 ms</span>
    <span class="isem-metric__label">一次 GSN-ISEM 径向求解</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">0.58 ms</span>
    <span class="isem-metric__label">每个模式，赤道偏心轨道（e = 0.7）</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">0.99 ms</span>
    <span class="isem-metric__label">每个模式，通用轨道（e = 0.7，x = 0.5）</span>
  </div>
  <div class="isem-metric__item">
    <span class="isem-metric__value">1.32 M modes in 21.8 min</span>
    <span class="isem-metric__label">通用轨道总通量，单线程</span>
  </div>
</div>

### 多条轨道一起算

径向求解、单模式和总通量的调用都是线程安全的，串行和多线程得到的数完全一样。因此通量网格可以直接分到多个线程上算。Julia 用 `--threads=auto` 启动，并设置 `BLAS.set_num_threads(1)`。

如果几次调用针对同一条轨道，可以放进一个 submission，共享轨迹、母网格和预计算表：

```julia
modes = with_pointparticle_submission(0.9, 10.0, 0.2, 0.3) do submission
    tasks = [spawn_pointparticle_submission!(submission) do
                 Teukolsky_pointparticle_mode(-2, 2, 2, n, 0, 0.9, 10.0, 0.2, 0.3; submission)
             end for n in 0:2]
    fetch.(tasks)
end
```

### 相关软件与模块

<div class="isem-links isem-compare">
  <a href="https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/claude/project-thread-s9q61h">GSN 代码</a>
  <a href="{{ '/zh/tools/#generalized-sasaki-nakamura' | relative_url }}">GSN 工具卡片</a>
  <a href="{{ '/zh/tools/#kerr-geodesics' | relative_url }}">KerrGeodesics 卡片</a>
  <a href="{{ '/zh/research/sasaki-nakamura-waveforms/' | relative_url }}">Sasaki-Nakamura 波形工作</a>
</div>

- [GeneralizedSasakiNakamura.jl](https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/claude/project-thread-s9q61h)，径向求解器和通量流程。
- [KerrGeodesics.jl](https://github.com/CuberYyc808/KerrGeodesics.jl)，测地线轨道。
- SpinWeightedSpheroidalHarmonics.jl，角向函数。
