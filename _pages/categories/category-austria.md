---
title: "Austria"
layout: archive
permalink: categories/austria
author_profile: true
types: posts
---

{% assign posts = site.categories['Austria']%}
{% for post in posts %} 
  {% include archive-single.html type=page.entries_layout %} 
{% endfor %}
