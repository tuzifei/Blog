### webSocket

WebSocket的诞生本质上就是为了解决HTTP协议本身的单向性问题：请求必须由客户端向服务端发起，然后服务端进行响应。

WebSocket在用于双向传输、推送消息方面能够做到灵活、简便、高效，优点：

* 在建立WebSocket连接的url里就能携带身份验证参数，验证不通过可以直接拒绝，不用设置状态
* 直接通过wss加密，还能顺便保证证书的可信性
* 收发完整数据包，不用自己处理

### WebSocket的实现和应用

WebSocket是HTML5中的协议，支持持久连续,WebSocket是基于Http协议的，或者说借用了Http协议来完成一部分握手，在握手阶段与Http是相同的。