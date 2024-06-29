---
title: "Vscode（视频版）"
date: 2024-02-21T16:00:01+08:00
draft: false
tags:
  - Vue
  - FE
categories:
  - FE
---

# 一、初识 Vue :

## 1.步骤：

想让 Vue 工作，就必须**创建一个 Vue 实例**，且要**传入一个配置对象**;

<video id="video" controls=""src="D:\哔哩哔哩 (゜-゜)つロ 干杯~-bilibili.webm" preload="none">

## 2.规范：

root 容器里的代码依然符合 html 规范，只不过混入了一些特殊的**Vue 语法**;

Vue 实例和容器是一一对应的；

真实开发中只有一个 Vue 实例，并且会配合着组件一起使用

{{xxx}}中的 xxx 要写 js 表达式，且 xxx 可以自动读取到 data 中的所有属性

# 二、Vue 模板语法

## 1.模板：

root 容器里的代码被称为**[Vue 模板];**

## 2.语法

### 1.插值语法：

​ 功能：用于解析标签体内容

​ 写法：{{xxx}}，xxx 是 js 表达式，且可以直接读取到 data 中的所有属性。

### 2.指令语法：

​ 功能：用于解析标签体内容

​ 举例：v-bind:href="xxx" 或 简写为 :href="xxx"，xxx 同样要写 js 表达式

​ 且可以直接读取到 data 中的所有属性。

​ 备注：Vue 中有很多的指令，且形式都是： v-????，可多层表示

# 三、数据绑定

- 1.单向绑定(v-bind)：数据只会从 data 流向页面

- 2.双向绑定(v-model)：数据不仅能从 data 流向页面，还可以从页面流向 data

  - 备注：

  1. 双向绑定一般都应用在表单类元素(如：input、select 等)
  2. v-mode:value 可以简写为 v-model，因为 v-model 默认收集就是 value 值

# 四、el 与 data 的两种写法

- 1.el 的两种写法

  - (1)new Vue 时候配置 el 属性。
  - (2)先创建 Vue 实例，随后再通过 vm.$mount('root')指定 el 的值

- 2.data 又两种写法

  - (1)对象式

  - (2)函数式

    如何选择:目前都可以，组件时候必须函数式

- 3.一个重要原则

  - 由 Vue 管理的函数，一定不要写箭头函数，一旦写了箭头函数，this 将是 window，不是 Vue 实例了

# 五、MVVM 模型

1. M：模型(Model)：data 中的数据

2. V：视图(View)：模板代码

3. VM：视图模型(ViewModel)：Vue 实例

   规律：

   1. data 中的所有的属性，最后都出现在了 vm 身上
   2. vm 身上所有的属性及 Vue 原型上所有属性，在 Vue 模板中都可以直接使用

# 六、数据代理

1. Vue 中的数据代理:
   通过 vm 对象来代理 data 对象中属性的操作(读/写)

2. Vue 中数据代理的好处

   ​ 更加方便的操作 data 中的数据

3. 基本原理：

   ​ 通过 Object.defineProperty()把 data 对象中所有属性添加到 vm 上

   ​ 为每一个添加到 vm 上的属性，都指定一个 getter/setter

   ​ 在 getter/setter 内部去操作（读/写）data 中对应的属性

# 七、事件处理

## 1.事件的基本使用：

1. 使用 v-on:xxx 或 @xxx 绑定事件，其中 xxx 是事件名;

2. 事件的回调需要配置在 methods 对象中，最终会在 vm 上;

3. methods 中配置的函数，不要用箭头函数！否则 this 就不是 vm 了;

4. methods 中配置的函数，都是被 Vue 所管理的函数，this 的只想是 vm 或组件实例对象

5. @click="demo" 和 @click="demo($event)"效果一致，但后者可以传参

## 2.Vue 中的事件修饰符:

1. prevent:阻止默认事件(常用);

2. stop:阻止事件冒泡(常用) ;

3. once:事件只触发一次(常用) ;

4. capture:使用事件的捕获模式;

5. self:只有 event . target 是当前操作的元素时才触发事件;

6. passive:事件的默认行为立即执行，无需等待事件回调执行完毕;

## 3.键盘事件

1. ### Vue 中常用的按键别名:

   - 回车 => enter

   - 删除 => delete (捕获"删除"和"退格"键)

   - 退出 => esc

   - 空格 => space

   - 换行 => tab （特殊，必须配合 keydown 去使用）

   - 上 => up

   - 下 => down

   - 左 => left

   - 右 => right

2. ### 绑定方法

   1. Vue 未提供别名的按键，可以使用按键原始的 key 值去绑定，但注意要转为 kebab-case（短横线命名）

   2. 系统修饰符（用法特殊）: ctrl、alt、shift、meta

      （1）配合 keyup 使用：按下修饰键的同时，在按下其他键，随后释放其他键，事件才被触发。

      （2）配合 keydown 使用：正常触发事件。

   3. 也可以使用 keyCode 去指定具体的按键（不推荐）

   4. Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名

      注：修饰符可以连写，例如：event.stop.prevent event.ctrl.y

# 八、计算属性

## 1.定义：

要用的属性不存在，要通过已有**属性**计算得来

## 2.原理：

底层接住了 object.defineproperty 方法提供的 getter 和 setter

## 3.get 函数什么时候执行？

1.初次读取时会执行一次

2.所依赖的数据发生变化时会被再次调用

## 4.优势:

与 methods 实现相比,内部有缓存机制(复用)，效率更高，调试方便

