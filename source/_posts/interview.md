---
title: 面试题整理归纳
tags:
  - 面试
copyright: true
comments: true
date: 2018-06-23 10:58:48
categories: 知识
photos:
---
字符串扩展的方法
- includes()：返回布尔值，表示是否找到了参数字符串。数组也可以 a[1]=1 且能判断undefined
```javascript
var a=[1,2,3]
a[4]=5 // [1, 2, 3, undefined × 1, 5] empty
// a[3]=undefined [1, 2, 3, undefined, 5] 

a.indexOf(undefined) // -1
a.includes(undefined) // true 
```
- startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
- endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。
str | index
- repeat()：返回一个新字符串，表示将原字符串重复n次。参数如果是小数，会被取整(不四舍五入)。参数是负数或者Infinity，会报错。0/Nan返回空字符串,参数是字符串，则会先转换成数字。
- padStart()：头部补全。
- padEnd()：尾部补全
~~~
'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'

'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
~~~
如果原字符串的长度，等于或大于指定的最小长度，则返回原字符串。默认使用空格

---

<!-- more -->

- 模板字符串（template string）是增强版的字符串，用反引号\`标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。\`${表达式、变量}\`
- commonjs 服务器端 amd 浏览器端
- const 必须赋值定义 let 在同一作用于无法重复命名 无法变量提升
- split(字符串或者正则,设置长度) 字符串=>数组
- substr(开始的索引//splice可以为负数-1则为字符串最后一个字符,length字符数)方法不同的是,substring(开始索引，结束索引+1)负的参数有区别
只有单参数时到字符串结尾
String exd=filePath.subString(filePath.lastIndexOf(".")+1,filePath.length)

1. 声明函数作用提升?声明变量和声明函数的提升有什么区别?

(1) 变量声明提升：变量申明在进入执行上下文就完成了。
只要变量在代码中进行了声明，无论它在哪个位置上进行声明， js引擎都会将它的声明放在范围作用域的顶部；

(2) 函数声明提升：执行代码之前会先读取函数声明，意味着可以把函数申明放在调用它的语句后面。
只要函数在代码中进行了声明，无论它在哪个位置上进行声明， js引擎都会将它的声明放在范围作用域的顶部；

(3) 变量or函数声明：函数声明会覆盖变量声明，但不会覆盖变量赋值。
同一个名称标识a，即有变量声明var a，又有函数声明function a() {}，不管二者声明的顺序，函数声明会覆盖变量声明，也就是说，此时a的值是声明的函数function a() {}。注意：如果在变量声明的同时初始化a，或是之后对a进行赋值，此时a的值变量的值。
```javascript
eg: var a; var c = 1; a = 1; function a() { return true; } console.log(a);
```

2. 如何判断数据类型？
typeof返回的类型都是字符串形式，可以判断function的类型；在判断除Object类型的对象时比较方便。
判断已知对象类型的方法： instanceof，后面一定要是对象类型，并且大小写不能错，该方法适合一些条件选择或分支。
```javascript
typeof null // object null instanceof object // error
```

3. 异步编程？
- 方法1：回调函数，优点是简单、容易理解和部署，缺点是不利于代码的阅读和维护，各个部分之间高度耦合（Coupling），流程会很混乱，而且每个任务只能指定一个回调函数。

- 方法2：事件监听，可以绑定多个事件，每个事件可以指定多个回调函数，而且可以“去耦合”（Decoupling），有利于实现模块化。缺点是整个程序都要变成事件驱动型，运行流程会变得很不清晰。

- 方法3：发布/订阅，性质与“事件监听”类似，但是明显优于后者。

- 方法4：Promises对象，是CommonJS工作组提出的一种规范，目的是为异步编程提供统一接口。简单说，它的思想是，每一个异步任务返回一个Promise对象，该对象有一个then方法，允许指定回调函数。

4. 事件流？事件捕获？事件冒泡？
    事件流：从页面中接收事件的顺序。也就是说当一个事件产生时，这个事件的传播过程，就是事件流。

    IE中的事件流叫事件冒泡；事件冒泡：事件开始时由最具体的元素接收，然后逐级向上传播到较为不具体的节点（文档）。对于html来说，就是当一个元素产生了一个事件，它会把这个事件传递给它的父元素，父元素接收到了之后，还要继续传递给它的上一级元素，就这样一直传播到document对象（亲测现在的浏览器到window对象，只有IE8及以下不这样。

    事件捕获是不太具体的元素应该更早接受到事件，而最具体的节点应该最后接收到事件。他们的用意是在事件到达目标之前就捕获它；也就是跟冒泡的过程正好相反，以html的click事件为例，document对象（DOM级规范要求从document开始传播，但是现在的浏览器是从window对象开始的）最先接收到click事件的然后事件沿着DOM树依次向下传播，一直传播到事件的实际目标；

5. 如何添加一个dom对象到body中?innerHTML和innerText区别?
    body.appendChild(dom元素)；  
    innerHTML:从对象的起始位置到终止位置的全部内容,包括Html标签。
    innerText:从起始位置到终止位置的内容, 但它去除Html标签 
    window.clearInterval()
    window.clearTimeout()

6. 简述ajax流程  
1)客户端产生触发js的事件  
2)创建XMLHttpRequest对象  
```javascript 
var client=null
  if(window.XMLHttpRequest){
       client = new XMLHttpRequest();
  }else{
        client = new ActiveXObject("Microsoft.XMLHTTP");
  }
