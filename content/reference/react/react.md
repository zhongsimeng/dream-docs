# React

The library for **web** and **native** user interfaces

> 用于 **Web** 和**原生**用户界面的库

## Create user interfaces from components | 用组件创建用户界面

React lets you build user interfaces out of **individual pieces** called **components**. Create your own React components like `Thumbnail`, `LikeButton`, and `Video`. Then combine them into entire screens, pages, and apps.

> React 让你使用称为组件的独立单元来构建用户界面。创建你自己的 React 组件，像 `Thumbnail`、`LikeButton` 和 `Video` 。让后将它们组合成完整的屏幕、页面和应用程序。

```jsx
// Video.js
function Video({ video }) {
  return (
    <div>
      <Thumbnail video={video} />
      <a href={video.url}>
        <h3>{video.title}</h3>
        <p>{video.description}</p>
      </a>
      <LinkButton video={video} />
    </div>
  )
}
```

Whether you work on your own or with thousands of other developers, using React **feels the same**. It is designed to let you **seamlessly combine components** written by independent people, teams, and organizations.

> 无论你是独自工作还是与成千上万的其他开发者合作，使用 React 的体验都是一样的。它的设计宗旨就是让你能够无缝的组合由独立开发者、团队和组织编写的组件。

## Write components with code and markup | 使用代码和标记编写组件

**React components are JavaScript functions**. Want to show some content conditionally? Use an `if` statement. Displaying a list? Try array `map()`. **Learning React is learning programming**.

> **React 组件本质上是 JavaScript 函数**。想要根据条件显示某些内容？使用条件 `if` 语句。想要显示列表？试试数组 `map()`。**学习 React 就是学习编程**。

```jsx
// VideoList.js
function VideoList({ videos, emptyHeading }) {
  const count = videos.length;
  let heading = emptyHeading;
  if(count > 0) {
    const noun = count > 1 ? 'Videos' : 'Video';
    heading = count + ' ' + noun;
  }
  return (
    <section>
      <h2>{heading}</h2>
      {videos.map(video =>
        <Video key={video.id} video={video} />
      )}
    </section>
  );
}
```

**This markup syntax is called JSX**. It is a **JavaScript syntax extension** popularized by React. Putting JSX markup close to related rendering logic makes React components easy to create, maintain, and delete.

> **这种标记语法称为 JSX**，他是 React 推广的一种 **JavaScript 语法扩展**。将 JSX 标记与相关的渲染逻辑放在一起，可以简化 React 组件的创建，维护和删除。

## Add interactivity wherever you need it | 根据需要添加交互功能

React components receive data and return what should appear on the screen. You can pass them new data in response to an **interaction**, like when the user types into an input. React will then update the screen to match the new data.

> React 组件接受数据并返回屏幕上应显示的内容。您可以根据**交互事件**（例如用户在输入框内输入内容）像组件传递新数据。React 随后回更新屏幕以匹配新数据。

```jsx
// SearchableVideoList.js
import { useState } from 'react';

function SearchableVideoList({ videos }) {
  const [searchText, setSearchText] = useState('');
  const foundVideos = filterVideos(videos, searchText);
  return (
    <>
    	<SearchInput
        value={searchText}
        onChange={newText => setSearchText(newText)}
      />
    	<VideoList
        videos={foundVideos}
        emptyHeading={`No matches fro "${searchText}"`}
      />
    </>
  );
}
```

You don’t have to build your whole page in React. Add React to your existing HTML page, and **render interactive React components** anywhere on it.

> 你不必用 React 构建整个页面。只需将 React 添加到现有的 HTML 页面中，即可在页面的任何位置**渲染交互式 React 组件**。

**Add React to your page**

```js
// index.js
import { createRoot } from 'react-dom/client';

// Clear the existing HTML content
document.body.innerHTML = '<div id="app"></div>';

// Render your React component instead
const root = createRoot(document.getElementById('app'));
root.render(<h1>Hello, world</h1>);
```

## Go full-stack with a framework | 

