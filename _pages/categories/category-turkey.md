---
title: "Turkey"
layout: archive
permalink: categories/turkey
author_profile: true
types: posts
---

{% assign posts = site.categories['Turkey']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
