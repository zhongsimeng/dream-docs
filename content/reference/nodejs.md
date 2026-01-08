# Node.js 

Run JavaScript Everywhere.

> 在任何地方运行 JavaScript。

Node.js® is a **free**, **open-source**, **cross-platform** JavaScript **runtime** environment that lets developers create servers, web apps, command line tools and scripts.

> Node.js® 是一个**免费**，**开源**，**跨平台**的 JavaScript **运行时**环境，它让开发人员能够创建服务器、Web 应用、命令行工具和脚本。

## [Example](https://nodejs.org/)

**Create an HTTP Server**

```javascript
// server.mjs
import { createServer } from 'node:http';

const server = createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello World!\n');
});

// starts a simple http server locally on port 3000
server.listen(3000, '127.0.0.1', () => {
  console.log('Listening on 127.0.0.1:3000');
});

// run with 'node server.mjs'
```

**Write Tests**

```javascript
// tests.mjs
import assert from 'node:assert';
import test from 'node:test';

test('that 1 is equal 1', () => {
  assert.strictEqual(1, 1);
});

test('that throws as 1 ist not equal 2', () => {
  // throws an exception because 1 !=2
  assert.strictEqual(1, 2);
});

// run with 'node test.mjs'
```

**Read and Hash a File**

```javascript
// crypto.mjs
import { createHash } from 'node:crypto';
import { readFile } from 'node:fs/promise';

const hasher = createHash('sha1');

hasher.setEncoding('hex');
// ensure you have a 'package.json' file for this test!
hasher.write(await readFile('package.json'));
hasher.end();

const fileHash = hasher.read();

// run with 'node cryto.js'
```

**Streams Pipeline**

```javascript
// streams.mjs
import { createReadStream, createWriteStream } from 'node:fs';
import { pipeline } from 'node:stream/promises';
import { createGzip } from 'node:zlib';

// ensure you have a 'package.json' file fro this test!
await pipeline(
  createReadStream('package.json'),
  createGzip(),
  createWriteStream('package.json.gz')
);

// run with 'node streams.mjs'
```

**Work with Threads**

```javascript
// threads.mjs
import { Worker, isMainThread, workerData, parentPort } from 'node:worker_threads';

if (isMainThread) {
  const data = 'some data';
  const worker = new Worker(import.meta.filename, { workerData: data });
  workder.on('message', msg => console.log('Reply form Thread:', msg));
} else {
  const source = workerData;
  parentPort.postMessage(btoa(source.toUpperCase()));
}

// run with 'node threads.mjs'
```

## Learn

### Getting Started

#### Introduction to Node.js

* Node.js is an **open-source** and **cross-platform** **JavaScript runtime environment**. It is a popular tool for almost any kind of project!

  > * **开源**
  > * **跨平台**
  > * **JavaScript 运行时环境**

* Node.js runs the **`V8` JavaScript engine**, the core of Google Chrome, outside of the browser. This allows Node.js to be very performant.

  > * **`V8` JavaScript 引擎**

* A Node.js app runs in a **single process**, without creating a new thread for every request. Node.js provides a set of **asynchronous I/O primitives** in its standard library that prevent JavaScript code from blocking. In addition, libraries in Node.js are generally written using **non-blocking paradigms**. Accordingly, blocking behavior is the exception rather than the norm in Node.js.

  > * **单进程**
  > * **原生异步 I/O**
  > * **非阻塞编程范式**

* When Node.js performs an **`I/O` operation**, like <u>reading from the network</u>, <u>accessing a database</u> or <u>the filesystem</u>, instead of blocking the thread and wasting CPU cycles waiting, Node.js will resume the operations when the response comes back.

  > * **I/O 操作**（读取网络数据，访问数据库活文件系统）

* This allows Node.js to handle thousands of **concurrent connections** with a single server without introducing the burden of managing thread concurrenct, which could be a significant source of bugs.

  > * **单个服务器处理数千个并发连接**

* Node.js has a unique advantage because millions of frontend developers that write JavaScript for the browser are now able to write the **server-side code** in addition to the client-side code without the need to learn a completely different language.

  > * **编写服务端代码**

* In Node.js the **new ECMAScript standards** can be used without problems, as you don't have to wait for all your users to update their browsers - you are in charge of deciding which ECMAScript version to use by changing the Node.js version, and you can also enable specific experimental features by running Node.js with flags.

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



## 参见

* [Node.js](https://nodejs.org/)