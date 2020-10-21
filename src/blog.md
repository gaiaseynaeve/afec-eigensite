---
title: 'BLOG'
layout: 'layouts/page.html'
---

Here is my blog about posts I find on the internet that are interesting to me.

### RECENT POSTS

<ul class="blog">
{%- for post in collections.post | reverse -%}
  <li>
    <a href="{{ post.url | url }}">{{ post.data.title }}</a>
 </li>
{%- endfor -%}
</ul>
