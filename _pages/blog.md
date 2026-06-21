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
  transition: border-color 160ms ease, box-shadow 160ms ease, transform 160ms ease;
}
.blog-card:hover,
.blog-card:focus-within {
  border-color: #52adc8;
  box-shadow: 0 8px 22px rgba(15, 23, 42, 0.08);
  transform: translateY(-2px);
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
.blog-card__links {
  display: flex;
  flex-wrap: wrap;
  gap: 0.85rem;
}
.blog-intro {
  color: var(--global-text-color-light);
  font-size: 0.98rem;
  line-height: 1.6;
  max-width: 760px;
  margin: 0.2rem 0 1.2rem;
}
</style>

<p class="blog-intro">This page collects technical notes and small ideas that come up during my research. Some of them are useful enough to share, but not necessarily complete enough to become standalone papers. I use this space to record the context, method, and implementation details in a more informal way.</p>

<div class="blog-list">
  <article class="blog-card">
    <h2><a href="{{ '/blog/isem-teukolsky-flux-generation/' | relative_url }}">A practical adiabatic (0PA) flux workflow for generic EMRIs</a></h2>
    <div class="blog-card__meta">June 21, 2026</div>
    <p>A technical note on radial Teukolsky solves, mode summation order, and Adaptive Levin integration for large scale 0PA flux generation.</p>
    <div class="blog-card__links">
      <a href="{{ '/blog/isem-teukolsky-flux-generation/' | relative_url }}">Read blog</a>
      <a href="{{ '/tools/#generalized-sasaki-nakamura' | relative_url }}">Related tools</a>
    </div>
  </article>
</div>
