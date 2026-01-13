# Expressions and operators

This chapter documents all the JavaScript language **operators**, **expressions** and **keywords**

> 该章节说明了 JavaScript 语言所有的运算符、表达式和关键字

## Primary Expressions | 主要表达式

**Basic keywords** and **general expressions** in JavaScript. These expressions have **the highest precedence** (higher than [operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence)).

> * 最高优先级

* **`this`**

  The `this` keyword refers to a special property of an **execution context/执行上下文**.

* **Literals**

  Basic `null`, boolean, number, and string literals.

* **`[]`**

  **Array** initializer/literal syntax.

* **`{}`**

  **Object** initializer/literal syntax.

* **`function`**

  The `function` keyword defines a function expression.

* **`class`**

  The `class` keyword defines a class expression.

* **`function*`**

  The `function*` keyword defines a **generator function expression/生成器函数表达式**.

* **`async function`**

  The `async function` defines an **async function expression/异步函数表达式**.

* **`async function`***

  The `async function*` keywords define an **async generator function expression/异步生成器函数表达式**.

* **`/ab+c/i`**

  **Regular/正则** expression literal syntax.

* **\`string\`**

  **Template/模版** literal syntax.

* **`(_)`**

  **Grouping/分组** operator.

## Left-hand-side expressions

Left values are the destination of an assignment.

> 左边的值是赋值的目标。

* **Property accessors | 属性访问符**

  Member operators provide access to a property or method of an object (`object.property` and `object["property"]`).

* **`?.` | 可选链运算符**

  The **optional chaining operator** returns `undefined` instead of causing an error if a reference is [nullish/空值](https://developer.mozilla.org/en-US/docs/Glossary/Nullish) ([`null`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/null) or [`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)).

* **`new`**

  The `new` operator creates an **instance/实例** of a constructor.

* **`new.target`**

  In constructors, `new.target` refers to the constructor that was **invoked/调用** by [`new`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new).

* **`import.meta`**

  An object exposing **context-specific/特定上下文** **metadata/元数据** to a JavaScript module.

* **`super`**

  The `super` keyword **calls/调用** the <u>parent constructor</u> or allows accessing properties of the <u>parent object</u>.

* **`import()`**

  The `import()` syntax allows loading a module **asynchronously/异步** and **dynamically/动态** into a potentially **non-module** environment.

## Increment and decrement | 自增和自减

Postfix/prefix **increment** and postfix/prefix **decrement** operators

> 前置或后置自增运算符和前置或后置自减运算符。

* A++

  Postfix increment operator.

* A--

  Postfix decrement operator.

* ++A

  Prefix increment operator.

* --A

  Prefix decrement operator.

## Unary operators | 一元运算符

A unary operation is an operation with **only one operand.**

> 一元运算符只有一个操作数。

* **`delete`**

  The `delete` operator deletes a property from an object.

* **`void`**
  The `void` operator **evaluates** an expression and <u>**discards** its return value/丢弃返回值</u>.

* **`typeof`**

  The `typeof` operator **determines/判断** the type of a given object.

* **`+`**

  The unary **plus** operator **converts** its operand to Number type.

* **`-`**

  The unary **negation** operator converts its operand to Number type and then **negates/取反** it.

* **`~`**

  **Bitwise/位** NOT operator.

* **`!`**

  **Logical/逻辑** NOT operator.

* **`await`**

  Pause and resume an async function and wait for the promise's fulfillment/rejection.

  > 暂停或恢复执行异步函数，并等待 promise 的兑现或拒绝

## Arithmetic operators | 算术运算符

Arithmetic operators take **numerical** values (either **literals** or **variables**) as their operands and return a single numerical value.

> 算术运算符以二个数值（字面量或变量）作为操作数，并返回单个数值。

* **
* **`**`**

  **Exponentiation/求幂** operator.

* **`*`**

  **Multiplication/乘法** operator.

* **`/`**

  **Division/除法** operator.

* **`%`**

  **Remainder/取模** operator.

* **`+`**

  **Addition/加法** operator.

* **`-`**

  **Subtraction/减法** operator.

## Relational operators | 关系远算符

A comparison operator <u>compares its **operands**</u> and <u>returns a **boolean** value</u> based on whether the comparison is true.

> 比较运算符比较两个操作数并返回基于比较结果的布尔值

* **`<`**

  **Less/小于** than operator.

* **`>`**

  **Greater/大于** than operator.

* **`<=`**

  **Less** than or **equal** operator.

* **`>=`**

  **Greater** than or **equal** operator.

* **`instanceof`**

  The `instanceof` operator **determines** whether an object is an **instance** of another object.

