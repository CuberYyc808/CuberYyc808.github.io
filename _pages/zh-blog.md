---
layout: single
title: "博客"
permalink: /zh/blog/
author_profile: true
lang: zh
lang_switch_url: /blog/
---

<style>
.blog-list {
  display: grid;
  gap: 1rem;
  margin-top: 1rem;
}
.blog-card {
  border: 1px solid var(--global-border-color);
  border-radius: 8px;
  padding: 1rem;
  background: var(--global-bg-color);
}
.blog-card h2 {
  font-size: 1.15rem;
  line-height: 1.25;
  margin: 0 0 0.35rem;
}
.blog-card__meta {
  color: var(--global-text-color-light);
  font-size: 0.85rem;
  margin-bottom: 0.6rem;
}
.blog-card p {
  color: var(--global-text-color-light);
  font-size: 0.95rem;
  line-height: 1.5;
  margin-bottom: 0.7rem;
}
</style>

<div class="blog-list">
  <article class="blog-card">
    <h2><a href="{{ '/zh/blog/isem-teukolsky-flux-generation/' | relative_url }}">面向偏心 EMRI 的 adiabatic (0PA) 能流生成流程</a></h2>
    <div class="blog-card__meta">2026 年 6 月 21 日</div>
    <p>关于 radial Teukolsky solves、mode summation 顺序，以及 Adaptive Levin 积分在大规模 0PA flux generation 中用法的技术说明。</p>
    <a href="{{ '/zh/blog/isem-teukolsky-flux-generation/' | relative_url }}">阅读博客</a>
  </article>
</div>
