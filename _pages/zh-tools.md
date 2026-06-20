---
layout: archive
title: "工具"
permalink: /zh/tools/
author_profile: true
lang: zh
lang_switch_url: /tools/
---

<style>
.tools-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 320px), 1fr));
  gap: 1.15rem;
  margin: 1.25rem 0;
}
@media (min-width: 900px) {
  .tools-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
.tool-card {
  border: 1px solid #d8dee4;
  border-radius: 8px;
  background: var(--global-bg-color);
  padding: 1.15rem;
  display: flex;
  flex-direction: column;
  min-height: 245px;
  overflow: hidden;
  transition: border-color 160ms ease, box-shadow 160ms ease, transform 160ms ease;
}
.tool-card:hover,
.tool-card:focus-within {
  border-color: #52adc8;
  box-shadow: 0 8px 22px rgba(15, 23, 42, 0.08);
  transform: translateY(-2px);
}
.tool-card__head {
  display: grid;
  grid-template-columns: 68px 1fr;
  gap: 0.9rem;
  align-items: center;
  margin-bottom: 0.85rem;
}
.tool-card__head > div {
  min-width: 0;
}
.tool-card__thumb {
  width: 68px;
  height: 68px;
  object-fit: contain;
  border: 1px solid #d8dee4;
  border-radius: 8px;
  background: var(--global-thead-color);
}
.tool-card h2 {
  font-size: 1.12rem;
  line-height: 1.2;
  margin: 0;
  overflow-wrap: anywhere;
}
.tool-card__tag {
  color: var(--global-text-color-light);
  font-size: 0.8rem;
  margin-top: 0.2rem;
}
.tool-card p {
  color: var(--global-text-color-light);
  font-size: 0.92rem;
  line-height: 1.45;
  margin: 0 0 0.75rem;
}
.tool-card__links {
  display: flex;
  flex-wrap: wrap;
  gap: 0.85rem;
  margin-top: auto;
}
.tool-card__links a {
  display: inline-block;
  font-weight: 600;
}
</style>

<div class="tools-grid">
  <article class="tool-card" id="generalized-sasaki-nakamura">
    <div class="tool-card__head">
      <img class="tool-card__thumb" src="{{ '/images/waveform_bound.png' | relative_url }}" alt="波形缩略图">
      <div>
        <h2>GeneralizedSasakiNakamura.jl</h2>
        <div class="tool-card__tag">黑洞微扰理论</div>
      </div>
    </div>
    <p>用于 Kerr 微扰计算的 Julia 工具，包含齐次解、源项驱动的非齐次流程，并与频域波形和能流生成直接相关。</p>
    <div class="tool-card__links">
      <a href="https://github.com/ricokaloklo/GeneralizedSasakiNakamura.jl">GitHub</a>
      <a href="{{ '/zh/blog/isem-teukolsky-flux-generation/' | relative_url }}#径向求解层">径向求解说明</a>
    </div>
  </article>

  <article class="tool-card" id="kerr-geodesics">
    <div class="tool-card__head">
      <img class="tool-card__thumb" src="{{ '/files/Trajectory_generic.gif' | relative_url }}" alt="Kerr 轨道缩略图">
      <div>
        <h2>KerrGeodesics.jl</h2>
        <div class="tool-card__tag">相对论轨道动力学</div>
      </div>
    </div>
    <p>用轨道根数参数化束缚类时 Kerr 测地线，为 EMRI 与 b-EMRI 波形流程提供轨道频率、相位和轨迹。</p>
    <div class="tool-card__links">
      <a href="https://github.com/CuberYyc808/KerrGeodesics.jl">GitHub</a>
      <a href="{{ '/zh/blog/isem-teukolsky-flux-generation/' | relative_url }}#mode-怎么加在一起">Mode-sum 背景</a>
    </div>
  </article>

  <article class="tool-card" id="adaptive-levin">
    <div class="tool-card__head">
      <img class="tool-card__thumb" src="{{ '/images/Waveform_horizon.png' | relative_url }}" alt="振荡信号缩略图">
      <div>
        <h2>AdaptiveLevin.jl</h2>
        <div class="tool-card__tag">数值算法</div>
      </div>
    </div>
    <p>用于一维和二维高振荡积分的自适应 Levin 方法，可处理高偏心率源项中快速振荡的高频结构。</p>
    <div class="tool-card__links">
      <a href="https://github.com/CuberYyc808/AdaptiveLevin.jl">GitHub</a>
      <a href="{{ '/zh/blog/isem-teukolsky-flux-generation/' | relative_url }}#adaptive-levin尾部-mode-要用对积分器">方法背景</a>
    </div>
  </article>
</div>