## 5.备注

1. 计算属性最终会出现在 vm 上，直接读取使用即可。
2. 如果计算属性要被修改，那必须写 set 函数去响应修改，且 set 中要引起计算时依赖的数据发生改变

## 6.简写

前提：**只考虑简写不考虑修改时候**

get 省略直接成为（）

```vue
计算属性名(){ console.log() return …… }
```

# 九、监视属性

## 1.监视属性 watch：

1. 当被监视的属性变化时，回调函数自动调用，进行相关操作

2. 监视的属性必须存在，才能进行监视！！

3. 监视的两种写法：

   （1）new Vue 时传入 watch 配置

   （2）通过 vm.$watch 监视

## 2.深度监视

1. Vue 中的 watch 默认不监测对象内部值的改变

2. 配置 deep：true 可以检测对象内部值改变（多层）

   备注：

   （1）Vue 自身可以检测对象内部值的改变，但 Vue 提供的 watch 默认不可以

   （2）使用 watch 时根据数据的具体结构，决定是否采用深度检测

## 总结:

computed 和 watch 之间的区别:

1. computed 能完成的功能，watch 都可以完成

2. watch 能完成的功能，computed 不一定能完成，例如：watch 能进行异步操作。

   两个重要的小原则：

   1. 所被 Vue 管理的函数，最好写成普通函数，这样 yhis 的指向才是 vm 或 组件实例对象

   2. 所有不被 Vue 所管理的函数（定时器的回调函数，ajax 的回调函数等），最好携程箭头函数。

      这样 this 的指向才是 vm 或组件实例对象

# 十、绑定样式

## 1.class 样式：

- 写法：class="xxx" xxx 可以是字符串、对象、数组

  ​ 字符串写法适用于：类名不确定，要动态获取

  ​ 对象写法适用于：要绑定多个样式，个数不确定，名字也不确定

  ​ 数组写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用

## 2.style 样式

- :style 样式="{fontSize: xxx}"其中 xxx 是动态值
- :style="[a,b]"其中 a、b 是样式对象

# 十一、条件渲染

## 1.v-if

- 写法：

  - （1).v-if="表达式"

  - （2).v-else-if="表达式"

  - （3).v-else="表达式"

    - 适用于：切换频率较低的场景。

    - 特点：不展示的 DOM 元素直接被移除。
    - 注意：v-if 可以和:v-else-if、v-else 一起使用，但要求结构不能被“打断”。

## 2.v-show

- 写法：v-show="表达式”

- 适用于：切换频率较高的场景。

- 特点：不展示的 DOM 元素未被移除，仅仅是使用样式隐藏掉

## 3.备注：

使用 v-if 的时，元素可能无法获取到，而使用 v-show 一定可以获取到。

## 4.v-for 指令

1. 用于展示列表数据
2. 语法：v-for="(item,index) in xxx" :key="yyy"
   1. 可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）

## 注：

## 面试题：react、vue 中的 key 有什么作用？（key 的内部原理）

### 1.虚拟 DOM 中 key 的作用：

- key 是虚拟 DOM 对象的标识，当数据发生变化时，Vue 会根据【新数据】生成【新的虚拟 DOM】，
- 随后 Vue 进行【新虚拟 DOM】与【I 旧虚拟 DOM】的差异比较，比较规则如下：

### 2.对比规则：

- (1)旧虚拟 DOM 中找到了与新虚拟 DOM 相同的 key：

  - ①.若虚拟 DOM 中内容没变，直接使用之前的真实 DOM！

  - ②.若虚拟 DOM 中内容变了，则生成新的真实 DOM，随后替换掉页面中之前的真实 DOM。

- (2)旧虚拟 DOM 中未找到与新虚拟 DOM 相同的 key

  - 创建新的真实 DOM，随后渲染到到页面。

### 3.用 index 作为 key 可能会引发的问题：

1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作：

   - 会产生没有必要的真实 DOM 更新==>界面效果没问题，但效率低。

2. 如果结构中还包含输入类的 DOM：会产生错误 DOM 更新==>界面有问题。

### 4.开发中如何选择 key？

1. 最好使用每条数据的唯一标识作为 key，比如 id、手机号、身份证号、学号等唯一值。

2. 如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，

   使用 index 作为 key 是没有问题的。

# 十二、Vue 监视数据的原理

## 1.vue 会监视 data 中所有层次的数据。

## 2.如何检测对象中的数据？

​ 通过 setter 实现监视，且要在 new Vue 时就传入要检测的数据

​ （1）对象中后追加的属性，Vue 默认不做响应式处理

​ （2）如需给后添加的属性做响应式，使用如下 API：

```vue
Vue.set(target, propertyName/index, value)或 vm.$set(target, propertyName/index,
value)
```

## 3.如何检测数组中的数据？

​ 通过包裹数组更新元素的方法实现，本质做两件事：

​ （1）调用原生对应的方法对数组进行更新。

​ （2）重新解析模板，进而更新页面

## 4.在 Vue 修改数组中的某个元素一定要用如下方法：

​ 1.使用这些 API：push()、pop()、unshift()、shift()、splice()、sort()、reverse()

​ 2.Vue.set() 或 vm.$set()

特别注意：Vue.set() 和 vm.$set() 不能给 vm 或 vm 的跟数据对象添加属性！！！

# 十三、收集表单数据

1.若：<input type="text"/>,则 v-model 收集的是 value 值，用户输入的就是 value 值。

