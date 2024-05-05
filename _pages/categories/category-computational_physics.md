---
title: "Computational Physics"
layout: archive
permalink: categories/computational_physics
author_profile: true
types: posts
---

{% assign posts = site.categories['Computatinal Physics']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}

