# NodeJs
Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. This is my learning


# NodeJS-Express-MongoDB

NodeJS相关内容:

Node.js 是一个让javaScript运行在服务器端的开发平台（为网络而生）试着用Node与java对比
javaScript是为客户端而生的；
Node.js最大的特性就是采用异步式I/O与事件驱动的架构设计
Node.js使用的引擎与谷歌使用的是一个版本，所以加载速度快

运行在NodeJS中的JS的用途是操作磁盘文件或搭建HTTP服务器

每一个node.js文件都是一个模块

模块的调用：
只需要require需要调用的文件即可。
在require了这个文件之后，定义在exports对象上的方法便可以随意调用。
circle.js:
var PI=Math.PI;
exports.area=function(r){
    return PI*r*r;
}
exports.circumference=function(r){
    return PI*r*2;
}

main.js:
var circle=require('./circle.js');
console.log('This circle's area is + ' circle.area(4)); 

模块的分类：
1.原生模块（核心模块）；加载速度最快，已编译成二进制执行文件；存放在lib库。
2.文件模块（通过命令行启动的文件）；存放位置不定（.js通过fs模块同步读取js文件编译执行、.node通过c/c++进行编写的 、.json读取文件，调用JSON。parse解析 加载）
加载模块的工作主要由module来实现和完成，原生模块在启用时就已被加载，进程直接调用runMain静态方法。
modelu.runMain=funtion(){};
require实际调用的是load方法。

加载模块的优先级：缓存区的文件模块->原生模块->文件模块（先缓冲区->再加载模块）

require方法接受以下几种参数的传递：
http、fs、path等，原生模块。
./mod或../mod，相对路径的文件模块。
/pathtomodule/mod，绝对路径的文件模块。
mod，非原生模块的文件模块。

module path:对于每一个被加载的文件模块，创建这个模块对象的时候，这个模块便会有一个paths属性，其值根据当前文件的路径计算得到。

包结构：
一个符合CommonJS规范的包应该是如下这种结构：
一个package.json文件应该存在于包顶级目录下
二进制文件应该包含在bin目录下。
JavaScript代码应该包含在lib目录下。
文档应该在doc目录下。
单元测试应该在test目录下。

使用模板引擎（这里的是ejs）：
在 routes/index.js 中通过调用 res.render() 渲染模版，并将其产生的页面直接返回给客户端。它接受两个参数，第一个是模板的名称，即 views 目录下的模板文件名，扩展名 .ejs 可选。第二个参数是传递给模板的数据对象，用于模板翻译。
eg: res.render('index',{title:'Express'});
模板中<% =title%>中的title替换成Express

判断用户登录状态：引入session机制



Express相关内容：
Express存在对于Node的意义:
Express是一个大型用的最多的一个Node.js的框架，用得最多的node框架，类似thinkphp对于php。
如何用Express创建一个项目：
首先是安装Express：
     1.下载安装好的Node.js已经顺带有npm，npm是管理node.js依赖的管理器（它的强大，让你很安心）；
     2.如果你想把Express与你的node_module放在一个目录夹下，就先cd进到该目录下，再使用npm i express-generation -e(其中-e表示，使用的模板引擎是ejx,默认引擎是jade);
     3.检测是否安装好，使用express -v，如果出现版本号，则安装成功。
其次是使用express创建一个项目（以blog为例）：
        1.>express -e blog (-e代表使用ejs引擎，默认为jade),之后自动生成一个名为blog的项目。
        2.打开你创建的目录看一下里面的模块。
        其中：
        bin/www--新版的入口文件
            node_module--存放依赖的依赖库
            routes--路由控制器
            views--视图
            public--用于存放静态文件（js、css、imgs etc.）
            app.js--主要页面
            pakeage.json--类似thinkphp的config文件，用于配置依赖库和开发者的相关信息
MongoDB相关内容：
Mongo的安装与启动：
npm install mongodb -g
MongoDB高性能、开源、无模式的文档型数据库，它基于分布式文件存储。介于关系数据库和非关系数据库之间的一种产品。其最大特点：查询语言功能十分强大。
传统关系型数据库：database+table+record
MongoDB:  database+collection+document

下载mongoDB安装包：http://www.mongodb.org/downloads
两个重要的文件：
Mongod.exe ------ 用来连接到mongo数据库服务器的，即服务器端。
 Mongo.exe ------ 用来启动MongoDB shell的，即客户端。

在D盘创建一个文件夹Mongodb，把bin文件放进去，同时创建  d:\mongodb\db   数据库目录
        d:\mongodb\log  日志存放目录
        d:\mongodb\log\mongoDB.log
注意：要把mongo的安装目录（D:\Mongodb\bin）设到系统环境变量里去
具体教程：http://www.cnblogs.com/wx1993/p/5206587.html（windows）
启动数据库命令：
在进入mongo的bin下（即：D:\Mongodb\bin>）输入命令：mongod --dbpath =D:\mongodb\db
然后在package.json的依赖里加一句：
"mongodb":"~2.2.0"


MongoDB出现的问题（FAQ）：
Q：无法获取主机名？连接不上？ 
A：打开两个dos命令窗口，一个输入：mongod -dbpath D:\mongodb\data\db；（我的放在D盘）；命令窗出现一大串内容不用理会，只需看到waiting for connect 
此时打开另一个cmd窗口：进入bin目录下输入：mongo

最后查看是否安装成功：从图中的信息中获知，mongodb采用27017端口，那么我们就在浏览器里面键入“localhost:27017”

开始使用MongoDB:

Mongodb创建collection:db.createUser('blog');

一：插入数据db.users.insert({'name':'xinxin','password':'123'});
db.users.insert({'name':'xiaoLin','password':'456'});
db.user.find()db.user.find()这句不能省我们将数据插入后，肯定是要find出来，不然插了也白插
万一数据存错了，怎么改呢：update：
二：update操作
1.db.users.update({'name':'xinxin','password':'111'});
2.db.user.find()
update方法的第一个参数为“查找的条件”，第二个参数为“更新的值”，学过C#，相信还是很好理解的。update之后还是得find()

三：remove操作（delete）
注意不带参数，代表删除所有数据，依旧的find()
