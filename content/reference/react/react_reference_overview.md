# React Reference Overview

This section provides **detailed reference documentatio**n for working with React. For an introduction to React, please visit the [Learn](https://react.dev/learn) section.

> 本节提供使用 React 的**详细参考文档**。如需了解 React 的入门知识，请访问[“学习”](https://react.dev/learn)部分。

The React reference documentation is broken down into **functional subsections**:

> React 参考文档被细分为多个功能性小节：

## React

Programmatic React features:

- [Hooks](https://react.dev/reference/react/hooks) - Use different **React features** from your components.

  > 在组件中使用不同的 React 特性

- [Components](https://react.dev/reference/react/components) - **Built-in components** that you can use in your JSX.

  > 可以在 JSX 中使用的内置组件

- [APIs](https://react.dev/reference/react/apis) - APIs that are useful for **defining components**.

  > 用于定义组件的 API

- [Directives](https://react.dev/reference/rsc/directives) - Provide instructions to **bundlers compatible** with React Server Components.

  > 为与 React 服务器组件兼容的打包器提供指令

## React DOM

React DOM contains features that are only supported for web applications (which run in the **browser DOM environment**). This section is broken into the following:

> React-dom 仅支持在 web 应用程序中使用（在浏览器 DOM 环境中运行）。本节分为以下部分：

- [Hooks](https://react.dev/reference/react-dom/hooks) - Hooks for web applications which run in the browser DOM environment.

  > 用于在浏览器 DOM 环境中运行的 Web 应用程序的钩子

- [Components](https://react.dev/reference/react-dom/components) - React supports all of the browser built-in HTML and SVG components.

  > React 支持所有浏览器内置的 HTML 和 SVG 组件

- [APIs](https://react.dev/reference/react-dom) - The `react-dom` package contains methods supported only in web applications.

  >  `react-dom` 包含仅在 web 应用程序中支持的方法

- [Client APIs](https://react.dev/reference/react-dom/client) - The `react-dom/client` APIs let you render React components on the client (in the browser).

  > `react-dom/client` API 运行在客户端（浏览器中）渲染 React 组件

- [Server APIs](https://react.dev/reference/react-dom/server) - The `react-dom/server` APIs let you render React components to HTML on the server.

  > `react-dom/server` API 允许在服务器端将 React 组件渲染为 HTML

- [Static APIs](https://react.dev/reference/react-dom/static) - The `react-dom/static` APIs let you generate static HTML for React components.

  > `react-dom/static` API 允许将 React 组件生成静态 HTML。

## React Compiler

The React Compiler is a **build-time optimization tool** that automatically **memoizes** your React components and values:

> React 编译器是一个构建时优化工具，可以自动为你的 React 组件和数值添加记忆优化（memoization）：

- [Configuration](https://react.dev/reference/react-compiler/configuration) - Configuration options for React Compiler.

  > React 编译器的配置选项

- [Directives](https://react.dev/reference/react-compiler/directives) - Function-level directives to control compilation.

  > 用于控制编译的函数级指令

- [Compiling Libraries](https://react.dev/reference/react-compiler/compiling-libraries) - Guide for shipping pre-compiled library code.

  > 发布预编译库代码的指南

## ESLint Plugin React Hooks

The [ESLint plugin for React Hooks](https://react.dev/reference/eslint-plugin-react-hooks) helps enforce the Rules of React:

> [针对 React Hook 的 ESLint 插件](https://zh-hans.react.dev/reference/eslint-plugin-react-hooks) 有助于强制执行 React 的规则：

- [Lints](https://react.dev/reference/eslint-plugin-react-hooks) - Detailed documentation for each lint with examples.

  > 每种 lint 的详细文档和示例

## Rules of React

React has idioms — or rules — for how to express patterns in a way that is easy to understand and yields high-quality applications:

> React 有一套表达模式的俗语与规则，它们以一种易于理解并能帮助实现高质量应用程序的方式表达出来：

- [Components and Hooks must be pure](https://react.dev/reference/rules/components-and-hooks-must-be-pure) – Purity makes your code easier to understand, debug, and allows React to automatically optimize your components and hooks correctly.

  > 组件与 Hook 的纯粹代码更易于理解、调试，并允许 React 自动优化组件与 Hook。

- [React calls Components and Hooks](https://react.dev/reference/rules/react-calls-components-and-hooks) – React is responsible for rendering components and hooks when necessary to optimize the user experience.

  > React 负责在必要时渲染组件与 Hook，以优化用户体验。

- [Rules of Hooks](https://react.dev/reference/rules/rules-of-hooks) – Hooks are defined using JavaScript functions, but they represent a special type of reusable UI logic with restrictions on where they can be called.

  > Hook 使用 JavaScript 函数定义，但它们代表一种特殊类型的可重用 UI 逻辑，对它们可以被调用的位置有限制。

## Legacy APIs

- [Legacy APIs](https://react.dev/reference/react/legacy) - Exported from the `react` package, but not recommended for use in newly written code.

  > 从 react 包中导出，但不建议在新编写的代码中使用。