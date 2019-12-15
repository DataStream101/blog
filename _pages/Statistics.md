---
layout: archive
permalink: /statistics/
title: "Statistics Posts"
author_profile: true
header:
  overlay_color: "#5e616c"
  overlay_image: /images/stat2.png
  caption: "Photo credit: [**Shutterstock**](https://www.shutterstock.com/)"
---


{% for post in site.posts %}
  {% if post.tags contains 'stat' %}
     {% include archive-single.html %}
  {% endif %}
{% endfor %}