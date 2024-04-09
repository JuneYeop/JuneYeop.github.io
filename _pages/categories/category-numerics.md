---
title: "Numerical Simulation"
layout: archive
permalink: categories/numerics
author_profile: true
types: posts
---

Numerical Simulation

{% assign posts = site.categories['numerics']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}

