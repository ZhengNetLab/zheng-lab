---
layout: default
title: Projects
permalink: /projects/
---

<section class="hero" style="padding-bottom:var(--space-12);">
  <div class="container">
    <div class="hero-eyebrow">From the Lab</div>
    <h1>Projects</h1>
  </div>
</section>

<section class="section" style="padding-top:0;">
  <div class="container">
    <div class="card-grid">
      {% assign docs = site.projects | sort: 'date' | reverse %}
      {% for area in site.data.projects %}
      {% assign prefix = '_projects/' | append: area.slug | append: '/' %}
      {% assign count = 0 %}
      {% assign latest = nil %}
      {% for doc in docs %}
        {% if doc.relative_path contains prefix %}
          {% assign count = count | plus: 1 %}
          {% unless latest %}{% assign latest = doc %}{% endunless %}
        {% endif %}
      {% endfor %}
      <article class="card">
        <span class="card-tag">{{ count }} {% if count == 1 %}article{% else %}articles{% endif %}</span>
        <h2 class="card-title" style="font-size:var(--fs-lg);"><a href="{{ '/projects/' | append: area.slug | append: '/' | relative_url }}">{{ area.title }}</a></h2>
        <p class="card-excerpt">{% if latest %}Latest: {{ latest.title }}{% else %}No articles yet.{% endif %}</p>
        <span class="card-arrow" aria-hidden="true">→</span>
      </article>
      {% endfor %}
    </div>
  </div>
</section>
