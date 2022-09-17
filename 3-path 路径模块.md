# path 路径模块

1. #### 什么是 path 路径模块？

   path 模块是 Node.js 官方提供的、用来<font color="red">处理路径</font>的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

   例如：

   + path.join() 方法，用来将多个路径片段拼接成一个完整的路径字符串
   + path.basename() 方法，用来从路径字符串中，将文件名解析出来

   

   如果要在 JavaScript 代码中，使用 path 模块来处理路径，则需要使用如下的方式先导入它：

   ~~~js
   const path = require('path')
   ~~~

   

2. #### 路径拼接

   + ##### path.join() 语法格式

     使用 path.join() 方法，可以把多个路径片段拼接为完整的路径字符串。

     ~~~js
     path.join([...paths])
     ~~~

     paths <string> 路径片段序列

     返回值：<string>

     

   + ##### path.join() 代码示例

     ~~~js
     const path = require('path')
     
     // ../ 会抵消前面的一层路径
     const pathStr = path.join('/a', '/b/c', '../', './d', 'e')
     console.log(pathStr); // /a/b/d/e
     
     fs.readFile(path.join(__dirname, './files/1.txt'), 'utf-8', (err, dataStr) => {
       if (err) {
         return console.log('读取文件失败！' + err.message);
       }
       console.log('读取文件成功！' + dataStr);
     })
     ~~~

     

3. #### 获取路径中的文件名

   + ##### path.basename() 语法格式

     使用 path.basename() 方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名。

     ~~~js
     path.basename(path[, ext])
     ~~~

     path <string> 必选参数，表示一个路径的字符串

     ext <string> 可选参数，表示文件扩展名

     返回值：<string> 表示路径中的最后一部分

     

   + ##### path.basename() 代码示例

     ~~~js
     const path = require('path')
     
     // 定义文件的存放路径
     const fpath = '/a/b/c/index.html'
     
     // 包含扩展名
     const fullName = path.basename(fpath)
     console.log(fullName);  // index.html
     
     // 不含扩展名
     const fullName2 = path.basename(fpath, '.html')
     console.log(fullName2); // index
     
     ~~~

     

4. #### 获取路径中的文件扩展名

   + ##### path.extname() 语法格式

     使用 path.extname() 方法，可以获取路径中的扩展名部分。

     ~~~js
     path.extname(path)
     ~~~

     

   + ##### path.extname() 代码示例

     ~~~js
     const path = require('path')
     
     const fpath = '/a/b/c/index.html'
     
     const fext = path.extname(fpath)
     console.log(fext);  // .html
     ~~~

   