---
title: "Numerical Simulation"
layout: archive
permalink: categories/numerical_simulation
author_profile: true
types: posts
---

{% assign posts = site.categories['numerical_simulation']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
