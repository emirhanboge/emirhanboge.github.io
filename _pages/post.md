---
layout: page
permalink: /posts/
title: posts
nav: true
nav_order: 2
---
<div class="post-list-container">
  <!-- Posts list -->
  <ul class="post-list">
    {% for post in site.posts %}
      <li>
        <h3>
          {% if post.title %}
            <a class="post-title" href="{{ post.url | relative_url }}">{{ post.title }}</a>
          {% else %}
            <a class="post-title" href="{{ post.url | relative_url }}">{{ post.path | split: '/' | last | replace: '-', ' ' | replace: '.md', '' }}</a>
          {% endif %}
        </h3>
        
        {% if post.description %}
          <p>{{ post.description }}</p>
        {% endif %}

        <p class="post-meta">
          {% assign words = post.content | number_of_words %}
          {% assign read_time = words | divided_by: 180 | plus: 1 %}
          {{ read_time }} min read &nbsp; &middot; &nbsp;
          {{ post.date | date: '%B %d, %Y' }}
        </p>

        {% if post.categories.size > 0 or post.tags.size > 0 %}
          <p class="post-tags">
            <a href="{{ post.date | date: '%Y' | prepend: '/blog/' | prepend: site.baseurl }}">
              <i class="fa-solid fa-calendar fa-sm"></i> {{ post.date | date: '%Y' }}
            </a>

            {% if post.categories.size > 0 %}
              &nbsp; &middot; &nbsp;
              {% for category in post.categories %}
                <a href="{{ category | slugify | prepend: '/blog/category/' | prepend: site.baseurl }}">
                  <i class="fa-solid fa-tag fa-sm"></i> {{ category }}</a>
                {% unless forloop.last %}&nbsp;{% endunless %}
              {% endfor %}
            {% endif %}

            {% if post.tags.size > 0 %}
              &nbsp; &middot; &nbsp;
              {% for tag in post.tags %}
                <a href="{{ tag | slugify | prepend: '/blog/tag/' | prepend: site.baseurl }}">
                  <i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}</a>
                {% unless forloop.last %}&nbsp;{% endunless %}
              {% endfor %}
            {% endif %}
          </p>
        {% endif %}
      </li>
    {% endfor %}
  </ul>
</div>