---
layout: page
title: Friends
description: 没有链接的博客是孤独的
keywords: 友情链接
comments: true
menu: Friends
permalink: /links/
---

> God made relatives. Thank God we can choose our friends.

{% for link in site.data.links %}
* [{{ link.name }}]({{ link.url }})
{% endfor %}