```
3)对XMLHttpRequest进行配置 
```javascript   
  client.open("GET", url);
  client.onreadystatechange = function(e) {
      if (request.readyState !== 4) { // client状态
        return;
      }
      if (request.status === 200) { // HTTP状态码
        console.log('success', request.responseText);
      } else {
        console.warn('error');
      }
  }; // 指定回调函数
  client.responseType = "json";
  client.setRequestHeader("Accept", "application/json;");
  client.setRequestHeader("Content-Type", "application/json;charset=utf-8");
```
4)通过AJAX引擎发送异步请求 
```javascript
  client.send()
```
5)服务器端接收请求并且处理请求，返回html或者xml内容  
6)XML调用一个callback()处理响应回来的内容  
7)使用JS和DOM实现局部刷新

7. 自执行函数？用于什么场景？好处？  
    1、声明一个匿名函数  
    2、马上调用这个匿名函数。  
    作用：创建一个独立的作用域。  

    好处：防止变量弥散到全局，以免各种js库冲突。隔离作用域避免污染，或者截断作用域链，避免闭包造成引用变量无法释放。利用立即执行特性，返回需要的业务函数或对象，避免每次通过条件判断来处理。

    场景：一般用于框架、插件等场景，设计私有变量和方法，封闭私有作用域。

8. 回调函数？（传递地址，由非实现方调用）  
回调函数就是一个通过函数指针调用的函数。如果你把函数的指针（地址）作为参数传递给另一个函数，当这个指针被用来调用其所指向的函数时，我们就说这是回调函数。回调函数不是由该函数的实现方直接调用，而是在特定的事件或条件发生时由另外的一方调用的，用于对该事件或条件进行响应。

9. 什么是闭包?堆栈溢出有什么区别？ 内存泄漏? 那些操作会造成内存泄漏？怎么样防止内存泄漏？impression  
    闭包：就是能够读取其他函数内部变量的函数。一般是指内层函数。(子函数在外调用，子函数所在的父函数的作用域不会被释放。) 

    堆栈溢出：就是不顾堆栈中分配的局部数据块大小，向该数据块写入了过多的数据，导致数据越界，结果覆盖了别的数据。经常会在递归中发生。

    内存泄露是指：用动态存储分配函数内存空间，在使用完毕后未释放，导致一直占据该内存单元。直到程序结束。指任何对象在您不再拥有或需要它之后仍然存在。

    造成内存泄漏：
    setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
    闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

    防止内存泄露：  
    1、不要动态绑定事件；      
    2、不要在动态添加，或者会被动态移除的dom上绑事件，用事件冒泡在父容器监听事件；  
    3、如果要违反上面的原则，必须提供destroy方法，保证移除dom后事件也被移除，这点可以参考Backbone的源代码，做的比较好；  
    4、单例化，少创建dom，少绑事件。  

10. html和xhtml有什么区别?
    HTML是一种基本的WEB网页设计语言，XHTML是一个基于XML的标记语言。

    1.XHTML 元素必须被正确地嵌套。

    2.XHTML 元素必须被关闭。

    3.标签名必须用小写字母。

    4.空标签也必须被关闭。

    5.XHTML 文档必须拥有根元素。

11. 什么是构造函数？与普通函数有什么区别?

    构造函数：是一种特殊的方法(函数、对象)、主要用来创建对象时初始化对象，总与new运算符一起使用，创建对象的语句中构造函数的函数名必须与类名完全相同。

    与普通函数相比只能由new关键字调用，构造函数是类的标识。

12. 通过new创建一个对象的时候，函数内部有哪些改变？
    ```javascript
    function Person(){}
    Person.prototype.friend = [];
    Person.prototype.age = 18;
     var a = new Person();
     a.friend[0] = '王琦'; // a.friend=['123'] 指向新对象 b.friend // []
     a.age = 18;
     var b = new Person();
     b.friend // ['王琦'] 
     b.age   // 18
    ```
    >1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。   
    >2、属性和方法被加入到 this 引用的对象中。  
    >3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。

`new 操作符新建了一个空对象，这个对象原型指向构造函数的prototype，执行构造函数后返回这个对象。`

13. 事件委托的好处都有啥？说对了都给它=3=
- 利用冒泡的原理，把事件加到父级上，触发执行效果  

- 好处：新添加的元素还会有之前的事件；提高性能。

14. 节点类型?判断当前节点类型?
- 元素节点 
- 属性节点 
- 文本节点 
- 注释节点 
- 文档节点

通过nodeObject.nodeType判断节点类型：其中，nodeObject 为DOM节点（节点对象）。该属性返回以数字表示的节点类型，例如，元素节点返回 1，属性节点返回 2 。

15. 数组合并的方法？
```javascript
// 四种方法。
var arr1=[1,2,3];
var arr2=[4,5,6];
arr1 = arr1.concat(arr2);
console.log(arr1); 