2.若：<input type="radio"/>则 v-model 收集的是 value 值，且要给标签配置 value 值。

3.若：<input type="checkbox"/>

​ 1.没有配置 input 的 value 属性，那么收集的就是 checked（勾选 or 未勾选，是布尔值）

​ 2.配置 input 的 value 属性：

​ （1）v-model 的初始值是非数组，那么收集的就是 checked（勾选 or 未勾选，是布尔值）

​ （2)v-model 的初始值是数组，那么收集的的就是 value 组成的数组

备注：V-model 的三个修饰符：

- lazy：失去焦点再收集数据
- number：输入字符串转为有效的数字
- trim：输入首尾空格过滤

# 十四、过滤器

1.定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。 2.语法： 1.注册过滤器：Vue.filter(name,callback) 或 new Vue{filters:{}} 2.使用过滤器：{{ xxx | 过滤器名}} 或 v-bind:属性 = "xxx | 过滤器名"
备注： 1.过滤器也可以接收额外参数、多个过滤器也可以串联 2.并没有改变原本的数据, 是产生新的对应的数据

# 十五、内置指令

## 1.已学过：

​ v-bind : 单向绑定解析表达式, 可简写为 :xxx

​ v-model : 双向数据绑定

​ v-for : 遍历数组/对象/字符串

​ v-on : 绑定事件监听, 可简写为@

​ v-if : 条件渲染（动态控制节点是否存存在）

​ v-else : 条件渲染（动态控制节点是否存存在）

​ v-show : 条件渲染 (动态控制节点是否展示)

## 2.未学过：

v-text 指令：

​ 1.作用：向其所在的节点中渲染文本内容。 (纯文本渲染)

​ 2.与插值语法的区别：v-text 会替换掉节点中的内容，{{xx}}则不会。这里有点不太灵活

v-cloak 指令（没有值）： 1.本质是一个特殊属性，Vue 实例创建完毕并接管容器后，会删掉 v-cloak 属性。 2.使用 css 配合 v-cloak 可以解决网速慢时页面展示出{{xxx}}的问题。

v-once 指令：
1.v-once 所在节点在初次动态渲染后，就视为静态内容了。 2.以后数据的改变不会引起 v-once 所在结构的更新，可以用于优化性能。

# 十六、自定义指令

1、定义语法：

​ (1).局部指令：

​ new Vue({directives:{指令名:配置对象} }) 或 new Vue({directives: {指令名:回调函数}})

​ (2).全局指令：

​ Vue.directive(指令名,配置对象) 或 Vue.directive(指令名,回调函数)

2、配置对象中常用的 3 个回调：

​ (1).bind：指令与元素成功绑定时调用。

​ (2).inserted：指令所在元素被插入页面时调用。

​ (3).update：指令所在模板结构被重新解析时调用。

3、备注：

​ 1.指令定义时不加 v-，但使用时要加 v-；

​ 2.指令名如果是多个单词，要使用 kebab-case 命名方式，不要用 camelCase 命名。

# 十七、生命周期

1.又名：生命周期回调函数、生命周期函数、生命周期钩子。

2.是什么：Vue 在关键时刻帮我们调用的一些特殊名称的函数。

3.生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。

4.生命周期函数中的 this 指向是 vm 或 组件实例对象。

5.常用的生命周期钩子：

- 1.mounted: 发送 ajax 请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】。

- 2.beforeDestroy: 清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】。

- 关于销毁 Vue 实例

  1. 销毁后借助 Vue 开发者工具看不到任何信息。
  2. 销毁后自定义事件会失效，但原生 DOM 事件依然有效。(click 之类的原生事件依然会被调用)
  3. 一般不会在 beforeDestroy 操作数据，因为即便操作数据，也不会再触发更新流程了。

# 十八、组件

1. ## Vue 中使用组件的三大步骤：

   1. 定义组件(创建组件)

   2. 注册组件

   3. 使用组件(写组件标签)

### （1） 如何定义一个组件？

​ 使用 Vue.extend(options)创建，其中 options 和 new Vue(options)时传入的那个 options 几乎一样，但也有点区别；

​ 区别如下：
​ 1.el 不要写，为什么？ ——— 最终所有的组件都要经过一个 vm 的管理，由 vm 中的 el 决定服务哪个容器。
​ 2.data 必须写成函数，为什么？ ———— 避免组件被复用时，数据存在引用关系。
备注：使用 template 可以配置组件结构。

### （2）如何注册组件？

​ 1.局部注册：靠 new Vue 的时候传入 components 选项

​ 2.全局注册：靠 Vue.component('组件名',组件)

### （3）编写组件标签：

​ <school></school>

## 2.几个注意点：

### 1.关于组件名:

#### 一个单词组成：

​ 第一种写法(首字母小写)：school

​ 第二种写法(首字母大写)：School

#### 多个单词组成：

​ 第一种写法(kebab-case 命名)：my-school

​ 第二种写法(CamelCase 命名)：MySchool (需要 Vue 脚手架支持)

#### 备注：

​ (1).组件名尽可能回避 HTML 中已有的元素名称，例如：h2、H2 都不行。

​ (2).可以使用 name 配置项指定组件在开发者工具中呈现的名字。

### 2.关于组件标签:

​ 第一种写法：<school></school>

​ 第二种写法：<school/>

​ 备注：不用使用脚手架时，<school/>会导致后续组件不能渲染。

### 3.一个简写方式：

​ const school = Vue.extend(options) 可简写为：const school = options

