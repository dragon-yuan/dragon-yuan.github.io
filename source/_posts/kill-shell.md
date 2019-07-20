---
title: Shell通过进程名称执行kill
categories:
  - Operations
date: 2019-07-20 15:36:03
---

ps -ef | grep procedure_name | grep -v grep | awk '{print $2}' | xargs kill -9
