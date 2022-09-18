# Express

1. #### 什么是 Express？

   Express 是基于 [Node.js](https://nodejs.org/en/) 平台，快速、开放、极简的 Web 开发框架。

   [官网地址：https://www.expressjs.com.cn](https://www.expressjs.com.cn)

   

2. #### Express 的基本使用

   + ##### 安装

     ~~~bash
     npm i express
     ~~~

     

   + ##### 创建基本的 Web 服务器

     ~~~js
     // 1. 导入 express
     const express = require('express')
     // 2. 创建 web 服务器
     const app = express()
     // 3. 启动 web 服务器
     app.listen(80, () => {
       console.log('express server running at http://127.0.0.1');
     })
     ~~~

     

   + ##### 监听 <font color="red">GET</font> 请求

     通过 <font color="red">**app.get()**</font> 方法，可以监听客户端的 GET 请求。

     ~~~js
     // 参数1: 客户端请求的 URL 地址
     // 参数2: 请求对应的处理函数
     // req: 请求对象（包含了与请求相关的属性与方法）
     // res: 响应对象（包含了与响应相关的属性与方法）
     app.get('请求URL', (req, res) => {})
     ~~~

     

   + ##### 监听 <font color="red">POST</font> 请求

     通过 <font color="red">**app.post()**</font> 方法，可以监听客户端的 POST 请求。

     ~~~js
     // 参数1: 客户端请求的 URL 地址
     // 参数2: 请求对应的处理函数
     // req: 请求对象（包含了与请求相关的属性与方法）
     // res: 响应对象（包含了与响应相关的属性与方法）
     app.post('请求URL', (req, res) => {})
     ~~~

     

   + ##### 把内容<font color="red">响应</font>给客户端

     ~~~js
     app.get('/user', (req, res) => {
       // 向客户端发送 JSON 对象
       res.send({ name: 'zs', age: 20, gender: '男' })
     })
     
     app.post('/user', (req, res) => {
       // 向客户端发送文本内容
       res.send('请求成功')
     })
     ~~~

     

   + ##### 获取 URL 中携带的<font color="red">查询参数</font>

     通过 <font color="red">**req.query**</font> 对象，可以访问到客户端通过<font color="red">查询字符串</font>的形式，发送到服务器的参数。

     ~~~js
     app.get('/', (req, res) => {
       // req.query 默认是一个空对象
       // 客户端使用 ?name=zs&age=20 这种查询字符串形式，发送到服务器的参数，
       // 可以通过 req.query 对象访问到
       // req.query.name req.query.age
       console.log(req.query)
     })
     ~~~

     

   + ##### 获取 URL 中的<font color="red">动态参数</font>

     通过 <font color="red">**req.params**</font> 对象，可以访问到 URL 中，通过 **:** 匹配到的动态参数。

     ~~~js
     app.get('/user/:id', (req, res) => {
       // req.params 默认是一个空对象
       // 里面存放着通过 : 动态匹配到的参数值
       console.log(req.params)
     })
     ~~~

     

3. #### 托管静态资源

   + ##### <font color="red">express.static()</font>

     express 提供了一个非常好用的函数，叫做 express.static()，通过它，我们可以非常方便地创建一个静态资源服务器，例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：

     ~~~js
     // 访问形式：http://localhost:8080/index.html
     app.use(express.static('public'))
     ~~~

     ⚠️ 注意：Express 在指定的静态目录中查找文件，并对外提供资源的访问路径。因此，<u>存放静态文件的目录名不会出现在 URL 中</u>。

     

   + ##### 托管多个静态资源

     只需<u>多次调用</u> express.static() 函数即可。

     ~~~js
     app.use(express.static('public'))
     app.use(express.static('files'))
     ~~~

     

   + ##### 挂载<font color="red">路径前缀</font>

     如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下方式：

     ~~~js
     // 访问形式：http://localhost:8080/public/index.html
     app.use('/public', express.static('public'))
     ~~~

     

4. #### nodemon

   ##### ⭐️ nodemon 工具能够监听项目文件的变动，自动帮助我们重启项目，极大方便了开发和测试。

   + ##### 安装

     ~~~bash
     // 安装为全局工具
     npm i -g nodemon
     ~~~

     

   + ##### 使用

     将原先的启动命令 `node app.js` 替换为 `nodemon app.js` 即可。

     

5. #### Express 路由

   + ##### 什么是路由？

     路由即<font color="red">映射关系</font>。

   + ##### Express 中的路由

     在Express 中，路由指的是客户端的请求与服务器处理函数之间的映射关系。

     Express 中的路由分 3 部分组成，分别是<font color="red">请求的类型</font>、<font color="red">请求的 URL 地址</font>、<font color="red">处理函数</font>，格式如下：

     ~~~js
     app.METHOD(PATH, HANDLER)
     ~~~

     

   + ##### 路由的使用

     + ###### 最简单的用法

       把路由挂载到 app 上

       ~~~js
       const express = require('express')
       const app = express()
       
       app.get('/', (req, res) => {
         res.send('hello world.')
       })
       
       app.post('/', (req, res) => {
         res.send('Post Request.')
       })
       
       app.listen(8080, () => {
         console.log('http://localhost:8080');
       })
       ~~~

       

     + ##### <font color="red">模块化路由</font>

       ~~~js
       /** 路由模块 router.js 的创建 */
       // 1. 导入 express
       const express = require('express')
       // 2. 创建路由对象
       const router = express.Router()
       
       // 3. 挂载具体的路由
       router.get('/user/list', (req, res) => {
         res.send('Get user list.')
       })
       
       router.post('/user/add', (req, res) => {
         res.send('Add new user.')
       })
       
       // 4. 向外导出路由对象
       module.exports = router
       
       /** 注册和使用路由模块 */
       const express = require('express')
       const app = express()
       
       // 1. 导入路由模块
       const router = require('./03.router')
       
       // 2. 注册路由模块
       app.use(router)
       
       app.listen(8080, () => {
         console.log('http://localhost:8080');
       })
       ~~~

       

     + ##### 为路由模块<font color="red">添加前缀</font>

       ~~~js
       // 注册路由模块时添加统一前缀，访问形式为:
       // http://localhost:8080/api/user/add
       // http://localhost:8080/api/user/list
       app.use('/api', router)
       ~~~

       

6. #### Express 中间件

   + ##### 定义中间件

     ~~~js
     const express = require('express')
     const app = express()
     
     // 定义中间件函数
     const mw = (req, res, next) => {
       console.log('这是简单的中间件函数');
       // 把流转关系，转交给下一个中间件或路由
       next()
     }
     
     app.listen(8080, () => {
       console.log('http://localhost:8080');
     })
     ~~~

     

   + ##### <font color="red">全局生效</font>的中间件

     **客户端发起的任何请求，到达服务器之后，都会触发的中间件**，叫做全局生效的中间件；

     通过调用 <font color="red">app.use(中间件函数)</font>，即可定义一个全局生效的中间件。

     ~~~js
     // 将 mw 注册为全局生效的中间件函数
     app.use(mw)
     
     // 全局中间件的简写形式
     app.use((req, res, next) => {
       console.log('全局中间件简写');
       next()
     })
     ~~~

     可以使用 app.use() 连续定义<font color="red">多个</font>全局中间件。客户端请求到达服务器之后，会按照中间件<u>定义的先后顺序</u>依次进行调用。

     ~~~js
     app.use((req, res, next) => {
       console.log('全局中间件1');
       next()
     })
     app.use((req, res, next) => {
       console.log('全局中间件2');
       next()
     })
     app.use((req, res, next) => {
       console.log('全局中间件3');
       next()
     })
     ~~~

     

   + ##### <font color="red">局部生效</font>的中间件

     **不使用 app.use() 定义的中间件**，叫做局部生效的中间件。

     ~~~js
     const mw = (req, res, next) => {
       console.log('局部中间件函数');
       next()
     }
     
     app.get('/', mw, (req, res) => {
       res.send('Home page.')
     })
     ~~~

     可以在路由中，通过一下两种<font color="red">等价</font>的方式，定义<font color="red">多个</font>局部中间件：

     ~~~js
     app.get('/', mw1, mw2, (req, res) => { res.send('Home page.') })
     app.get('/', [mw1, mw2], (req, res) => { res.send('Home page.') })
     ~~~

     

   + ##### 中间件使用注意事项 ⚠️

     + 一定要在<u>路由之前</u>注册中间件
     + 客户端发送过来的请求，<u>可以连续调用多个</u>中间件进行处理
     + 执行完中间件的业务代码之后，<u>不要忘记调用 next() 函数</u>
     + 为了防止代码逻辑混乱，<u>调用 next() 函数后不要再写额外的代码</u>
     + 连续调用多个中间件时，多个中间件之间，<u>共享 req 和 res 对象</u>

   

7. #### 使用 Express 写接口

   + ##### 创建基本的服务器

     ~~~js
     const express = require('express')
     const app = express()
     
     // wirte your code here...
     
     app.listen(8080, () => {
       console.log('http://localhost:8080');
     })
     ~~~

     

   + ##### 创建 API 路由模块

     ~~~js
     /** apiRouter.js */
     const express = require('express')
     const router = express.Router()
     
     // 在这里挂载对应的路由
     
     module.exports = router
     
     /** app.js */
     // 导入路由模块
     const apiRouter = require('./08.apiRouter')
     // 把路由模块注册到 app 上
     app.use('/api', apiRouter)
     ~~~

     

   + ##### 编写 GET 接口

     ~~~js
     /** apiRouter.js */
     // 在这里挂载对应的路由
     router.get('/get', (req, res) => {
       // 通过 req.query 获取客户端通过查询字符串，发送到服务器的数据
       const query = req.query
       // 调用 res.send() 方法，向客户端响应处理的结果
       res.send({
         status: 0,  // 0成功，1失败
         msg: 'GET 请求成功！',  // 状态的描述
         data: query // 需要响应给客户端的数据
       })
     })
     ~~~

     

   + ##### 编写 POST 接口

     ~~~js
     /** apiRouter.js */
     router.post('/post', (req, res) => {
       const body = req.body
       res.send({
         status: 0,
         msg: 'POST 请求成功！',
         data: body
       })
     })
     
     /** app.js */
     const express = require('express')
     const app = express()
     // 配置解析表单数据的中间件
     app.use(express.urlencoded({ extended: false }))
     ~~~

     

   + ##### CORS 跨域资源共享

     使用 <font color="red">cors 中间件</font>解决跨域问题。

     ~~~
     // 1. 安装中间件
     npm i cors
     
     // 2. 导入中间件
     const cors = require('cors')
     
     // 3. 配置中间件
     app.use(cors())
     ~~~

     

     ##### 👉 完整代码

     ~~~js
     // app.js
     const express = require('express')
     const app = express()
     
     // 配置解析表单数据的中间件
     app.use(express.urlencoded({ extended: false }))
     
     // 在路由之前，配置 cors 中间件
     const cors = require('cors')
     app.use(cors())
     
     // 导入路由模块
     const router = require('./08.apiRouter')
     // 把路由模块注册到 app 上
     app.use('/api', router)
     
     app.listen(8080, () => {
       console.log('http://localhost:8080');
     })
     ~~~

     ~~~js
     // apiRouter.js
     const express = require('express')
     const router = express.Router()
     
     // 在这里挂载对应的路由
     router.get('/get', (req, res) => {
       // 通过 req.query 获取客户端通过查询字符串，发送到服务器的数据
       const query = req.query
       // 调用 res.send() 方法，向客户端响应处理的结果
       res.send({
         status: 0,  // 0成功，1失败
         msg: 'GET 请求成功！',  // 状态的描述
         data: query // 需要响应给客户端的数据
       })
     })
     
     router.post('/post', (req, res) => {
       const body = req.body
       res.send({
         status: 0,
         msg: 'POST 请求成功！',
         data: body
       })
     })
     
     module.exports = router
     ~~~

     ~~~html
     <!DOCTYPE html>
     <html lang="en">
     
     <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
       <script src="https://cdn.staticfile.org/jquery/3.6.1/jquery.min.js"></script>
     </head>
     
     <body>
       <button id="btnGET">GET</button>
       <button id="btnPOST">POST</button>
     
       <script>
         $(function () {
           $('#btnGET').on('click', function () {
             $.ajax({
               type: 'GET',
               url: 'http://localhost:8080/api/get',
               data: { name: 'zs', age: 20 },
               success: function (res) {
                 console.log(res);
               }
             })
           }),
           $('#btnPOST').on('click', function () {
             $.ajax({
               type: 'POST',
               url: 'http://localhost:8080/api/post',
               data: { bookname: '西游记', author: '吴承恩' },
               success: function (res) {
                 console.log(res);
               }
             })
           })
         })
       </script>
     </body>
     
     </html>
     ~~~

     