### 4. 关于 VueComponent：

1. school 组件本质是一个名为 VueComponent 的构造函数，且不是程序员定义的，是 Vue.extend 生成的。

2. 我们只需要写<school/>或<school></school>，Vue 解析时会帮我们创建 school 组件的实例对象，

   即 Vue 帮我们执行的：new VueComponent(options)。

3. 特别注意：每次调用 Vue.extend，返回的都是一个全新的 VueComponent！！！！注意这一点很重要

4. 关于 this 指向：

   (1).组件配置中：

   data 函数、methods 中的函数、watch 中的函数、computed 中的函数 它们的 this 均为 【VueComponent 实例对象】。

   (2).new Vue(options)配置中：

   data 函数、methods 中的函数、watch 中的函数、computed 中的函数 它们的 this 均是【Vue 实例对 象】。

5. VueComponent 的实例对象，以后简称 vc（也可称之为：组件实例对象）。

   Vue 的实例对象，以后简称 vm。 vm 管理着一个又一个 vc，vc 可以再管理 vc

6. 因为组件是可复用的 Vue 实例，所以它们与 new Vue 接收相同的选项，例如 data、computed、watch、methods 以及生命周期钩子等。仅有的例外是像 el 这样根实例特有的选项。
   所以，vm 与 vc 属性配置并不是一模一样，尽管 vc 底层复用了很多 vm 的逻辑

### 5.一个重要的内置关系

> 1.一个重要的内置关系：VueComponent.prototype.**proto** === Vue.prototype
>
> 2.为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue 原型上的属性、方法。

​

# 十九、脚手架

## 1.关于不同版本的 Vue：

> 1.vue.js 与 vue.runtime.xxx.js 的区别：
>
> ​ （1）.vue.js 是完整版的 Vue，包含：核心功能+模板解析器。
>
> ​ （2）.vue.runtime.xxx.js 是运行版的 Vue，只包含：核心功能；没有模板解析器。
>
> 2.因为 vue.runtime.xxx.js 没有模板解析器，所以不能使用 template 配置项，
>
> ​ 需要使用**render 函数**接收到的 createElement 函数去指定具体内容。

## 2.脚手架文件结构：

> ├── node_modules
> ├── public
> │ ├── favicon.ico: 页签图标
> │ └── index.html: 主页面
> ├── src
> │ ├── assets: 存放静态资源
> │ │ └── logo.png
> │ │── component: 存放组件
> │ │ └── HelloWorld.vue
> │ │── App.vue: 汇总所有组件
> │ │── main.js: 入口文件
> ├── .gitignore: git 版本管制忽略的配置
> ├── babel.config.js: babel 的配置文件
> ├── package.json: 应用包配置文件
> ├── README.md: 应用描述文件
> ├── package-lock.json：包版本控制文件

## 3.vue.config·js 配置文件

> 使用 vueinspect>output.js 可以查看到 vue 脚手架的默认配置。
>
> 使用 vue.config.js 可以对脚手架进行个性化定制，详情见：https：//cli.vuejs.org/zh

## 4.ref 属性

> 1.被用来给元素或子组件注册引用信息（id 的替代者）
>
> 2.应用在 html 标签上获取的是真实 DOM 元素，应用在组件标签上是组件实例对象（vc）
>
> 3.使用方式：打标识：<h1 ref="xxx">.....</h1>或<School ref="xxx"></School>
>
> 获取：this.$refs.xxx

## 5.props 配置项

1. 功能：让组件接收外部传过来的数据

2. 传递数据：`<Demo name="xxx"/>`

3. 接收数据：

   1. 第一种方式（只接收）：`props:['name'] `

   2. 第二种方式（限制类型）：`props:{name:String}`

   3. 第三种方式（限制类型、限制必要性、指定默认值）：

      ```vue
      props:{ name:{ type:String, //类型 required:true, //必要性 default:'老王'
      //默认值 } }
      ```

   > 备注：props 是只读的，Vue 底层会监测你对 props 的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制 props 的内容到 data 中一份，然后去修改 data 中的数据。

## 6.mixin(混入)

> 1.功能：可以把多个组件共用的配置提取成一个混入对象
>
> (1)使用方式：
>
> 第一步定义混合：
>
> ```
> {
>  data(){....},
>  methods:{....}
>  ....
> }
> ```
>
> 第二步使用混入：
>
> 全局混入：`Vue.mixin(xxx)` 局部混入：`mixins:['xxx']	`

## 7.插件

> 1.  功能：用于增强 Vue
>
> 2.  本质：包含 install 方法的一个对象，install 的第一个参数是 Vue，第二个以后的参数是插件使用者传递的数据。
>
> 3.  定义插件：
>
> ```
> 对象.install = function (Vue, options) {
>     // 1. 添加全局过滤器
>     Vue.filter(....)
>
>     // 2. 添加全局指令
>     Vue.directive(....)
>
>     // 3. 配置全局混入(合)
>     Vue.mixin(....)
>
>     // 4. 添加实例方法
>     Vue.prototype.$myMethod = function () {...}
>     Vue.prototype.$myProperty = xxxx
> }
> ```
>
> 4.  使用插件：`Vue.use()`

## 8.scoped 样式

1. 作用：让样式在局部生效，防止冲突。
2. 写法：`<style scoped>`

## 9.总结 TodoList 案例

