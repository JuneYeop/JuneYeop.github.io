---
title: "Tokyo"
permalink: tokyo
layout: archive
author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.tokyo %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
