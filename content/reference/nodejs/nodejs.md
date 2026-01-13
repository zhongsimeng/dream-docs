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

## 参见

* [Node.js](https://nodejs.org/)