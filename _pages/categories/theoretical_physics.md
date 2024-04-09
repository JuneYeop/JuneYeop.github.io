---
title: "Theoretical Physics"
permalink: theoretical_physics
layout: archive
author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.theoretical_physics %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