1. 组件化编码流程：

   (1).拆分静态组件：组件要按照功能点拆分，命名不要与 html 元素冲突。

   (2).实现动态组件：考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用：

   1).一个组件在用：放在组件自身即可。

   2). 一些组件在用：放在他们共同的父组件上（状态提升）。

   (3).实现交互：从绑定事件开始。

2. props 适用于：

   (1).父组件 ==> 子组件 通信

   (2).子组件 ==> 父组件 通信（要求父先给子一个函数）

3. 使用 v-model 时要切记：v-model 绑定的值不能是 props 传过来的值，因为 props 是不可以修改的！

4. props 传过来的若是对象类型的值，修改对象中的属性时 Vue 不会报错，但不推荐这样做。

## 10.webStorage

1. 存储内容大小一般支持 5MB 左右（不同浏览器可能还不一样）

2. 浏览器端通过 Window.sessionStorage 和 Window.localStorage 属性来实现本地存储机制。

3. 相关 API：

   1. `xxxxxStorage.setItem('key', 'value');` 该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值。

   2. `xxxxxStorage.getItem('person');`

      该方法接受一个键名作为参数，返回键名对应的值。

   3. `xxxxxStorage.removeItem('key');`

      该方法接受一个键名作为参数，并把该键名从存储中删除。

   4. ` xxxxxStorage.clear()`

      该方法会清空存储中的所有数据。

4. 备注：

   1. SessionStorage 存储的内容会随着浏览器窗口关闭而消失。
   2. LocalStorage 存储的内容，需要手动清除才会消失。
   3. `xxxxxStorage.getItem(xxx)`如果 xxx 对应的 value 获取不到，那么 getItem 的返回值是 null。
   4. `JSON.parse(null)`的结果依然是 null。

## 11.组件的自定义事件

1. 一种组件间通信的方式，适用于：**子组件 ===> 父组件**

2. 使用场景：A 是父组件，B 是子组件，B 想给 A 传数据，那么就要在 A 中给 B 绑定自定义事件（事件的回调在 A 中）。

3. 绑定自定义事件：

   1. 第一种方式，在父组件中：`<Demo @atguigu="test"/>` 或 `<Demo v-on:atguigu="test"/>`

   2. 第二种方式，在父组件中：

      ```
      <Demo ref="demo"/>
      ......
      mounted(){
         this.$refs.xxx.$on('atguigu',this.test)
      }
      ```

   3. 若想让自定义事件只能触发一次，可以使用`once`修饰符，或`$once`方法。

4. 触发自定义事件：`this.$emit('atguigu',数据)`

5. 解绑自定义事件`this.$off('atguigu')`

6. 组件上也可以绑定原生 DOM 事件，需要使用`native`修饰符。

7. 注意：通过`this.$refs.xxx.$on('atguigu',回调)`绑定自定义事件时，回调要么配置在 methods 中，要么用箭头函数，否则 this 指向会出问题！

## 12.全局事件总线（GlobalEventBus）

1. 一种组件间通信的方式，适用于任意组件间通信。

2. 安装全局事件总线：

   ```
   new Vue({
   	......
   	beforeCreate() {
   		Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm
   	},
       ......
   })
   ```

3. 使用事件总线：

   1. 接收数据：A 组件想接收数据，则在 A 组件中给$bus 绑定自定义事件，事件的回调留在 A 组件自身。

      ```
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.$bus.$on('xxxx',this.demo)
      }
      ```

   2. 提供数据：`this.$bus.$emit('xxxx',数据)`

4. 最好在 beforeDestroy 钩子中，用$off 去解绑当前组件所用到的事件。

## 13.消息订阅与发布（pubsub）

1. 一种组件间通信的方式，适用于任意组件间通信。

2. 使用步骤：

   1. 安装 pubsub：`npm i pubsub-js`

   2. 引入: `import pubsub from 'pubsub-js'`

   3. 接收数据：A 组件想接收数据，则在 A 组件中订阅消息，订阅的回调留在 A 组件自身。

      ```
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息
      }
      ```

   4. 提供数据：`pubsub.publish('xxx',数据)`

   5. 最好在 beforeDestroy 钩子中，用`PubSub.unsubscribe(pid)`去取消订阅。

## 14.nextTick

1. 语法：`this.$nextTick(回调函数)`
2. 作用：在下一次 DOM 更新结束后执行其指定的回调。
3. 什么时候用：当改变数据后，要基于更新后的新 DOM 进行某些操作时，要在 nextTick 所指定的回调函数中执行。

## 15.Vue 封装的过度与动画

1. 作用：在插入、更新或移除 DOM 元素时，在合适的时候给元素添加样式类名。

2. 写法：

   1. 准备好样式：

      - 元素进入的样式：
        1. v-enter：进入的起点
        2. v-enter-active：进入过程中
        3. v-enter-to：进入的终点
      - 元素离开的样式：
        1. v-leave：离开的起点
        2. v-leave-active：离开过程中
        3. v-leave-to：离开的终点

   2. 使用`<transition>`包裹要过度的元素，并配置 name 属性,注意如果配置了 appear 属性的话就代表一开始挂载真实 dom 的时候就开启动画的效果：

      ```
      <transition name="hello" appear>
      	<h1 v-show="isShow">你好啊！</h1>
      </transition>
      ```

   3. 备注：若有多个元素需要过度，则需要使用：`<transition-group>`，且每个元素都要指定`key`值。

## 16.vue 脚手架配置代理

#### 方法一

在 vue.config.js 中添加如下配置：

```
devServer:{
  proxy:"http://localhost:5000"
}
```

说明：

