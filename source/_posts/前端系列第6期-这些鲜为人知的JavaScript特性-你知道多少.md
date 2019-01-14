---
title: '前端系列第6期-这些鲜为人知的JavaScript特性,你知道多少?'
date: 2018-12-25 21:56:01
tags: js
keywords: js特征
categories: "前端系列"
---
![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/1.png)
### 前言
JavaScript 通常被认为是最容易入门却最难以掌握的编程语言。这是因为 JavaScript 是一门非常古老却又非常灵活的语言。它有着各种各样神秘的语法和古老的特性。直到现在，我仍然会时不时地发现一些我从来都不知道的隐藏语法或技巧。
<!--more-->
![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/2.png)
我将在这篇文章中列出一些鲜为人知的 JavaScript 特性。虽然其中一些在 strict 模式下是无效的，但它们仍然是有效的 JavaScript 代码。但请注意，我不建议你使用所有这些特性。虽然它们看起来很酷，但如果你真的使用了这些特性，很有可能会让你的队友吐血。  

注意：我不会提及诸如 Hoisting、闭包、代理、原型继承、async/await、生成器，等等。虽然这些特性可能不太好理解，但它们其实是众所周知的。
### void运算符
JavaScript 提供了一个一元运算符 void，你可能已经看到过它的这种用法，比如 void(0) 或 void 0。它的作用只有一个——计算其右边的表达式并返回 undefined。使用“0”只是一种惯例，你不一定要使用“0”，它可以是任何有效的表达式，如 void，它仍然会返回 undefined。

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/3.png)
为什么要创建一个特殊的关键字来返回 undefined，而不是直接返回 undefined？这似乎有点多余，不是吗？

实际上，在 ES5 之前，你可以在大多数浏览器中为给 undeunfined 赋值，比如 undeunfined = “abc”。在那个时候，使用 void 是一种确保总是能够返回 undefined 的方法。
### 构造函数的括号是可选的
在调用构造函数时，类名后面的括号是可选的（前提是你不需要传递任何参数）！

下面的代码都是有效的 JS 语法，并且会给你完全相同的结果！

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/4.png)
void 运算符告诉解析器后面的代码是函数表达式。因此，我们可以跳过函数定义周围的括号。我们还可以使用任何一元运算符（void、+、!、-，等等），它们都是有效的！

你可能会想，一元运算符不会影响 IIFE 返回的结果吗？

它确实会影响返回的结果。但如果你关心结果，并希望将结果赋给在某个变量，那么首先你就不需要额外的括号。

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/5.png)
我们添加这些括号只是为了更好的可读性。
### with语句
JavaScript 也支持 with 块？with 实际上是 JS 的一个关键字。with 块的语法如下：

```js
    with (object)
        statement 
    // for multiple statements add a block
    with (object) {
        statement
        statement
        ...
    }
```

with 将“对象”的所有属性添加到用于计算语句的作用域链中。

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/6.png)
with 块看起来非常酷，它甚至比对象解构更好，但其实并不尽然。

通常不鼓励使用 with 语句，因为它已经被弃用。在 strict 模式下是被完全禁止的。事实证明，使用 with 块会带来一些性能和安全方面的问题。
### Function 构造函数
function 语句并不是定义新函数的唯一方法，你可以使用 Function() 构造函数和 new 运算符动态定义函数。

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/7.png)
最后一个参数是函数的字符串化代码，前面的其他参数是函数的参数。

Function 构造函数是 JavaScript 中所有构造函数的祖先。甚至 Object 的构造函数也是 Function。而 Function 自己的构造函数也是 Function 本身。因此，如果调用 object.constructor.constructor…足够多的次数，最后将获得 Function 构造函数。
### 函数属性
我们都知道，函数是 JavaScript 的一等对象。因此，我们当然可以向函数添加自定义属性。这样做是完全有效的。然而，它很少被这样使用。

那么，我们什么时候会这么做呢？
#### 可配置的函数
假设我们有一个叫作 greet 的函数。我们希望它能够根据不同的区域设置打印出不同的问候语。区域设置也应该是可配置的。我们可以在某处维护一个全局区域环境变量，或者我们也可以使用函数属性来实现这个函数，如下所示：

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/8.png)
#### 具有静态变量的函数
另一个类似的例子，假设你想要实现一个生成一系列有序数字的数字生成器。通常，你会使用 Class 或 IIFE，并使用一个静态计数器变量来跟踪最后一个值。这样我们就可以限制对计数器的访问，并避免使用额外的变量来污染全局命名空间。

