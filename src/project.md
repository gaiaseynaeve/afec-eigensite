---
title: 'Projects'
layout: 'layouts/page.html'
---

As a student I made some logos for assignments at school and for some friends. Below are the logos I made. Click on each logo to get more information.

### LOGOS

<div class="werkjes">
{% for item in collections.featuredWork %}
  <a class="werktitels" href="{{ item.url }}">
    <img src="{{ item.data.image }}" alt="{{ item.data.summary }}"/>
  </a>
{% endfor %}
</div>
