---
title: "Mathematical Physics"
layout: archive
permalink: https://juneyeop.github.io/_pages/categories/category-mathematical_physics.md/
author_profile: true
types: posts
---

{% assign posts = site.categories['mathematical_physics']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
