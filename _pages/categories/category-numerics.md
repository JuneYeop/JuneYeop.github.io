---
title: "Numerical Simulation"
layout: archive
permalink: https://juneyeop.github.io/_pages/categories/category-numerics.md
author_profile: true
types: posts
---

{% assign posts = site.categories.numerics %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}
