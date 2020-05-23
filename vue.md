## 怎么理解MVVM模式的这些框架？ 即Model-View-ViewModel
1. M就是Model层代表数据模型，定义数据修改和操作的业务逻辑。
2. V就是View视图层，它负责将数据模型转化成UI 展现出来，所有的html节点在这一层。
3. VM就是ViewModel，它通过data属性连接Model模型层，通过el属性连接View视图层。

Vue是以数据为驱动的，Vue自身将DOM和数据进行绑定，一旦创建绑定，DOM和数据将保持同步，每当数据发生变化， DOM会跟着变化。
ViewModel是Vue的核心，它是Vue的一个实例。Vue实例时作用域某个HTML元素上
DOM Listeners和Data Bindings是实现双向绑定的关键。 DOM Listeners监听页面所有 View层 DOM元素的变化，当发生变化， Model层的数据随之变化； Data Bindings 监听Model层的数据，当数据发生变化， View 层的 DOM元素随之变化。

## vue组件通信
* props


## vue生命周期
1. 什么是vue生命周期？
`Vue 实例从创建到销毁的过程，就是生命周期。也就是从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、卸载等一系列过程，我们称这是 Vue 的生命周期。`

2. vue生命周期的作用是什么？
`它的生命周期中有多个事件钩子，让我们在控制整个Vue实例的过程时更容易形成好的逻辑。`

3. vue生命周期总共有几个阶段？
`它可以总共分为8个阶段：创建前/后, 载入前/后,更新前/后,销毁前/销毁后`
创建前/后： 在beforeCreated阶段，vue实例的挂载元素$el和数据对象data都为undefined，还未初始化。在created阶段，vue实例的数据对象data有了，$el还没有。
载入前/后：在beforeMount阶段，vue实例的$el和data都初始化了，但还是挂载之前为虚拟的dom节点，data.message还未替换。在mounted阶段，vue实例挂载完成，data.message成功渲染。
更新前/后：当data变化时，会触发beforeUpdate和updated方法。
销毁前/后：在执行destroy方法后，对data的改变不会再触发周期函数，说明此时vue实例已经解除了事件监听以及和dom的绑定，但是dom结构依然存在

4. 第一次页面加载会触发哪几个钩子？
`第一次页面加载时会触发 beforeCreate, created, beforeMount, mounted 这几个钩子`

5. DOM 渲染在 哪个周期中就已经完成？
`DOM 渲染在 mounted 中就已经完成了。`

6. 简单描述每个周期具体适合哪些场景？
`生命周期钩子的一些使用方法：beforecreate: 可以在这加个loading事件，在加载实例时触发 created: 初始化完成时的事件写在这里，如在这结束loading事件，异步请求也适宜在这里调用 mounted: 挂载元素，获取到DOM节点 updated: 如果对数据统一处理，在这里写上相应函数 beforeDestroy: 可以做一个确认停止事件的确认框 nextTick: 更新数据后立即操作dom`



## vue-router 路由
1. active-class是哪个组件的属性？
`vue-router模块的router-link组件。`
2. 怎么定义vue-router的动态路由？怎么获取传过来的动态参数？ 
`在router目录下的index.js文件中，对path属性加上/:id。  使用router对象的params.id`
3. vue-router有哪几种导航钩子？    
`三种，一种是全局导航钩子：router.beforeEach(to,from,next)，作用：跳转前进行判断拦截。第二种：组件内的钩子；第三种：单独路由独享组件`
4. vue-router是什么？它有哪些组件？
`vue用来写路由一个插件。router-link、router-view`
5. 导航钩子有哪些？它们有哪些参数？
`导航钩子有：a/全局钩子和组件内独享的钩子。b/beforeRouteEnter、afterEnter、beforeRouterUpdate、beforeRouteLeave`
`参数：有to（去的那个路由）、from（离开的路由）、next（一定要用这个函数才能去到下一个路由，如果不用就拦截）最常用就这几种`
6. Vue的双向数据绑定原理是什么？
`vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。`
具体步骤：
第一步：需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter和getter
这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化
第二步：compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图
第三步：Watcher订阅者是Observer和Compile之间通信的桥梁，主要做的事情是:
1、在自身实例化时往属性订阅器(dep)里面添加自己
2、自身必须有一个update()方法
3、待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调，则功成身退。
第四步：MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。

## 基础

* v-show 指令， v-if 的区别
条件渲染指令，无论v-show的值为true或false，元素都会存在于HTML代码中； 
而只有当v-if的值为true，元素才会存在于HTML代码中。
v-show指令是通过修改元素的display的CSS属性让其显示或者隐藏
v-if指令是直接销毁和重建DOM达到让元素显示和隐藏的效果

* 如何让 css 只在当前组件中起作用
如果希望组件内写的css只对当前组件起作用，只需要在style中写入scoped，即：`<style scoped></style>`

