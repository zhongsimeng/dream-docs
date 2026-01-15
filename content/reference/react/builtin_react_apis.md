# Built-in React APIs

In addition to [Hooks](https://react.dev/reference/react/hooks) and [Components](https://react.dev/reference/react/components), the `react` package exports a few other APIs that are useful for **defining components**. This page lists all the remaining modern React APIs.

> react 软件包还导出了一些其他用于定义组件的 API。

- [`createContext`](https://react.dev/reference/react/createContext) lets you define and provide context to the child components. Used with [`useContext`.](https://react.dev/reference/react/useContext)

  > 允许你定义子组件并提供上下文。

- [`lazy`](https://react.dev/reference/react/lazy) lets you defer loading a component’s code until it’s rendered for the first time.

  > 允许你延迟价值组件的代码，知道该组件首次渲染时才加载。

- [`memo`](https://react.dev/reference/react/memo) lets your component skip re-renders with same props. Used with [`useMemo`](https://react.dev/reference/react/useMemo) and [`useCallback`.](https://react.dev/reference/react/useCallback)

  > 允许组件跳过使用相同 props 的重新渲染。

- [`startTransition`](https://react.dev/reference/react/startTransition) lets you mark a state update as non-urgent. Similar to [`useTransition`.](https://react.dev/reference/react/useTransition)

  > 允许你讲状态更新标记为非紧急

- [`act`](https://react.dev/reference/react/act) lets you wrap renders and interactions in tests to ensure updates have processed before making **assertions**.

  > 允许你讲渲染和交互式操作包装在测试中，以确保在进行断言之前更新已处理完毕。

## Resource APIs 

*Resources* can be accessed by a component without having them as part of their state. For example, a component can read a message from a Promise or read styling information from a context.

> 组件无需将资源作为其状态的一部分即可访问*这些资源。例如，组件可以从 Promise 中读取消息，或者从上下文中读取样式信息。*

To read a value from a resource, use this API:

- [`use`](https://react.dev/reference/react/use) lets you read the value of a resource like a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) or [context](https://react.dev/learn/passing-data-deeply-with-context).

  > 允许你读取资源（例如 Promise 或 上下文）的值

```jsx
function MessageComponent({ messagePromise }) {
  const message = use(messagePromise);
  const theme = use(ThemeContext);
  // ...
}
```

