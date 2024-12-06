---
title: "Daily Life"
layout: archive
permalink: categories/life
author_profile: true
types: posts
---

{% assign posts = site.categories['Daily Life']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
