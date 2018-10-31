---
layout: project
title: projects
description: 人越学越觉得自己无知
keywords: Project
comments: false
menu: 项目
permalink: /project/
---

> 分享是一种美德。

<ul class="listing">
{% for project in site.project %}
{% if project.title != "project Template" %}
<li class="listing-item"><a href="{{ site.url }}{{ project.url }}">{{ project.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
