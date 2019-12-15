---
layout: archive
permalink: /projects/
title: "Projects"
author_profile: true
header:
  overlay_color: "#5e616c"
  overlay_image: /images/project.jpeg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
---


{% for post in site.posts %}
  {% if post.tags contains 'project' %}
     {% include archive-single.html %}
  {% endif %}
{% endfor %}

