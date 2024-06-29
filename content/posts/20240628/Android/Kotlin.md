---
title: "Kotlin"
date: 2024-04-16T16:00:01+08:00
draft: false
tags:
  - Kotlin
  - FE
categories:
  - FE
---

## 一、基础语法

### 1.变量和函数

（1）变量

1. 定义变量的方式

- val：声明一个不可变的变量，对应 Java 中的 final 变量

- var：声明一个可变的变量，对应 Java 中的非 final 变量

2. 显式地声明变量类型

```kotlin
val a: Int = 10
```

| Java 基本数据类型 | Kotlin 对象数据类型 | 数据类型说明 |
| ----------------- | ------------------- | ------------ |
| int               | Int                 | 整型         |
| long              | Long                | 长整型       |
| short             | Short               | 短整型       |
| float             | Float               | 单精度浮点型 |
| double            | Double              | 双精度浮点型 |
| boolean           | Boolean             | 布尔型       |
| char              | Char                | 字符型       |
| byte              | Byte                | 字节型       |
|                   |                     |              |

（2）函数

```kotlin
fun methodName(param1: Int, param2: Int): Int {
	return 0
}
```

- 定义关键字+函数名+参数+{返回类型}
  - fun（function 的简写）是定义函数的关键字，定义函数一定要使用 fun 来声明
  - 函数名，根据喜好，但最好语义化命名
  - 括号，声明该函数接收什么参数，格式“参数名: 参数类型”，可不写
  - 返回类型，声明该函数会返回什么类型的数据，可选
  - 函数体，两个大括号内容，编写一个函数的具体逻辑

### 2.程序的逻辑控制

#### （1）条件语句

##### i）if 语句

```kotlin
fun largerNumber(num1: Int, num2: Int): Int {
	var value = 0
	if (num1 > num2) {
		value = num1
	} else {
		value = num2
	}
	return value
}
```

由于特性：Kotlin 中的 if 语句相比于 Java 有一个额外的功能，它是可以有返回值的，返回值就是 if 语句每一个条件中最后一行代码的返回值。
简化为如下：

```kotlin
fun largerNumber(num1: Int, num2: Int): Int {
	val value = if (num1 > num2) {
		num1
	} else {
		num2
	}
	return value
}
```

你会发现 value 其实也是一个多余的变量，我们可以直接将 if 语句返回，这样代码将会变得更加精简

​ 更简化的：

```kotlin
fun largerNumber(num1: Int, num2: Int): Int {
	return if (num1 > num2) {
		num1
	} else {
		num2
    }
}
```

当一个函数只有一行代码时，可以省略函数体部分，直接将这一行代码使用等号串连在函数定义的尾部。

```kotlin
fun largerNumber(num1: Int, num2: Int) = if (num1 > num2) {
	num1
} else {
	num2
}
```

最简：

```kotlin
fun largerNumber(num1: Int, num2: Int) = if (num1 > num2) num1 else num2
```

##### ii）when 语句

```kotlin
fun getScore(name: String) = when (name) {
    "Tom" -> 86
    "Jim" -> 77
    "Jack" -> 95
    "Lily" -> 100
    else -> 0
}
```

注：is 关键字就是类型匹配的核心，它相当于 Java 中的 instanceof 关键字

​ 一种不带参数的用法：

```kotlin
fun getScore(name: String) = when {
    name == "Tom" -> 86
    name == "Jim" -> 77
    name == "Jack" -> 95
    name == "Lily" -> 100
    else -> 0
}
```

#### （2）循环语句

for 循环

```kotlin
//区间：
// ①0..10 = [0, 10]，两端都是闭区间
val range = 0..10
// ②用until关键字，左闭右开
val range = 0 until 10
```

```kotlin
// ..区间
fun main() {
	for (i in 0..10) {
		println(i)
	}
}

//until区间，step关键字，步长为2
fun main() {
	for (i in 0 until 10 step 2) {
		println(i)
	}
}

//downTo关键字，降序区间
fun main() {
	for (i in 10 downTo 1) {
		println(i)
	}
}
```

3.面向对象编程

（1）类与对象

​ 类的创建

```kotlin
class Person {
	var name = ""
	var age = 0

    fun eat() {
		println(name + " is eating. He is " + age + " years old.")
	}
}
```
