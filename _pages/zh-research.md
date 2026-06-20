---
layout: archive
title: "研究"
permalink: /zh/research/
author_profile: true
lang: zh
lang_switch_url: /research/
---

<style>
.research-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 320px), 1fr));
  gap: 1.15rem;
  margin: 1.25rem 0;
}
@media (min-width: 900px) {
  .research-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
.research-card {
  border: 1px solid #d8dee4;
  border-radius: 8px;
  background: #fff;
  overflow: hidden;
}
.research-card a {
  text-decoration: none;
}
.research-card img {
  width: 100%;
  height: 165px;
  object-fit: contain;
  display: block;
  background: #f6f8fa;
}
.research-card__body {
  padding: 0.9rem;
}
.research-card__body h2 {
  font-size: 1.05rem;
  line-height: 1.25;
  margin: 0 0 0.4rem;
}
.research-card__body p {
  color: #57606a;
  font-size: 0.88rem;
  line-height: 1.45;
  margin: 0 0 0.75rem;
}
.research-card__meta {
  color: #6e7781;
  font-size: 0.78rem;
  margin-bottom: 0.45rem;
}
.research-card__link {
  font-weight: 600;
}
</style>

<div class="research-grid">
  <article class="research-card">
    <a href="{{ '/zh/research/near-horizon-kerr-perturbations/' | relative_url }}">
      <img src="{{ '/images/Waveform_horizon.png' | relative_url }}" alt="近视界 Kerr 微扰波形">
    </a>
    <div class="research-card__body">
      <div class="research-card__meta">Kerr 微扰理论</div>
      <h2><a href="{{ '/zh/research/near-horizon-kerr-perturbations/' | relative_url }}">近视界 Kerr 微扰</a></h2>
      <p>研究旋转黑洞视界附近自旋权重 +2 引力微扰的收敛源项构造。</p>
      <a class="research-card__link" href="https://arxiv.org/abs/2512.07937">阅读论文</a>
    </div>
  </article>

  <article class="research-card">
    <a href="{{ '/zh/research/sasaki-nakamura-waveforms/' | relative_url }}">
      <img src="{{ '/images/waveform_bound.png' | relative_url }}" alt="Sasaki-Nakamura 形式下的束缚轨道波形">
    </a>
    <div class="research-card__body">
      <div class="research-card__meta">EMRI 波形</div>
      <h2><a href="{{ '/zh/research/sasaki-nakamura-waveforms/' | relative_url }}">Sasaki-Nakamura 波形</a></h2>
      <p>基于短程 Sasaki-Nakamura 方程，在频域中计算引力波波形和能流。</p>
      <a class="research-card__link" href="https://arxiv.org/abs/2511.08673">阅读论文</a>
    </div>
  </article>

  <article class="research-card">
    <a href="{{ '/zh/research/binary-emri-waveform-modeling/' | relative_url }}">
      <img src="{{ '/images/b-EMRI.png' | relative_url }}" alt="双星极端质量比旋近系统">
    </a>
    <div class="research-card__body">
      <div class="research-card__meta">相对论三体系统</div>
      <h2><a href="{{ '/zh/research/binary-emri-waveform-modeling/' | relative_url }}">双星 EMRI 波形建模</a></h2>
      <p>结合相对论三体动力学与黑洞微扰理论，描述围绕超大质量黑洞运动的紧致双星。</p>
      <a class="research-card__link" href="https://arxiv.org/abs/2410.09796">阅读论文</a>
    </div>
  </article>
</div>
