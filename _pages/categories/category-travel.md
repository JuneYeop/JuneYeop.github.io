---
title: "Travel"
layout: archive
permalink: categories/travel
author_profile: true
types: posts
---

{% assign posts = site.categories['Travel']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
