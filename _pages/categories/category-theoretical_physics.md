---
title: "Theoretical Physics"
layout: archive
permalink: categories/theoretical_physics
author_profile: true
types: posts
---

Theoretical Physics

{% assign posts = site.categories['theoretical_physics']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