var arr1=[1,2,3];
var arr2=[4,5,6];
Array.prototype.push.apply(arr1,arr2);
console.log(arr1);

var arr1=[1,2,3];
var arr2=[4,5,6];
for (var i=0; i < arr2.length; i++) {
arr1.push( arr2[i] );
}
console.log(arr1); 

var arr1=[1,2,3];
var arr2=[4,5,6];

arr1.push(...arr2)
```

16. jquery和zepto有什么区别?
- 针对移动端程序，Zepto有一些基本的触摸事件可以用来做触摸屏交互（tap事件、swipe事件），Zepto是不支持IE浏览器的，这不是Zepto的开发者Thomas Fucks在跨浏览器问题上犯了迷糊，而是经过了认真考虑后为了降低文件尺寸而做出的决定，就像jQuery的团队在2.0版中不再支持旧版的IE（6 7 8）一样。因为Zepto使用jQuery句法，所以它在文档中建议把jQuery作为IE上的后备库。那样程序仍能在IE中，而其他浏览器则能享受到Zepto在文件大小上的优势，然而它们两个的API不是完全兼容的，所以使用这种方法时一定要小心，并要做充分的测试。

- Dom操作的区别：添加id时jQuery不会生效而Zepto会生效。

- zepto主要用在移动设备上，只支持较新的浏览器，好处是代码量比较小，性能也较好。
jquery主要是兼容性好，可以跑在各种pc，移动上，好处是兼容各种浏览器，缺点是代码量大，同时考虑兼容，性能也不够好。

17. $(function(){})和window.onload 和 $(document).ready(function(){})

- window.onload:用于当页面的所有元素，包括外部引用文件，图片等都加载完毕时运行函数内的函数。load方法只能执行一次，如果在js文件里写了多个，只能执行最后一个。

- $(document).ready(function(){})和$(function(){})都是用于当页面的标准DOM元素被解析成DOM树后就执行内部函数。这个函数是可以在js文件里多次编写的，对于多人共同编写的js就有很大的优势，因为所有行为函数都会执行到。而且$(document).ready()函数在HMTL结构加载完后就可以执行，不需要等大型文件加载或者不存在的连接等耗时工作完成才执行，效率高。

18. 简述下 this 和定义属性和方法的时候有什么区别?Prototype？

- this表示当前对象，如果在全局作用范围内使用this，则指代当前页面对象window； 如果在函数中使用this，则this指代什么是根据运行时此函数在什么对象上被调用。 我们还可以使用apply和call两个全局方法来改变函数中this的具体指向。

- prototype本质上还是一个JavaScript对象。 并且每个函数都有一个默认的prototype属性。

- 在prototype上定义的属性方法为所有实例共享，所有实例皆引用到同一个对象，单一实例对原型上的属性进行修改，也会影响到所有其他实例。

19. ajax和jsonp的区别？
- 相同点：都是请求一个url
- 不同点：ajax的核心是通过XMLHttpRequest获取内容
- jsonp的核心则是动态添加<script>标签来调用服务器提供的js脚本。

20. 常见的http协议状态码？

```javascript
200：请求成功
201：请求成功并且服务器创建了新的资源
302：服务器目前从不同位置的网页响应请求，但请求者应继续使用原有位置来响应以后的请求。
304：自从上次请求后，请求的网页未修改过。服务器返回此响应时，不会返回网页内容。
400：服务器不理解请求的语法。
404：请求的资源（网页等）不存在
403：该状态表示服务器理解了本次请求但是拒绝执行该任务
405：方法不被允许
500：内部服务器错误
```

21. sessionStorage和localstroage与cookie之间有什么关联, cookie最大存放多少字节？
```javascript
三者共同点：都是保存在浏览器端，且同源的。

