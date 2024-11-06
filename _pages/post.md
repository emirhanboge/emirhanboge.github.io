---
layout: page
permalink: /posts/
title: posts
nav: true
nav_order: 2
---
<div class="post-list-container">
  <ul class="post-list">
    {% for post in site.posts %}
      <li>
        <h3>
          {% if post.title %}
            {% assign url_title = post.title | slugify: "latin" %}
            <a class="post-title" href="{{ post.url }}">{{ post.title }}</a>
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
            <a href="{{ post.date | date: '%Y' | prepend: '/posts/' }}">
              <i class="fa-solid fa-calendar fa-sm"></i> {{ post.date | date: '%Y' }}
            </a>

            {% if post.categories.size > 0 %}
              &nbsp; &middot; &nbsp;
              {% for category in post.categories %}
                <a href="{{ category | slugify | prepend: '/posts/category/' }}">
                  <i class="fa-solid fa-tag fa-sm"></i> {{ category }}</a>
                {% unless forloop.last %}&nbsp;{% endunless %}
              {% endfor %}
            {% endif %}

            {% if post.tags.size > 0 %}
              &nbsp; &middot; &nbsp;
              {% for tag in post.tags %}
                <a href="{{ tag | slugify | prepend: '/posts/tag/' }}">
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