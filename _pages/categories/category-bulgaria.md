---
title: "Bulgaria"
layout: archive
permalink: categories/bulgaria
author_profile: true
types: posts
---

{% assign posts = site.categories['Bulgaria']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
