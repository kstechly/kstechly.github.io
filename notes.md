---
layout: page
title: Notes
---

{% for post in site.notes %}
  <div class="post">
    <span class="post-title">
        {{ post.author }}
        <h4><a href="{{ post.url }}">{{ post.title }}</a></h4>
    </span>
    {{ post.excerpt }}
  </div>
{% endfor %}