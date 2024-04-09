---
title: "Tokyo"
permalink: tokyo
layout: archive
author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.tokyo %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}