区别:
1、cookie在浏览器和服务器间来回传递。而sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存

2、存储大小限制也不同，cookie数据不能超过4k，sessionStorage和localStorage 但比cookie大得多，可以达到5M

3、数据有效期不同，sessionStorage：仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持；localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据；cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭

4、作用域不同，sessionStorage不在不同的浏览器窗口中共享，即使是同一个页面(即数据不共享)；localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的( 即数据共享 )。
```

22. ajax的get与post区别？
- get和post都是数据提交的方式。
- get的数据是通过网址问号后边拼接的字符串进行传递的。post是通过一个HTTP包体进行传递数据的。
- get的传输量是有限制的，post是没有限制的。(实际上HTTP 协议从未规定 GET/POST 的请求长度限制是多少。对get请求参数的限制是来源与浏览器或web服务器，浏览器或web服务器限制了url的长度)
- get的安全性可能没有post高，所以我们一般用get来获取数据，post一般用来修改数据。
- get就是将货品放在车顶，post放在车内

23. GC机制？为什么闭包不会被回收变量和函数？
- GC：垃圾回收机制;  
- 外部变量没释放仍然保持着引用，所以指向的大函数内的小函数也释放不了。

24. 面向对象？
```javascript
万物皆对象，把一个对象抽象成类，具体上就是把一个对象的静态特征和动态特征抽象成属性（属性名、属性值）和方法，也就是把一类事物的算法和数据结构封装在一个类之中，程序就是多个对象和互相之间的通信组成的。

面向对象具有封装性，继承性，多态性。
封装：隐蔽了对象内部不需要暴露的细节，使得内部细节的变动跟外界脱离，只依靠接口进行通信。封装性降低了编程的复杂性。通过继承，使得新建一个类变得容易，一个类从派生类那里获得其非私有的方法和公用属性的繁琐工作交给了编译器。而继承和实现接口和运行时的类型绑定机制所产生的多态，使得不同的类所产生的对象能够对相同的消息作出不同的反应，极大地提高了代码的通用性。

