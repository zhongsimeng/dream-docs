# Lexical grammar

JavaScript **source text** is just a sequence of characters — in order for the **interpreter/解释器** to understand it, the string has to be **parsed** to a more structured representation. The initial step of parsing is called [lexical analysis](https://en.wikipedia.org/wiki/Lexical_analysis), in which **<u>the text gets scanned from left to right</u>** and is converted into a sequence of individual, **atomic input elements**. 

> * ECMAScript **源码文本**会被**从左到右扫描**，并被转换为一系列的**原子输入元素**。

* **Format-control characters | 格式控制符**

  Format-control characters have **no visual representation** but are used to control the **interpretation** of the text.

  > 格式控制符用于控制对源码文本的解释，但是并不会显示出来。
  >
  > ---
  >
  > * `U+200C` | `<ZWNJ>` | 零宽度非结合子
  > * `U+200D` | `<ZWJ>` | 零宽度结合子
  > * `U+FEFF` | ` <BOM>` | 字节流方向标识

* **White space | 空白符**

  [White space](https://developer.mozilla.org/en-US/docs/Glossary/Whitespace) characters improve the **readability** of source text and separate **tokens** from each other. These characters are usually unnecessary for the functionality of the code. [Minification tools](https://en.wikipedia.org/wiki/Minification_(programming)) are often used to remove whitespace in order to reduce the amount of data that needs to be transferred.

  > * 空白符提升了源码的**可读性**，并将**标记 (tokens)** 区分开。
  >
  > * 通常不影响源码的功能。
  >
  > * 通常可以用[压缩器](http://en.wikipedia.org/wiki/Minification_(programming))来移除源码中的空白，减少数据传输量。
  >
  > ---
  >
  > * `U+009` | `<HT>` | 制表符 |` \t`
  > * `U+00B` | `<VT>` | 垂直制表符 | `\v`
  > * `U+00C` | `<FF>` | 分页符 | `\f`
  > * `U+0020` | `<SP>` | 空格
  > * `U+00A0` | `<NBSP>` | 无间断空格
  > * `Others` | `<USP>` | 其他 Unicode 空白

* **Line terminators | 行终止符**

  Line terminator characters are used to improve the **readability** of the source text. However, in some cases, line terminators can influence the **execution** of JavaScript code as there are a few places where they are forbidden. Line terminators also affect the process of [automatic semicolon insertion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#automatic_semicolon_insertion).

  The `\s` [character class escape](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Character_classes) in regular expressions matches all white space and line terminators.

  > * 提高源码的可读性。
  > * 影响 JavaScript 代码的执行。
  > * 影响[自动分号补全](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Lexical_grammar#automatic_semicolon_insertion)的执行。
  > * 在[正则表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_expressions)中，行终止符会被 **\s** 匹配。
  >
  > ---
  >
  > * `U+00A` | `<LF>` | 换行符 |  `\n`
  > * `U+00D` | `<CR>` | 回车符 |  `\r`
  > * `U+2028` | `<LS>` | 行分隔符
  > * `U+2029` | `<PS>` | 段分隔符

* **Comments | 注释**

  Comments are used to add hints, notes, suggestions, or warnings to JavaScript code. This can make it easier to read and understand. They can also be used to disable code to prevent it from being executed.

  JavaScript has two long-standing ways to add comments to code: **line comments** and **block comments**. In addition, there's a special **hashbang comment syntax**.

  > * 注释用来在源码中增加提示、笔记、建议、警告等信息，可以帮助阅读和理解源码。
  >
  > * 在调试时，可以用来将一段代码屏蔽掉，防止其运行；
  >
  > ---
  >
  > * **Line comments** | 行注释
  > * **Block comments** ｜ 块注释
  > * **Hashbang comments**

* **Indentifiers | 标识符**

  An identifier is used to **link a value with a name**. Identifiers can be used in various places:

  > * 标识符用于将值与名字进行连接。

* **Keywords | 关键字**

  *Keywords* are **tokens** that look like identifiers but have **special meanings** in JavaScript. 

  > * *关键字*是 JavaScript 中看起来像标识符但又具有特殊含义的标记。
  >
  > ---
  >
  > * break
  > * case
  > * catch
  > * class
  > * const
  > * continue
  > * debugger
  > * default
  > * delete
  > * do
  > * else
  > * export
  > * extends
  > * false
  > * finally
  > * for
  > * function
  > * if
  > * import
  > * in
  > * instanceof
  > * new
  > * null
  > * return
  > * super
  > * switch
  > * this
  > * throw
  > * true
  > * try
  > * typeof
  > * var
  > * void
  > * while
  > * with
  >
  > ---
  >
  > * enum
  > * implements
  > * interface
  > * let
  > * package
  > * private
  > * protected
  > * public
  > * static
  >
  > ---
  >
  > * await
  > * abstract
  > * boolean
  > * byte
  > * char
  > * double
  > * final
  > * float
  > * goto
  > * int
  > * long
  > * native
  > * short
  > * synchronized
  > * transient
  > * volatile
  >
  > ---
  >
  > * null
  > * true
  > * False

* **Literals | 字面量**

  **Note:** This section discusses literals that are atomic tokens. [Object literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer) and [array literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Array#array_literal_notation) are [expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators) that consist of a series of tokens.

  > * atomic tokens
  >
  > ---
  >
  > * Null literal
  > * Boolean literal
  > * Numeric literal
  > * String literals
  > * Regular expression literals
  > * Template literals

* **Automatic semicolon insertion | 自动分号补全(ASI)**

  Some [JavaScript statements](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements)' syntax definitions require semicolons (`;`) at the end. 

  > 一些 [JavaScript 语句](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements)必须用分号结束，所以会被自动分号补全 (ASI) 影响：
  >
  > ---
  >
  > * `var`, `let`, `const`, `using`, `await using`
  > * `Expression statements`
  > * `do...while`
  > * `continue`, `break`, `return`, `throw`
  > * `debugger`
  > * Class field declarations (public or private)
  > * `import`, `export`
