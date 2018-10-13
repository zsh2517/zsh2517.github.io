---
layout: categories
title: 索引
description: 哈哈，你找到了我的文章基因库
keywords: 分类
comments: false
menu: 索引
permalink: /categories/
---

<section class="container posts-content">
<div id="blog-tags">
  <ul class="list-group">
    {% assign sorted_tags = site.tags | sort %}
    {% for tag in sorted_tags %}
    <!-- <li class="list-group-item"> -->
    <a href="#{{ tag[0] }}">{{ tag | first }}[{{ tag[1].size }}]</a>
    <!-- <span class="badge">{{ tag[1].size }}</span> -->
    <!-- </li> -->
    {% endfor %}
  </ul>
</div>

<p><h2>分类</h2></p>
{% assign sorted_categories = site.categories | sort %}
{% for category in sorted_categories %}
<h3>{{ category | first }}</h3>
<ol class="posts-list" id="{{ category[0] }}">
{% for post in category.last %}
<li class="posts-list-item">
<span class="posts-list-meta">{{ post.date | date:"%Y-%m-%d" }}</span>
<a class="posts-list-name" href="{{ site.url }}{{ post.url }}">{{ post.title }}</a>
<font face="consolas" color="#00F"> | Tags.</font> 
{% for tag in post.tags %}
<a class="posts-tag" href="#tag{{tag}}"><font face="consolas" color="#00F">{{ tag }}</font></a>
{% endfor %}
</li>
{% endfor %}
</ol>
{% endfor %}
<!-- ================================================================================== -->
<p><h2>标签</h2></p>
{% assign sorted_tags = site.tags | sort %}
{% for tag in sorted_tags %}
<h3>{{ tag | first }}</h3>
<ol class="posts-list" id="tag{{tag[0]}}">
{% for post in tag.last %}
<li class="posts-list-item">
<span class="posts-list-meta">{{ post.date | date:"%Y-%m-%d" }}</span>
<a class="posts-list-name" href="{{ site.url }}{{ post.url }}">{{ post.title }}</a>
<font face="consolas" color="#FF0000"> | In.</font> 
{% for category in post.categories %}
<a class="posts-category" href="#{{category}}"><font face="consolas" color="#FF0000">{{ category }}</font></a>
{% endfor %}
</li>
{% endfor %}
</ol>
{% endfor %}

</section>
<!-- /section.content -->
