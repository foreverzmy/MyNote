# Scoket.io

## 认识 Socket.io

## 在 koa 中使用

```js
const Koa = require('koa');
const http = require('http');
const socket = require('socket.io');

const app = new Koa();
const server = http.Server(app.callback());
const io = socket(server);

app.get('/', function (req, res) {
  res.sendfile(__dirname + '/index.html');
});

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
```

## 发送和接受事件

Sockrt.io 允许你发送和接收自定义事件。除了 `connect` , `message` 和 `disconnect` 以外，你还可以发送自定义事件。


* 服务器端

```js
const io = require('socket.io')(9000);

io.on('connection', socket => {
  io.emit('this', { will: 'be received by everyone'});

  socket.on('private message', (from, msg) => {
    console.log('I received a private message by ', from, ' saying ', msg);
  });

  socket.on('disconnect', () => {
    io.sockets.emit('user disconnected');
  });
});
```

## 命名空间

如果你想要掌控来自一个特定应用的所有消息和事件，那么使用默认的 `/` 命名空间即可。如果你想要使用第三方的代码，或者编写能够和别人分享的代码，socket.io提供了一种方式来将一个socket放入命名空间中。

这将会在单个连接中带来 `multiplexing` (多路技术)的好处。你不需要用socket.io开启两个WebSocket连接，只需要使用一个即可。

* 服务端

```js
const io = require('socket.io').listen(80);
const chat = io
  .of('/chat')
  .on('connection', socket => {
    socket.emit('a message', {
        that: 'only'
      , '/chat': 'will get'
    });
    chat.emit('a message', {
        everyone: 'in'
      , '/chat': 'will get'
    });
  });

const news = io
  .of('/news')
  .on('connection', socket => {
    socket.emit('item', { news: 'item' });
  });
```

* 客户端

```html
<script>
  const chat = io.connect('http://localhost/chat')
  const news = io.connect('http://localhost/news');
  
  chat.on('connect', () => {
    chat.emit('hi!');
  });
  
  news.on('news', () => {
    news.emit('woot');
  });
</script>
```

## 发送不稳定的信息

有时某些特定信息可能会发生失败。假设你现在有一个应用，它会实时显示推特上关于贾斯汀比伯的推文。

如果有某个客户端没有准备好接收信息（因为网速太慢或者其他原因，或者因为他通过长轮询来进行连接并正好位于请求相应循环的中间），如果他没有接收到所有关于比伯的推文你的应用也不会受影响。

在这种情况下，你可能想要将这些信息作为不稳定信息来发送。


* 服务器端

```js
const io = require('socket.io').listen(80);

io.sockets.on('connection', socket => {
  var tweets = setInterval(() => {
    getBieberTweet( tweet => {
      socket.volatile.emit('bieber tweet', tweet);
    });
  }, 100);

  socket.on('disconnect', () => {
    clearInterval(tweets);
  });
});
```

## 确认消息

有时，你可能在客户端确认接收到信息时获得一个反馈。

为了做这件事，你只需要将一个函数作为 `.send` 或者 `.emit` 方法的最后一个参数传递。另外，当你使用 `.emit` 时，你需要自己进行确认，这意味着你还需要传递数据：

* 服务器端

```js
var io = require('socket.io').listen(80);

io.sockets.on('connection', function (socket) {
  socket.on('ferret', function (name, fn) {
    fn('woot');
  });
});
```

* 客户端

```html
<script>
  const socket = io(); // TIP: io() with no args does auto-discovery
  socket.on('connect', () => { // TIP: you can avoid listening on `connect` and listen on events directly too!
    socket.emit('ferret', 'tobi', data => {
      console.log(data); // data will be 'woot'
    });
  });
</script>
```

## 广播消息

为了广播消息，你只需要简单地在 `emit` 和 `send` 方法之前加上 `broadcast` 标示符。广播意味着给所有人除了自己发送一条消息。

```js
const io = require('socket.io').listen(80);

io.sockets.on('connection', socket => {
  socket.broadcast.emit('user connected');
});
```