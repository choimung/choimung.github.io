---
title: "TIL"
layout: archive
permalink: /TIL
author_profile: true
sidebar:
    nav: "sidebar-category"
---

{% assign posts = site.categories.TIL %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}