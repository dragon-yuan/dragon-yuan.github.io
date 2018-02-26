---
title: 'Sublime Text 3 安装Package Control '
categories:
  - Web Design
id: 165
date: 2016-03-09 12:09:53
tags:
---

<div class="line number1 index0 alt2">`view ----- show control`</div>

<div class="line number1 index0 alt2">`import` `urllib.request,os; pf` `=` `'Package Control.sublime-package'``; ipp` `=` `sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) );` `open``(os.path.join(ipp, pf),` `'wb'``).write(urllib.request.urlopen(` `'[http://sublime.wbond.net/](http://sublime.wbond.net/)'` `+` `pf.replace(``' '``,``'%20'``)).read())`</div>