1. 优点：配置简单，请求资源时直接发给前端（8080）即可。
2. 缺点：不能配置多个代理，不能灵活的控制请求是否走代理。
3. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器 （优先匹配前端资源）

#### 方法二

编写 vue.config.js 配置具体代理规则：

```
module.exports = {
	devServer: {
      proxy: {
      '/api1': {// 匹配所有以 '/api1'开头的请求路径
        target: 'http://localhost:5000',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api1': ''}
      },
      '/api2': {// 匹配所有以 '/api2'开头的请求路径
        target: 'http://localhost:5001',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api2': ''}
      }
    }
  }
}
/*
   changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
   changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:8080
   changeOrigin默认值为true
*/
```

说明：

1. 优点：可以配置多个代理，且可以灵活的控制请求是否走代理。
2. 缺点：配置略微繁琐，请求资源时必须加前缀。

##

## 17.插槽

1. 作用：让父组件可以向子组件指定位置插入 html 结构，也是一种组件间通信的方式，适用于 **父组件 ===> 子组件** 。

2. 分类：默认插槽、具名插槽、作用域插槽

3. 使用方式：

   1. 默认插槽：

      ```
      父组件中：
              <Category>
                 <div>html结构1</div>
              </Category>
      子组件中：
              <template>
                  <div>
                     <!-- 定义插槽 -->
                     <slot>插槽默认内容...</slot>
                  </div>
              </template>
      ```

   2. 具名插槽：

      ```
      父组件中：
              <Category>
                  <template slot="center">
                    <div>html结构1</div>
                  </template>

                  <template v-slot:footer>
                     <div>html结构2</div>
                  </template>
              </Category>
      子组件中：
              <template>
                  <div>
                     <!-- 定义插槽 -->
                     <slot name="center">插槽默认内容...</slot>
                     <slot name="footer">插槽默认内容...</slot>
                  </div>
              </template>
      ```

   3. 作用域插槽：

      1. 理解：数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。（games 数据在 Category 组件中，但使用数据所遍历出来的结构由 App 组件决定）

      2. 具体编码：

         ```
         父组件中：
         		<Category>
         			<template scope="scopeData">
         				<!-- 生成的是ul列表 -->
         				<ul>
         					<li v-for="g in scopeData.games" :key="g">{{g}}</li>
         				</ul>
         			</template>
         		</Category>

         		<Category>
         			<template slot-scope="scopeData">
         				<!-- 生成的是h4标题 -->
         				<h4 v-for="g in scopeData.games" :key="g">{{g}}</h4>
         			</template>
         		</Category>
         子组件中：
                 <template>
                     <div>
                         <slot :games="games"></slot>
                     </div>
                 </template>

                 <script>
                     export default {
                         name:'Category',
                         props:['title'],
                         //数据在子组件自身
                         data() {
                             return {
                                 games:['红色警戒','穿越火线','劲舞团','超级玛丽']
                             }
                         },
                     }
                 </script>
         ```

## 18.Vuex

### 1.概念

在 Vue 中实现集中式状态（数据）管理的一个 Vue 插件，对 vue 应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。

### 2.何时使用？

多个组件需要共享数据时

### 3.搭建 vuex 环境

1. 创建文件：`src/store/index.js`

   ```
   //引入Vue核心库
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //应用Vuex插件
   Vue.use(Vuex)

   //准备actions对象——响应组件中用户的动作
   const actions = {}
   //准备mutations对象——修改state中的数据
   const mutations = {}
   //准备state对象——保存具体的数据
   const state = {}

   //创建并暴露store
   export default new Vuex.Store({
   	actions,
   	mutations,
   	state
   })
   ```

2. 在`main.js`中创建 vm 时传入`store`配置项

   ```
   ......
   //引入store
   import store from './store'
   ......

   //创建vm
   new Vue({
   	el:'#app',
   	render: h => h(App),
   	store
   })
   ```

### 4.基本使用

1. 初始化数据、配置`actions`、配置`mutations`，操作文件`store.js`

   ```
   //引入Vue核心库
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //引用Vuex
   Vue.use(Vuex)

   const actions = {
       //响应组件中加的动作
   	jia(context,value){
   		// console.log('actions中的jia被调用了',miniStore,value)
   		context.commit('JIA',value)
   	},
   }

   const mutations = {
       //执行加
   	JIA(state,value){
   		// console.log('mutations中的JIA被调用了',state,value)
   		state.sum += value
   	}
   }

   //初始化数据
   const state = {
      sum:0
   }

   //创建并暴露store
   export default new Vuex.Store({
   	actions,
   	mutations,
   	state,
   })
   ```

2. 组件中读取 vuex 中的数据：`$store.state.sum`

3. 组件中修改 vuex 中的数据：`$store.dispatch('action中的方法名',数据)` 或 `$store.commit('mutations中的方法名',数据)`

   > 备注：若没有网络请求或其他业务逻辑，组件中也可以越过 actions，即不写`dispatch`，直接编写`commit`

### 5.getters 的使用

1. 概念：当 state 中的数据需要经过加工后再使用时，可以使用 getters 加工。

2. 在`store.js`中追加`getters`配置

   ```
   ......

   const getters = {
       bigSum(state){
           return state.sum * 10
       }
   }

   //创建并暴露store
   export default new Vuex.Store({
       ......
       getters
   })
   ```

3. 组件中读取数据：`$store.getters.bigSum`

### 6.四个 map 方法的使用

