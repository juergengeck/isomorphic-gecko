# isomorphic-gecko

WebSocket client with support for Node.js, browsers, and Expo/React Native.

Isomorphic implementation of WebSocket.

It uses:
- [ws](https://github.com/websockets/ws) on Node
- [global.WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket) in browsers
- [expo.WebSocket](https://docs.expo.dev/versions/latest/sdk/websocket/) in Expo environments

## Limitations

Before using this module you should know that
[`ws`](https://github.com/websockets/ws/blob/master/doc/ws.md#class-websocket)
is not perfectly API compatible with
[WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket),
you should always test your code against all target environments (Node, browsers, and Expo).

Some major differences:

- no `Server` implementation in browsers or Expo
- no support for the constructor
  [`options`](https://github.com/websockets/ws/blob/master/doc/ws.md#new-websocketaddress-protocols-options)
  argument in browsers or Expo

## Installation

### Node.js
For Node.js environments, you need to install both this package and [ws](https://github.com/websockets/ws):

```
> npm i isomorphic-gecko ws
```

### Browsers and Expo
For browser or Expo environments, you only need to install this package:

```
> npm i isomorphic-gecko
```

## Usage

```js
const WebSocket = require('isomorphic-gecko');

const ws = new WebSocket('wss://websocket-echo.com/');

ws.onopen = function open() {
  console.log('connected');
  ws.send(Date.now());
};

ws.onclose = function close() {
  console.log('disconnected');
};

ws.onmessage = function incoming(data) {
  console.log(`Roundtrip time: ${Date.now() - data.data} ms`);

  setTimeout(function timeout() {
    ws.send(Date.now());
  }, 500);
};
```

### Expo Usage

When using this package in an Expo environment, it will automatically detect and use Expo's WebSocket implementation. No additional configuration is needed.

## License

[MIT](LICENSE)
