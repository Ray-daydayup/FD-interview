# HTTP的Cookie机制

## Cookie 的工作过程

两个字段：响应头字段 **Set-Cookie** 和请求头字段 **Cookie**。

## Cookie 的属性

1. 设置 Cookie 的生存周期:可以使用 **Expires** 和 **Max-Age** 两个属性来设置。“Expires”俗称“过期时间”，用的是绝对时间点，可以理解为“截止日期”（deadline）。“Max-Age”用的是相对时间，单位是秒，浏览器用收到报文的时间点再加上 Max-Age，就可以得到失效的绝对时间。
2. 设置 Cookie 的作用域: **Domain**”和“**Path**”指定了 Cookie 所属的域名和路径，浏览器在发送 Cookie 前会从 URI 中提取出 host 和 path 部分，对比 Cookie 的属性。如果不满足条件，就不会在请求头里发送 Cookie。
3. Cookie 的安全性:
   - 属性“**HttpOnly**”会告诉浏览器，此 Cookie 只能通过浏览器 HTTP 协议传输，禁止其他方式访问，浏览器的 JS 引擎就会禁用 document.cookie 等一切相关的 API，**跨站脚本攻击(XSS)**也就无从谈起了。
   - 另一个属性“**SameSite**”可以防范“**跨站请求伪造”（XSRF）**攻击，设置成“**SameSite=Strict**”可以严格限定 Cookie 不能随着跳转链接跨站发送，而“**SameSite=Lax**”则略宽松一点，允许 GET/HEAD 等安全方法，但禁止 POST 跨站发送。
   - “**Secure**”，表示这个 Cookie 仅能用 HTTPS 协议加密传输，明文的 HTTP 协议会禁止发送。但 Cookie 本身不是加密的，浏览器里还是以明文

## 小结

1. Cookie 是服务器委托浏览器存储的一些数据，让服务器有了“记忆能力”；
2. 响应报文使用 Set-Cookie 字段发送“key=value”形式的 Cookie 值；
3. 请求报文里用 Cookie 字段发送多个 Cookie 值；
4. 为了保护 Cookie，还要给它设置有效期、作用域等属性，常用的有 Max-Age、Expires、Domain、HttpOnly 等；
5. Cookie 最基本的用途是身份识别，实现有状态的会话事务。
