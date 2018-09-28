---
layout: page
title: Wiki
description: WIKI是什么鬼、、
keywords: 维基, W
comments: false
menu: 维基
permalink: /wiki/
---

~~WIKI是什么鬼，能吃吗？~~

专门记一些~~不正经~~（奇怪）的东西。。

<ul class="listing">
{% for wiki in site.wiki %}
{% if wiki.title != "Wiki Template" %}
<li class="listing-item"><a href="{{ site.url }}{{ wiki.url }}">{{ wiki.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
