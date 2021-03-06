---
title: MySQL中字段类型
categories:
  - Java
date: 2015-12-22 12:34:33
---

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">基础：</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">char</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">、<span lang="EN-US">varchar</span>、<span lang="EN-US">text</span>和<span lang="EN-US">nchar</span>、<span lang="EN-US">nvarchar</span>、<span lang="EN-US">ntext</span>的区别</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">1</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">、<span lang="EN-US">CHAR</span>。<span lang="EN-US">CHAR</span>存储定长数据很方便，<span lang="EN-US">CHAR</span>字段上的索引效率级高，比如定义<span lang="EN-US">char(10)</span>，那么不论你存储的数据是否达到了<span lang="EN-US">10</span>个字节，都要占去<span lang="EN-US">10</span>个字节的空间<span lang="EN-US">,</span>不足的自动用空格填充。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">2</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">、<span lang="EN-US">VARCHAR</span>。存储变长数据，但存储效率没有<span lang="EN-US">CHAR</span>高。如果一个字段可能的值是不固定长度的，我们只知道它不可能超过<span lang="EN-US">10</span>个字符，把它定义为 <span lang="EN-US">VARCHAR(10)</span>是最合算的。<span lang="EN-US">VARCHAR</span>类型的实际长度是它的值的实际长度<span lang="EN-US">+1</span>。为什么“<span lang="EN-US">+1</span>”呢？这一个字节用于保存实际使用了多大的长度。从空间上考虑，用<span lang="EN-US">varchar</span>合适；从效率上考虑，用<span lang="EN-US">char</span>合适，关键是根据实际情况找到权衡点。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">3</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">、<span lang="EN-US">TEXT</span>。<span lang="EN-US">text</span>存储可变长度的非<span lang="EN-US">Unicode</span>数据，最大长度为<span lang="EN-US">2^31-1(2,147,483,647)</span>个字符。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">4</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">、<span lang="EN-US">NCHAR</span>、<span lang="EN-US">NVARCHAR</span>、<span lang="EN-US">NTEXT</span>。这三种从名字上看比前面三种多了个“<span lang="EN-US">N</span>”。它表示存储的是<span lang="EN-US">Unicode</span>数据类型的字符。我们知道字符中，英文字符只需要一个字节存储就足够了，但汉字众多，需要两个字节存储，英文与汉字同时存在时容易造成混乱，<span lang="EN-US">Unicode</span>字符集就是为了解决字符集这种不兼容的问题而产生的，它所有的字符都用两个字节表示，即英文字符也是用两个字节表示。<span lang="EN-US">nchar</span>、<span lang="EN-US">nvarchar</span>的长度是在<span lang="EN-US">1</span>到<span lang="EN-US">4000</span>之间。和<span lang="EN-US">char</span>、<span lang="EN-US">varchar</span>比较起来，<span lang="EN-US">nchar</span>、<span lang="EN-US">nvarchar</span>则最多存储<span lang="EN-US">4000</span>个字符，不论是英文还是汉字；而<span lang="EN-US">char</span>、<span lang="EN-US">varchar</span>最多能存储<span lang="EN-US">8000</span>个英文，<span lang="EN-US">4000</span>个汉字。可以看出使用<span lang="EN-US">nchar</span>、<span lang="EN-US">nvarchar</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">数据类型时不用担心输入的字符是英文还是汉字，较为方便，但在存储英文时数量上有些损失。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">进一步学习：</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">char</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">、<span lang="EN-US">varchar</span>、<span lang="EN-US">text</span>、<span lang="EN-US">ntext</span>、<span lang="EN-US">bigint</span>、<span lang="EN-US">int</span>、<span lang="EN-US">smallint</span>、<span lang="EN-US">tinyint</span>和<span lang="EN-US">bit</span>的区别及数据库的数据类型</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Varchar</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">对每个英文<span lang="EN-US">(ASCII)</span>字符都占用<span lang="EN-US">2</span>个字节，对一个汉字也只占用两个字节</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">char</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">对英文<span lang="EN-US">(ASCII)</span>字符占用<span lang="EN-US">1</span>个字节，对一个汉字占用<span lang="EN-US">2</span>个字节<span lang="EN-US">Varchar</span> 的类型不以空格填满，比如<span lang="EN-US">varchar(100)</span>，但它的值只是<span lang="EN-US">"qian",</span>则它的值就是<span lang="EN-US">"qian"</span>而<span lang="EN-US">char</span> 不一样，比如<span lang="EN-US">char(100),</span>它的值是<span lang="EN-US">"qian"</span>，而实际上它在数据库中是<span lang="EN-US">"qian "(qian</span>后共有<span lang="EN-US">96</span>个空格，就是把它填满为<span lang="EN-US">100</span>个字节<span lang="EN-US">)</span>。由于<span lang="EN-US">char</span>是以固定长度的，所以它的速度会比<span lang="EN-US">varchar</span>快得多<span lang="EN-US">!</span>但程序处理起来要麻烦一点，要用<span lang="EN-US">trim</span>之类的函数把两边的空格去掉<span lang="EN-US">!</span></span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">ntext</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">可变长度 <span lang="EN-US">Unicode</span> 数据的最大长度为 <span lang="EN-US">230 - 1 (1,073,741,823)</span> 个字符。存储大小是所输入字符个数的两倍（以字节为单位）。<span lang="EN-US">ntext</span> 在 <span lang="EN-US">SQL-92</span> 中的同义词是 <span lang="EN-US">national text</span>。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">text</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">服务器代码页中的可变长度非 <span lang="EN-US">Unicode</span> 数据的最大长度为 <span lang="EN-US">231-1 (2,147,483,647)</span> 个字符。当服务器代码页使用双字节字符时，存储量仍是 <span lang="EN-US">2,147,483,647</span> 字节。存储大小可能小于 <span lang="EN-US">2,147,483,647</span> 字节（取决于字符串）。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">bigint</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">：从<span lang="EN-US">-2^63(-9223372036854775808)</span>到<span lang="EN-US">2^63-1(9223372036854775807)</span>的整型数据，存储大小为 <span lang="EN-US">8</span> 个字节。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">int</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">：从<span lang="EN-US">-2^31(-2,147,483,648)</span>到<span lang="EN-US">2^31-1(2,147,483,647)</span>的整型数据，存储大小为 <span lang="EN-US">4</span> 个字节。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">smallint</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">：从<span lang="EN-US">-2^15(-32,768)</span>到<span lang="EN-US">2^15-1(32,767)</span>的整数数据，存储大小为 <span lang="EN-US">2</span> 个字节。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">tinyint</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">：从<span lang="EN-US">0</span>到<span lang="EN-US">255</span>的整数数据，存储大小为 <span lang="EN-US">1</span> 字节。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">bit</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">：<span lang="EN-US">1</span>或<span lang="EN-US">0</span>的整数数据，存储大小为 <span lang="EN-US">1</span> 字节。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Unicode</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">数据</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">在 <span lang="EN-US">Microsoft SQL Server 2000</span> 中，传统上非 <span lang="EN-US">Unicode</span> 数据类型允许使用由特定字符集定义的字符。字符集是在安装 <span lang="EN-US">SQL Server</span> 时选择的，不能更改。使用 <span lang="EN-US">Unicode</span> 数据类型，列可存储由 <span lang="EN-US">Unicode</span> 标准定义的任何字符，包含由不同字符集定义的所有字符。<span lang="EN-US">Unicode</span> 数据类型需要相当于非 <span lang="EN-US">Unicode</span> 数据类型两倍的存储空间。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Unicode</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">数据使用 <span lang="EN-US">SQL Server</span> 中的 <span lang="EN-US">nchar</span>、<span lang="EN-US">varchar</span> 和 <span lang="EN-US">ntext</span> 数据类型进行存储。对于存储来源于多种字符集的字符的列，可采用这些数据类型。当列中各项所包含的 <span lang="EN-US">Unicode</span> 字符数不同时（至多为 <span lang="EN-US">4000</span>），使用 <span lang="EN-US">nvarchar</span> 类型。当列中各项为同一固定长度时（至多为 <span lang="EN-US">4000</span> 个 <span lang="EN-US">Unicode</span> 字符），使用 <span lang="EN-US">nchar</span> 类型。当列中任意项超过 <span lang="EN-US">4000</span> 个 <span lang="EN-US">Unicode</span>字符时，使用 <span lang="EN-US">ntext</span> 类型。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">说明：<span lang="EN-US">SQL Server</span> 的 <span lang="EN-US">Unicode</span> 数据类型是基于 <span lang="EN-US">SQL-92</span> 标准中的国家字符数据类型。<span lang="EN-US">SQL-92</span> 使用前缀字符 <span lang="EN-US">n</span> 标识这些数据类型及其值。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">数据类型：</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">数据类弄是数据的一种属性，表示数据所表示信息的类型。任何一种计算机语言都定义了自己的数据类型。当然，不同的程序语言都具有不同的特点，所定义的数据类型的各类和名称都或多或少有些不同。<span lang="EN-US">SQL Server</span> 提供了 <span lang="EN-US">25</span> 种数据类型：</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Binary [(N)]</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Varbinary [(N)]</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Char [(N)]</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Varchar[(N)]</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Nchar[(N)]</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Nvarchar[(N)]</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Datetime</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Smalldatetime</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Decimal[(p[,s])]</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Numeric[(p[,s])]</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Float[(N)]</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Real</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Int</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Smallint</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Tinyint</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Money</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Smallmoney</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Bit</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Cursor</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Sysname</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Timestamp</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Uniqueidentifier</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Text</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Image</span></span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">·<span lang="EN-US">Ntext</span></span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;"> </span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">(1)</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">二进制数据类型</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">二进制数据包括 <span lang="EN-US">Binary</span>、<span lang="EN-US">Varbinary</span> 和 <span lang="EN-US">Image.</span></span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Binary</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">数据类型既可以是固定长度的<span lang="EN-US">(Binary),</span>也可以是变长度的。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Binary[(N)]</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">是 <span lang="EN-US">n</span> 位固定的二进制数据。其中，<span lang="EN-US">n</span> 的取值范围是从 <span lang="EN-US">1</span> 到 <span lang="EN-US">8000</span>。其存储窨的大小是 <span lang="EN-US">n + 4</span> 个字节。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Varbinary[(N)]</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">是 <span lang="EN-US">n</span> 位变长度的二进制数据。其中，<span lang="EN-US">n</span> 的取值范围是从 <span lang="EN-US">1</span> 到 <span lang="EN-US">8000</span>。其存储窨的大小是 <span lang="EN-US">n + 4</span>个字节，不是 <span lang="EN-US">n</span> 个字节。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">在 <span lang="EN-US">Image</span> 数据类型中存储的数据是以位字符串存储的，不是由 <span lang="EN-US">SQL Server</span> 解释的，必须由应用程序来解释。例如，应用程序可以使用 <span lang="EN-US">BMP</span>、<span lang="EN-US">TIEF</span>、<span lang="EN-US">GIF</span> 和 <span lang="EN-US">JPEG</span> 格式把数据存储在 <span lang="EN-US">Image</span> 数据类型中。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">(2)</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">字符数据类型</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">字符数据的类型包括 <span lang="EN-US">Char</span>，<span lang="EN-US">Varchar</span> 和 <span lang="EN-US">Text</span>。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">字符数据是由任何字母、符号和数字任意组合而成的数据。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Varchar</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">是变长字符数据，其长度不超过 <span lang="EN-US">8KB</span>。<span lang="EN-US">Char</span> 是定长字符数据，其长度最多为 <span lang="EN-US">8KB</span>。超过 <span lang="EN-US">8KB</span> 的<span lang="EN-US">ASCII</span> 数据可以使用<span lang="EN-US">Text</span> 数据类型存储。例如<span lang="EN-US">:</span>因为 <span lang="EN-US">Html</span> 文档全部都是 <span lang="EN-US">ASCII</span> 字符，并且在一般情况下长度超过 <span lang="EN-US">8KB</span>，所以这些文档可以 <span lang="EN-US">Text</span> 数据类型存储在 <span lang="EN-US">SQL Server</span> 中。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">(3)Unicode</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">数据类型</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Unicode</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">数据类型包括 <span lang="EN-US">Nchar,Nvarchar</span> 和<span lang="EN-US">Ntext</span>。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">在 <span lang="EN-US">Microsoft SQL Server</span> 中，传统的非 <span lang="EN-US">Unicode</span> 数据类型允许使用由特定字符集定义的字符。在 <span lang="EN-US">SQL Server</span> 安装过程中，允许选择一种字符集。使用 <span lang="EN-US">Unicode</span> 数据类型，列中可以存储任何由<span lang="EN-US">Unicode</span> 标准定义的字符。在 <span lang="EN-US">Unicode</span> 标准中，包括了以各种字符集定义的全部字符。使用<span lang="EN-US">Unicode</span> 数据类型，所占的空间是使用非 <span lang="EN-US">Unicode</span> 数据类型所占用的空间大小的两倍。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">在 <span lang="EN-US">SQL Server</span> 中，<span lang="EN-US">Unicode</span> 数据以 <span lang="EN-US">Nchar</span>、<span lang="EN-US">Nvarchar</span> 和 <span lang="EN-US">Ntext</span> 数据类型存储。使用这种字符类型存储的列可以存储多个字符集中的字符。当列的长度变化时，应该使用 <span lang="EN-US">Nvarchar</span> 字符类型，这时最多可以存储 <span lang="EN-US">4000</span> 个字符。当列的长度固定不变时，应该使用 <span lang="EN-US">Nchar</span> 字符类型，同样，这时最多可以存储 <span lang="EN-US">4000</span> 个字符。当使用 <span lang="EN-US">Ntext</span> 数据类型时，该列可以存储多于 <span lang="EN-US">4000</span> 个字符。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">(4)</span><span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">日期和时间数据类型</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">日期和时间数据类型包括 <span lang="EN-US">Datetime</span> 和 <span lang="EN-US">Smalldatetime</span> 两种类型。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">日期和时间数据类型由有效的日期和时间组成。例如，有效的日期和时间数据包括<span lang="EN-US">"4/01/98 12:15:00:00:00 PM"</span>和<span lang="EN-US">"1:28:29:15:01 AM 8/17/98"</span>。前一个数据类型是日期在前，时间在后一个数据类型是霎时间在前，日期在后。在 <span lang="EN-US">Microsoft SQL Server</span> 中，日期和时间数据类型包括<span lang="EN-US">Datetime</span> 和 <span lang="EN-US">Smalldatetime</span> 两种类型时，所存储的日期范围是从 <span lang="EN-US">1753</span> 年 <span lang="EN-US">1</span> 月 <span lang="EN-US">1</span> 日开始，到 <span lang="EN-US">9999</span> 年<span lang="EN-US">12</span> 月 <span lang="EN-US">31</span> 日结束<span lang="EN-US">(</span>每一个值要求 <span lang="EN-US">8</span> 个存储字节<span lang="EN-US">)</span>。使用 <span lang="EN-US">Smalldatetime</span> 数据类型时，所存储的日期范围是 <span lang="EN-US">1900</span> 年 <span lang="EN-US">1</span> 月 <span lang="EN-US">1</span>日 开始，到 <span lang="EN-US">2079</span> 年 <span lang="EN-US">12</span> 月 <span lang="EN-US">31</span> 日结束<span lang="EN-US">(</span>每一个值要求 <span lang="EN-US">4</span> 个存储字节<span lang="EN-US">)</span>。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">日期的格式可以设定。设置日期格式的命令如下：</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Set DateFormat {format | @format _var|</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">其中，<span lang="EN-US">format | @format_var</span> 是日期的顺序。有效的参数包括 <span lang="EN-US">MDY</span>、<span lang="EN-US">DMY</span>、<span lang="EN-US">YMD</span>、<span lang="EN-US">YDM</span>、<span lang="EN-US">MYD</span> 和 <span lang="EN-US">DYM</span>。在默认情况下，日期格式为 <span lang="EN-US">MDY</span>。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">例如，当执行 <span lang="EN-US">Set DateFormat YMD</span> 之后，日期的格式为年 月 日 形式；当执行 <span lang="EN-US">Set DateFormat DMY</span> 之后，日期的格式为 日 月有年 形式</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">（<span lang="EN-US">5</span>）数字数据类型</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">数字数据只包含数字。数字数据类型包括正数和负数、小数（浮点数）和整数 。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">整数由正整数和负整数组成，例如 <span lang="EN-US">39</span>、<span lang="EN-US">25</span>、<span lang="EN-US">0-2</span> 和 <span lang="EN-US">33967</span>。在 <span lang="EN-US">Micrsoft SQL Server</span> 中，整数存储的数据类型是 <span lang="EN-US">Int</span>，<span lang="EN-US">Smallint</span> 和 <span lang="EN-US">Tinyint</span>。<span lang="EN-US">Int</span> 数据类型存储数据的范围大于 <span lang="EN-US">Smallint</span> 数据类型存储数据的范围，而 <span lang="EN-US">Smallint</span> 据类型存储数据的范围大于 <span lang="EN-US">Tinyint</span> 数据类型存储数据的范围。使用 <span lang="EN-US">Int</span> 数据狗昔存储数据的范围是从 <span lang="EN-US">-2 147 483 648</span> 到 <span lang="EN-US">2 147 483 647</span>（每一个值要求 <span lang="EN-US">4</span>个字节存储空间）。使用 <span lang="EN-US">Smallint</span> 数据类型时，存储数据的范围从 <span lang="EN-US">-32 768</span> 到 <span lang="EN-US">32 767</span>（每一个值要求<span lang="EN-US">2</span>个字节存储空间）。使用 <span lang="EN-US">Tinyint</span> 数据类型时，存储数据的范围是从<span lang="EN-US">0</span> 到<span lang="EN-US">255</span>（每一个值要求<span lang="EN-US">1</span>个字节存储空间）。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">精确小娄数据在 <span lang="EN-US">SQL Server</span> 中的数据类型是 <span lang="EN-US">Decimal</span> 和 <span lang="EN-US">Numeric</span>。这种数据所占的存储空间根据该数据的位数后的位数来确定。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">在<span lang="EN-US">SQL Server</span> 中，近似小数数据的数据类型是 <span lang="EN-US">Float</span> 和 <span lang="EN-US">Real</span>。例如，三分之一这个分数记作。<span lang="EN-US">3333333</span>，当使用近似数据类型时能准确表示。因此，从系统中检索到的数据可能与存储在该列中数据不完全一样。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">（<span lang="EN-US">6</span>）货币数据表示正的或者负的货币数量 。在 <span lang="EN-US">Microsoft SQL Server</span> 中，货币数据的数据类型是<span lang="EN-US">Money</span> 和 <span lang="EN-US">Smallmoney</span>。<span lang="EN-US">Money</span> 数据类型要求 <span lang="EN-US">8</span> 个存储字节，<span lang="EN-US">Smallmoney</span> 数据类型要求 <span lang="EN-US">4</span> 个存储字节。</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">（<span lang="EN-US">7</span>）特殊数据类型</span>

<span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">特殊数据类型包括前面没有提过的数据类型。特殊的数据类型有<span lang="EN-US">3</span>种，即 <span lang="EN-US">Timestamp</span>、<span lang="EN-US">Bit</span> 和 <span lang="EN-US">Uniqueidentifier</span>。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Timestamp</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">用于表示<span lang="EN-US">SQL Server</span> 活动的先后顺序，以二进投影的格式表示。<span lang="EN-US">Timestamp</span> 数据与插入数据或者日期和时间没有关系。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Bit</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">由 <span lang="EN-US">1</span> 或者 <span lang="EN-US">0</span> 组成。当表示真或者假、<span lang="EN-US">ON</span> 或者 <span lang="EN-US">OFF</span> 时，使用 <span lang="EN-US">Bit</span> 数据类型。例如，询问是否是每一次访问的客户机请求可以存储在这种数据类型的列中。</span>

<span lang="EN-US" style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">Uniqueidentifier</span> <span style="font-size: 14.0pt; font-family: 宋体; mso-ascii-theme-font: minor-fareast; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-theme-font: minor-fareast;">由 <span lang="EN-US">16</span> 字节的十六进制数字组成，表示一个全局唯一的。当表的记录行要求唯一时，<span lang="EN-US">GUID</span>是非常有用。例如，在客户标识号列使用这种数据类型可以区别不同的客户。</span>
