---
layout: page
title: Wiki
description: WIKI是什么鬼、、
keywords: 维基, Wiki
comments: false
menu: 百科
permalink: /wiki/
---

~~WIKI是什么鬼，能吃吗？~~

**大佬**们的经典作品（来自网络，部分已授权转载）
<!-- 专门记一些~~不正经~~（奇怪）的东西。。 -->

如果需要翻唱等建议去联系一下作者本人吧。qwq

| 待更新列表 |
| :--- | 
|[【外传】【初音×OI】状态转移](https://www.bilibili.com/video/av29799588/?spm_id_from=333.788.videocard.18) |
| [阳光码农](https://www.bilibili.com/video/av4022496/?spm_id_from=333.788.reco_list.25) |
| ~~还有很多这个列表都懒得更，逐渐添加QAQ~~ |

<ul class="listing">
{% for wiki in site.wiki %}
{% if wiki.show == true %}
<li class="listing-item"><a href="{{ site.url }}{{ wiki.url }}">{{ wiki.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
