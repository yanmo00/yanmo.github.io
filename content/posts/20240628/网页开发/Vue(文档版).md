---
title: "Vscode（文档版）"
date: 2024-01-17T16:00:01+08:00
draft: false
tags:
  - Vue
  - FE
categories:
  - FE
---

选项式 API

```vue
<script>
export default {
  data() {
    return;
  },
  methods: {},
};
</script>
```

组合式 API（简化版如下）

```vue
<script setup>
import { ref } from "vue";
const count = ref(0);
</script>

<template>
  <button @click="count++">Count is {{ count }}</button>
</template>
```

组合式 API（非简化版）

```vue
<script>
    import { ref } from 'vue'
    export default {
         // `setup` 是一个特殊的钩子，专门用于组合式 API。
		setup(){
        	const const count = ref(0)

            function increment(){
                count.value++
            }
       // 将 ref 暴露给模板
        return{
            // 暴露的方法可以被用作事件监听器：
            count,
            increment
        }
       }
     }
```

传值的几种方法，ref，props，组件

> 1. data 数据直接插值语法导入
>
> 2. 组件方法导入，但在 script 导入时候需要 script setup
>
> 3. props
>
> 4. 通过 ref，const 一个响应式数据、字符串、对象
>
> 5. $attrs
>
>    ```js
>    <!-- MyComponent 模板使用 $attrs 时 -->
>    <p :class="$attrs.class">Hi!</p>
>    <span>This is a child component</span>
>
>    <MyComponent class="baz" />
>    ```

# ref 函数的应用

> 1.作用：ref 函数创建一个响应式变量(例如，count)，初始化为 0，会根据响应式特性，数据不断更新

```vue
import { ref } from 'vue'; const count = ref(0); //
创建一个初始值为0的响应式引用
```

> 要在组件模板中访问 ref，请从组件的 `setup()` 函数中声明并返回它们
>
> ```vue
> import { ref } from 'vue' export default { // `setup`
> 是一个特殊的钩子，专门用于组合式 API。 setup() { const count = ref(0) // 将
> ref 暴露给模板 return { count } } }
> ```

## ref 函数与 reactive 函数

> ref 将数据赋予了`.value` 的值，使访问可被追踪
>
> `reactive()` 将使对象本身具有响应性

用 ref 函数的理由

> reactive() 的局限性
>
> 1.有限的值类型:用于对象类型，基本数据类型不适用
>
> 2.不能替换整个对象
>
> ```js
> let state = reactive({ count: 0 });
>
> // 上面的 ({ count: 0 }) 引用将不再被追踪
> // (响应性连接已丢失！)
> state = reactive({ count: 1 });
> ```
>
> 3.对解构操作不友好
>
> ```js
> const state = reactive({ count: 0 });
>
> // 解构操作：响应式对象结构为本地变量，不需要读取.valuez
> // 当解构时，count 已经与 state.count 断开连接
> let { count } = state;
> // 不会影响原始的 state
> count++;
>
> // 该函数接收到的是一个普通的数字
> // 并且无法追踪 state.count 的变化
> // 我们必须传入整个对象以保持响应性
> callSomeFunction(state.count);
> ```
>
> 由于这些限制，建议使用 `ref()` 作为声明响应式状态的主要 API。

## ref 与 computed

> `ref`：`ref`用于创建一个可变的响应式数据，它可以存储和操作数据。
>
> `computed`：`computed`用于创建一个计算属性，它根据其他响应式数据的值进行计算，并返回一个新的响应式数据。计算属性的值是根据其依赖的响应式数据动态计算得到的，当依赖的数据发生变化时，计算属性会自动重新计算其值。
>
> ref 与 computed 区别是：computed 能处理需要计算逻辑的（经过计算得到的属性），例如
>
> ```js
> const seen = computed(() => {
>   return count.value > 5;
> });
> ```

# computed

> 组合式 api 写法
>
> ```js
> // 正常写法
> const fullName = computed({
>   get() {
>     return firstName.value + " " + secondName.value + " " + lastName.value;
>   },
>   set(newVal) {
>     [firstName.value, secondName.value, lastName.value] = newVal.split(" ");
>   },
> });
>
> // 简写
> const fullName = computed(
>   () => firstName.value + " " + secondName.value + " " + lastName.value
> );
> ```
>
> 注：正常写法和简写的区别：正常写法能修改值
>
> 选项式 api 写法
>
> ```js
> // 正常写法
> computed:{
>     fullName(){
>         get(){
>             return this.firstName + "-" + this.lastName
>         },
>         set(){
>             const arr = value.split("-");
>             this.firstName = arr[0];
>             this.lastName = arr[1];
>         }
>     }
> }
> ```
>
> ```
> 简写
> fullName() {
>                 console.log("get被调用了");
>                 return this.firstName + "-" + this.lastName
> ```

# 绑定样式

## 两种绑定样式的方法

> `:style` 支持绑定 JavaScript 对象值
>
> ```vue
> <template>
>   <div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
> </template>
>
> <!-- 组合式API -->
> <script setup>
> import { ref } from "vue";
>
> const activeColor = ref("red");
> const fontSize = ref(30);
> </script>
>
> <!-- 选项式API -->
> <script>
> export default {
>   data() {
>     return {
>       activeColor: "blue",
>       fontsize: 35,
>     };
>   },
> };
> </script>
> ```
>
> 绑定一个样式对象
>
> ```vue
> <template>
> <div :style="styleObject"></div>
> </template>
>
> <script setup>
> const styleObject = reactive({
>   color: 'red',
>   fontSize: '13px'
> })
> <script>
> ```

# 列表渲染

> 列表的标准格式
>
> 列表遍历
>
> ```vue
> <li v-for="({ message }, index) in items">
>   {{ message }} {{ index }}
> </li>
> ```

> 对象遍历

> ```vue
> <li v-for="(value, key, index) in myObject">
>   {{ index }}. {{ key }}: {{ value }}
> </li>
> ```

>

> ```vue
> <ul>
>   <template v-for="n in 10">
>     <li>{{ item.msg }}</li>
>     <li class="divider" role="presentation"></li>
>   </template>
> </ul>
> ```

> ```vue
> <ul>
>   <template v-for="item in items">
>     <li>{{ item.msg }}</li>
>     <li class="divider" role="presentation"></li>
>   </template>
> </ul>
> ```
