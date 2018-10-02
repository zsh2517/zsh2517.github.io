---
layout: page
title: qwq
description: 人越学越觉得自己无知
keywords: 维基, qwq
comments: true
menu: Test
permalink: /qwq/
---

<!-- > 记多少命令和快捷键会让脑袋爆炸呢？ -->

<ul class="listing">
{% for qwq in site.qwq %}
{% if qwq.title != "qwq Template" %}
<li class="listing-item"><a href="{{ site.url }}{{ qwq.url }}">{{ qwq.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