**React is a library**. It lets you put components together, but it doesn’t prescribe how to do **routing** and **data fetching**. To build an entire app with React, we recommend a **full-stack React framework** like [Next.js](https://nextjs.org/) or [React Router](https://reactrouter.com/).

> **React 是一个库**。它允许你组装组件，但它并不规定如何进行**路由**和**数据获取**。要使用 React 构建完整的应用程序，我们建议使用像 Next.js 或 React Router 这样的**全栈 React 框架**。

```js
// confs/[slug].js
import { db } from './database.js'
import { Suspense } from 'react';

async function ConferencePage({ slug }) {
  const conf = await db.Confs.find({ slug })
  return (
    <ConferenceLayout conf={conf}>
    	<Suspense fallback={<TalksLoading />}>
        <Talk confId={conf.id} />
      </Suspense>
		</ConferenceLayout>
  );
}

async function Talks({ confId }) {
  const talks = await db.Talks.findAll({ confiId });
  const videos = talks.map(talk => talk.video);
  return <SearchableVideoList videos={videos} />;
}
```

**React is also an architecture**. Frameworks that implement it let you fetch data in **asynchronous components** that run on the **server** or even **during the build**. Read data from a **file** or a **database**, and pass it down to your interactive components.

> **React 也是一种架构**。实现它的框架允许你在**服务器端**，甚至是**构建阶段**使用**异步组件**来获取数据。你可以从文件或数据库读取数据，并将它传递给你的交互式组件。

**Get started with a framework**

Full-stack frameworks

> Full-stack frameworks do not require a server.
>
> * **Client-side rendering (CSR | 客户端渲染)**
>
>   generating HTML content using JavaScript in the browser.
>
> * **Single-page application (SPA | 单页面应用)**
>
>   loads only a single web document.
>
> * **Static site generator (SSG | 静态站点生成)**
>
>   a software used to generate *static* websites

* **Next.js (App Router)**

  ```
  npx create-next-app@latest
  ```

* **React Router (v7)**

  ```
  npx create-react-router@latest
  ```

* **Expo (for native apps)**

  ```
  npx create-expo-app@latest
  ```

## Use the best from every platform | 博采众长

People love web and native apps for different reasons. React lets you build both web apps and native apps **using the same skills**. It leans upon each platform’s **unique strengths** to let your interfaces feel just right on every platform.

> 人们喜欢 Web 应用和原生应用的原因各不相同。React 让你能够**使用相同的技能构建 Web 应用和原生应用**。它充分利用了**每个平台的独特优势**，确保你的界面在每个平台上都能完美呈现。

**Stay true to the web**

People expect web app pages to load fast. On the server, React lets you **start streaming HTML while you’re still fetching data**, progressively filling in the remaining content before any JavaScript code loads. On the client, React can **use standard web APIs to keep your UI responsive** even in the middle of rendering.

>人们期望网页应用页面加载速度快。在服务端，React 允许你**在获取数据的同时开始流式传输 HTML**，并在任何 JavaScript 代码加载之前逐步填充剩余内容。在客户端，React 可以**使用标准的 Web API 来保持 UI 的响应性**，即使在渲染过程中也是如此。

**Go truly native**

People expect native apps to look and feel like their platform. [React Native](https://reactnative.dev/) and [Expo](https://github.com/expo/expo) let you build apps in React for Android, iOS, and more. They look and feel native because their UIs *are* truly native. It’s not a web view—**your React components render real Android and iOS views provided by the platform.**

>人们希望原生应用的外观和体验与平台本身一致。React Native 和 Expo 让你能够使用 React 为 Android、iOS 等平台构建应用。它们的外观和体验与原生应用无异，因为它们的 UI 是真正原生的。它不是网页视图——**你的 React 组件渲染的是平台提供的真实 Android 和 iOS 视图。**

With React, you can be a web *and* a native developer. Your team can ship to many platforms without sacrificing the user experience. Your organization can bridge the platform silos, and form teams that own entire features end-to-end.

> 借助 React，您可以**同时胜任 Web 和原生开发**。您的团队可以面向多个平台发布产品，而无需牺牲用户体验。你可以打破平台壁垒，组建负责端到端完整功能的团队。

**Build for native platforms**

* [React Native](https://reactnative.dev/)

## Upgrade when the future is ready

React approaches changes with care. Every React commit is tested on business-critical surfaces with over a billion users. Over 100,000 React components at Meta help validate every migration strategy.

> React 对变更的处理非常谨慎。每一次 React 提交都会在拥有超过十亿用户的关键业务接口上进行测试。Meta 上超过 10 万个 React 组件有助于验证每一项迁移策略。

The React team is always researching how to improve React. Some research takes years to pay off. React has a high bar for taking a research idea into production. Only proven approaches become a part of React.

> React 团队一直在研究如何改进 React。有些研究需要数年才能见效。React 对将研究成果转化为生产环境有着很高的标准。只有经过验证的方法才能成为 React 的一部分。

## Join a community of millions

You’re not alone. Two million developers from all over the world visit the React docs every month. React is something that people and teams can agree on.

> 你并不孤单。每月有来自世界各地的两百万开发者访问 React 文档。React 是人们和团队都能达成共识的工具。

**This is why React is more than a library, an architecture, or even an ecosystem.** React is a community. It’s a place where you can ask for help, find opportunities, and meet new friends. You will meet both developers and designers, beginners and experts, researchers and artists, teachers and students. Our backgrounds may be very different, but React lets us all create user interfaces together.

> 这就是为什么 **React 不仅仅是一个库、一种架构，甚至一个生态系统。**React 是一个社区。在这里，你可以寻求帮助、寻找机会、结识新朋友。你会遇到开发者和设计师、初学者和专家、研究人员和艺术家、教师和学生。我们的背景可能千差万别，但 React 让我们能够共同创建用户界面。

## Welcome to the React community

* [Get Started](https://react.dev/learn)

## See Also

* [React](https://react.dev/)