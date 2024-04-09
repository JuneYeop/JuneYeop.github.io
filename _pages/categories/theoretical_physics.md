---
title: "Theoretical Physics"
permalink: theoretical_physics
layout: archive
author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.theoretical_physics %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}