1. **mapState 方法：**用于帮助我们映射`state`中的数据为计算属性

   ```
   computed: {
       //借助mapState生成计算属性：sum、school、subject（对象写法）
        ...mapState({sum:'sum',school:'school',subject:'subject'}),

       //借助mapState生成计算属性：sum、school、subject（数组写法）
       ...mapState(['sum','school','subject']),
   },
   ```

2. **mapGetters 方法：**用于帮助我们映射`getters`中的数据为计算属性

   ```
   computed: {
       //借助mapGetters生成计算属性：bigSum（对象写法）
       ...mapGetters({bigSum:'bigSum'}),

       //借助mapGetters生成计算属性：bigSum（数组写法）
       ...mapGetters(['bigSum'])
   },
   ```

3. **mapMutations 方法：**用于帮助我们生成与`mutations`对话的方法，即：包含`$store.commit(xxx)`的函数

   ```
   methods:{
       //靠mapActions生成：increment、decrement（对象形式）
       ...mapMutations({increment:'JIA',decrement:'JIAN'}),

       //靠mapMutations生成：JIA、JIAN（对象形式）
       ...mapMutations(['JIA','JIAN']),
   }
   ```

> 备注：mapActions 与 mapMutations 使用时，若需要传递参数需要：在模板中绑定事件时传递好参数，否则参数是事件对象。

### 7.模块化+命名空间

1. 目的：让代码更好维护，让多种数据分类更加明确。

2. 修改`store.js`

   ```
   const countAbout = {
     namespaced:true,//开启命名空间
     state:{x:1},
     mutations: { ... },
     actions: { ... },
     getters: {
       bigSum(state){
          return state.sum * 10
       }
     }
   }

   const personAbout = {
     namespaced:true,//开启命名空间
     state:{ ... },
     mutations: { ... },
     actions: { ... }
   }

   const store = new Vuex.Store({
     modules: {
       countAbout,
       personAbout
     }
   })
   ```

3. 开启命名空间后，组件中读取 state 数据：

   ```
   //方式一：自己直接读取
   this.$store.state.personAbout.list
   //方式二：借助mapState读取：
   ...mapState('countAbout',['sum','school','subject']),
   ```

4. 开启命名空间后，组件中读取 getters 数据：

   ```
   //方式一：自己直接读取
   this.$store.getters['personAbout/firstPersonName']
   //方式二：借助mapGetters读取：
   ...mapGetters('countAbout',['bigSum'])
   ```

5. 开启命名空间后，组件中调用 dispatch

   ```
   //方式一：自己直接dispatch
   this.$store.dispatch('personAbout/addPersonWang',person)
   //方式二：借助mapActions：
   ...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   ```

6. 开启命名空间后，组件中调用 commit

   ```
   //方式一：自己直接commit
   this.$store.commit('personAbout/ADD_PERSON',person)
   //方式二：借助mapMutations：
   ...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
   ```

## 19.路由

1. 理解： 一个路由（route）就是一组映射关系（key - value），多个路由需要路由器（router）进行管理。
2. 前端路由：key 是路径，value 是组件。

### 1.基本使用

1. 安装 vue-router，命令：`npm i vue-router`

2. 应用插件：`Vue.use(VueRouter)`

3. 编写 router 配置项:

   ```
   //引入VueRouter
   import VueRouter from 'vue-router'
   //引入Luyou 组件
   import About from '../components/About'
   import Home from '../components/Home'

   //创建router实例对象，去管理一组一组的路由规则
   const router = new VueRouter({
   	routes:[
   		{
   			path:'/about',
   			component:About
   		},
   		{
   			path:'/home',
   			component:Home
   		}
   	]
   })

   //暴露router
   export default router
   ```

4. 实现切换（active-class 可配置高亮样式）

   ```
   <router-link active-class="active" to="/about">About</router-link>
   ```

5. 指定展示位置

   ```
   <router-view></router-view>
   ```

### 2.几个注意点

1. 路由组件通常存放在`pages`文件夹，一般组件通常存放在`components`文件夹。
2. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载。
3. 每个组件都有自己的`$route`属性，里面存储着自己的路由信息。
4. 整个应用只有一个 router，可以通过组件的`$router`属性获取到。

### 3.多级路由（多级路由）

1. 配置路由规则，使用 children 配置项：

   ```
   routes:[
   	{
   		path:'/about',
   		component:About,
   	},
   	{
   		path:'/home',
   		component:Home,
   		children:[ //通过children配置子级路由
   			{
   				path:'news', //此处一定不要写：/news
   				component:News
   			},
   			{
   				path:'message',//此处一定不要写：/message
   				component:Message
   			}
   		]
   	}
   ]
   ```

2. 跳转（要写完整路径）：

   ```
   <router-link to="/home/news">News</router-link>
   ```

### 4.路由的 query 参数

