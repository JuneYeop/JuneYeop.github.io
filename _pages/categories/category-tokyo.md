---
title: "Tokyo"
layout: archive
permalink: categories/tokyo
author_profile: true
types: posts
---

{% assign posts = site.categories['tokyo']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
