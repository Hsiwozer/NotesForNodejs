# npm 与包

### 👉 [npm 社区：https://www.npmjs.com](https://www.npmjs.com)

1. #### 包

   即第三方模块。

   

2. #### 在项目中安装包

   ~~~bash
   // 默认安装最新版本的包
   npm i 包的完整名称
   
   // 安装指定版本的包，使用 @ 指定版本号
   npm i 包名称@版本号
   ~~~

   

3. #### 在项目中使用包

   ###### 以 moment 为例

   ~~~js
   const moment = require('moment')
   
   const dt = moment().format('YYYY-MM-DD HH:mm:ss')
   
   console.log(dt);
   ~~~

   

4. #### 包管理配置文件

   在项目根目录中，存在（创建）一个名为 <font color="red">package.json</font> 的配置文件，即可以用来记录项目中安装了哪些包。从而方便剔除 node_modules 目录（由于 node_modules 目录占整个项目非常大的体积）后，在团队成员之间共享项目的源代码。

   ###### ⚠️注意：在项目开发中，务必把 node_modules 文件夹，添加到 .gitignore 忽略文件中！

   

   ##### 快速创建 package.json 配置文件：

   ~~~bash
   npm init -y
   ~~~

   

5. #### <font color="red">dependencies</font> 节点

   在 package.json 文件中，有一个 dependencies 节点，专门用来记录使用 `npm i` 命令安装了哪些包。

   

6. #### <font color="red">一次性</font>安装所有依赖包

   ~~~bash
   npm i
   ~~~

   

7. #### 卸载包

   ~~~bash
   npm uninstall 包名
   ~~~

   

8. #### <font color="red">devDependencies</font> 节点

   记录只在**项目开发阶段**使用到的依赖包。

   而 dependencies 节点中记录了开发和项目上线后都需要使用到的依赖包。

   ~~~bash
   // 简写
   npm i 包名 -D
   
   // 完整写法
   npm install 包名 --save-dev
   ~~~

   

9. #### 解决下包速度慢的问题

   ##### <font color="blue">淘宝 NPM 镜像服务器</font>

   ~~~bash
   // 查看当前的下包镜像源，默认为国外镜像源 https://registry.npmjs.org/
   npm config get registry
   
   // 将下包的镜像源切换为淘宝镜像源
   npm config set registry=https://registry.npmmirror.com/
   ~~~

   

   ##### nrm

   为了更方便的切换下包的镜像源，可以利用 nrm 提供的终端命令，快速查看和切换下包的镜像源。

   ~~~bash
   // 通过 npm 包管理工具，将 nrm 安装为全局可用的工具
   // 如果是 windows 系统需要使用管理员权限
   sudo npm i nrm -g
   
   // 查看所有可用的镜像源
   nrm ls
   
   // 将下包的镜像源切换为 taobao 镜像
   nrm use taobao
   ~~~

10. #### 全局包

    在执行 `npm i` 命令时，如果提供了 **-g** 参数，则会把包安装为全局包。

    ~~~bash
    // 查看全局包的安装路径
    npm root -g
    ~~~

    

11. #### <font color="red">i5ting_toc</font>

    i5ting_toc 是一个可以**把 md 文档转换为 html 页面**的小工具。

    ~~~bash
    // 将 i5ting_toc 安装为全局包
    npm i -g i5ting_toc
    
    // 调用 i5ting_toc，轻松实现 md 转 html 的功能
    i5ting_toc -f 要转换的 md 文件路径 -o
    ~~~