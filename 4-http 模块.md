# http 模块

1. #### 什么是 http 模块？

   <font color="red">http 模块</font>是 Node.js 官方提供的、用来创建 web 服务器的模块。通过 http 模块提供的 <font color="blue">http.createServer()</font> 方法，就能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。

   

   如果要希望使用 http 模块创建 Web 服务器，则需要先导入它：

   ~~~js
   const http = require('http')
   ~~~

   

2. #### 创建基本的 web 服务器

   + ##### 导入 http 模块

     ~~~js
     const http = require('http')
     ~~~

     

   + ##### 创建 web 服务器实例

     ~~~js
     const server = http.createServer()
     ~~~

     

   + ##### 为服务器实例绑定 <font color="red">request 事件</font>，<font color="blue">监听客户端的请求</font>

     ~~~js
     server.on('request', (req, res) => {
       console.log('Someone visit our web server.');
     })
     ~~~

     

   + ##### 启动服务器

     ~~~js
     server.listen(8080, () => {
       console.log('server running at http://127.0.0.1:8080');
     })
     ~~~

     

3. #### <font color="red">req</font> 请求对象

   只要服务器接收到了客户端的请求，就会调用通过 <font color="red">server.on()</font> 为服务器绑定的 <font color="blue">request 事件处理函数</font>。如果想在事件处理函数中，<font color="orange">访问与客户端相关的**数据**或**属性**</font>，可以使用如下的方式：

   ~~~js
   // req 是请求对象，包含了客户端相关的数据和属性
   server.on('request', (req) => {
     // req.url 是客户端请求的 URL 地址
     const url = req.url
   
     // req.method 是客户端请求的 method 类型
     const method = req.method
     
     const str = `Your request url is ${url}, and request method is ${method}`
     console.log(str);
   })
   ~~~

   <img src="/Users/hsiwozer/Library/Application Support/typora-user-images/image-20220916232623370.png" alt="image-20220916232623370" style="zoom:50%;" />

   

4. #### <font color="red">res</font> 响应对象

   在服务器的 request 事件处理函数中，如果想<font color="orange">访问与服务器相关的**数据**或**属性**</font>，可以使用如下方式：

   ~~~js
   // res 是响应对象，包含了与服务器相关的数据和属性
   server.on('request', (req, res) => {
     const url = req.url
     const method = req.method
     // 要发送到客户端的字符串
     const str = `Your request url is ${url}, and request method is ${method}`
   
     // res.end() 方法的作用：向客户端发送指定的内容，并结束这次请求的处理过程
     res.end(str)
   })
   ~~~

   <img src="/Users/hsiwozer/Library/Application Support/typora-user-images/image-20220916232817656.png" alt="image-20220916232817656" style="zoom:50%;" />

   

5. #### 解决<font color="red">中文乱码</font>问题

   <img src="/Users/hsiwozer/Library/Application Support/typora-user-images/image-20220916233251418.png" alt="image-20220916233251418" style="zoom:50%;" />

   ~~~js
   const http = require('http')
   const server = http.createServer()
   
   server.on('request', (req, res) => {
     const str = `你请求的 URL 地址是 ${req.url}, 请求的 method 类型是 ${req.method}`
   
     // 设置响应头以解决中文乱码问题
     res.setHeader('Content-Type', 'text/html; charset=utf-8')
   
     res.end(str)
   })
   
   server.listen(8080, () => {
     console.log('server running at http://127.0.0.1:8080');
   })
   ~~~

   <img src="/Users/hsiwozer/Library/Application Support/typora-user-images/image-20220916233448638.png" alt="image-20220916233448638" style="zoom:50%;" />

   

6. #### 根据不同的 url 响应不同的 html 内容

   + 获取请求的 url 地址
   + 设置默认的响应内容为 404 Not Found
   + 判断用户请求的是否为 / 或 /index.html 首页
   + 判断用户请求的是否为 /about.html 关于页面
   + 设置 Content-Type 响应头，防止中文乱码
   + 使用 res.end() 把内容响应给客户端

   ~~~js
   const http = require('http')
   const server = http.createServer()
   
   server.on('request', (req, res) => {
     const url = req.url
     let content = '<h1>404 Not Found</h1>'
     if (url === '/' || url === '/index.html') {
       content = '<h1>首页</h1>'
     } else if (url === '/about.html') {
       content = '<h1>关于</h1>'
     }
     res.setHeader('Content-Type', 'text/html; charset=utf-8')
     res.end(content)
   })
   
   server.listen(8080, () => {
     console.log('server running at http://127.0.0.1:8080');
   })
   ~~~