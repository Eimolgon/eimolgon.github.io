---
layout: default
title: Blog
permalink: /blog/
---

<h1> Blog </h1>
<div class="cards-container">
  {% for post in site.articles %}
    <div class="card-link-wrapper" style="cursor: pointer; display: block;" onclick="window.location='{{ post.url }}';">
        <div class="card">
            <div class="card-header">
                <h3 style="margin: 0;"><a href="{{ post.url }}" style="text-decoration: none; color: inherit;">{{ post.title }}</a></h3>
                <span class="card-year">{{ post.display_date }}</span>
            </div>
            <div class="card-content">
                <p style="margin: 8px 0;">{{ post.description }}</p>
                {% if post.authors %}
                  <p class="card-authors" style="font-size: 0.9em; opacity: 0.8;">{{ post.authors }}</p>
                {% endif %}
                {% if post.tags %}
                  <div class="card-tags" style="margin-top: 10px;">
                    {% for tag in post.tags %}
                      <span class="tag">{{ tag }}</span>
                    {% endfor %}
                  </div>
                {% endif %}
            </div>
        </div>
    </div>
  {% endfor %}
</div>