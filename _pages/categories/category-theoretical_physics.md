---
title: "Theoretical Physics"
layout: archive
permalink: https://juneyeop.github.io/_pages/categories/category-theoretical_physics.md/
author_profile: true
types: posts
---

{% assign posts = site.categories['theoretical_physics']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
