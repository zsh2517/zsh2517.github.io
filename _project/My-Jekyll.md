---
layout: project
title: Jekyll Blog
categories: 
description: 就是这个网站
keywords: 
author: zsh2517
time: 持续更新
show: true
ads_u_share: true
---

博客采用`Jekyll`制作。基于**[mzlogin@GitHub](https://github.com/mazhuang)**的**[博客](https://mazhuang.org)**修改。

在向上追溯一层是**[dongchuan@GitHub](https://github.com/dongchuan)**的[**博客**](https://dongchuan.github.io)。

**在此表示感谢！**

推荐链接

- [中文文案排版指北（简体中文版）](https://github.com/mzlogin/chinese-copywriting-guidelines)

---

其他说明：

基于原模板添加修改的东西

1. POST的tag标签。

2. 部分CSS。

3. MathJax （原来的好像没找到怎么用。。）后来切换到了本地Katex模式 [help](https://www.jianshu.com/p/bb184f61c9ae)

4. 首页。由于Jekyll不支持除了`/index.html`之外的页面调用分页功能。。采用JS实现跳转到新的首页。。

    跳转条件：通过URL或者非同域网站进入首页（index.html，默认不显示）。跳转到`reveal.js`页面。路径是`slide/indexpage#/`

    这里添加指向首页的链接。

    `head.html`中，定义了强制性跳转 `?force` 和强制性不跳转 `notjump` 两个参数。便于调试。（只在jekyll页面有效。）

暂时先到这