---
title: "Numerical Simulation"
permalink: numerics
layout: archive
author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.numerics %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}
