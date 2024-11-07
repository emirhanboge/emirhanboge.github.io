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
          <a class="post-title" href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
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

        <p class="post-tags">
          <a href="{{ site.baseurl }}/posts/{{ post.date | date: '%Y' }}">
            <i class="fa-solid fa-calendar fa-sm"></i> {{ post.date | date: '%Y' }}
          </a>

          {% if post.categories.size > 0 %}
            &nbsp; &middot; &nbsp;
            {% for category in post.categories %}
              <a href="{{ site.baseurl }}/posts/category/{{ category | slugify }}">
                <i class="fa-solid fa-tag fa-sm"></i> {{ category }}</a>
              {% unless forloop.last %}&nbsp;{% endunless %}
            {% endfor %}
          {% endif %}

          {% if post.tags.size > 0 %}
            &nbsp; &middot; &nbsp;
            {% for tag in post.tags %}
              <a href="{{ site.baseurl }}/posts/tag/{{ tag | slugify }}">
                <i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}</a>
              {% unless forloop.last %}&nbsp;{% endunless %}
            {% endfor %}
          {% endif %}
        </p>
      </li>
    {% endfor %}
  </ul>
</div>