但是，如果我们希望能够灵活地读取甚至是修改计数器，并且不污染全局命名空间呢？

我们仍然可以创建一个 Class，带有一个计数器变量和一些额外的方法来读取它，或者我们可以使用函数的属性。

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/9.png)

### 参数属性
我相信大多数人都知道函数的 arguments 对象。它是一种类似于数组的对象，所有函数都包含了它。它包含了在调用函数时传给函数的所有参数，但它也有一些其他有趣的属性：

arguments.callee：指当前调用的函数；

arguments.callee.caller：指调用当前函数的函数。

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/10.png)
注意：尽管 ES5 禁止在 strict 模式下使用 callee 和 caller，但在很多编译库中仍然很常见。
### 标记模板字面量
除非你与世隔绝，否则你一定听说过模板字面量。模板字面量是 ES6 的众多很酷的补充特性之一。但是，你知道标记模板字面量吗？

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/11.png)
在使用标记模板字面量时，你可以通过向模板字面量添加自定义标记来更好地控制如何将模板字面量解析为字符串。标记只是一个解析器函数，它获取字符串模板中所有的字符串和值。标记函数负责返回最终的字符串。

在下面的示例中，我们的自定义标记——highlight，解释模板字面量的值，并使用`元素将解释的值包装在结果字符串中，以突出显示。`

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/12.png)
### Getter 和 Setter
JavaScript 对象的大部分东西是很简单的。假设我们有一个 user 对象，并且我们使用 user.age 来访问它的 age 属性，如果定义了 age 属性，我们就会得到它的值，如果没有，我们就会得到 undefined。

但是，它也可能不会这么简单。JavaScript 对象也有 Getter 和 Setter 的概念。我们可以编写自定义的 Getter 函数来返回我们想要的任何东西，而不是直接返回对象的值。设置值也是一样的。

这样我们在获取或设置字段时就拥有了一些强大的概念，如虚拟字段、字段验证、副作用，等等。

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/13.png)
Getter 和 Setter 并不是 ES5 的新增功能，它们一直都存在。ES5 只是为它们添加了方便的语法。
### 逗号运算符
JavaScript 提供了一个逗号运算符，我们可以用它在一行中编写由逗号分隔的多个表达式，并返回最后一个表达式的结果。

```js
    let result = expression1, expression2,... expressionN
```

这里所有的表达式都会被计算，并将 expressionN 返回的值赋给 result 变量。

你可能已经在 for 循环中使用了逗号运算符：

```js
    for (var a = 0, b = 10; a <= 10; a++, b--)
```

有时候，在一行中编写多个语句会有所帮助：

```js
    function getNextValue() {
        return counter++, console.log(counter), counter
    }
```

或者用它编写很短的 lamda 表达式：

```js
    const getSquare = x => (console.log (x), x * x)
```
### 加号运算符
你是否曾经想过快速将字符串转换为数字？

只需在字符串前面加上加号即可。

加号运算符也适用于负数、八进制、十六进制、指数。它甚至可以将 Date 或 Moment.js 对象转换为时间戳！

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/14.png)
### !! 运算符
从技术上讲，它并不是一个单独的 JavaScript 运算符。它的效果与使用两次 JavaScript 否定运算符是一样的。

!! 是将任何表达式转换为布尔值的一个巧妙的技巧。

如果表达式是真值，则返回 true，否则返回 false。

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/15.png)
### ~ 运算符
没有人会关心位运算符，因为我们几乎很少会用它！但它确实有一些使用场景！

当与数字一起使用时，比如~N => -(N + 1)。这个表达式只在 N == -1 时结果为“0”。

我们可以在 indexOf(…) 函数前面加一个~ 来进行布尔检查，看看一个项是否存在于 String 或 Array 中。

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/16.png)
注意：ES6 和 ES7 分别在 String 和 Array 中添加了一个新的.includes() 方法。当然，它比使用~ 运算符检查项目是否存在于 Array 或 String 中更清晰一些。
### 标签语句
JavaScript 也有标签语句的概念。我们可以在 JavaScript 中使用标签来命名循环和代码块。然后，我们可以在 break 或 continue 时通过这些标签返回到之前的代码。

在嵌套循环中使用标签语句会非常方便，我们也可以使用它们来将代码组织成代码块或创建可 break 的代码块。

![image](https://github.com/yuhongjing/img-folder/raw/master/img/js-mimi/17.png)
注意：与其他一些语言不同，JavaScript 中没有 goto。因此，我们只能使用在 break 和 continue 中使用标签。