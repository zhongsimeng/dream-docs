# 针对 MDN 文档的本地化指南

本文是针对简体中文（zh-CN）文档的翻译指南。

## 元数据

```
title: HTMLAnchorElement：hash 属性
slug: Web/API/HTMLAnchorElement/hash
l10n:
  sourceCommit: a3d9f61a8990ba7b53bda9748d1f26a9e9810b18
```

## 常见问题

为保证简体中文文档格式的一致性，翻译指南列出了部分规范。

### 标点符号

使用中文全角符号

* 我们可以学习 JavaScript——一种很酷的语言
* 以下示例是“可交互的”
* a、b 和 c

**常见中/英文标点**

| 名称   | 中文 | 英文    |
| ------ | ---- | ------- |
| 括号   | （） | ()      |
| 冒号   | ：   | :       |
| 引号   | “”   | ""      |
| 破折号 | ——   | -- 、 — |

简体中文标点符号参考资源：

- [GB/T 15834―2011 标点符号用法](https://people.ubuntu.com/~happyaron/l10n/GB(T)15834-2011.html)
- [维基百科：标点符号](https://zh.wikipedia.org/zh-cn/标点符号)

### 中文和拉丁语系文字间加空格

对于简体中文文档，请在中文和拉丁语系文字之间保留**一个空格**。

数字与中文之间也请保留空格。

但在拉丁语系文字和中文标点之间，则无需保留空格。

* 学习 Web 开发
* 学习 JavaScript、HTML、CSS 等
* 应用程序接口（API）
* 它指向一个[示例](#示例)
* 指向 [MDN 开发者文档](https://developer.mozilla.org/)的链接
* 需 10 个小时完成

### 排版

英文文档中，对于较长的段落，会通过断行的形式截断，以方便维护文档。但在 Markdown 中，断行会引入空格，在简体中文翻译中，我们有如下约定：

- 在段落不是特别长的情况下（200 个字符以内），请不要断行。
- 若段落过长，也请在中文与拉丁语系文字、数字之间，或是句子末尾断行。

例如：

```
This is an example.
We usually write a paragraph into multiple lines.
Like this.
```

而在中文文档中，应该使它们在同一行内：

```
这是一个示例。我们不应该断行写这一段话。就像这样。
```

### 词语翻译

我们无需将“you”翻译为“您”，在文档正文部分的翻译中，请统一使用“你”。

### 复数形式

英文文档中，为了使语句的语法正确，会使用大量的复数形式。在中文翻译中，则无需保留这些复数的形式（未翻译的英文名词也同理）。

- 原文：`Application Programming Interfaces (APIs)`
- 宜：`应用程序接口（API）`
- 不宜：`应用程序接口（APIs）`
- 不宜：`应用程序接口们（APIs）`

## 参见

* [针对 MDN 文档的本地化指南](https://github.com/mdn/translated-content/blob/main/docs/zh-cn/translation-guide.md)