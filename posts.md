---
layout: page
title: Posts
---

<div>
{% for post in site.posts %}
  {% assign currentdate = post.date | date: "%B %Y" %}
  {% if currentdate != date %}
    <h2>{{ currentdate }}</h2>
    {% assign date = currentdate %} 
  {% endif %}
    <p><a href="{{ post.url }}">{{ post.title }}</a></p>
{% endfor %}
</div>

