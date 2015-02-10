---
layout: page
title: About
permalink: /about/
---

This handbook has been compiled to help you along the path of becoming software engineers.
It will be improved throughout the year, please let us know any if you have any suggestions. 


{% for author in site.authors %}
  {{author.name}} {{author.email}}
{% endfor %}