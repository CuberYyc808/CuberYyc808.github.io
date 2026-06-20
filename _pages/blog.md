---
layout: single
title: "Blog"
permalink: /blog/
author_profile: true
lang: en
lang_switch_url: /zh/blog/
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
    <h2><a href="{{ '/blog/isem-teukolsky-flux-generation/' | relative_url }}">A practical adiabatic (0PA) flux workflow for eccentric EMRIs</a></h2>
    <div class="blog-card__meta">June 21, 2026</div>
    <p>A technical note on radial Teukolsky solves, mode summation order, and Adaptive Levin integration for large scale 0PA flux generation.</p>
    <a href="{{ '/blog/isem-teukolsky-flux-generation/' | relative_url }}">Read blog</a>
  </article>
</div>
