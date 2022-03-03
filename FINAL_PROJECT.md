# FINAL PROJECT

## hosting p5.js scripts on github pages
* https://www.youtube.com/watch?v=ZneWjyn18e8

## node.js
* https://nodejs.org/en/
* https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-up-node-on-ec2-instance.html
* https://nodejs.org/en/docs/guides/getting-started-guide/

## socket.io

* https://gabrieltanner.org/blog/realtime-drawing-app
* https://editor.p5js.org/lisajamhoury/sketches/nMXZgHOXH


## Examples
* WebRTC: https://editor.p5js.org/lisajamhoury/sketches/nMXZgHOXH
* Games:
  * https://editor.p5js.org/annawasson/sketches/BQFIoo6s2
  * https://editor.p5js.org/ARatherLongUsername/sketches/ryo2_4GS7

```js
let handleRequest = function (request, response) {
  response.writeHead(200, {'Content-Type': 'text/plain'});
  response.end('Hello World\n');
};

const http = require('http');
let server = http.createServer(handleRequest);
server.listen(3000);
console.log('listening on 3000')
```

* `npm install socket.io`

```js
let handleRequest = function (request, response) {
  response.writeHead(200, {'Content-Type': 'text/plain'});
response.end('Hello World\n');
};

let http = require('http');
let server = http.createServer(handleRequest);
let io = require('socket.io')(server);

server.listen(3000, () => {
    console.log('Server started on port 3000');
})
```

```html
<head>
  <script language="javascript" type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/p5.js/0.2.8/p5.min.js"></script>
  <script language="javascript" type="text/javascript" src="sketch.js"></script>
</head>

<body>
</body>
```

```js
var http = require('http');
var path = require('path');
var fs = require('fs');

var server = http.createServer(handleRequest);
server.listen(3000);

console.log('Server started on port 3000');

function handleRequest(req, res) {

  var pathname = req.url;
  
  if (pathname == '/') {
    pathname = '/index.html';
  }

  var ext = path.extname(pathname);


  var typeExt = {
    '.html': 'text/html',
    '.js':   'text/javascript',
    '.css':  'text/css'
  };


  var contentType = typeExt[ext] || 'text/plain';

  fs.readFile(__dirname + pathname,

    function (err, data) {

      if (err) {
        res.writeHead(500);
        return res.end('Error loading ' + pathname);
      }

      res.writeHead(200,{ 'Content-Type': contentType });
      res.end(data);
    }
  );
}
```