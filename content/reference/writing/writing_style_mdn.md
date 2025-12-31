# Writing style guide / 文档写作规范

文档写作规范写作准则

- “3C”准则：**清晰性（clearly）**、**简洁性（concisely）**、**一致性（consistently）**
- 描述性介绍：在开篇充分概括该页将涵盖的信息，读者在浏览完内容后可能会取得的成果。
- SEO 意识：搜索引擎优化

## 示例

```
# 文档写作规范

本篇写作风格指南描述了 MDN Web 文档上的内容应该如何书写、组织、拼写和格式化。

## 写作准则

我们的目标是写出包括读者可能需要的所有信息的页面，以了解手头的主题。

## 写作风格

除了用英语写出语法正确的句子外，我们建议你遵循这些准则，以保持 MDN Web 文档的内容一致。

## 页面部件

本节列出了通常出现在页面上的标题、注释、链接和示例等组件应遵循的准则。

## 参见

* [MDN 文档写作规范](https://developer.mozilla.org/zh-CN/docs/MDN/Writing_guidelines/Writing_style_guide#%E5%85%B6%E4%BB%96%E5%8F%82%E8%80%83%E8%B5%84%E6%96%99)
```

## 写作风格

### 缩写和缩略语

缩写是一个较长单词的缩短版本，而首字母缩写是使用短语中每个单词的第一个字母创造的新单词。

* 扩展形式：XUL (XML User Interface Language) is Mozilla's XML-based language...
* 大写形式及句点：XUL
* 拉丁文缩写：Web browsers (e.g., Firefox) can be used ...
* 缩写和缩略语的复数形式：CD-ROMs
* this vs. that

### 大写

在文章内容中请使用标准英文大写规则。

* World Wide Web

对于键盘按键，应该使用普通的大写规则。

* Enter
* ESC

某些单词应始终大写（例如商标中的大写字母）

- Boolean（其源自英国数学家和逻辑学家的姓名 [George Boole](https://zh.wikipedia.org/wiki/乔治·布尔)）
- JavaScript（甲骨文公司的商标，应始终写成商标的样式）
- Python、TypeScript、Django 以及其他编程语言和框架名称

### 口头缩略

我们倾向于宽松的写作风格，所以你可以按你的喜好来决定是否使用简写

* don't
* can't
* shouldn't

### 数字和数词

* 逗号：54,000（位数大约 5 位时使用）
* 日期：January 1, 1990 或者 1906/02/24（YYYY/MM/DD格式）
* 年代：1990s
* 数词的复数：486s

### 复数形式

请使用英语风格的复数形式，不要使用拉丁文或希腊文的形式。

* syllabuses、octopuses

### 撇号和引号

在 MDN Web 文档中，我们只使用直角引号和直角撇号。

* Please don't use "curly quotes."

### 逗号

串行逗号（也称为“牛津逗号”）是指在三个或更多项目的系列中出现在连词前的逗号。

* I will travel on trains, planes, and automobiles.

### 连字符

当两个单词连起来组成另一个单词时，如果前一个单词的最后一个字母是元音字母，并且与后一个单词的第一个字母相同时，应使用连字符。

* re-elect
* co-op
* email

### 拼写形式

请使用美式英语拼写。

一般来说，使用 [Dictionary.com](https://www.dictionary.com/) 中的第一个条目，除非该条目被列为变体拼写或主要用于非美国形式的英语中。

### 术语

* 使用 `element` 表示 HTML 和 XML 元素
* 使用 `parameters` ，避免使用arguments

### 语态

推荐使用主动语态。

## 页面部件

### 代码示例

* 标题：一个简短的 `###`（`<h3>`）标题，用来描述通过代码实例演示的情景。
* **描述**：在示例代码前的简短描述，说明你想引起读者注意的示例的具体内容。
* **结果解释**：在示例代码之后的解释，描述结果和代码的工作原理。

### 外部链接

良好的外部链接：

- 独特或不可缺少的（例如，IETF RFC）。
- 对归属、引用或鸣谢是必要的（例如，作为知识共享署名的一部分）
- 比起将这些内容纳入 MDN Web 文档本身，更有可能对该主题进行维护（例如，供应商的发布说明）。
- 开源或社区驱动，就像 MDN Web 文档本身一样

### 短链接

URL 缩短器（如 TinyURL 或 Bitly）可以很好地将长链接缩短为小的、更容易记住的 URL（也称为“短链接”）。

### 标题级别

* 按照递减的顺序使用级别。
* `#` 是保留给页面标题的，`##` 是允许的最高级别 。
* 建议不要添加超过三层的标题。
* 不要在标题中使用内联样式、类或宏调用。
* 不要让两个小节标题紧挨在一起，每个小节标题的下面至少要放上一段对后面各子小节的简短说明。

### 图片及其他媒体

如果要在一个页面上包括图像或其他媒体，请遵循以下准则：

- 确保媒体许可证允许你使用它们。
- 对于图片，请使用 [https://tinypng.com](https://tinypng.com/) 或 [https://imageoptim.com](https://imageoptim.com/) 工具处理它们，以减少页面的大小。
- 对于 `SVG`，通过 [SVGOMG](https://jakearchibald.github.io/svgomg/) 运行代码，并确保 `SVG` 文件在文件末尾有一个空行。

### 列表

列表的格式应该在所有文章中保持一致，并且应在列表中恰当使用标点和结构合理的句子。

* 无序列表：应使用无序列表来分组相关的简明信息。
* 有序列表：有序列表主要用于列举一套指令中的步骤。

### "参见"部分

一般来说，在“参见”部分的链接以[项目符号列表](https://developer.mozilla.org/zh-CN/docs/MDN/Writing_guidelines/Writing_style_guide#列表)格式呈现，列表中的每一项都是一个短语。

- [ARIA 状态和属性](https://developer.mozilla.org/zh-CN/docs/Web/Accessibility/ARIA/Reference/Attributes)
- [Top-level await](https://v8.dev/features/top-level-await) on v8.dev (October 8, 2019)

### 子页面

当你需要添加一些关于某个主题或专题领域的文章时，你通常会通过创建一个着陆页，然后为每篇单独的文章添加子页面来实现。

### 路径名

* `/zh-CN/docs/Learn/HTML/Introduction_to_HTML/Getting_started` 

### 标题

页面标题在搜索结果中使用，也用于在页面顶部的面包屑列表中构建页面层次。

* 大写风格：仅大写第一个单词和专有名词

  * A new method for creating JavaScript rollovers

* 通用原则

  - **由浅入深**

    如[标题级别](https://developer.mozilla.org/zh-CN/docs/MDN/Writing_guidelines/Writing_style_guide#标题级别)部分所述，从较高的 `##` 到较低的 `####` 排布内容，中间不要跳级。

  - **按逻辑分组**

    确保所有相关的小节都在一个较高层次的标题下有逻辑地组合在一起。

  - **保持标题简短**

  - **保持标题具体**

  - **保持标题的重点**

  - **使用平行结构**

    在同一标题层次上，使用类似的语言作为标题。

  - **避免在较低层次的标题中使用普通术语**

  - **不要以冠词开头**

  - **添加引导性信息**

## 参见

* [文档写作规范](https://developer.mozilla.org/zh-CN/docs/MDN/Writing_guidelines/Writing_style_guide)
