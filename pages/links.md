---
layout: page
title: Links
description: 没有链接的博客是孤独的
keywords: 友情链接
comments: true
menu: Links
permalink: /links/
---

> Knowledge is power... but remember, ignorance is bliss

<ul>
{% for link in site.data.links %}
  <li><a href="{{ link.url }}" target="_blank">{{ link.name}}</a></li>
{% endfor %}
</ul>
