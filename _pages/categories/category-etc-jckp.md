---
title: "정보처리기사 필기"
layout: archive
permalink: categories/jckp
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.JCKP %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}