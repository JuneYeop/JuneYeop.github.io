---
title: "Mathematical Physics"
permalink: mathematical_physics
layout: archive
author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.mathematical_physics %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}
