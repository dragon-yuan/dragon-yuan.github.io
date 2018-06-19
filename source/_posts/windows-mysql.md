---
title: Windows - MySQL设置编码
categories:
  - Java
date: 2016-04-24 08:35:43
---

mysql> SHOW VARIABLES `` LIKE `` 'character%' ``;

SET character_set_client = utf8;

SET character_set_connection = utf8;

SET character_set_database = utf8;

SET character_set_results = utf8;

SET character_set_server = utf8;
