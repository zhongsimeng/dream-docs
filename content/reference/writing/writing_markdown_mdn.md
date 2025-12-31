# Writing Markdown guide / 如何使用 Markdown 来撰写文档

本文介绍了如何使用 Markdown 来编写 MDN Web 文档项目中的文档。我们以 GitHub 风格的 Markdown（GFM）为基础，并添加了一些扩展来支持一些我们在 MDN 上需要而 GFM 仍不支持的东西。

## [基础：Github 风格的 Markdown](https://developer.mozilla.org/zh-CN/docs/MDN/Writing_guidelines/Howto/Markdown_in_MDN#基础：github_风格的_markdown)

MDN Markdown 的基础是 Github 风格的 Markdown（GFM）：https://github.github.com/gfm/。这意味着，对于本文中未指定的内容，你可以参考 GFM 规范。而 GFM 又是 CommonMark（https://spec.commonmark.org/）的超集。

### [链接](https://developer.mozilla.org/zh-CN/docs/MDN/Writing_guidelines/Howto/Markdown_in_MDN#链接)

GFM 规范定义了两种基础的链接类型：

- [内联链接](https://github.github.com/gfm/#inline-link)：在链接显示的文字后面紧跟链接的地址。
- [引用链接](https://github.github.com/gfm/#reference-link)：链接的目标在当前文档的其他地方定义。

```
[马卡龙](https://zh.wikipedia.org/wiki/馬卡龍)虽然美味，但制作难度大。
```

### 示例代码块

在 MDN，你可以使用围栏代码块展现示例代码块。且必须使用信息字符串的第一个单词指定示例代码的语言，这将用于提供代码块的语法高亮。

```javascript
const greeting = "我会得到 JavaScript 语法高亮";
```

你可以为任何语言标识符添加 `-nolint` 后缀：

```html-nolint
<p>
我不会被 lint。
</p>
```

GFM 支持[信息字符串](https://github.github.com/gfm/#info-string)，它允许作者提供有关代码块的附加信息。

- `example-good`：将其标注为良好示例（可被参考）
- `example-bad`：将其标注为错误示例（应避免使用）
- `hidden`：不在网页中展示此代码块。代码仅用于运行实例。

```javascript example-good
const greeting = "这是一个良好示例";
```

### 备注、警告和标注

有时作者需要特别强调某些内容。要做到这一点，可以使用 [GFM 备注块语法](https://github.com/orgs/community/discussions/16925)，这是一种带有特殊起始行的 GFM 块引用。一共有三种类型：备注、警告和标注。

- 要添加备注，请创建一个 GFM 块引用，起始行为 `[!NOTE]`。
- 要添加警告，请创建一个 GFM 块引用，起始行为 `[!WARNING]`。
- 要添加标注，请创建一个 GFM 块引用，起始行为 `[!CALLOUT]`。

### 定义列表

为了在 MDN 中创建定义列表，你需要编写一个 GFM 无序列表（[``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/ul)）的修改形式。

### 表格

GFM 提供了创建[表格](https://github.github.com/gfm/#tables-extension-)的语法，我们在 MDN 中使用了它。

```markdown
| Heading 1 | Heading 2 | Heading 3 |
| --------- | --------- | --------- |
| cell 1    | cell 2    | cell 3    |
| cell 4    | cell 5    | cell 6    |
```

### 上标和下标

如果有必要，你可以使用 HTML [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/sup) 和 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/sub) 元素，但应尽可能使用替代品。

### 网页摘要

*网页摘要*是页面中的第一个“内容”段落——出现在页面元数据（front matter）以及任何[侧边栏](https://developer.mozilla.org/zh-CN/docs/MDN/Writing_guidelines/Page_structures/Macros/Commonly_used_macros#添加侧边栏)和[网页横幅](https://developer.mozilla.org/zh-CN/docs/MDN/Writing_guidelines/Page_structures/Macros/Commonly_used_macros#页面或章节头部的指示器)宏之后的第一段文本内容。

此摘要用于搜索引擎优化（SEO），也被一些宏自动包含在网页列表旁。因此，第一段应即简洁又翔实。

## 参见

* [如何使用 Markdown 来撰写文档](https://developer.mozilla.org/zh-CN/docs/MDN/Writing_guidelines/Howto/Markdown_in_MDN)
