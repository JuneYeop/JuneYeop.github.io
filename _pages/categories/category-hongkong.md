---
title: "Hong Kong"
layout: archive
permalink: categories/hongkong
author_profile: true
types: posts
---

{% assign posts = site.categories['Hong Kong']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
