---
title: 解决java compiler level does not match the version of the installed java project facet
categories:
  - Java
date: 2016-06-21 13:14:08
---

<span style="text-align: center;">其实要解决也很简单，在资源管理器下，找到项目所在的目录，在.settings子目录里面，用文本编辑器打开org.eclipse.wst.common.project.facet.core.xml配置文件，如图所示：</span>

<span style="text-align: center;">![](http://img.my.csdn.net/uploads/201210/29/1351513323_5843.jpg)  
</span>

<span style="text-align: center;">修改红色画线部分，让它与项目的编译器版本设置保持一致即可。</span>

<span style="text-align: center;">要查看项目的编译器版本设置，在Eclipse环境中，鼠标右键选择项目，点击Properties，选择Java Compiler，可以在窗口右边看到编译器版本，如图所示：</span>

<span style="text-align: center;">![](http://img.my.csdn.net/uploads/201210/29/1351513471_5803.jpg)</span>

转载：http://blog.csdn.net/chszs/article/details/8125828 感谢博主
