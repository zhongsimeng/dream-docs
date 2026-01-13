# Introduction to Node.js

Node.js is an **open-source** and **cross-platform** **JavaScript runtime environment**. It is a popular tool for almost any kind of project!

> * **开源**
> * **跨平台**
> * **JavaScript 运行时环境**

Node.js runs the **`V8` JavaScript engine**, the core of Google Chrome, outside of the browser. This allows Node.js to be very performant.

> * **`V8` JavaScript 引擎**

A Node.js app runs in a **single process**, without creating a new **thread/线程** for every request. Node.js provides a set of **asynchronous I/O primitives** in its standard library that prevent JavaScript code from blocking. In addition, libraries in Node.js are generally written using **non-blocking paradigms**. Accordingly, blocking behavior is the exception rather than the norm in Node.js.

> * **单进程**
> * **原生异步 I/O**
> * **非阻塞编程范式**

When Node.js performs an **`I/O` operation**, like <u>reading from the network</u>, <u>accessing a database</u> or <u>the filesystem</u>, instead of blocking the thread and wasting CPU cycles waiting, Node.js will resume the operations when the response comes back.

> * **I/O 操作**（读取网络数据，访问数据库活文件系统）

This allows Node.js to handle thousands of **concurrent connections** with a single server without introducing the burden of managing thread concurrenct, which could be a significant source of bugs.

> * **单个服务器处理数千个并发连接**

Node.js has a unique advantage because millions of frontend developers that write JavaScript for the browser are now able to write the **server-side code** in addition to the client-side code without the need to learn a completely different language.

> * **编写服务端代码**

In Node.js the **new ECMAScript standards** can be used without problems, as you don't have to wait for all your users to update their browsers - you are in charge of deciding which ECMAScript version to use by changing the Node.js version, and you can also enable specific experimental features by running Node.js with flags.

> * **使用新的 ECMAScript 标准**

**example**

```javascript
import { createServer } from 'node:http'; // http module

const hostname = '127.0.0.1';
const port = 3000;

/**
 * 创建一个新的 HTTP 服务器并返回它
 * 每当接收到新的请求时，都会调用 request event，并提供两个对象：
 * 请求/request（http.IncomingMessage 对象）：提供请求详情
 * 响应/response（http.ServerResponse 对象）：向调用者返回数据
*/
const server = createServer((req, res) => {
  res.statusCode = 200; // 表示响应成功
  res.sestHeader('Content-Type', 'text/plain');// 设置响应头
  res.end('Hello World'); // 关闭响应，添加内容作为参数
});

// 设置服务器监听指定的端口和主机名
server.listen(port, hostname, () => {
  // 当服务器准备就绪，回调函数将被调用
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

#### 