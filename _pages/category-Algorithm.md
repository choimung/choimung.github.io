---

title: "Algorithm"
layout: archive
permalink: /Algorithm
author_profile: true
sidebar:
    nav: "sidebar-category"
    
---

{% assign posts = site.categories.Algorithm %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}