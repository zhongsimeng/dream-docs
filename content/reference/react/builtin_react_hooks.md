# Built-in React Hooks

*Hooks* let you use different React features from your components. You can either use the built-in Hooks or combine them to build your own. This page lists all built-in Hooks in React.

> Hook 允许你在组件中使用不同的 React 功能。你可以使用内置的 Hooks，也可以组合使用它们来构建自己的 Hooks。本页面列出了 React 中所有的内置 Hooks。

## State Hooks 

*State* lets a component [“remember” information like user input.](https://react.dev/learn/state-a-components-memory) For example, a form component can use state to store the input value, while an image gallery component can use state to store the selected image index.

> 状态帮助组件“记住”用户输入信息。

To add state to a component, use one of these Hooks:

- [`useState`](https://react.dev/reference/react/useState) declares a state variable that you can update directly.

  > 声明可以直接更新的状态变量。

- [`useReducer`](https://react.dev/reference/react/useReducer) declares a state variable with the update logic inside a [reducer function.](https://react.dev/learn/extracting-state-logic-into-a-reducer)

  > 在 reducer 函数中声明带有更新逻辑的 state 变量。

```jsx
function ImageGallery() {
  const [index, setIndex] = useState(0);
  // ...
```

## Context Hooks 

*Context* lets a component [receive information from distant parents without passing it as props.](https://react.dev/learn/passing-props-to-a-component) For example, your app’s top-level component can pass the current UI theme to all components below, no matter how deep.

> 上下文帮助组件从祖先组件接收信息，而无需将其作为 props 传递。

- [`useContext`](https://react.dev/reference/react/useContext) reads and subscribes to a context.

  > 读取和订阅上下文。

```jsx
function Button() {
  const theme = useContext(ThemeContext);
  // ...
```

## Ref Hooks 

*Refs* let a component [hold some information that isn’t used for rendering,](https://react.dev/learn/referencing-values-with-refs) like a DOM node or a timeout ID. Unlike with state, updating a ref does **not re-render** your component. Refs are an “**escape hatch**” from the React paradigm. They are useful when you need to work with non-React systems, such as the built-in browser APIs.

> Refs 允许组件保存一些不用于渲染的信息，比如 DOM 节点或 timeout ID。
>
> 与状态不同，更新 ref 不会重新渲染组件。ref 是从 React 范例中的“脱围机制”。
>
> 当需要与非 React 系统如浏览器内置API一同工作时，ref 将会非常有用。

- [`useRef`](https://react.dev/reference/react/useRef) declares a ref. You can hold any value in it, but most often it’s used to hold a DOM node.

  > 你可以在其中保存任何值，但最常用于保存 DOM 节点。

- [`useImperativeHandle`](https://react.dev/reference/react/useImperativeHandle) lets you customize the ref exposed by your component. This is rarely used.

  > 自定义从组件中暴露的 ref，但是很少使用。

```jsx
function Form() {
  const inputRef = useRef(null);
  // ...
```

## Effect Hooks 

*Effects* let a component [connect to and synchronize with external systems.](https://react.dev/learn/synchronizing-with-effects) This includes dealing with **network**, **browser DOM**, **animations**, widgets written using a different **UI library**, and other **non-React code**.

> Effect 允许组件连接到外部系统并与之同步。这包括处理网络、浏览器 DOM、动画、使用不同 UI 库编写小部件以及其他非 React 代码。

- [`useEffect`](https://react.dev/reference/react/useEffect) **connects** a component to an external system.

  > 将组件连接到外部系统。

```jsx
function ChatRoom({ roomId }) {
  useEffect(() => {
    const connection = createConnection(roomId);
    connection.connect();
    return () => connection.disconnect();
  }, [roomId]);
  // ...
```

Effects are an “escape hatch” from the React paradigm. Don’t use Effects to orchestrate the data flow of your application. If you’re not interacting with an external system, [you might not need an Effect.](https://react.dev/learn/you-might-not-need-an-effect)

> Effect 是从 React 范式中的“脱围机制”。避免使用 Effect 协调应用程序的数据流。如果不需要与外部系统交互，那么可能不需要 Effect。

There are two rarely used variations of `useEffect` with differences in timing:

> `useEffect` 有两个很少使用的变换形式，它们在执行时机有所不同：

- [`useLayoutEffect`](https://react.dev/reference/react/useLayoutEffect) fires before the browser repaints the screen. You can measure layout here.

  > 在浏览器重新绘制屏幕前执行，可以在此处测量布局。

- [`useInsertionEffect`](https://react.dev/reference/react/useInsertionEffect) fires before React makes changes to the DOM. Libraries can insert dynamic CSS here.

  > 在 React 对 DOM 进行更改之前触发，库可以在此处插入动态 CSS。

## Performance Hooks 

A common way to optimize re-rendering performance is to skip unnecessary work. For example, you can tell React to reuse a cached calculation or to skip a re-render if the data has not changed since the previous render.

> 优化重新渲染性能的一种常见方法是跳过不必要的工作。例如，可以告诉 React 重用缓存的计算结果，或者如果数据自上次渲染以来没有更改，则跳过重新渲染。

To skip calculations and unnecessary re-rendering, use one of these Hooks:

- [`useMemo`](https://react.dev/reference/react/useMemo) lets you cache the result of an expensive calculation.

  > 缓存计算代价昂贵的计算结果

- [`useCallback`](https://react.dev/reference/react/useCallback) lets you cache a function definition before passing it down to an optimized component.

  > 将函数传递给优化组件之前缓存函数定义。

```jsx
function TodoList({ todos, tab, theme }) {
  const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
  // ...
}
```

Sometimes, you can’t skip re-rendering because the screen actually needs to update. In that case, you can improve performance by **separating blocking updates** that must be synchronous (like typing into an input) from non-blocking updates which don’t need to block the user interface (like updating a chart).

> 有时由于屏幕确实需要更新，无法跳过重新渲染。在这种情况下，可以通过将必须同步的阻塞更新（比如使用输入法输入内容）与不需要阻塞用户界面的非阻塞更新（比如更新图标）分离以提高性能。

To prioritize rendering, use one of these Hooks:

- [`useTransition`](https://react.dev/reference/react/useTransition) lets you mark a state transition as non-blocking and allow other updates to interrupt it.

  > 允许将状态转换标记为非阻塞，并允许其他更新中断它。

- [`useDeferredValue`](https://react.dev/reference/react/useDeferredValue) lets you defer updating a non-critical part of the UI and let other parts update first.

  > 允许延迟更新 UI 的非关键部分，以让其他部分先更新。

## Other Hooks 

These Hooks are mostly useful to library authors and aren’t commonly used in the application code.

- [`useDebugValue`](https://react.dev/reference/react/useDebugValue) lets you customize the label React DevTools displays for your custom Hook.

  > 自定义 React 开发者工具为自定义 Hook 添加的标签

- [`useId`](https://react.dev/reference/react/useId) lets a component associate a unique ID with itself. Typically used with accessibility APIs.

  > 将唯一的 ID 与组件相关联，其通常与可访问性 API 一起使用

- [`useSyncExternalStore`](https://react.dev/reference/react/useSyncExternalStore) lets a component subscribe to an external store.

  > 订阅外部 store

- [`useActionState`](https://react.dev/reference/react/useActionState) allows you to manage state of actions.

  > 允许你管理动作的状态

## Your own Hooks 

You can also [define your own custom Hooks](https://react.dev/learn/reusing-logic-with-custom-hooks#extracting-your-own-custom-hook-from-a-component) as JavaScript functions.

> 开发者可以 [自定义 Hook](https://zh-hans.react.dev/learn/reusing-logic-with-custom-hooks#extracting-your-own-custom-hook-from-a-component) 作为 JavaScript 函数。