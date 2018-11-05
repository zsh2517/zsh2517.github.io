---
layout: project
title: projects
description: 人越学越觉得自己无知
keywords: Project
comments: false
menu: 项目
permalink: /project/
ads_u_share: true
---

> 分享是一种美德。

<!-- <ul class="listing"> -->
<!-- <li class="listing-item"> -->
<table>
    <tr>
        <th>Name</th>
        <th>Author</th>
        <th>description</th>
        <th>Time</th>
    </tr>
{% for project in site.project %}
    {% if project.show %}
        {% if project.title != "project Template" %}
            <tr>
                <th><a href="{{ site.url }}{{ project.url }}">{{ project.title }}</a></th>
                <th>{{ project.author }}</th>
                <th>{{ project.description }}</th>
                {% if project.time %}
                    <th>{{ project.time | date: "%Y/%m/%d" }}</th>
                {% else %}
                    <th></th>
                <!-- <th>{{ project.time }}</th> -->
                {% endif %}
            </tr>
        {% endif %}
    {% endif %}
{% endfor %}
<!-- </ul> -->
</table>