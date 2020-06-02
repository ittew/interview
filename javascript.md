#### JavaScript的数据类型都有什么？
* 基本数据类型：String,boolean,Number,Undefined, Null, symbol(es6), bigint(es10)
* 引用数据类型：Object(Array,Date,RegExp,Function)
#### javascript的typeof返回哪些数据类型
1. javascript的typeof返回那些数据类型？
`object number function boolean undefined string symbol bigint`

2. 检测数组的几种方式
`Array.isArray(arr)`
`arr.toString().call([]) // [Object Array]`
```js
// 获取数据类型 类似typeof 但比typeof强大
function getType(v){
  // .+?  惰匹匹配
  return Object.prototype.toString.call(v).match(/\[object (.+?)\]/)[1].toLowerCase()
}
getType([]) // "array"
getType(NaN) // "number"
getType(Symbol(1)) // "symbol"
getType(BigInt("9007199254740995")) // "bigint"
getType(null) // "null"
getType(undefined) // "undefined"
getType('0') // "string"
getType({}) // "object"
getType(parseInt) // "function"
getType(new Date()) // "date"
```
#### 事件绑定和普通事件有什么区别
* 普通事件onclick的方法不支持添加多个事件，最下面的事件会覆盖上面的
* 事件绑定（addEventListener）方式添加事件可以添加多个, 支持事件冒泡和事件捕获

#### call和apply的区别
* 参数的不同 call 第二个参数以后是参数列表  apply第二个参数是参数序列（数组）

#### window.onload和$(document).ready区别
* window.onload 是在dom文档树加载完和所有文件加载完之后执行的函数
* $(document).ready 在dom文档树加载完之后执行的函数（文档树加载完不代表全部文件加载完）
* $(document).ready要比window.onload先执行
* window.onload只能出来一次，$(document).ready可以出现多次

#### 判断数组方式
```js
if(typeof Array.isArray === "undefined"){
  Array.isArray = function(arg){
     return Object.prototype.toString.call(arg)==="[object Array]"
  }
}
```

#### Javascript中callee和caller的作用？
* caller是返回一个对函数的引用，该函数调用了当前函数；
* callee是返回正在被执行的function函数，也就是所指定的function对象的正文。

#### 谈谈Cookie的弊端？
* Cookie数量和长度的限制。每个domain最多只能有20条cookie，每个cookie长度不能超过4KB，否则会被截掉。
* 安全性问题。如果cookie被拦截了，就可以取得所有的session信息。即使加密也与事无补，因为拦截者并不需要知道cookie的意义，他只要原样转发cookie就可以达到目的了。

#### 哪些操作会造成内存泄漏？
* 内存泄漏: 指任何对象在您不再拥有或需要它之后仍然存在
* 垃圾回收: 如果一个对象的引用数量为0(没有其他对象引用过该对象)，那么该对象的内存即可回收。
1. setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
2. 闭包
3. 控制台日志
4. 循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

#### javascript 中的垃圾回收机制？
* 在Javascript中，如果一个对象不再被引用，那么这个对象就会被GC回收。如果两个对象互相引用，而不再  被第3者所引用，那么这两个互相引用的对象也会被回收。

#### 获取非行间样式
```js
function getStyle(obj,attr,value){
  return obj.currentStyle ? obj.currentStyle(attr) : obj.getComputedStyle(attr, false)
}
```

#### 事件委托是什么
* 利用事件冒泡的原理，自己要触发的事件，让他的父元素代替执行！

#### 原生ajax步骤
```js
var xhr =null;//创建对象 
if (window.XMLHttpRequest) {
	xhr = new XMLHttpRequest()
} else {
	xhr = new ActiveXObject("Microsoft.XMLHTTP")
}
xhr.open('方式','地址','标志位') // 初始化请求 
xhr.setRequestHeader('', '') // 设置http头信息 
xhr.onreadystatechange = function(){} // 指定回调函数 
xhr.send() // 发送请求 
```

#### 请解释一下 JavaScript 的同源策略。
* 同源策略是一种安全协议，指一段脚本只能读取来自同一来源的窗口和文档的属性。所谓同源指的是：协议，域名，端口三者都相同

#### 一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？
1. 当发送一个 URL 请求时，浏览器都会开启一个线程来处理这个请求，同时在远程 DNS 服务器上启动一个 DNS 查询。这能使浏览器获得请求对应的 IP 地址。
2. 浏览器与远程 Web 服务器通过 TCP 三次握手协商来建立一个 TCP/IP 连接。该握手包括一个同步报文，一个同步-应答报文和一个应答报文，这三个报文在 浏览器和服务器之间传递。该握手首先由客户端尝试建立起通信，而后服务器应答并接受客户端的请求，最后由客户端发出该请求已经被接受的报文。
3. 一旦 TCP/IP 连接建立，浏览器会通过该连接向远程服务器发送 HTTP 的 GET 请求。远程服务器找到资源并使用 HTTP 响应返回该资源，值为 200 的 HTTP 响应状态表示一个正确的响应。
4. 此时，Web 服务器提供资源服务，客户端开始下载资源。

#### 什么是伪数组？如何将伪数组转化为标准数组？
* 伪数组（类数组）：无法直接调用数组方法或期望length属性有什么特殊的行为，但仍可以对真正数组遍历方法来遍历它们.如 argument, NodeList
* 可以使用Array.prototype.slice.call(argument)将数组转化为真正的Array对象

