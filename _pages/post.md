---
layout: page
permalink: /posts/
title: posts
nav: true
nav_order: 2
---

<div class="posts">
  {% assign posts = site.posts %}
  {% for post in posts %}
    <div class="post">
      <h3>
        <a href="/blog/{{ post.date | date: "%Y/%m/%d" }}/{{ post.title | slugify }}">
          {{ post.title }}
        </a>
      </h3>
      <p class="post-meta">{{ post.date | date: '%B %d, %Y' }}</p>
      <p>{{ post.description }}</p>
    </div>
    <hr>
  {% endfor %}
</div>