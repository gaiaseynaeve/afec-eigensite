---
title: 'Projects'
layout: 'layouts/page.html'
---

As a student I made some assignments at school, but I also had some assignments for acquaintances or family. Below are some of the projects I worked on. Click on each picture to get more information.

<div class="werkjes">
{% for item in collections.featuredWork %}
  <a class="werktitels" href="{{ item.url }}">
    <img src="{{ item.data.image }}" alt="{{ item.data.summary }}"/>
  </a>
{% endfor %}
</div>