总之，面向对象的特性提高了大型程序的重用性和可维护性。
```

25. jsonp的原理和缺点？
- 原理：使用script标签实现跨域访问，可在url中指定回调函数，获取JSON数据并在指定的回调函数中执行jquery实现jsop。
- 缺点：只支持GET方式的jsonp实现，是一种脚本注入行为存在一定的安全隐患。如果返回的数据格式有问题或者返回失败了，并不会报错。

26. call和apply两者的区别和好处？
- call和apply都是改变this指向的方法，区别在于call可以写多个参数，而apply只能写两个参数，第二个参数是一个数组，用于存放要传的参数。
- 用call和apply实现更好的继承和扩展，更安全。

27. 压缩合并目的？http请求的优化方式？
- Web性能优化最佳实践中最重要的一条是减少HTTP请求。而减少HTTP请求的最主要的方式就是，合并并压缩JavaScript和CSS文件。 

- CSS Sprites（CSS精灵）：把全站的图标都放在一个图像文件中，然后用CSS的background-image和background-position属性定位来显示其中的一小部分。 

- 合并脚本和样式表; 图片地图：利用image map标签定义一个客户端图像映射，（图像映射指带有可点击区域的一幅图像）具体看：http://club.topsage.com/thread-2527479-1-1.html 

- 图片js/css等静态资源放在静态服务器或CDN服时，尽量采用不用的域名，这样能防止cookie不会互相污染，减少每次请求的往返数据。 

- css替代图片, 缓存一些数据 

- 少用location.reload()：使用location.reload() 会刷新页面，刷新页面时页面所有资源 (css，js，img等) 会重新请求服务器。建议使用location.href="当前页url" 代替location.reload() ，使用location.href 浏览器会读取本地缓存资源。

28. commonjs?requirejs?AMD|CMD|UMD?
- CommonJS就是为JS的表现来制定规范，NodeJS是这种规范的实现，webpack 也是以CommonJS的形式来书写。因为js没有模块的功能，所以CommonJS应运而生。但它不能在浏览器中运行。 CommonJS定义的模块分为:{模块引用(require)} {模块定义(exports)} {模块标识(module)} 

- RequireJS 是一个JavaScript模块加载器。 RequireJS有两个主要方法(method): define()和require()。这两个方法基本上拥有相同的定义(declaration) 并且它们都知道如何加载的依赖关系，然后执行一个回调函数(callback function)。与require()不同的是， define()用来存储代码作为一个已命名的模块。 因此define()的回调函数需要有一个返回值作为这个模块定义。这些类似被定义的模块叫作AMD (Asynchronous Module Definition，异步模块定义)。 

- AMD 是 RequireJS 在推广过程中对模块定义的规范化产出 AMD异步加载模块。它的模块支持对象 函数 构造器 字符串 JSON等各种类型的模块。 适用AMD规范适用define方法定义模块。

- CMD是SeaJS 在推广过程中对模块定义的规范化产出
AMD与CMD的区别：
（1）对于于依赖的模块，AMD 是提前执行(好像现在也可以延迟执行了)，CMD 是延迟执行。
（2）AMD 推崇依赖前置，CMD 推崇依赖就近。
（3）AMD 推崇复用接口，CMD 推崇单用接口。
（4）书写规范的差异。

- umd是AMD和CommonJS的糅合。
AMD 浏览器第一的原则发展 异步加载模块。
CommonJS模块以服务器第一原则发展，选择同步加载，它的模块无需包装(unwrapped modules)。这迫使人们又想出另一个更通用的模式UMD ( Universal Module Definition ), 希望解决跨平台的解决方案。UMD先判断是否支持Node.js的模块( exports )是否存在，存在则使用Node.js模块模式。

29. js的几种继承方式？
- 使用对象冒充实现继承
- call、apply改变函数上下文实现继承
- 原型链方式实现继承

30. js原型、原型链，有什么特点？
```javascript
在JavaScript中,一共有两种类型的值,原始值和对象值.每个对象都有一个内部属性[[prototype]],我们通常称之为原型.原型的值可以是一个对象,也可以是null.如果它的值是一个对象,则这个对象也一定有自己的原型.这样就形成了一条线性的链,我们称之为原型链. 

