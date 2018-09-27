---
layout: page
title: down
description: 人越学越觉得自己无知
keywords: down
comments: false
menu: 下载
permalink: /down/
---

> 记多少命令和快捷键会让脑袋爆炸呢？

<ul class="listing">
{% for down in site.down %}
{% if down.title != "down Template" %}
<li class="listing-item"><a href="{{ site.url }}{{ down.url }}">{{ down.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