* **`in`**

  The `in` operator **determines** whether an object has a **given property**.

## Equality operators | 相等运算符

The result of **evaluating** an equality operator is always of **type boolean** based on whether the comparison is true.

> 相等运算符的求值结果始终是布尔类型（基于比较是否为 true）。

* **`==`**

  **Equality/相等** operator.

* **`!=`**

  **Inequality/不相等** operator.

* **`===`**

  **Strict equality/严格相等** operator.

* **`!==`**

  **Strict inequality/严格不相等** operator.

## Bitwise ship operators | 位移运算符

Operations to **shift** all bits of the operand.

> 对操作数的所有二进制位进行移动操作。

* **`<<`**

  Bitwise **left shift** operator.

* **`>>`**

  Bitwise **right shift** operator.

* **`>>>`**

  Bitwise **unsigned right shift** operator.

## Binary bitwise operators | 二进制运算符

Bitwise operators treat their operands as <u>**a set of 32 bits (zeros and ones)**</u> and return standard JavaScript numerical values.

> 二进制运算符将它们的操作数作为 **32 个二进制位（0 或 1）的集合**，并返回标准的 JavaScript 数值。

* **`&`**

  Bitwise **AND/与**.

* **`|`**

  Bitwise **OR/或**.

* `^`

  Bitwise **XOR/异或**.

## Binary logical operators | 二元逻辑远算符

Logical operators implement **boolean (logical)** values and have [short-circuiting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence#short-circuiting) behavior.

> 逻辑运算符实现布尔（逻辑）值运算，并具有[短路](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Operator_precedence#短路)行为。

* **`&&`**

  Logical **AND/与**.

* **`||`**

  Logical **OR/或**.

* **`??`**

  **Nullish Coalescing/空值合并** Operator.

## Conditional(ternary) operator | 条件（三元）运算符

The conditional operator returns one of two values based on the **logical value of the condition**.

> 条件运算符返回两个值中**符合条件逻辑值**的那个值。

* **`(Condition ? ifTrue : ifFlase)`**

## Assignment operators | 赋值运算符

An assignment operator **assigns** a value to its **left** operand based on the value of its **right** operand.

> 赋值运算符将右边的操作数的值赋给左边的操作数。

* **`=`**

  **Assignment/赋值** operator.

* **`*=`**

  **Multiplication/乘积** assignment.

* **`/=`**

  **Division/商** assignment.

* **`%=`**

  **Remainder/求余** assignment.

* **`+=`**

  **Addition/求和** assignment.

* **`-=`**

  **Subtraction/求差** assignment

* **`<<=`**

  **Left shift/左位移** assignment.

* **`>>=`**

  **Right shift/右位移** assignment.

* **`>>>=`**

  **Unsigned right shift/无符号右位移** assignment.

* **`&=`**

  **Bitwise AND/按位与** assignment.

* **`^=`**

  **Bitwise XOR/按位异或** assignment.

* **`|=`**

  **Bitwise OR/按位或** assignment.

* **`**=`**

  **Exponentiation/求幂** assignment.

* **`&&=`**

  **Logical AND/逻辑与** assignment.

* **`||=`**

  **Logical OR/逻辑或** assignment.

* **`??=`**

  **Nullish coalescing/空值合并** assignment.

* **`[a, b] = arr, {a, b} = obj`**

  **Destructuring** allows you to assign the properties of an array or object to variables using syntax that looks similar to array or object literals.

  > **解构**允许你使用类似于数组或对象字面量的语法将数组或对象的属性赋值给变量。

## Yield operators

* **`yield`**

  **Pause/暂停** and **resume/恢复** a generator function.

* **`yield*`**

  **Delegate/委派** to another generator function or **iterable object**.

## Spread syntax | 展开语法

* **`...obj`**

  Spread syntax allows an **iterable**, such as an **array** or **string**, to be **expanded** in places where zero or more arguments (for function calls) or elements (for array literals) are expected. In an object literal, the spread syntax **enumerates** the properties of an object and adds the key-value pairs to the object being created.

  > 展开语法允许在需要零个或多个参数（对于函数调用）或者元素（对于数组字面量）的地方展开可迭代对象（例如，数组或字符串）。而在对象字面量中，展开语法枚举对象的属性，并将其键值对添加到正在创建的对象中。

## Comma operator | 逗号运算符

* **`,`**

  The comma operator allows **multiple expressions** to be evaluated in a single statement and returns the result of the last expression.

  > 逗号运算符允许在单个语句中对多个表达式进行求值，并返回最后一个表达式的结果。