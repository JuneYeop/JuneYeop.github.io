---
title: "Theoretical Physics"
layout: archive
permalink: categories/theoretical_physics
author_profile: true
types: posts
---

{% assign posts = site.categories['Theoretical Physics']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
