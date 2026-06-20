---
permalink: /zh/
title: "关于我"
author_profile: true
lang: zh
lang_switch_url: /
---

我现在在 [Niels Bohr Institute](https://www.nbi.ku.dk/english/) 的 [Strong Group](https://strong-gr.com) 做 Visiting Fellow。此前我在[北京大学物理学院](https://www.phy.pku.edu.cn)读本科，2025 年 7 月毕业。

我主要做 black hole perturbation theory，以及它在 gravitational-wave modeling 里的应用。最近比较关心 EMRI / b-EMRI 波形、black-hole quasi-normal modes，以及黑洞对 gravitational waves 的散射。

邮箱：cuber.ycyin@gmail.com

<style>
.news-list {
  margin-top: 1.2rem;
}
.news-item {
  display: grid;
  grid-template-columns: 7.2rem 1fr;
  gap: 1rem;
  padding: 0.9rem 0;
  border-top: 1px solid #d8dee4;
}
.news-date {
  color: var(--global-text-color-light);
  font-size: 0.86rem;
  font-weight: 600;
}
.news-item h3 {
  font-size: 1rem;
  margin: 0 0 0.25rem;
}
.news-item p {
  margin: 0;
  color: var(--global-text-color-light);
  font-size: 0.92rem;
  line-height: 1.55;
}
@media (max-width: 620px) {
  .news-item {
    grid-template-columns: 1fr;
    gap: 0.25rem;
  }
}
</style>

## Recent News

<div class="news-list">
  <div class="news-item">
    <div class="news-date">2026 年 6 月 21 日</div>
    <div>
      <h3>第一篇技术博客更新。</h3>
      <p>关于 <a href="{{ '/zh/blog/isem-teukolsky-flux-generation/' | relative_url }}">adiabatic (0PA) flux workflow</a> 的博客已经上线。</p>
    </div>
  </div>
  <div class="news-item">
    <div class="news-date">2026 年 6 月</div>
    <div>
      <h3>GSN <code>0.9.0</code> 的 ISEM 分支基本就位。</h3>
      <p><a href="https://github.com/CuberYyc808/GeneralizedSasakiNakamura.jl/tree/ISEM">GeneralizedSasakiNakamura.jl</a> 里加入了 ISEM 相关的基础设施，用来做 Teukolsky point-particle flux 的 mode summation。这里面包括 radial Teukolsky equation、generalized Sasaki-Nakamura equation，以及新的 <code>Y</code> 变量约定；<code>Y</code> 的定义和用法可以和两篇 PRD 工作一起看：<a href="{{ '/zh/research/sasaki-nakamura-waveforms/' | relative_url }}">Sasaki-Nakamura waveforms</a> 与 <a href="{{ '/zh/research/near-horizon-kerr-perturbations/' | relative_url }}">near-horizon Kerr perturbations</a>。</p>
    </div>
  </div>
  <div class="news-item">
    <div class="news-date">2026 年 6 月</div>
    <div>
      <h3>KerrGeodesics.jl <code>0.3.0</code> 支持 plunge orbits。</h3>
      <p>除了 bound Kerr geodesics，现在也可以生成 plunge 轨道了，后面可以直接接到 waveform / flux pipeline 里。</p>
    </div>
  </div>
  <div class="news-item">
    <div class="news-date">2026 年 4 月</div>
    <div>
      <h3>Sasaki-Nakamura waveform 那篇被 PRD 接收。</h3>
      <p>*Gravitational Radiation from Kerr Black Holes using the Sasaki-Nakamura Formalism* 于 2026 年 4 月 27 日被 *Physical Review D* 接收。</p>
    </div>
  </div>
  <div class="news-item">
    <div class="news-date">2026 年 3 月</div>
    <div>
      <h3>Near-horizon Kerr perturbation 那篇被 PRD 接收。</h3>
      <p>*Near-Horizon Perturbations of Rotating Black Holes* 于 2026 年 3 月 10 日被 *Physical Review D* 接收。</p>
    </div>
  </div>
</div>