#### javascript继承的方法
1. 原型链继承
2. 借用构造函数继承
3. 组合继承(原型+借用构造)
4. 原型式继承
5. 寄生式继承
6. 寄生组合式继承

#### 关于javascript中apply()和call()方法的区别？
* 相同点:两个方法产生的作用是完全一样的
* 不同点:方法传递的参数不同
```js
Object.call(this,obj1,obj2,obj3)
Object.apply(this,arguments)
// apply()接收两个参数，第一个是函数运行的作用域(this)，另一个是参数数组。
// call()接收多个参数方法, 第一个参数为函数运行的作用域(this)，其他参数为传递给函数的参数列表
```

#### 通用的事件侦听器函数
```js
markyun.Event = {
  // 页面加载完成后
  readyEvent: function(fn) {
    if (fn==null) {
      fn=document
    }
    var oldonload = window.onload
    if (typeof window.onload != 'function') {
      window.onload = fn
    } else {
      window.onload = function() {
          oldonload()
          fn()
      }
    }
  },
  // 视能力分别使用dom0||dom2||IE方式 来绑定事件
  // 参数： 操作的元素,事件名称 ,事件处理程序
  addEvent: function(element, type, handler) {
    if (element.addEventListener) {
      //事件类型、需要执行的函数、是否捕捉
      element.addEventListener(type, handler, false)
    } else if (element.attachEvent) {
      element.attachEvent('on' + type, function() {
        handler.call(element)
      })
    } else {
      element['on' + type] = handler
    }
  },
  // 移除事件
  removeEvent: function(element, type, handler) {
    if (element.removeEnentListener) {
      element.removeEnentListener(type, handler, false)
    } else if (element.datachEvent) {
      element.detachEvent('on' + type, handler)
    } else {
      element['on' + type] = null
    }
  }, 
  // 阻止事件 (主要是事件冒泡，因为IE不支持事件捕获)
  stopPropagation: function(ev) {
    if (ev.stopPropagation) {
      ev.stopPropagation()
    } else {
      ev.cancelBubble = true
    }
  },
  // 取消事件的默认行为
  preventDefault : function(event) {
    if (event.preventDefault) {
      event.preventDefault()
    } else {
      event.returnValue = false
    }
  },
  // 获取事件目标
  getTarget: function(event) {
    return event.target || event.srcElement
  },
  // 获取event对象的引用，取到事件的所有信息，确保随时能使用event；
  getEvent: function(e) {
    var ev = e || window.event
    if (!ev) {
      var c = this.getEvent.caller
      while (c) {
        ev = c.arguments[0]
        if (ev && Event == ev.constructor) {
          break
        }
        c = c.caller
      }
    }
    return ev
  }
}
```

#### javascript继承的方式？
`原型链继承 借用构造函数继承 原型+构造函数继承 寄生式继承`
```js
// 1. 原型链继承
function Animal () {
  this.age = 20
}
function Cat () {
  this.name = 'jack'
}
var cat = new Cat()
console.log(cat.name); // jaack
console.log(cat.age); // undefined
// 让Cat对象拥有了Animal对象的属性和方法
Cat.prototype = new Animal()
var cat = new Cat()
console.log(cat.name); // jaack
console.log(cat.age); // 20

// 2. 借用构造函数继承
function Animal () {
  this.age = 20
}
function Cat () {
  // Cat的所有对象借用了Animal对象的构造函数
  Animal.call(this)
  this.name = 'jack'
}
var cat = new Cat()
console.log(cat.name); // jaack
console.log(cat.age); // 20

// 3. 原型 + 构造函数继承组合继承
// 4. 寄生式继承
function Person(name, age){
  this.name = name
  this.age = age
}
function  createPerson(name, age){
  var obj = {}
  Person.call(obj, name, age)
  return obj
}
var person = createPerson('tew', 28)
console.log(person) // {name: "tew", age: 28}
console.log(person.constructor) // ƒ Object() { [native code] }
```

#### 如何理解闭包?
使用闭包主要是为了设计私有的方法和变量.
闭包的优点是可以避免全局变量的污染
闭包的缺点是变量会常驻内存,会增大内存使用量,使用不当很容易造成内存泄漏
闭包的三个特性:
  函数嵌套函数
  函数内部可以引用外部的参数和变量
  参数和变量不会被垃圾回收机制回收


#### 用js将字符串str的所有单词的首字母大写
```js     
var test = 'a tom is stupid,sda.';
var a = test.replace(/\b\w+\b/g,function(word){
  return word.substr(0,1).toUpperCase() + word.substr(1)
})
console.log(a)  // A Tom Is Stupid,Sda.
```

#### “use strict” 严格模式有哪些问题
A.全局变量必须显示声明,给一个未用var声明的全局变量赋值会报错
B.禁止删除变量, configurable设置为true的属性才能被删除
C.对象不能有重名的属性,函数不能有重名的参数
D.函数必须声明在顶层(if/for中声明函数会报错)

#### 栈和队列的区别
栈的插入和删除操作都是在一端进行的,而队列的操作却是在两端进行的.
队列先进先出,栈先进后出
栈只允许在末尾一端进行插入和删除,而队列只允许在末尾插入,在表头一端进行删除

#### 栈和堆的区别
栈区(stack) 由编译器自动分配释放, 存放函数的参数值,局部变量的值等     一种先进后出的数据结构
堆区(heap)  一般由程序员分配释放, 若程序员不释放,程序结束时可能被系统回收.   堆可以被看成是一棵树



## 其他
* `注意: 一个函数的父级作用域是它定义时的作用域  而不是他执行时的作用域`
