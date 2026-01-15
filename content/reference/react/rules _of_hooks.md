# Rules of Hooks

Hooks are defined using JavaScript functions, but they represent a special type of **reusable UI logic** with restrictions on where they can be called.

> Hooks 是使用 JavaScript 函数定义的，但它们代表了一种特殊的可重用的 UI 逻辑，并且对它们可以被的调用位置有限制。

- [Only call Hooks at the top level](https://react.dev/reference/rules/rules-of-hooks#only-call-hooks-at-the-top-level)

  > 只在顶层调用 Hook

- [Only call Hooks from React functions](https://react.dev/reference/rules/rules-of-hooks#only-call-hooks-from-react-functions)

  > 仅在函数中调用 Hook

## Only call Hooks at the top level 

Functions whose names start with `use` are called [*Hooks*](https://react.dev/reference/react) in React.

> 在 React 中，以 `use` 开头命名的函数被称为 **[Hook](https://zh-hans.react.dev/reference/react)**。

**Don’t call Hooks inside loops, conditions, nested functions, or `try`/`catch`/`finally` blocks.** Instead, always use Hooks at the top level of your React function, before any early returns. You can only call Hooks while React is rendering a function component:

> 不要在循环、条件语句、嵌套函数或 try/catch/finally 代码块中调用 Hook。
>
> 相反，请始终在 React 函数组件的顶层，在任何提前返回之前使用 Hooks。
>
> 你只能在 React 渲染函数组件时调用 Hooks：

- ✅ Call them at the t**op level in the body** of a [function component](https://react.dev/learn/your-first-component).

  > 在函数组件主体的顶层调用它们

- ✅ Call them at the top level in the body of a [custom Hook](https://react.dev/learn/reusing-logic-with-custom-hooks).

  > 在自定义 Hook 主体 的顶层调用它们

```jsx
function Counter() {
  // ✅ Good: top-level in a function component
  const [count, setCount] = useState(0);
  // ...
}

function useWindowWidth() {
  // ✅ Good: top-level in a custom Hook
  const [width, setWidth] = useState(window.innerWidth);
  // ...
}
```

It’s **not** supported to call Hooks (functions starting with `use`) in any other cases, for example:

> 不支持在其他任何情况下调用以 `use` 开头的 Hook，例如：

- 🔴 Do not call Hooks inside conditions or loops.

  > 不要在条件语句或循环中调用 Hook。

- 🔴 Do not call Hooks after a conditional `return` statement.

  > 不要在条件性的 return 语句之后调用 Hook。

- 🔴 Do not call Hooks in event handlers.

  > 不要在事件处理函数中调用 Hook。

- 🔴 Do not call Hooks in class components.

  > 不要在类组件中调用 Hook。

- 🔴 Do not call Hooks inside functions passed to `useMemo`, `useReducer`, or `useEffect`.

  > 不要在传递给 `useMemo`、`useReducer` 或 `useEffect` 的函数内部调用 Hook。

- 🔴 Do not call Hooks inside `try`/`catch`/`finally` blocks.

  > 不要在 `try`/`catch`/`finally` 代码块中调用 Hook。

If you break these rules, you might see this error.

```jsx
function Bad({ cond }) {
  if (cond) {
    // 🔴 Bad: inside a condition (to fix, move it outside!)
    const theme = useContext(ThemeContext);
  }
  // ...
}

function Bad() {
  for (let i = 0; i < 10; i++) {
    // 🔴 Bad: inside a loop (to fix, move it outside!)
    const theme = useContext(ThemeContext);
  }
  // ...
}

function Bad({ cond }) {
  if (cond) {
    return;
  }

  // 🔴 Bad: after a conditional return (to fix, move it before the return!)
  const theme = useContext(ThemeContext);
  // ...
}

function Bad() {
  function handleClick() {
    // 🔴 Bad: inside an event handler (to fix, move it outside!)
    const theme = useContext(ThemeContext);
  }
  // ...
}

function Bad() {
  const style = useMemo(() => {
    // 🔴 Bad: inside useMemo (to fix, move it outside!)
    const theme = useContext(ThemeContext);
    return createStyle(theme);
  });
  // ...
}

class Bad extends React.Component {
  render() {
    // 🔴 Bad: inside a class component (to fix, write a function component instead of a class!)
    useEffect(() => {})
    // ...
  }
}

function Bad() {
  try {
    // 🔴 Bad: inside try/catch/finally block (to fix, move it outside!)
    const [x, setX] = useState(0);
  } catch {
    const [x, setX] = useState(1);
  }
}
```

You can use the [`eslint-plugin-react-hooks` plugin](https://www.npmjs.com/package/eslint-plugin-react-hooks) to catch these mistakes.

> 你可以使用 [`eslint-plugin-react-hooks` 插件](https://www.npmjs.com/package/eslint-plugin-react-hooks) 来捕获这些错误。

### Note

[Custom Hooks](https://react.dev/learn/reusing-logic-with-custom-hooks) *may* call other Hooks (that’s their whole purpose). This works because custom Hooks are also supposed to only be called while a function component is rendering.

> 

## Only call Hooks from React functions 

Don’t call Hooks from regular JavaScript functions. Instead, you can:

✅ Call Hooks from React function components.

> 在 React 函数组件中调用 Hook

 ✅ Call Hooks from [custom Hooks](https://react.dev/learn/reusing-logic-with-custom-hooks#extracting-your-own-custom-hook-from-a-component).

> 在自定义 Hook 中调用 Hook。

By following this rule, you ensure that all stateful logic in a component is clearly visible from its source code.

> 遵循这条规则，你可以确保组件中的所有状态逻辑在其源代码中清晰可见。

```jsx
function FriendList() {
  const [onlineStatus, setOnlineStatus] = useOnlineStatus(); // ✅
}

function setOnlineStatus() { 
  // ❌ Not a component or custom Hook!
  const [onlineStatus, setOnlineStatus] = useOnlineStatus();
}
```