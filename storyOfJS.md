# JS诞生记
## JS的诞生
JS的父亲是布兰登·艾克。

1995年，网景招募了布兰登·艾克，目标是把Scheme语言嵌入到Netscape Navigator浏览器当中。但更早之前，网景已经在Netscape Navigator中支持Java，这时网景内部产生激烈的争论。

后来网景决定发明一种与Java搭配使用的辅助脚本语言并且语法上有些类似，这个决策导致排除了采用现有的语言，例如Perl、Python、Tcl或Scheme。为了在其他竞争提案中捍卫JavaScript这个想法，公司需要有一个可以运作的原型。

于是艾克在1995年5月仅花了十天时间就把原型设计出来了。

JS最初命名为Mocha，1995年9月在Netscape Navigator 2.0的Beta版中改名为LiveScript，同年12月，Netscape Navigator 2.0 Beta 3中部署时被重命名为JavaScript，当时网景公司与昇阳电脑公司组成的开发联盟为了让这门语言搭上Java这个编程语言“热词”蹭热点，因此将其临时改名为JavaScript。

## JS动荡的生平
JavaScript推出后在浏览器上大获成功，微软公司在不久后就为Internet Explorer 3浏览器推出了JScript，以与处于市场领导地位的网景产品同台竞争。

JScript也是一种JavaScript实现，这两个JavaScript语言版本在浏览器端共存意味着语言标准化的缺失，发展初期，JavaScript的标准并未确定，同期有网景的JavaScript，微软的JScript双峰并峙。除此之外，微软也在网页技术上加入了不少专属对象，使不少网页使用非微软平台及浏览器无法正常显示，导致在浏览器大战期间网页设计者通常会把“用Netscape可达到最佳效果”或“用IE可达到最佳效果”的标志放在主页。随着Internet Explorer 4的发布，微软引入了动态HTML的概念，但语言实现和不同专有化的文档对象模型的差异仍然存在，成为网络上普及使用JavaScript的阻碍。

但ECMA标准的制定，极大促进了js的发展，从此以后，JS渐渐称霸web市场。

## JS设计缺陷
由于JS设计阶段过于仓促，没有先例，过早的标准化，导致了一系列的缺陷，约有十种：
1. 不适合开发大型程序
Javascript没有名称空间（namespace），很难模块化；没有如何将代码分布在多个文件的规范；允许同名函数的重复定义，后面的定义可以覆盖前面的定义，很不利于模块化加载。
2. 非常小的标准库
Javascript提供的标准函数库非常小，只能完成一些基本操作，很多功能都不具备。
3. null和undefined
null属于对象（object）的一种，意思是该对象为空；undefined则是一种数据类型，表示未定义。两者非常容易混淆，但是含义完全不同。在编程实践中，null几乎没用，根本不应该设计它。
4. 全局变量难以控制
Javascript的全局变量，在所有模块中都是可见的；任何一个函数内部都可以生成全局变量，这大大加剧了程序的复杂性。
5. 自动插入行尾分号
Javascript的所有语句，都必须以分号结尾。但是，如果你忘记加分号，解释器并不报错，而是为你自动加上分号。有时候，这会导致一些难以发现的错误。
6. 加号运算符
+号作为运算符，有两个含义，可以表示数字与数字的和，也可以表示字符与字符的连接。
~~~javascript
   alert(1+10); // 11

　　alert("1"+"10"); // 110 
~~~
如果一个操作项是字符，另一个操作项是数字，则数字自动转化为字符。
~~~javascript
   alert(1+"10"); // 110

　　alert("10"+1); // 101
~~~
这样的设计，不必要地加剧了运算的复杂性，完全可以另行设置一个字符连接的运算符。

7. NaN
NaN是一种数字，表示超出了解释器的极限。它有一些很奇怪的特性：
~~~javascript
   NaN === NaN; //false

　　NaN !== NaN; //true

　　alert( 1 + NaN ); // NaN   
~~~
与其设计NaN，不如解释器直接报错，反而有利于简化程序。
8. 数组和对象的区分
由于Javascript的数组也属于对象（object），所以要区分一个对象到底是不是数组，相当麻烦。Douglas Crockford的代码是这样的：
~~~javascript
   if ( arr &&
　　　　typeof arr === 'object' &&
　　　　typeof arr.length === 'number' &&
　　　　!arr.propertyIsEnumerable('length')){

　　　　alert("arr is an array");

　　}
~~~
9. == 和 ===
==用来判断两个值是否相等。当两个值类型不同时，会发生自动转换，得到的结果非常不符合直觉。
因此，推荐任何时候都使用"==="（精确判断）.
10. 基本类型的包装对象
Javascript有三种基本数据类型：字符串、数字和布尔值。它们都有相应的建构函数，可以生成字符串对象、数字对象和布尔值对象。
~~~javascript
   new Boolean(false);

　　new Number(1234);

　　new String("Hello World");
~~~
与基本数据类型对应的对象类型，作用很小，造成的混淆却很大。
~~~javascript
   alert( typeof 1234); // number

　　alert( typeof new Number(1234)); // object
~~~

## 如何看待这些设计缺陷

既然Javascript有缺陷，数量还不少，那么它是不是一种很糟糕的语言？有没有前途？
回答是Javascript并不算糟糕，相反它的编程能力很强大，前途很光明。

* 如果遵守良好的编程规范，加上第三方函数库的帮助，Javascript的这些缺陷大部分可以回避。
* Javascript目前是网页编程的唯一语言，只要互联网继续发展，它就必然一起发展。目前，许多新项目大大扩展了它的用途，node.js使得Javascript可以用于后端的服务器编程，coffeeScript使你可以用python和ruby的语法，撰写Javascript。
* 只要发布新版本的语言标准（比如 ECMAscript 5），就可以弥补这些设计缺陷。当然，标准的发布和标准的实现是两回事，上述的很多缺陷也许会一直伴随到Javascript存在的最后一天。



