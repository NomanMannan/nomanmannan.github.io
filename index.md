---
layout: page
title: Welcome to Noman's Blog!
tagline: Gaining and Sharing Knowledge 
---
{% include JB/setup %}

Here's all "posts list".

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