访问一个对象的原型可以使用ES5中的Object.getPrototypeOf方法,或者ES6中的__proto__属性. 原型链的作用是用来实现继承,比如我们新建一个数组,数组的方法就是从数组的原型上继承而来的。

类的继承
特点：基于原型链，既是父类的实例，也是子类的实例
缺点：无法实现多继承

构造继承、实例继承和拷贝继承...
```

31. eval是做什么的？
- 将把对应的字符串解析成JS代码并运行； 应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。

32. null和undefined
- undefined表示变量声明未初始化的，null表示对象的空值（空对象指针）。

33. json的理解？
- JSON（轻量级的数据交换格式），基于JS的子集，数据格式简单，易于读写，占用带宽小。
```javascript
JSON.parse() // 解析成JSON对象

JSON.strinify() // 解析成JSON字符串
```

34. js延时加载的方式？
- defer和async
- 动态创建DOM
- 按需异步加载JS

35. ajax（异步的js和xml）
- ajax是指一种创建交互式网页应用的网页开发技术。通过后台与服务器进行少量数据交换，AJAX可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

36. 同异步的区别？
- 同步(sync)：按顺序执行。
- 异步(async)：不按顺序执行，可以跳过执行下面的代码。

37. ajax的缺点？
- 不支持浏览器的back按钮(事件由浏览器内核控制)
- ajax暴露了与服务器的交互
- 对搜索引擎的支持较弱
- 破坏了程序的异常机制
- 不容易调试

38. 跨域问题？
- 协议不同
- 端口不同
- 域名不同
- 常用解决方案：jsonp、iframe、window.name、window.postMessage、服务器设置代理页面/header配置cors

39. 解决异步回调地狱有哪些方案？
promise、generator、async/await

40. 图片的预加载和懒加载？
- 预加载：提前加载图片，当用户需要查看时可直接从本地缓存中渲染。
- 懒加载：懒加载的主要目的是作为服务器前端的优化，减少请求数或延迟请求数。

两种技术的本质：两者的行为是相反的，一个是提前加载，一个是迟缓甚至不加载。 懒加载对服务器前端有一定的缓解压力作用，预加载则会增加服务器前端压力。

41. mouseover和mouseenter的区别？
- mouseover：当鼠标移入元素或其子元素都会触发事件，所以有一个重复触发，冒泡的过程。对应的移除事件是mouseout

- mouseenter：当鼠标移除元素本身（不包含元素的子元素）会触发事件，也就是不会冒泡，对应的移除事件是mouseleave

42. 改变函数内部this指针的指向函数（bind，apply，call的区别）？
- 通过apply和call改变函数的this指向，他们两个函数的第一个参数都是一样的表示要改变指向的那个对象，第二个参数，apply是数组，而call则是arg1,arg2...这种形式。

- 通过bind改变this作用域会返回一个新的函数，这个函数不会马上执行。

43.  说说前端中的事件流
HTML中与javascript交互是通过事件驱动来实现的，例如鼠标点击事件onclick、页面的滚动事件onscroll等等，可以向文档或者文档中的元素添加事件侦听器来预订事件。想要知道这些事件是在什么时候进行调用的，就需要了解一下“事件流”的概念。
什么是事件流：事件流描述的是从页面中接收事件的顺序,DOM2级事件流包括下面几个阶段。

事件捕获阶段
处于目标阶段
事件冒泡阶段

addEventListener：addEventListener 是DOM2 级事件新增的指定事件处理程序的操作，这个方法接收3个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。最后这个布尔值参数如果是true，表示在捕获阶段调用事件处理程序；如果是false，表示在冒泡阶段调用事件处理程序。
IE只支持事件冒泡。

44. 如何让事件先冒泡后执行？
在DOM标准事件模型中，是先捕获后冒泡。但是如果要实现先冒泡后捕获的效果，对于同一个事件，监听捕获和冒泡，分别对应相应的处理函数，监听到捕获事件，先暂缓执行，直到冒泡事件被捕获后再执行捕获事件。

45. 什么是事件委托？
简介：事件委托指的是，不在事件的发生地（直接dom）上设置监听函数，而是在其父元素上设置监听函数，通过事件冒泡，父元素可以监听到子元素上事件的触发，通过判断事件发生元素DOM的类型，来做出不同的响应。


举例：最经典的就是ul和li标签的事件监听，比如我们在添加事件时候，采用事件委托机制，不会在li标签上直接添加，而是在ul父元素上添加。


好处：比较合适动态元素的绑定，新添加的子元素也会有监听函数，也可以有事件触发机制。

45. 垂直居中
- margin:auto法 relative -> absolute -> marin:0 auto
- margin负值法 relative -> absolute -> top:50% left:50% marin-top:height的一半 margin-left:width的一半或者transform：translateX(-50%)和transform：translateY(-50%)
- table-cell未脱离文档流 设置父元素的display:table-cell,并且vertical-align:middle，这样子元素可以实现垂直居中。
- flex布局

46. visibility=hidden, opacity=0，display:none
- opacity=0，该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定一些事件，如click事件，那么点击该区域，也能触发点击事件的
- visibility=hidden，该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件。
- display=none，把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素删除掉一样。

47. 块元素和行内元素
- 块元素：独占一行，并且有自动填满父元素，可以设置margin和padding以及高度和宽度。
- 行元素：不会独占一行，width和height会失效，并且在垂直方向的padding和margin会失效。    

48. 深拷贝
- 深拷贝的方法 1-2适用于一般的对象和数组 4-5适用于数组 3通用
let obj = {
    a: 1,
    arr: [1, 2]
};
let obj2 = deepCopy(obj);
obj2.a = 2
console.log(obj) // { a:1, arr: [1,2] };
2.es6
Object.assign()方法(深复制只有一层，之后为浅复制（除非再次使用Object.assign嵌套方式赋值）)
let obj = {
    a: 1,
    arr: [1, 2]
};
let obj1 = Object.assign({}, obj);
obj1.a = 2
//不变
console.log(obj) // { a:1, arr: [1,2] };
3.immutable
4.arr1=arr.slice(0) slice() 返回新数组
5.arr1=arr.concat()
var deepCopy= function(source) { 
    var result={};
    for (var key in source) {
        result[key] = typeof source[key]==='object'? deepCoypy(source[key]): source[key];
     } 
   return result; 
}

49. 判断一个变量是否是数组
```javascript
var a = []; 
// 1.基于instanceof 
a instanceof Array; 
// 2.基于constructor 
a.constructor === Array; 
// 3.基于Object.prototype.isPrototypeOf 
Array.prototype.isPrototypeOf(a); 
// 4.基于getPrototypeOf 
Object.getPrototypeOf(a) === Array.prototype; 
// 5.基于Object.prototype.toString 
Object.prototype.toString.apply(a) === '[object Array]';
// 6.Array.isArray
Array.isArray([]); // true
```
以上，除了Object.prototype.toString外，其它方法都不能正确判断变量的类型。

49. 优化
- 按需加载路由
- 代码拆分
- 第三方库提取vendor

- 压缩文件图片，合并文件 减少http请求
- 网络图、字体图标
- 上cnd

50. 行内、块级、空元素 
- 行内元素：a、b、span、img、input、strong、select、label、em、button、textarea
- 块级元素：div、ul、li、dl、dt、dd、p、h1-h6、blockquote
- 空元素：即没有内容的HTML元素，例如：br、meta、hr、link、input、img

51. px、em、rem的区别
px和em都是长度单位,px的只是固定的,em的值是相对的继承父类元素的字体大小。浏览器的默认字体高位16px。1em=16px;
rem单位基于html元素的字体大小