1. 传递参数

   ```
   <!-- 跳转并携带query参数，to的字符串写法 -->
   <router-link :to="/home/message/detail?id=666&title=你好">跳转</router-link>

   <!-- 跳转并携带query参数，to的对象写法 -->
   <router-link
   	:to="{
   		path:'/home/message/detail',
   		query:{
   		   id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

2. 接收参数：

   ```
   $route.query.id
   $route.query.title
   ```

### 5.命名路由

1. 作用：可以简化路由的跳转。

2. 如何使用

   1. 给路由命名：

      ```
      {
      	path:'/demo',
      	component:Demo,
      	children:[
      		{
      			path:'test',
      			component:Test,
      			children:[
      				{
                            name:'hello' //给路由命名
      					path:'welcome',
      					component:Hello,
      				}
      			]
      		}
      	]
      }
      ```

   2. 简化跳转：

      ```
      <!--简化前，需要写完整的路径 -->
      <router-link to="/demo/test/welcome">跳转</router-link>

      <!--简化后，直接通过名字跳转 -->
      <router-link :to="{name:'hello'}">跳转</router-link>

      <!--简化写法配合传递参数 -->
      <router-link
      	:to="{
      		name:'hello',
      		query:{
      		   id:666,
                  title:'你好'
      		}
      	}"
      >跳转</router-link>
      ```

### 6.路由的 params 参数

1. 配置路由，声明接收 params 参数

   ```
   {
   	path:'/home',
   	component:Home,
   	children:[
   		{
   			path:'news',
   			component:News
   		},
   		{
   			component:Message,
   			children:[
   				{
   					name:'xiangqing',
   					path:'detail/:id/:title', //使用占位符声明接收params参数
   					component:Detail
   				}
   			]
   		}
   	]
   }
   ```

2. 传递参数

   ```
   <!-- 跳转并携带params参数，to的字符串写法 -->
   <router-link :to="/home/message/detail/666/你好">跳转</router-link>

   <!-- 跳转并携带params参数，to的对象写法 -->
   <router-link
   	:to="{
   		name:'xiangqing',
   		params:{
   		   id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

   > 特别注意：路由携带 params 参数时，若使用 to 的对象写法，则不能使用 path 配置项，必须使用 name 配置！

3. 接收参数：

   ```
   $route.params.id
   $route.params.title
   ```

### 7.路由的 props 配置

作用：让路由组件更方便的收到参数

```
{
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,

	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
	// props:{a:900}

	//第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数通过props传给Detail组件
	// props:true

	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
	props(route){
		return {
			id:route.query.id,
			title:route.query.title
		}
	}
}
```

### 8.`<router-link>`的 replace 属性

1. 作用：控制路由跳转时操作浏览器历史记录的模式
2. 浏览器的历史记录有两种写入方式：分别为`push`和`replace`，`push`是追加历史记录，`replace`是替换当前记录。路由跳转时候默认为`push`
3. 如何开启`replace`模式：`<router-link replace .......>News</router-link>`

### 9.编程式路由导航

1. 作用：不借助`<router-link> `实现路由跳转，让路由跳转更加灵活

2. 具体编码：

   ```
   //$router的两个API
   this.$router.push({
   	name:'xiangqing',
   		params:{
   			id:xxx,
   			title:xxx
   		}
   })

   this.$router.replace({
   	name:'xiangqing',
   		params:{
   			id:xxx,
   			title:xxx
   		}
   })
   this.$router.forward() //前进
   this.$router.back() //后退
   this.$router.go() //可前进也可后退 参数是number类型(正数为前进的步数,负数为后退的部署)
   ```

### 10.缓存路由组件

1. 作用：让不展示的路由组件保持挂载，不被销毁。

2. 具体编码：

   ```
   <keep-alive include="News">
       <router-view></router-view>
   </keep-alive>
   ```

### 11.两个新的生命周期钩子

1. 作用：路由组件所独有的两个钩子，用于捕获路由组件的激活状态。
2. 具体名字：
   1. `activated`路由组件被激活时触发。
   2. `deactivated`路由组件失活时触发。

### 12.路由守卫

1. 作用：对路由进行权限控制

2. 分类：全局守卫、独享守卫、组件内守卫

3. 全局守卫:

   ```
   //全局前置守卫：初始化时执行、每次路由切换前执行
   router.beforeEach((to,from,next)=>{
   	console.log('beforeEach',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
   		if(localStorage.getItem('school') === 'atguigu'){ //权限控制的具体规则
   			next() //放行
   		}else{
   			alert('暂无权限查看')
   			// next({name:'guanyu'})
   		}
   	}else{
   		next() //放行
   	}
   })

   //全局后置守卫：初始化时执行、每次路由切换后执行
   router.afterEach((to,from)=>{
   	console.log('afterEach',to,from)
   	if(to.meta.title){
   		document.title = to.meta.title //修改网页的title
   	}else{
   		document.title = 'vue_test'
   	}
   })
   ```

4. 独享守卫:

   ```
   beforeEnter(to,from,next){
   	console.log('beforeEnter',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
   		if(localStorage.getItem('school') === 'atguigu'){
   			next()
   		}else{
   			alert('暂无权限查看')
   			// next({name:'guanyu'})
   		}
   	}else{
   		next()
   	}
   }
   ```

5. 组件内守卫：

   ```
   //进入守卫：通过路由规则，进入该组件时被调用
   beforeRouteEnter (to, from, next) {
   },
   //离开守卫：通过路由规则，离开该组件时被调用
   beforeRouteLeave (to, from, next) {
   }
   ```

### 13.路由器的两种工作模式

1. 对于一个 url 来说，什么是 hash 值？—— #及其后面的内容就是 hash 值。
2. hash 值不会包含在 HTTP 请求中，即：hash 值不会带给服务器。
3. hash 模式：
   1. 地址中永远带着#号，不美观 。
   2. 若以后将地址通过第三方手机 app 分享，若 app 校验严格，则地址会被标记为不合法。
   3. 兼容性较好。
4. history 模式：
   1. 地址干净，美观 。
   2. 兼容性和 hash 模式相比略差。
   3.
