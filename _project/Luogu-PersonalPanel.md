---
layout: project
title: 洛谷个人信息面板滚动
categories: 
description: 【stylish】洛谷个人信息面板滚动条的支持。
keywords: 
author: zsh2517
time: 2018-09-28
show: true
ads_u_share: true
---

### 洛谷讨论

[洛谷讨论](https://www.luogu.org/discuss/show/79531)

### 安装链接

安装链接[userstyles.org](https://userstyles.org/styles/165582/luogu)

### 源码

#### for Chrome

```css
.am-dropdown-flip .am-dropdown-content {
    left: auto;
    right: 0;
    height: 500px;
    overflow-y: scroll;
}
```

#### For Firefox

```css
@-moz-document domain("luogu.org") {
.am-dropdown-flip .am-dropdown-content {
    left: auto;
    right: 0;
    height: 500px;
    overflow-y: scroll;
}
}
```