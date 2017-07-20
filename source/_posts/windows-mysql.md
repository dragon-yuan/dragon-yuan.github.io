---
title: Windows - MySQL设置编码
categories:
  - Java
id: 167
date: 2016-04-24 08:35:43
tags:
---

`mysql> SHOW VARIABLES ``LIKE`<span style="font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace; letter-spacing: normal; line-height: 13.75px; white-space: pre;"> </span>`'character%'``;`

SET character_set_client = utf8;

SET character_set_connection = utf8;

SET character_set_database = utf8;

SET character_set_results = utf8;

SET character_set_server = utf8;
