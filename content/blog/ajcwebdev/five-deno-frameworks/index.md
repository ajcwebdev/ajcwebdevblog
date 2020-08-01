---
title: five deno frameworks
date: "2020-07-22"
description: oak, servest, drash, pogo, abc
---

When building a web server with NodeJS, most developers use a framework such as Express, Koa, or (the newly resurrected) Hapi. There are many frameworks currently being built for Deno that take inspiration from Node frameworks and frameworks from other languages like Flask or Sinatra.

I'm going to do a series of posts building a basic REST API with different Deno frameworks. To select the frameworks I consulted Craig Morten's excellent overview [What Is The Best Deno Web Framework?](https://dev.to/craigmorten/what-is-the-best-deno-web-framework-2k69) I picked the five most popular frameworks for the sake of time and my own sanity.

Popularity is not always the best metric, but when it comes to open source projects it signals a greater level of developers are working with a framework which means more bug fixes, more feature requests, and more resources online to learn that framework. The five frameworks will be:

1. [Oak](https://github.com/oakserver/oak)
2. [Servest](https://github.com/keroxp/servest)
3. [Drash](https://github.com/drashland/deno-drash)
4. [Pogo](https://github.com/sholladay/pogo)
5. [abc](https://github.com/zhmushan/abc)

Craig's own framework, [Opine](https://github.com/asos-craigmorten/opine), would be next on the list, and I'll probably do a bonus post about it at the end of the series as a thanks for all the excellent Deno content he's been writing. Make sure to follow him if you want to stay current with Denoland.

## Deno HTTP

Before diving into the frameworks it's useful to see the underlying server code they are building upon. The [Deno Standard Library](https://deno.land/std) has an [http](https://deno.land/std/http) module with a basic hello world application. First make sure you have [Deno installed](https://deno.land/#installation).

Save the following code in a file called `hello.ts`:

```javascript
import { serve } from "https://deno.land/std/http/server.ts";
const server = serve({ port: 8000 });
console.log("http://localhost:8000/");
for await (const req of server) {
  req.respond({ body: "Hello World\n" });
}
```

Open your terminal in the directory containing `hello.ts` and enter the following command:

![01-deno-run](https://dev-to-uploads.s3.amazonaws.com/i/2fgze5mvdyj4vb5e2b51.jpg)

Open your browser to `localhost:8000`

![02-deno-hello-world](https://dev-to-uploads.s3.amazonaws.com/i/xkg2si9pcysed5z5tc32.jpg)

We can contrast this with a similar example in Node. Save the following code in a file called `hello.js`:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(3000, '127.0.0.1', () => {
  console.log(`Server running at http://127.0.0.1:3000/`);
});
```
Open your terminal in the directory containing `hello.js` and enter the following command:

![03-node-run](https://dev-to-uploads.s3.amazonaws.com/i/22wtzt5dc6u9eo4ff95m.jpg)

Open your browser to `http://127.0.0.1:3000`

![04-node-hello-world](https://dev-to-uploads.s3.amazonaws.com/i/grpylovf1ijrjlk7ohl8.jpg)