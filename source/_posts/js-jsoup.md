---
title: 网页信息抓取进阶 支持Js生成数据 Jsoup的不足之处
categories:
  - Web Design
date: 2016-07-27 01:42:23
---

首先在这里写下在抓取页面数据时候遇到的问题：

经测试发现，Jsoup无法加载JS，所以无法获取到通过JS调用的数据资源。

J<span style="color: #000000; font-family: 'Microsoft YaHei', Verdana, sans-serif, SimSun; font-size: 14px; line-height: normal;">s乃防抓取的利器，不过同时也毁了SEO</span>

通过HTMLUnit这个开源项目，可以模拟浏览器获取到页面信息
