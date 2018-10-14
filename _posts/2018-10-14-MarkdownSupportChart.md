---
layout: post
title: markdown 对表格的支持
categories: blog
description: markdown 对表格的支持
keywords: 
tags: 
show: true
---

# markdown 对表格的支持

```markdown
| 第一行第一列 | 第一行第二列 | 第一行第三列 |
| --: | :--: | :-- |
| 右对齐 | 居中 | 左对齐 |
| 第三行第一列 | 第三行第二列 | 第三行第三列 |
```

| 第一行第一列 | 第一行第二列 | 第一行第三列 |
| --: | :--: | :-- |
| 右对齐 | 居中 | 左对齐 |
| 第三行第一列 | 第三行第二列 | 第三行第三列 |

```html
<table>
    <tr>
        <th>第一行第一列</th>
        <th>第一行第二列</th>
        <th>第一行第三列</th>
    </tr>
    <tr>
        <th>第二行第一列</th>
        <th>第二行第二列</th>
        <th>第二行第三列</th>
    </tr>
    <tr>
        <th>第三行第一列</th>
        <th>第三行第二列</th>
        <th>第三行第三列</th>
    </tr>
</table>
```

<table>
    <tr>
        <th>第一行第一列</th>
        <th>第一行第二列</th>
        <th>第一行第三列</th>
    </tr>
    <tr>
        <th>第二行第一列</th>
        <th>第二行第二列</th>
        <th>第二行第三列</th>
    </tr>
    <tr>
        <th>第三行第一列</th>
        <th>第三行第二列</th>
        <th>第三行第三列</th>
    </tr>
</table>