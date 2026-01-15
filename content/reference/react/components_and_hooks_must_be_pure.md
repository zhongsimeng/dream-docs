# Components and Hooks must be pure

**Pure functions only perform a calculation and nothing more.** It makes your code easier to understand, debug, and allows React to automatically optimize your components and Hooks correctly.

> 纯函数仅仅执行计算，除此之外不做任何事情。这使得你的代码更易于理解和调试，并允许 React 能够正确地自动优化你的组件和 Hook。

> Note
> This reference page covers advanced topics and requires familiarity with the concepts covered in the [Keeping Components Pure](https://react.dev/learn/keeping-components-pure) page.
>
> 本参考文档讨论了一些高级议题，因此建议先了解 [保持组件纯粹](https://zh-hans.react.dev/learn/keeping-components-pure) 页面中涉及的相关概念。

- [Why does purity matter?](https://react.dev/reference/rules/components-and-hooks-must-be-pure#why-does-purity-matter)
- [Components and Hooks must be idempotent](https://react.dev/reference/rules/components-and-hooks-must-be-pure#components-and-hooks-must-be-idempotent)
- Side effects must run outside of render
  - [When is it okay to have mutation?](https://react.dev/reference/rules/components-and-hooks-must-be-pure#mutation)
- Props and state are immutable
  - [Don’t mutate Props](https://react.dev/reference/rules/components-and-hooks-must-be-pure#props)
  - [Don’t mutate State](https://react.dev/reference/rules/components-and-hooks-must-be-pure#state)
- [Return values and arguments to Hooks are immutable](https://react.dev/reference/rules/components-and-hooks-must-be-pure#return-values-and-arguments-to-hooks-are-immutable)
- [Values are immutable after being passed to JSX](https://react.dev/reference/rules/components-and-hooks-must-be-pure#values-are-immutable-after-being-passed-to-jsx)

### Why does purity matter? 

One of the key concepts that makes React, ***React* is *purity***. A pure component or hook is one that is:

> React 中的一个核心概念是保持纯粹。一个纯组件或 Hook 应该是：

- **Idempotent** – You [always get the same result every time](https://react.dev/learn/keeping-components-pure#purity-components-as-formulas) you run it with the same inputs – props, state, context for component inputs; and arguments for hook inputs.

  > 幂等的——每次使用相同的输入（组件输入的props，state，contenxt 以及 Hook 输入的参数）允许它，你总是得到相同的结果。

- **Has no side effects in render** – Code with side effects should run [**separately from rendering**](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code). For example as an [event handler](https://react.dev/learn/responding-to-events) – where the user interacts with the UI and causes it to update; or as an [Effect](https://react.dev/reference/react/useEffect) – which runs after render.

  > 在渲染中没有副作用——具有副作用的代码应该与渲染过程分开执行。例如，可以作为响应事件，在用户与用户界面交互并导致其更新时触发。或者作为一个 Effect，在渲染之后运行。

- **Does not mutate non-local values**: Components and Hooks should [never modify values that aren’t created locally](https://react.dev/reference/rules/components-and-hooks-must-be-pure#mutation) in render.

  > 不要修改非局部作用域中的值：组件和 Hook 在渲染时中 绝不应该修改非局部创建的值。

When render is kept pure, React can understand how to prioritize which updates are most important for the user to see first. This is made possible because of render purity: since components don’t have side effects [in render](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code), **React can pause rendering components** that aren’t as important to update, and only come back to them later when it’s needed.

> 当渲染保持纯粹时，React 能够理解哪些更新对用户来说最重要，应该优先显示。因为渲染的纯粹，即组件 [在渲染过程中](https://zh-hans.react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code) 不会产生副作用，React 可以暂停渲染那些不是那么重要的组件，等到真正需要时再继续渲染它们。

Concretely, this means that **rendering logic can be run multiple times** in a way that allows React to give your user a pleasant user experience. However, if your component has an untracked side effect – like modifying the value of a global variable [during render](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code) – when React runs your rendering code again, your side effects will be triggered in a way that won’t match what you want. This often leads to unexpected bugs that can degrade how your users experience your app. You can see an [example of this in the Keeping Components Pure page](https://react.dev/learn/keeping-components-pure#side-effects-unintended-consequences).

> 具体来说，这意味着渲染逻辑可以多次运行，这样 React 就能够为你的用户提供最佳的体验。然而，如果你的组件 [在渲染过程中](https://zh-hans.react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code) 有无追踪的副作用，比如修改全局变量的值，那么当 React 再次运行你的渲染代码时，这些副作用会以你不希望的方式被触发。这通常会导致意外的 bug，从而降低用户对你应用的体验感。你可以再 [保持组件纯粹页面中](https://zh-hans.react.dev/learn/keeping-components-pure#side-effects-unintended-consequences) 看到这样一个例子。

#### How does React run your code? 

**React is declarative**: you tell React *what* to render, and React will figure out *how* best to display it to your user. To do this, React has a few phases where it runs your code. You don’t need to know about all of these phases to use React well. But at a high level, you should know about what code runs in *render*, and what runs outside of it.

> React 是声明式的，即你告诉 React 你想要渲染的内容，React 会自己选择最佳的方式向用户展示它。为了做到这一点，React 在执行你的代码时分为几个阶段。虽然你不必了解所有这些阶段就能很好地使用 React。但是，了解哪些代码在渲染阶段运行，哪些代码在渲染阶段之外运行，可以让你更高层次地理解 React。

***Rendering* refers to calculating what the next version of your UI should look like.** After rendering, [Effects](https://react.dev/reference/react/useEffect) are *flushed* (meaning they are run until there are no more left) and may update the calculation if the Effects have impacts on layout. React takes this new calculation and compares it to the calculation used to create the previous version of your UI, then *commits* just the minimum changes needed to the [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) (what your user actually sees) to catch it up to the latest version.

> “渲染”指的是计算你的用户界面（UI）下一个版本应该呈现的样子。渲染完成后，Effect 会被“清空”（意思是一直运行完所有的 Effect 为止），如果这些 Effect 对布局有影响，比如它们可能会改变之前的计算结果。React 会用这个新的计算结果与你 UI 上一个版本所用的计算结果进行比较，然后仅对 DOM，也就是用户实际看到的部分进行最小的必要修改，以确保 UI 更新至最新内容。

## Components and Hooks must be idempotent 

Components must always return the same output with respect to their inputs – props, state, and context. This is known as *idempotency*. [Idempotency](https://en.wikipedia.org/wiki/Idempotence) is a term popularized in functional programming. It refers to the idea that you [always get the same result every time](https://react.dev/learn/keeping-components-pure) you run that piece of code with the same inputs.

> 组件必须始终根据其输入（props，state、和context）返回相同的输出。这被称为“幂等性”。幂等性是函数式编程中经常使用的一个术语，它指的是只要你使用相同的输入运行代码，得到的结果总是一样的。

This means that *all* code that runs [during render](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code) must also be idempotent in order for this rule to hold. For example, this line of code is not idempotent (and therefore, neither is the component):

> 这意味着，为了遵循这一规则，所有在渲染期间执行的代码也必须是幂等的。例如，以下这行代码就不是幂等的（因此，包含这行代码的组件也不是幂等的）：

```jsx
function Clock() {
  const time = new Date(); // 🔴 Bad: always returns a different result!
  return <span>{time.toLocaleString()}</span>
}
```

`new Date()` is not idempotent as it always returns the current date and changes its result every time it’s called. When you render the above component, the time displayed on the screen will stay stuck on the time that the component was rendered. Similarly, functions like `Math.random()` also aren’t idempotent, because they return different results every time they’re called, even when the inputs are the same.

> `new Date()` 函数不是幂等的，因为每次调用时返回的结果都不同，它总是返回调用时刻的日期和时间。当你渲染上面的组件时，屏幕上显示的时间将会停留在组件被渲染的那一刻的时间。类似地，像 `Math.random()` 这样的函数也不是幂等的，因为即使输入相同，它们每次调用也都会返回不同的结果。

This doesn’t mean you shouldn’t use non-idempotent functions like `new Date()` *at all* – you should just avoid using them [during render](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code). In this case, we can *synchronize* the latest date to this component using an [Effect](https://react.dev/reference/react/useEffect):

> 这并不意味着你完全不能使用像 `new Date()` 这样非幂等的函数，你只需要避免 [在渲染过程](https://zh-hans.react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code) 中使用它们即可。在这种情况下，我们可以使用一个 [Effect](https://zh-hans.react.dev/reference/react/useEffect) 来将最新的日期与这个组件进行“同步”：

**App.js**

```jsx
import { useState, useEffect } from 'react';

function useTime() {
  // 1. Keep track of the current date's state. `useState` receives an initializer function as its
  //    initial state. It only runs once when the hook is called, so only the current date at the
  //    time the hook is called is set first.
  const [time, setTime] = useState(() => new Date());

  useEffect(() => {
    // 2. Update the current date every second using `setInterval`.
    const id = setInterval(() => {
      setTime(new Date()); // ✅ Good: non-idempotent code no longer runs in render
    }, 1000);
    // 3. Return a cleanup function so we don't leak the `setInterval` timer.
    return () => clearInterval(id);
  }, []);

  return time;
}

export default function Clock() {
  const time = useTime();
  return <span>{time.toLocaleString()}</span>;
}
```

By wrapping the non-idempotent `new Date()` call in an Effect, it moves that calculation [outside of rendering](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code).

> 通过将非幂等的 `new Date()` 调用包装在一个 Effect 中，就可以将这个计算移动到 [渲染之外](https://zh-hans.react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code)。

If you don’t need to synchronize some external state with React, you can also consider using an [event handler](https://react.dev/learn/responding-to-events) if it only needs to be updated in response to a user interaction.

> 如果你不需要将某些外部状态与 React 同步，只需要在响应用户交互时更新，你可以考虑使用一个 [事件处理函数](https://zh-hans.react.dev/learn/responding-to-events)。

## Side effects must run outside of render 

[Side effects](https://react.dev/learn/keeping-components-pure#side-effects-unintended-consequences) should not run [in render](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code), as React can render components multiple times to create the best possible user experience.

> 副作用不应该在渲染中执行，因为 React 可能会多次渲染组件以提供最佳的用户体验

> Note
>
> Side effects are a broader term than Effects. Effects specifically refer to code that’s wrapped in `useEffect`, while a side effect is a general term for code that has any observable effect other than its primary result of returning a value to the caller.
>
> 副作用是一个比 Effect 更广泛的概念。Effect 特指被包裹在 useEffect 中的代码，而“副作用”是一般术语，指除了将其主要结果（返回值）传递给调用者之外，对外部环境有任何可观察影响的代码。
>
> Side effects are typically written inside of [event handlers](https://react.dev/learn/responding-to-events) or Effects. But never during render.
>
> 副作用通常写在 事件处理函数 或 Effect 内部。但绝对不能在渲染过程中写。

While render must be kept pure, side effects are necessary at some point in order for your app to do anything interesting, like showing something on the screen! The key point of this rule is that side effects should not run [in render](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code), as React can render components multiple times. In most cases, you’ll use [event handlers](https://react.dev/learn/responding-to-events) to handle side effects. Using an event handler explicitly tells React that this code doesn’t need to run during render, keeping render pure. If you’ve exhausted all options – and only as a last resort – you can also handle side effects using `useEffect`.

> 尽管渲染必须保持纯净，但副作用对于你的应用来说是也是非常必要的，这样才能做一些有趣的事情，比如在屏幕上显示内容！这条规则的关键点在于，副作用不应该 [在渲染中](https://zh-hans.react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code) 执行，因为 React 可能会多次渲染组件。在大多数情况下，你会使用 [事件处理函数](https://zh-hans.react.dev/learn/responding-to-events) 来处理副作用。使用事件处理函数明确地告诉 React 这段代码不需要在渲染过程中执行，从而保持渲染的纯粹。如果你已经尝试了所有可能的方法，并且只是作为最后的解决办法，你也可以使用 `useEffect` 来处理副作用。

### When is it okay to have mutation? 

#### Local mutation 

One common example of a side effect is mutation, which in JavaScript refers to changing the value of a non-[primitive](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) value. In general, while mutation is not idiomatic in React, *local* mutation is absolutely fine:

> 一个常见的副作用的例子是突变（mutation），在 JavaScript 中指的是改变一个非 原始值的值。通常来说，在 React 中 mutation 操作并不符合最佳实践，但是进行局部 mutation 是完全可以接受的：

```jsx
function FriendList({ friends }) {
  const items = []; // ✅ Good: locally created
  for (let i = 0; i < friends.length; i++) {
    const friend = friends[i];
    items.push(
      <Friend key={friend.id} friend={friend} />
    ); // ✅ Good: local mutation is okay
  }

  return <section>{items}</section>;
}
```

There is no need to contort your code to avoid local mutation. [`Array.map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) could also be used here for brevity, but there is nothing wrong with creating a local array and then pushing items into it [during render](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code).

> 你没有必要为了回避局部 mutation 而刻意编写复杂的代码。虽然为了简洁，这里可以使用 [`Array.map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)，但创建一个局部数组，然后 [在渲染时](https://zh-hans.react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code) 向其中添加数组项也是完全可以的。

Even though it looks like we are mutating `items`, the key point to note is that this code only does so *locally* – the mutation isn’t “remembered” when the component is rendered again. In other words, `items` only stays around as long as the component does. Because `items` is always *recreated* every time `<FriendList />` is rendered, the component will always return the same result.

> 尽管看起来我们正在修改 `items`，但关键的一点是这种 mutation 是局部的，当组件再次渲染时，这种 mutation 不会被“记住”。换句话说，`items` 只在组件存在期间有效。因为每次渲染 `<FriendList />` 时，`items` 都会被重新创建，所以组件总能返回相同的结果。

On the other hand, if `items` was created outside of the component, it holds on to its previous values and remembers changes:

> 另一方面，如果 `items` 是在组件外部创建的，那么它会保留其之前的值，并记住所做的更改：

```jsx
const items = []; // 🔴 Bad: created outside of the component
function FriendList({ friends }) {
  for (let i = 0; i < friends.length; i++) {
    const friend = friends[i];
    items.push(
      <Friend key={friend.id} friend={friend} />
    ); // 🔴 Bad: mutates a value created outside of render
  }

  return <section>{items}</section>;
}
```

When `<FriendList />` runs again, we will continue appending `friends` to `items` every time that component is run, leading to multiple duplicated results. This version of `<FriendList />` has observable side effects [during render](https://react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code) and **breaks the rule**.

> 每当 `<FriendList />` 组件再次运行时，我们都会持续地向 `items` 数组追加 `friends`，这会产生多个重复的结果。`<FriendList />` [在渲染中](https://zh-hans.react.dev/reference/rules/components-and-hooks-must-be-pure#how-does-react-run-your-code) 具有了可观察的副作用，所以违反了规则。

#### Lazy initialization 

Lazy initialization is also fine despite not being fully “pure”:

> 即使不是完全“纯粹”的，延迟初始化也是完全可以接受的

```jsx
function ExpenseForm() {
  SuperCalculator.initializeIfNotReady(); // ✅ Good: if it doesn't affect other components
  // Continue rendering...
}
```

#### Changing the DOM 

Side effects that are directly visible to the user are not allowed in the render logic of React components. In other words, merely calling a component function shouldn’t by itself produce a change on the screen.

> 在 React 组件的渲染逻辑中不允许有直接对用户可见的副作用。换句话说，仅仅调用一个组件函数本身不应当在屏幕上产生变化。

```jsx
function ProductDetailPage({ product }) {
  document.title = product.title; // 🔴 Bad: Changes the DOM
}
```

One way to achieve the desired result of updating `document.title` outside of render is to [synchronize the component with `document`](https://react.dev/learn/synchronizing-with-effects).

> 在渲染之外更新 `document.title` 的一个方法是 [将组件与 `document` 进行同步](https://zh-hans.react.dev/learn/synchronizing-with-effects)。

As long as calling a component multiple times is safe and doesn’t affect the rendering of other components, React doesn’t care if it’s 100% pure in the strict functional programming sense of the word. It is more important that [components must be idempotent](https://react.dev/reference/rules/components-and-hooks-must-be-pure).

> 只要多次调用组件是安全的，并且不会影响其他组件的渲染，React 就不会在意组件是否在严格的函数式编程意义上是百分之百纯粹的。更重要的是，组件必须是幂等的。

## Props and state are immutable 

A component’s props and state are immutable [snapshots](https://react.dev/learn/state-as-a-snapshot). Never mutate them directly. Instead, pass new props down, and use the setter function from `useState`.

> 组件的 props 和 state 是不可变的快照。永远不要直接修改它们。相反，你应该向下传递新的属性，以及使用 useState 提供的 setter 函数。

You can think of the props and state values as snapshots that are updated after rendering. For this reason, you don’t modify the props or state variables directly: instead you pass new props, or use the setter function provided to you to tell React that state needs to update the next time the component is rendered.

> 你可以将 props 和 state 视为在渲染后更新的快照。因此，你不会直接修改 props 或 state，相反，你传递新的 props，或者使用提供给你的 setter 函数来告诉 React，state 需要在下一次组件渲染时更新。

### Don’t mutate Props 

Props are immutable because if you mutate them, the application will produce inconsistent output, which can be hard to debug as it may or may not work depending on the circumstances.

> props 是不可变的，因为如果你改变了它们，应用程序可能会产生不一致的结果，这会让调试变得困难，因为程序可能会在某些情况下工作，而在另一些情况下不工作。

```jsx
function Post({ item }) {
  item.url = new Url(item.url, base); // 🔴 Bad: never mutate props directly
  return <Link url={item.url}>{item.title}</Link>;
}

function Post({ item }) {
  const url = new Url(item.url, base); // ✅ Good: make a copy instead
  return <Link url={url}>{item.title}</Link>;
}
```

### Don’t mutate State 

`useState` returns the state variable and a setter to update that state.

> `useState` 返回一个 state 和一个用于更新该状态的 setter。

```
const [stateVariable, setter] = useState(0);
```

Rather than updating the state variable in-place, we need to update it using the setter function that is returned by `useState`. Changing values on the state variable doesn’t cause the component to update, leaving your users with an outdated UI. Using the setter function informs React that the state has changed, and that we need to queue a re-render to update the UI.

> 我们不应该直接在 state 变量上进行更新，而应该使用 `useState` 返回的 setter 函数来进行更新。如果在 state 变量上直接修改值，并不会导致组件界面更新，这样用户界面就会显示过时的信息。通过使用 setter 函数，我们告诉 React 状态已经发生了变化，需要进行重新渲染，以便更新用户界面。

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    count = count + 1; // 🔴 Bad: never mutate state directly
  }

  return (
    <button onClick={handleClick}>
      You pressed me {count} times
    </button>
  );
}

function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1); // ✅ Good: use the setter function returned by useState
  }

  return (
    <button onClick={handleClick}>
      You pressed me {count} times
    </button>
  );
}
```

## Return values and arguments to Hooks are immutable 

Once values are passed to a hook, you should not modify them. Like props in JSX, values become immutable when passed to a hook.

> 一旦值被传递给 Hook，就不应该再对它们进行修改。就像在 JSX 中的 props 一样，当值被传递给 Hook 时，它们就应该是不可变的了。

```jsx
function useIconStyle(icon) {
  const theme = useContext(ThemeContext);
  if (icon.enabled) {
    icon.className = computeStyle(icon, theme); // 🔴 Bad: never mutate hook arguments directly
  }
  return icon;
}

function useIconStyle(icon) {
  const theme = useContext(ThemeContext);
  const newIcon = { ...icon }; // ✅ Good: make a copy instead
  if (icon.enabled) {
    newIcon.className = computeStyle(icon, theme);
  }
  return newIcon;
}
```

One important principle in React is *local reasoning*: the ability to understand what a component or hook does by looking at its code in isolation. Hooks should be treated like “black boxes” when they are called. For example, a custom hook might have used its arguments as dependencies to memoize values inside it:

> 在 React 中有一个重要的原则叫做局部推理，即通过单独查看组件或 Hook 的代码，就能理解它的作用。当调用 Hook 时，应该把它们当作“黑盒子”。例如，自定义 Hook 可能使用其参数作为依赖项，在内部缓存值：

```jsx
function useIconStyle(icon) {
  const theme = useContext(ThemeContext);

  return useMemo(() => {
    const newIcon = { ...icon };
    if (icon.enabled) {
      newIcon.className = computeStyle(icon, theme);
    }
    return newIcon;
  }, [icon, theme]);
}
```

If you were to mutate the Hook’s arguments, the custom hook’s memoization will become incorrect,  so it’s important to avoid doing that.

> 如果你改变了 Hook 的参数，那么自定义 Hook 的缓存（memoization）就会变得不正确，因此避免这样做非常重要。

```jsx
style = useIconStyle(icon);         // `style` is memoized based on `icon`
icon.enabled = false;               // Bad: 🔴 never mutate hook arguments directly
style = useIconStyle(icon);         // previously memoized result is returned

style = useIconStyle(icon);         // `style` is memoized based on `icon`
icon = { ...icon, enabled: false }; // Good: ✅ make a copy instead
style = useIconStyle(icon);         // new value of `style` is calculated
```

Similarly, it’s important to not modify the return values of Hooks, as they may have been memoized.

> 同样重要的是不要修改 Hook 的返回值，因为这些值可能已经被缓存了。

## Values are immutable after being passed to JSX 

Don’t mutate values after they’ve been used in JSX. Move the mutation to before the JSX is created.

> 不要在 JSX 使用过值之后改变它们。应该在创建 JSX 之前完成值的更改。

When you use JSX in an expression, React may eagerly evaluate the JSX before the component finishes rendering. This means that mutating values after they’ve been passed to JSX can lead to outdated UIs, as React won’t know to update the component’s output.

> 当你在表达式中使用 JSX 时，React 可能会在组件完成渲染之前就急于计算 JSX。这意味着，如果在将值传递给 JSX 之后对它们进行更改，可能会导致 UI 过时，因为 React 不会知道需要更新组件的输出。

```jsx
function Page({ colour }) {
  const styles = { colour, size: "large" };
  const header = <Header styles={styles} />;
  styles.size = "small"; // 🔴 Bad: styles was already used in the JSX above
  const footer = <Footer styles={styles} />;

  return (
    <>
      {header}
      <Content />
      {footer}
    </>
  );
}

function Page({ colour }) {
  const headerStyles = { colour, size: "large" };
  const header = <Header styles={headerStyles} />;
  const footerStyles = { colour, size: "small" }; // ✅ Good: we created a new value
  const footer = <Footer styles={footerStyles} />;

  return (
    <>
      {header}
      <Content />
      {footer}
    </>
  );
}
```
