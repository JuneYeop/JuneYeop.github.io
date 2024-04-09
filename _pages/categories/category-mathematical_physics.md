---
title: "Mathematical Physics"
layout: archive
permalink: categories/mathematical_physics
author_profile: true
types: posts
---

Mathematical Physics

{% assign posts = site.categories['mathematical_physics']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