* 指令 keep-alive 
keep-alive 的含义：把切换出去的组件保留在内存中，可以保留它的状态或避免重新渲染。
`<component :is='curremtView' keep-alive></component> `

* Vuejs 组件
vuejs 构建组件使用
Vue.component('componentName',{ /*component*/ }) ； 这里注意一点，组件要先注册再使用

* 为什么使用key？
`当有相同标签名的元素切换时，需要通过 key 特性设置唯一的值来标记以让 Vue 区分它们，否则 Vue 为了效率只会替换相同标签内部的内容`




* Vue.js 和 AngularJS 之间的区别是什么 ? 
Vue.js 是一个更加灵活开放的解决方案。它允许你以希望的方式组织你的应用程序，而不
是任何时候都必须遵循 Angular 制定的规则。它仅仅是一个视图层，所以你可以将它嵌入
一个现有页面而不一定要做成一个庞大的单页应用。 在结合其他库方面它给了你更大的的空
间，但相应，你也需要做更多的架构决策。例如， Vue.js 核心默认不包含路由和 ajax 功
能，并且通常假定你在用应用中使用了一个外部的模块构建系统。这可能是最重要的区别
在 API 和内部设计方面， Vue.js 比 Angular 简单得多 , 因此你可以快速地掌握它的全部
特性并投入开发。
Vue.js 拥有更好的性能，因为它不使用脏检查。当 watcher 越来越多时 , Angular 会变得
越来越慢，因为作用域内的每一次数据变更，所有的 watcher 都需要被重新求值。 Vue 则
根本没有这个问题， 因为它采用的是基于依赖追踪的观察系统， 所以所有的数据变更触发都
是独立的，除非它们之间有明确的依赖关系。
Vue.js 中指令和组件的概念区分得更为清晰。 指令只负责封装 DOM 操作，而组件代表一个
自给自足的独立单元 —— 它拥有自己的视图和数据逻辑。在 Angular 中它们两者间有不
少概念上的混淆。
* Vue.js 和 React.js 有什么区别 ? 
React.js 和 Vue.js 确实有一些相似——它们都提供数据驱动、可组合搭建的视图组件。
然而，它们的内部实现是完全不同的。 React 是基于 Virtual DOM ——一种在内存中描述
DOM 树状态的数据结构。 React 中的数据通常被看作是不可变的，而 DOM 操作则是通过
Virtual DOM 的 diff 来计算的。与之相比， Vue.js 中的数据默认是可变的，而数据的变
更会直接出发对应的 DOM 更新。相比于 Virtual DOM，Vue.js 使用实际的 DOM 作为模板，
并且保持对真实节点的引用来进行数据绑定。
Virtual DOM 提供了一个函数式的描述视图的方法，这很 cool 。因为它不使用数据观察机
制，每次更新都会重新渲染整个应用， 因此从定义上保证了视图通与数据的同步。 它也开辟
了 JavaScript 同构应用的可能性。
实话实说， 我自己对 React 的设计理念也是十分欣赏的。 但 React 有一个问题就是组件的
逻辑和视图结合得非常紧密。 对于部分开发者来说， 他们可能觉得这是个优点， 但对那些像
我一样兼顾设计和开发的人来说， 还是更偏好模板， 因为模板能让我们更好地在视觉上思考
设计和 CSS。JSX 和 JavaScript 逻辑的混合干扰了我将代码映射到设计的思维过程。 相反，
Vue.js 通过在模板中加入一个轻量级的 DSL ( 指令系统 ) ，换来一个依旧直观的模板，且能
够将逻辑封装进指令和过滤器中。
React 的另一个问题是：由于 DOM 更新完全交由 Virtual DOM 管理，当你真的想要自己控
制 DOM 是就有点棘手了 （虽然理论上你可以， 但这样做时你本质上在对抗 React 的设计思
想）。对于需要复杂时间控制的动画来说这就变成了一项很讨人厌的限制。 在这方面， Vue.js 
允许更多的灵活性，并且有不少用 Vue.js 构建的富交互实例

* 相同点
  - 都有组件化开发和Virtual DOM
  - 都支持props进行父子组件间数据通信
  - 都支持数据驱动视图，不直接操作真实DOM，更新状态数据界面就自动更新
  - 都支持服务端渲染
  - 都支持native的方案，React Native及Weex
* 不同点
  - 数据绑定：vue实现了数据的双向绑定， react数据流动是单向的
  - 组件写法不一样，React采用JSX, html和css全写进js中， vue单文件组件格式（html，css，js在同一个文件）
  - React中state数据，需要使用setState去改变
  - virtual Dom不一样， vue会跟踪每一个组件的依赖关系， 不需要重新渲染整个组件树，React每当应用状态改变时，全部组件都会重新渲染（使用shouldComponentUpdate控制）


## Vuex
Vuex是专门为vue应用程序开发的状态管理的vue插件， 集中式管理vue多个组件共享的状态和从后台获取的数据
