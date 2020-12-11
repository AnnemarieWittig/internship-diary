 
|  | request | got | node-fetch | axios | superagent | needle | urllib | 
|--|--|--|--|--|--|--|--|  
| HTTP/2 support | n | ? | n | n | y** |  | HttpClient2 is a new instance for future. request method only return a promise, compatible with  `async/await`  and generator in co. |  |
| Browser support | n | n | y* | y | y 	|  |  |
| Electron support | n | y | n | n | n 	|  |  | 
| Promise API | y | y | y | y | y	| As you can see, you can use Needle with Promises or without them. When using Promises or when a callback is passed, the response's body will be buffered and written to `response.body`, and the callback will be fired when all of the data has been collected and processed (e.g. decompressed, decoded and/or parsed). | If you've installed  [bluebird](https://github.com/petkaantonov/bluebird),  [bluebird](https://github.com/petkaantonov/bluebird)  will be used.  `urllib`  does not install  [bluebird](https://github.com/petkaantonov/bluebird)  for you. Otherwise, if you're using a node that has native v8 Promises (v0.11.13+), then that will be used. Otherwise, this library will crash the process and exit, so you might as well install  [bluebird](https://github.com/petkaantonov/bluebird)  as a dependency! |
| Stream API 			| y | y | Node.js only | n | y 	| Streaming non-UTF-8 charset decoding, via  `iconv-lite` | allows stream functions in http.request |
| Request cancelation | n | y | y | y | y 	|  | Calling `.abort()` method of the request stream can cancel the request. |
| RFC compliant caching | n | y | n | n | n 	| Or use [RFC-1738](http://tools.ietf.org/html/rfc1738#section-3.1) basic auth URL syntax |  |
| Cookies (out-of-box) | y | y | n | n | n 	| has cookie function | (mentioned in introduction but not again) |  |  |
| Follows redirects | y | y | y | y | y 	| 301/302/303 redirect following, with fine-grained tuning; HTTP Proxy forwarding, optionally with authentication | Auto redirect handle |
| Retries on failure | n | y | n | n | y 	|  | _retry_ Number - a retry count, when get an error, it will request again until reach the retry count. |
| Progress events | n | y | n | Browser only | y 	|  |  |
| Handles gzip/deflate | y | y | y | y | y 	| Streaming gzip, deflate, and brotli decompression | Support `Accept-Encoding=gzip` by `options.gzip = true` |
| Advanced timeouts	| n | y | n | n | n 	| supports timeout | Connection timeout & Response timeout |
| Timings | y | y | n | n | n 	|  | -   _timing_  Boolean - Enable timing or not, default is  `false`. |
| Errors with metadata 	| n | y | n | y | n 	|  |  |
| JSON mode	| y | y | y | y | y 	| Automatic XML & JSON parsing | json supports |
| Custom defaults | y | y | n | y | n 	| Needle includes a `defaults()` method, that lets you override some of the defaults for all future requests | n |
| Composable | n | y | n | n | y 	|  |  |
| Hooks | n | y | n | y | n 	|  |  |
| Issues open | 222 | 21 | 47 | 466 	| 118 | 53 | 24 |
| Issues closed | 1.81K | 396 | 319 | 1.15k | 780 | 175 | 76 |
| Npm link |  | [npm](https://www.npmjs.com/package/got) | [node-fetch](https://www.npmjs.com/package/node-fetch) | [npm](https://www.npmjs.com/package/axios) | [npm](https://www.npmjs.com/package/superagent) | [npm](https://www.npmjs.com/package/needle) | [npm](https://www.npmjs.com/package/urllib) |
| Github link |  | [github](https://github.com/sindresorhus/got) | [github](https://github.com/node-fetch/node-fetch) | [github](https://github.com/axios/axios) | [github](https://github.com/visionmedia/superagent) | [github](https://github.com/tomas/needle) | [github](https://github.com/node-modules/urllib) |
| Comments |  | Currently strongly growing in users; specifically created due to request being bloated |  |  | The build of Superagent is currently failing. Also, it doesn’t support monitoring upload progress like  `XMLHttpRequest`. | HTTP/HTTPS requests, with the usual verbs you would expect; All of Node's native TLS options, such as 'rejectUnauthorized' (see below); Basic & Digest authentication with auto-detection; Multipart form-data (e.g. file uploads); Automatic XML & JSON parsing |
very immsersive documentation  |

Base table from [here](https://nodesource.com/blog/express-going-into-maintenance-mode).  
Empty fields are due to me not finding the according functions in the documentation but it is possiblte I oversaw.

| Package Name | Bundle Size | API Style | Summary | My Commwnts |
|--|--|--|--|--|
|[node-fetch](https://www.npmjs.com/package/node-fetch)|[0.4kb](https://bundlephobia.com/result?p=node-fetch@2.3.0)|promise / stream|A light-weight module that brings window.fetch to Node.js| Details above |
|[bent](https://github.com/mikeal/bent)|[1kb](https://bundlephobia.com/result?p=bent@6.1.0)|fp / promise / stream|Functional HTTP client w/ async/await| Very short documentation |
|[got](https://www.npmjs.com/package/got)|[48.4kb](https://bundlephobia.com/result?p=got@9.6.0)|promise / stream|Simplified HTTP requests| above |
|[make-fetch-happen](https://www.npmjs.com/package/make-fetch-happen)|[442kb](https://bundlephobia.com/result?p=make-fetch-happen@4.0.1)|promise / stream|make-fetch-happen is a Node.js library that wraps node-fetch-npm with additional features node-fetch doesn't intend to include, including HTTP Cache support, request pooling, proxies, retries, and more!| short documentation |
|[axios](https://www.npmjs.com/package/axios)|[11.9kb](https://bundlephobia.com/result?p=axios@0.18.0)|promise / stream|Promise based HTTP client for the browser and node.js| above |
|[unfetch](https://www.npmjs.com/package/unfetch)|[1kb](https://bundlephobia.com/result?p=unfetch@4.1.0)|promise / stream|Tiny 500b fetch "barely-polyfill"| small documentation |
|[superagent](https://www.npmjs.com/package/superagent)|[18kb](https://bundlephobia.com/result?p=superagent@5.0.2)|chaining / promise|Small progressive client-side HTTP request library, and Node.js module with the same API, sporting many high-level HTTP client features| above |
|[tiny-json-http](https://www.npmjs.com/package/tiny-json-http)|[22kb](https://bundlephobia.com/result?p=tiny-json-http@7.0.2)|promise|Minimalist HTTP client for GET and POSTing JSON payloads| small documentation |
|[needle](https://www.npmjs.com/package/needle)|[164kb](https://bundlephobia.com/result?p=needle@2.2.4)|chaining / promise|The leanest and most handsome HTTP client in the Nodelands| above |
|[urllib](https://www.npmjs.com/package/urllib)|[816kb](https://bundlephobia.com/result?p=urllib@2.33.2)|callback / promise|Help in opening URLs (mostly HTTP) in a complex world — basic and digest authentication, redirections, cookies and more.| above |

Table can be found [here](https://github.com/request/request/issues/3143).  I only transfered the libraries to the big table when the documentation was big enough.

In my research the most mentioned libraries were Got and Axios so I think those would be the best starting point.
