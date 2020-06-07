## 描述new一个对象额过程
```js
/*
 1. 创建一个新对象
 2. this指向这个新对象
 3. 执行代码 即对this赋值
 4. 返回this（默认）
*/
function Foo(name){
  this.name = name
  // return this 默认有着一行
}
```

##  