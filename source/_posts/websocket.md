title: Websocket协议调试
tags:
    - websocket nodejs
---
>使用websocket协议 + nodeJS实现即时通讯

### 1.websocket + nodejS
* 1)到websocket目录下安装依赖:npm install --save-dev nodejs-websocket
* 2)运行 node websocketServer.js
* 3)同时打开sendMessage.hrml 和 getMessage.html, 分别发送消息和接收消息

### 2.socket.io + nodeJS
* 1)到socket.io目录下安装依赖项: npm install --save-dev express socket.io
* 2)运行 node socketIoServer.js
* 3)页面打开socket.io.html (在多个终端下打开,测试同步性)
* 4)socket.io.html注意引用socket.io模块中的socket.io.js

### 3.相关资料
* 1）[【websocket测试代码】](https://github.com/HoldCast/websocket)

* 2）[【websocket协议原理说明】](https://www.zhihu.com/question/20215561)
