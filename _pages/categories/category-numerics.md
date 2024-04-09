---
title: "Numerical Simulation"
layout: archive
permalink: https://juneyeop.github.io/_pages/categories/category-numerics.md
author_profile: true
types: posts
---

{% assign posts = site.categories['numerical_simulation']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
