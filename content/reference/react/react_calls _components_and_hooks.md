# React calls Components and Hooks

React is **responsible for rendering** components and Hooks when necessary to **optimize the user experience**. It is declarative: you tell React what to render in your component’s logic, and React will figure out how best to display it to your user.

> React 负责在**必要时渲染**组件和 Hook，**以优化用户体验**。它是声明式的，你只需要告诉 React 在你的组件逻辑中渲染什么，React 会决定最佳的渲染方式以展示给用户。

- [Never call component functions directly](https://react.dev/reference/rules/react-calls-components-and-hooks#never-call-component-functions-directly)

  > 绝不要直接调用组件函数

- Never pass around Hooks as regular values

  > 绝不要像传递常规值一样传递 Hook

  - [Don’t dynamically mutate a Hook](https://react.dev/reference/rules/react-calls-components-and-hooks#dont-dynamically-mutate-a-hook)

    > 不要在运行时动态修改 Hook

  - [Don’t dynamically use Hooks](https://react.dev/reference/rules/react-calls-components-and-hooks#dont-dynamically-use-hooks)

    > 不要动态地使用 Hook

## Never call component functions directly 

Components should **only be used in JSX**. Don’t call them as regular functions. React should call it.

> 组件应该仅在 JSX 中被使用。不要将它们作为普通函数调用。应该由 React 来调用它们。

React must decide when your component function is called [during rendering](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code). In React, you do this using JSX.

> **React 必须决定在渲染过程中何时调用你的组件函数**。在 React 中，你可以通过 JSX 来实现这一点。

```jsx
function BlogPost() {
  // ✅ Good: Only use components in JSX
  return <Layout><Article /></Layout>;
}

function BlogPost() {
  // 🔴 Bad: Never call them directly
  return <Layout>{Article()}</Layout>;
}
```

If a component contains Hooks, it’s easy to violate the [Rules of Hooks](https://react.dev/reference/rules/rules-of-hooks) when components are called directly in a loop or conditionally.

> 如果组件包含 Hook，在循环或条件语句中直接调用它们时，很容易违反 [Hook 的规则](https://zh-hans.react.dev/reference/rules/rules-of-hooks)。

Letting React orchestrate rendering also allows a number of benefits:

> 让 React 来协调渲染还有许多好处：

- **Components become more than functions.** React can augment them with features like *local state* through Hooks that are tied to the component’s identity in the tree.

  > 组件不仅仅是函数。React 可以通过 Hook 向它们添加特性，如与**组件在树中**身份相关联的局部状态。

- **Component types participate in reconciliation.** By letting React call your components, you also tell it more about the **conceptual structure of your tree**. For example, when you move from rendering `<Feed>` to the `<Profile>` page, React won’t attempt to re-use them.

  > 组件类型参与协调。通过让 React 来调用你的组件，你也向它展示了你的**组件树的结构**。

- **React can enhance your user experience.** For example, it can let the browser do some work between component calls so that **re-rendering** a large component tree **doesn’t block the main thread**.

  > React 可以提升你的用户体验。例如，它可以在组件调用期间中断，允许浏览器执行一些工作，这样重新渲染大型组件树就不会阻塞主线程。

- **A better debugging story.** If components are first-class citizens that the library is aware of, we can build rich **developer tools** for introspection in development.

  > 更好的调试体验。如果组件在库中被视为“一等公民”，我们可以围绕这些组件构建丰富的开发者工具，以便在开发过程中进行检查和理解程序内容结构和状态。

- **More efficient reconciliation.** **React can decide exactly which components in the tree need re-rendering** and skip over the ones that don’t. That makes your app faster and more snappy.

  > 更高效的协调。**React 可以决定树中哪些组件需要重新渲染**，并跳过那些无需重新渲染的组件。使得你的应用程序运行更快，响应更敏捷。

## Never pass around Hooks as regular values 

Hooks should only be called inside of components or Hooks. Never pass it around as a regular value.

> Hook 只能在组件或 Hook 内部调用。永远不要像常规值一样传递它们。

Hooks allow you to **augment a component with React features**. They should **always be called as a function**, and never passed around as a regular value. This enables *local reasoning*, or the ability for developers to understand everything a component can do by looking at that component in isolation.

> Hook 允许你使用 React 功能来增强组件。它们应该**始终作为函数来调用**，而绝不作为常规值传递。这使得局部推理成为可能，即开发者可以通过单独审视一个组件，就能理解该组件所能执行的所有操作。

Breaking this rule will cause React to not automatically optimize your component.

> 违反此规则将导致 React 无法自动优化你的组件。

### Don’t dynamically mutate a Hook 

Hooks should **be as “static” as possible**. This means you shouldn’t dynamically mutate them. For example, this means you shouldn’t write **higher order Hooks**:

> Hook 应当尽可能保持“静态”。这意味着你不应该动态地改变它们。这意味着你不应该编写高阶组件。

```jsx
function ChatInput() {
  // 🔴 Bad: don't write higher order Hooks
  const useDataWithLogging = withLogging(useData);
  const data = useDataWithLogging();
}
```

Hooks should be immutable and not be mutated. Instead of mutating a Hook dynamically, create a static version of the Hook with the desired functionality.

> Hook 应该是不可变的，不应该被动态改变；与其动态地改变 Hook，不如在创建时就定义一个包含所需功能的静态版本的 Hook。

```jsx
function ChatInput() {
  // ✅ Good: Create a new version of the Hook
  const data = useDataWithLogging();
}

function useDataWithLogging() {
  // ... Create a new version of the Hook and inline the logic here
}
```

### Don’t dynamically use Hooks 

Hooks should also not be dynamically used: for example, instead of doing dependency injection in a component by passing a Hook as a value:

> Hook 也不应该被动态使用，例如，不应该通过将 Hook 作为值传递来在一个组件中实现依赖注入。

```jsx
function ChatInput() {
  // 🔴 Bad: don't pass Hooks as props
  return <Button useData={useDataWithLogging} />
}
```

You should always inline the call of the Hook into that component and handle any logic in there.

> 你应该始终将 Hook 的调用内联到组件内部，并在其中处理所有逻辑。

```jsx
function ChatInput() {
  return <Button />
}

function Button() {
  const data = useDataWithLogging(); // ✅ Good: Use the Hook directly
}

function useDataWithLogging() {
  // If there's any conditional logic to change the Hook's behavior, it should be inlined into
  // the Hook
}
```

This way, `<Button />` is much easier to understand and debug. When Hooks are used in dynamic ways, it increases the complexity of your app greatly and inhibits local reasoning, making your team less productive in the long term. It also makes it easier to accidentally break the [Rules of Hooks](https://react.dev/reference/rules/rules-of-hooks) that Hooks should not be called conditionally. If you find yourself needing to mock components for tests, it’s better to mock the server instead to respond with canned data. If possible, it’s also usually more effective to test your app with end-to-end tests.

> 这样，`<Button />` 组件更容易理解也更易于调试。当 Hook 以动态方式使用时，会大大增加应用的复杂性，并妨碍局部推理，这从长远来看会降低团队的生产力。它还更容易意外地违反 [Hook 的规则](https://zh-hans.react.dev/reference/rules/rules-of-hooks)，即 Hook 不应该被条件性地调用。如果你发现自己需要为测试而模拟组件，最好是模拟服务器返回以响应预设数据。如果可能，通常进行端到端测试你的应用是更有效的方法。
