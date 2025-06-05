---
title: "Japan"
layout: archive
permalink: categories/japan
author_profile: true
types: posts
---

{% assign posts = site.categories['Japan']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
