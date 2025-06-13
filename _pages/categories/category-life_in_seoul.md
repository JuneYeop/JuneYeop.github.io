---
title: "Life in Seoul"
layout: archive
permalink: categories/life_in_seoul
author_profile: true
types: posts
---

{% assign posts = site.categories['Life in Seoul']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
