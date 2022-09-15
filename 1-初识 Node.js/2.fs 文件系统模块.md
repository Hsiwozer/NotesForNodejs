# fs 文件系统模块

1. #### 什么是 fs 文件系统模块 ？

   <font color="red">fs 模块</font>是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。

   例如：

   + <font color="blue">fs.readFile()</font> 方法，用来读取指定文件中的内容
   + <font color="blue">fs.writeFile()</font> 方法，用来向指定的文件中写入内容

   

   如果要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它：

   ~~~js
   const fs = require('fs')
   ~~~

   

2. #### <font color="red">读取</font>指定文件中的内容

   - ##### fs.readFile() 语法格式

     ~~~js
     fs.readFile(path[, options], callback)
     ~~~

     path： 必选参数，字符串，表示文件的路径。

     options：可选参数，表示以什么编码格式来读取文件。

     callback：必须参数，文件读取完成后，通过回调函数拿到读取的结果。

     

   - ##### fs.readFile() 示例代码

     以 utf8 的编码格式，读取指定文件的内容，并打印 err 和 dataStr 的值：

     ~~~js
     const fs = require('fs')
     fs.readFile('./files/1.txt', 'utf-8', (err, dataStr) => {
       // 如果读取成功，则 err 的值为 null
       // 如果读取失败，则 err 的值为 错误对象，dataStr 的值为 undefined
       console.log(err);
       console.log(dataStr);
     })
     ~~~

     

   - ##### 判断文件是否读取成功

     ~~~js
     const fs = require('fs')
     fs.readFile('./files/2.txt', 'utf-8', (err, dataStr) => {
       if (err) {
         return console.log('读取文件失败！' + err.message);
       }
       console.log('读取文件成功！' + dataStr);
     })
     ~~~

     

3. #### 向指定文件中<font color="red">写入</font>内容

   - ##### fs.writeFile() 语法格式

     ~~~js
     fs.writeFile(file, data[, options], callback)
     ~~~

     file：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径。

     data：必选参数，表示要写入什么内容。

     options：可选参数，表示以什么编码格式来写入文件内容，默认为 utf-8。

     callback：必选参数，文件写入完成后的回调函数。

     

   - ##### fs.writeFile() 示例代码

     向指定文件路径中，写入文件内容：

     ```js
     const fs = require('fs')
     fs.writeFile('./files/2.txt', 'abcdefg', (err) => {
       // 如果文件写入成功，则 err 的值为 null
       // 如果文件写入失败，则 err 的值为错误对象
       console.log(err);
     })
     ```

     

   - ##### 判断文件是否写入成功

     ~~~js
     const fs = require('fs')
     fs.writeFile('./files/3.txt', 'hello world', (err) => {
       if (err) {
         return console.log('文件写入失败！' + err.message);
       }
       console.log('文件写入成功！');
     })
     ~~~

     

4. #### fs 模块 - 路径动态拼接问题

   在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 ../ 开头的<font color="red">相对路径</font>时，很容易出现路径动态拼接错误的问题。

   原因：代码在运行的时候，会以执行 <font color="red">node 命令时所处的目录</font>，动态拼接出被操作文件的完整路径。

   解决方案：在使用 fs 模块操作文件时，直接<font color="red">提供完整的路径（绝对路径）</font>，不要提供 ./ 或../ 开头的相对路径，从而防止路径动态拼接的问题。**但是，这种方法移植性非常差，且不利于维护。**

   

   ##### ✅ <font color="red">__dirname</font>

   ~~~js
   // 正解
   const fs = require('fs')
   fs.readFile(__dirname + '/files/2.txt', 'utf-8', (err, dataStr) => {
     if (err) {
       return console.log('读取文件失败！' + err.message);
     }
     console.log('读取文件成功！' + dataStr);
   })
   ~~~

   ###### __dirname 表示当前文件所处的目录

