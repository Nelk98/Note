# 一.	Node.js



1.1	JavaScript运行时环境

- 可以解析和运行JavaScript代码（ECMA Script）
- ==没有DOM、BOM==
- 网络服务的构建
- 网络通信
- ==web服务器后台==
- ==接口服务器==
- ==http服务器==



## 1.2	特点

- 事件驱动 event-driven 
- 非阻塞 i/o 模型 ==异步== non-blocking I/O model 
- 轻量和高效
- ==npm== 基于node.js 包管理工具 世界上最大的开源库生态系统
- 构建于 Chrome 的 v8引擎之上 ==目前公认最好的引擎==
  - 渲染引擎： 解析结构、样式
  - js引擎：解析js代码
- ==node代码 引入html中因为环境不一样，可以不能正常运行==



## 1.3	B/S 模型

- Browser-Server
- back-end 后端
- 任何服务端 的b/s模型 都是一样的，和语言无关
- node 是  b/s 模型的一个工具



## 1.4	模块化

- 什么是模块化？
  - 文件作用域
  - 通信规则
    - 加载
    - 导出 
- CommonJS 模块规范
  - 模块作用域，==防止变量污染==
  - ==require 方法加载模块==
  - ==exports 接口对象导出模块成员==



### module

- 在==Node中==每个模块都==默认有一个 module对象==
- 每一个module对象中都有一个成员 ： ==expoerts 默认为 { }（空对象）==
- 模块最后都会有 ==return module.exports==，谁require就return给谁
- ==Node底层隐式调用==

```javascript
var module = {
  exports: {
    
  }
}

var exports = module.exports //指向同一个对象 如果重新指向则导出失败
//所以必须挂载到exports对象的属性上

return module.exports 
```



### 加载模块

两个作用：

- 执行被加载模块中的代码
- 得到模块中的公开变量

```javascript
var 自定义变量 = require('模块')
```

- ==优先从缓存中加载==：对于已经加载过的模块不会重新执行模块里面的代码，但是可以获取模块导出的接口对象==



### 导出模块

- 模块作用域，默认文件中所有成员变量只在当前文件模块有效
- 对于希望可以被其他模块访问的成员，需要将这些公开成员都挂载到==exports==接口对象上
- 导出多个成员（必须在对象中）：==exports指向地址==

```javascript
exports.name = 'Nelk'
exports.say = function() {
  console.log('哈哈哈')
}

//引入
var ret = require(./xxx.js)
ret.say()   //哈哈哈
```

- 导出单个成员：

```javascript
module.exports = 'Nelk' 
```

- 导出多个成员 (重新定义)：

```javascript
module.expoets = {
 	name: 'Nelk',
  say() {
    console.log('hhh')
  }
}
```







- RequireJS
- SeaJS

- `@import('文件路径')`

```javascript
//require('核心模块') 无需完整路径
require('fs')

//require('自定义模块') 需要完整路径 可以省略.js
// 即使是当前目录下 ./ 也不能省略
require('./js/moduleA.js')
```

- ==模块作用域（文件作用域）==所有变量、方法 都只能在该文件内使用
- ==exports== 模块默认导出对象{}
- var ret = require(./xxx.js) 接收

```javascript
//导出  直接导出
exports.name = 'Nelk'
exports.say = function() {
  console.log('哈哈哈')
}

//引入
var ret = require(./xxx.js)
ret.say()   //哈哈哈

```





## 1.5	安装

- 官网下载
- `node --version`
- ==添加环境变量==



## 1.6	执行js文件

- 在文件目录下 运行 node xxx.js 
- ==文件名不能是  node.js==
- 最好不用中文



## 1.7 res 和 ret

```
return (ret)
返回结果，多用在函数返回结果
resource (res)
资源，多用在ajax返回的结果
```



# 二.	核心模块

- ==在node命令行窗口 可以直接使用内置核心模块==
- 核心模块已经被编译成二进制文件 只需要 require模块名就可以

## 2.1	fs

### 2.1.1	readFile

- 加载 fs 内置模块
- `const fs = require('fs')`
- `fs.readFile('文件路径', function(err, data){})`
- ==读取失败 err是错误对象，data为 null==
- ==读取成功 err为 null，data为读取数据==
- ==读取的数据是字符串或二进制数据==
  - JSON.pase(xxx) ==转成对象==
  - JSON.stringify(xxx) ==转成字符串==

```javascript
var fs = require('fs')
//按照utf-8 编码
fs.readFile('xxx', 'utf-8', function(err, date){
  
})
```





### 2.1.2	writeFile

- 加载 fs 内置模块
- ``const fs = require('fs')``
- `fs.readFile('写入路径','写入内容', function(err){})`
- ==写入成功 err 为空==
- ==写入失败，err为错误对象==



### 2.1.3	mkdir	

- 读取目录

### 2.1.4	readdir

- 创建文件夹



## 2.2	path





## 2.3	http

### 2.3.1	基本使用

- ==1.  加载http模块==
- `const http = require('http')`
- ==2.  创建web服务器实例==
- `var server = http.createServer()`
- ==3.  监听request==
- `server.on('request', function(){})`
- ==4.  监听端口一般是3000==，浏览器默认端口是80
- `server.listen(xxxx, function(){})`

```javascript
const http = require('http')
var server = http.createServer()

server.on('request', function() {
  console.log('接收到请求了')
})

server.linsten(3000, function() {
  console.log('Server is runing...')
})
```



### 2.3.1	发送请求

- 两个参数
- ==resquest：请求对象==
- ==response：响应对象==
- ==request.url 请求路径==，不带主机名和端口
- response.write( ) 响应数据
- response.end( ) 结束响应 ==只能响应字符串 和 二进制数据==
- write( )可以使用多次，==但最后必须end( )==，否则请求会一直被挂载，请求方处于一直等待的状态
- 只有一次响应数据的话可以直接 response.end( 数据 )
- `response.setHeater('Content-Type', 'text/plain; charset=utf-8')`
- 告诉请求方，响应的数据是普通文本 还是 html文本 或者其他  
- text/plain 普通文本
- text/html  html标签   ==默认==
- image/jpeg  等等，==不同文件类型的Content-Type不同==

```javascript
const http = require('http')
var server = http.createServer()

server.on('request', function(request, response) {
  console.log(request.url)// 访问路径
  response.write('xxxx')
  response.end()
  //response.end('xxx')
})

server.linsten(3000, function() {
  console.log('Server is runing...')
})
```



## 2.4	url

- 加载 url 模块
- `require('url')`
- `url.pase('请求路径', true)`
- true 表示将查询字符串解析成 query对象

```javascript
var url = require('url')
var obj = url.parse('/home?name="Nelk"&age=18', true)

obj.pathname  => '/home'  不包含查询字符串的路径
obj.query => {
  name: 'Nelk',
  age: 18
}

```



# 第三方模块

- ==加载用法和核心模块一样==

- 一个项目有且只有一个==node_modules==，且在==项目根目录==

- ==加载规则==：

  - 先找文件夹 node_modules/模块名/ 
  - 再找该文件夹下的 package.json
  - 再找package.json 中 的 main 属性
  - main属性 记录了当前模块的入口模块
  - ==如果package.json 或 main 找不到 则默认加载当前文件夹下的 index.js==
  - 如果index.js 也找不到 则会从当前目录往上一层一层找==node_modules==，直到磁盘根目录找，最后找不到就会报错，查找不到

  ```
  {
  ......
  	"main": "index.js"
  }
  ```

  

## template

- ```shell
  npm install art-template --save
  ```

- 模板引擎只关心 mustache 语法，不关心其他内容

- 使用

```html
<script src="xxx/xxx/template-web.js"></script>
<script type="text/template" id="tp">
我是，{{name}}
我今年{{age}}岁了
我喜欢{{each hobbies}} {{$value}} {{/each}}
</script>
<script>
var ret=template('tp', {
  name: 'Nelk',
  age: 18,
  hobbies: ['看电视', '吃饭', '睡觉']
})
</script>
```



## body-parser



# 常用知识

## 客户端渲染

- 访问网页，第一次响应了一个简单的页面结构
- ==通过异步请求==，获取数据，来局部刷新页面内容 
- 不利于==SEO优化==（搜索引擎优化）
- 可以尽早看到页面
- ==源代码看不到数据内容==



## 服务端渲染

- ==为了SEO优化==

- 发起一次服务器请求
- 服务器直接将页面渲染好再发送给客户端
- ==速度更快==，响应的就是最终结果，通常不需要再进行异步请求
- ==服务器压力大==
- ==可以在网页源代码看到数据内容==



## 开放静态资源

- ==默认所有url都不允许用户访问==（黑盒子）
- 通过路由来控制响应内容

- ==public文件夹==
- 



## 网页重定向

- 客户端收到重定向状态码 301/302 会自动去响应头 找Location 进行重定向
- ==301 永久重定向==，浏览器会记录重定向地址，以后每次访问原地址 都==不会再请求服务器==，而是直接重定向到新地址
- ==302 临时重定向==，浏览器每次访问原地址==都会向服务器发送请求==。

```javascript
server.on('request', function(request, response) {
  res.statusCode = 302
  res.setHeader('Location', '/home')
  res.end()
})
```



## nodemon

nodemon 是基于 node.js 的第三方命令行工具，==需全局安装==

```shell
npm i nodemon --global
```

使用时，会实时监控服务文件的修改，自动重启服务器

```shell
nodemon app.js
```





# npm

## 是什么

- ==node-package-manager==
- 官方网站：npmjs.com



## npm常用命令

- ==npm init== 项目初始化 生成 package.json
- npm init -y 跳过选项 快速初始化
- ==npm install== 下载全部依赖项
  - install 简写 i
- ==npm install== 包名 --save
  - --save 下载并保存依赖项
  - --save 简写 -S
- ==npm uninstall== 包名
  - uninstall 简写 un
  - 只删除
  - 依赖项依然保存
- ==npm help==查看使用帮助
  - npm xxx --help 查看某个命令的帮助



## package.json

- ==记录项目依赖项信息==
- 通过npm install 会自动下载依赖项
- 版本号带 ==^==,安装的时候一该版本为最低版本，往上安装
- ==^3.1.4  不会安装到 ^4.x.x==

```json
{
"dependencies": {
    "better-scroll": "^1.15.2",
    "core-js": "^3.6.4",
    "vue": "^2.6.11",
    "vue-awesome-swiper": "^3.1.3",
    "vue-router": "^3.1.5"
  }
}
```



## package-lock.json

- ==保存所有node_modules的依赖信息== 即 模块信息 和 模块的依赖信息
- 有package-lock.json 安装速度更快

- ==npm5 之后加入的==
- 不需要再 --save
- 版本号带 ~ 的指定安装这个版本 ==锁定版本==



# Express

原生的 http 模块在某些方面不足以快速开发需求，框架的目的就是为了提高开发效率，让代码高度统一。

在Node 中有很多开发框架 Express 就是其中一种



## 基本使用

- `npm init`
- `npm install express --save`
- ==在入口引入模块==

```javascript
//0. 安装
//1. 引包
var express = require('express')
//2. 创建服务器应用程序 相当于 http.createServer
var app = express()

// 服务器接收到get请求 / 执行回调函数
app.get('/', function(req,res) {
  res.send('响应数据')  //send 类似 write和end 的结合
})

app.listen(3000, function() {
  console.log('Server is running...')
})
```



## 基本路由

==根据不同 请求，响应不同的请求处理函数==

- get

```javascript
app.get('/', function(req,res) {
  res.send('响应数据')
})
```

- post

```javascript
app.post('/', function(req,res) {
  res.send('响应数据')  
})
```







## 指定公开静态资源

```javascript
var express = require('express')
var app = express()

//公开指定目录
//客户端可以直接通过 /public/xxx/xx 直接访问 public 目录下的所有资源内容
app.use('/public/', express.static('./public/'))

app.listen(3000, function() {
  console.log('Server is running...')
})
```

```javascript
//无需 /public/xxx/xx
//直接 /xxx/xx
app.use(express.static('./public/'))
```





## express-art-template

安装：==依赖 art-template==

```shell
npm install art-template --save
npm install express-art-template --save
```

配置：

```javascript
//开启res.render方法
//匹配拓展名.html
app.engine('html', require('expess-art-template'))
```

- ==express 默认约定 视图文件放在 /views/ 目录==
- `app.set('views', 目录路径)` ==修改==

```javascript
var express = require('express')
var app = express()

app.engine('html', require('expess-art-template'))

app.get('/',function(req, res) {
  res.render('index.html', { 模板数据 })
})

app.listen(3000, function() {
  console.log('Server is running...')
})
```



## 获取GET请求数据

无需解析==get请求==查询字符串

express 底层经过处理

直接获取 query 对象

```javascript
app.get('/home', function(req, res) {
  console.log(req.query)
  res.send('')
})
```



## 获取POST请求数据

==Express 无内置获取post请求体的api，需要安装 第三方插件==

安装：

```shell
npm install body-parser --save
```

配置：

```javascript
var express = require('express')
var app = express()

var bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extend: false }))
app.use(bodyParser.json())

app.listen(3000, function() {
  console.log('Server is running...')
})
```





## express-重定向

底层封装了方法 res.redirect

```javascript
app.get('/home', function(req, res) {
  res.redirect('/')
})
```



## 路由模块提取

==router.js==

```javascript
module.exports = function(app) {
  app.get('/',function(req, res) {
    
  })
  app.get('/home',function(req, res) {
    
  })
  app.post('/home',function(req, res) {
    
  })
}
```

```javascript
var express = require('express')
var app = express()

//加载路由模块
var router = require('./router.js')
//把app对象传入router模块
router(app)

app.listen(3000, function() {
  console.log('Server is running...')
})
```

==但是这样做不方便，Express提供了更好的方法==

==专门用来包装路由==

```javascript
var express = require('express')

//1. 创建路由容器
var router = express.Router()

//2. 挂载路由
router.get('/', function(req, res) {})
router.get('/home', function(req, res) {})
router.get('/about', function(req, res) {})

//3. 导出路由模块
module.exports = router

```

```javascript
var express = require('express')
var app = express()

//4. 加载路由模块
var router = require('./router.js')
//5. 把路由容器挂载到 app 服务中
app.use(router)

app.listen(3000, function() {
  console.log('Server is running...')
})
```



## 数据操作模块提取

==需要获取一个函数中一个异步操作的结果，不需使用回调函数==

==异步函数没有return 直接返回undefined==

```javascript
exports.find = function(xxx,callback){
  xxxx
  callback(err,data)
}
```

```javascript
// 加载数据操作模块
var xxx = require('./xxx.js')
//调用数据操作方法
xxx.find(xxx,function(err, data) {
  
})

```



# MongoDB

==no sql 非关系型数据库==不需要使用SQL语句

- 数据库 -> 数据库
- 数据表 -> 集合（数组）
- 表记录 -> 对象

mongoDB不需要设计表结构

==MongoDB中可以有多个数据库==

### 安装配置

- 安装默认路径
- ==配置环境变量==
- 创建默认数据存储目录  /data/db



### 启动

==mongodb 默认使用 命令行所处盘符的 根目录 /data/db/ 作为数据存储目录==

==需要手动创建==

C: -->   C:/data/db/

D: -->   D:/data/db/

命令行窗口启动：

```shell
mongod
```

- 启动时 不使用默认路径 /data/db

```shell
mongod --dbpath=数据存储路径
```



### 连接和退出

连接：

==前提是已经启动数据库==

```shell
# 默认连接本地mongodb
mongo
```

退出：

```shell
exit
```



### 基本命令

- `show dbs`
  - 查看显示所有数据库
  - admin、local 系统数据库
- `use 数据库名称`
  - 切换到指定的数据库
  - ==如果没有对应数据库，会自动创建==（当插入数据后）
- db.table.insertOne(xxx)
  - db 为当前所在的数据库 ==简写成 db==
  - table 为操作的数据集合（表），需要写出具体名称
  - ==每条数据会自动生成一个 24位 唯一不重复的 "_id"==
- `show clooections`
  - 显示当前数据库的 所有集合（表）





# Mongoose

安装：

```shell
npm install mongoose --save
```

使用：

```javascript
//1.	加载模块
const mongoose = require('mongoose');

//2. 连接数据库  数据库不需要存在, 会自动创建
mongoose.connect('mongodb://localhost/库名');

//3. 发布数据模型 会生成 Cat小写复数数 cats数据集合
const Cat = mongoose.model('Cat', { name: String });

//4. 创建一个Cat实例对象
const kitty = new Cat({ name: 'Nelk' });

//5. 持久化存储到数据库
kitty.save().then(() => console.log('存储成功'));
```



## 设计结构

==设计Schema 发布 model==

设计结合结构（表结构）

字段名就是表结构中的属性名

约束的目的是为了保证数据的完整性，不要有脏数据

创建文档结构：

```javascript
var userSchema = new Scheme({
  userName: { 
    type: String,  	   // 数据类型
    required: true,		// 必须
    default: '名字'   //	默认值
  }
})
```

发布模型

- 第一个参数传入 ==大写单数名词== 用来表示 数据库 集合，会自动将大写名词单数==转换成小写复数==形式 在数据库中创建或链接 集合
- ==第二个参数 将 数据架构传入==
- ==返回值是 模型构造函数==

```javascript
var User = moogoose.model('User', userSchema)
```



## 插入数据

```javascript
User.insertMany({
    name: 'Nelk1',
    password: '3445566'
}, function(err, ret) {
    if (err) {
        console.log('删除失败');
    } else {
        console.log('删除成功');
    }
})
```



## 查询数据

==find 输出为 数组集合（尽管只有一个对象）==

==find( ) 无条件时 查找全部==

```javascript
User.find({ name: 'Nelk2' }, function(err, ret) {
	if (err) {
		console.log('查询失败');
	} else {
     console.log(ret);
  }
})
```





==findOne 输出的 是对象==

==找到第一个符合条件的数据就会停止查询==

```javascript
User.findOne({ name: 'Nelk2' }, function(err, ret) {
	if (err) {
    console.log('查询失败');
	} else {
		console.log(ret);
	}
})
```







## 删除数据

==deleteOne==

```javascript
News.deleteOne(
  
    {'_id':'5cf5e613ba3c6298a8734973'}, //查找条件
  
  	//回调函数
    (err, ret)=>{
        if(err){return console.log('删除数据失败')}
        console.log(ret);
    }

)
```

==remove==

==deleteMany==

## 修改数据

==updateOne==

```javascript
News.updateOne(
    {'_id':'5cf5e613ba3c6298a8734973'}, //条件
    {title: '这是一则新闻111'},     //要更新的内容
    /*回调函数*/
    (err, ret)=>{
        if(err){return console.log('更新数据失败');}
        console.log(ret);
    }
)
```

==findOneAndUpdate==

查找一个并更新



==findByIdAndUpdate==

```javascript
User.findByIdAndUpdate('5df0ad73bf2baf38fcaac183',
  {
		name: '我被更新了哦'
	}, function(err, ret) {
		if (err) {
			console.log('更新失败');
		} else {
			console.log('更新成功');
		}
})
```

==upadte==

==updateMany==

==replaceOne==



## 条件操作符 where

==$操作符 和 操作( ) 一样的功能==

```javascript
query.find({age : {$equals: 12}});

query.where('age').equals(12)
```



### where	*

```javascript
// find 写法：
User.find({age: {$gte: 21, $lte: 65}}, callback);

// where 替换写法：
User.where('age').gte(21).lte(65);

// 也可以传入 query condition
User.find().where({ name: 'vonderful' })

// 链式写法
User
.where('age').gte(21).lte(65)
.where('name', /^vonderful/i)
.where('friends').slice(10)
.exec(callback)
```

==只有当 MongoDB 其他操作符（如 `$lt`）不能表达你的查询条件时再使用 `$where`==

```javascript
query.$where('this.comments.length === 10 || this.name.length === 5')
```



==许多查询api==

==只传入一个参数则对前一个 where( ) 生效==



### exists

==匹配字段是否存在==

```javascript
// 有onsale 字段的数据
query.where('onSale').exists(true)

// 没有onsale 字段的数据
query.where('onSale').exists(false)
```



### mod 

==取模运算==

```javascript
//取模5为1 
query.where('age').mod([5, 1])
```





### or、and、nor

==与或非==

```javascript
query.or([{ color: 'red' }, { status: 'emergency' }])
```



### gt、lt、eq	*

- gt：大于
- lt：小于
- equals： 等于
- gte：大于等于
- lte：小于等于
- ne：不等于

```javascript
Thing.find().where('age').gt(21)
//等同于
Thing.find().gt('age', 21)

query.find({ "field" : { $gt: value } } ); // 大于: field > value
query.find({ "field" : { $lt: value } } ); // 小于: field < value
query.find({ "field" : { $gte: value } } ); // 大于等于: field >= value
query.find({ "field" : { $lte: value } } ); // 小于等于: field <= value

// value1 < field < value2
query.find({ "field" : { $gt: value1, $lt: value2 } } ); 
```



### in、nin

- in：包含
- nin： 不包含

```javascript
Thing.find().where('age').in([18, 19, 20])
//等同于
Thing.find().in('age', [18, 19, 20])
```



### all

- 和in 不同于
  - in只需包含其中一个
  - all 必须匹配条件的所有

```javascript
query.find({fruits : {$all : ['apple', 'banana']}});

query.where('fruits').all(['apple', 'banana'])
```



### size

==匹配数组元素个数==

```javascript
query.where('fruits').size(3)
//[xxx, xxx, xxx]
```



### regex *

==匹配正则表达式==

```javascript
query.where('phone').regex(/^131/)
```



### count

==返回查询数量==





### limit	*

==指定查询结果的最大条数==

```javascript
//限制查询20条数据
query.find().limit(20)
```



### skip 

==跳过数据==

```javascript
跳过前20条数据
query.find().skip(20)	
```



### sort	*

==排序==

```javascript
//按年龄升序 asc
query.find().sort({age: 1})

//按年龄降序 desc
query.find().sort({age: -1})
```



### exec、then	*

==查询结束回调数据==

==exec 一次性动作==

==then连续性动作==

```javascript
query.find().limit(20).exec(function(err, ret) {
  
})
```







## crud-api

 `update()`, `updateOne()`, `updateMany()`, `replaceOne()`, `findOneAndUpdate()`, `findByIdAndUpdate()`

 `find()`, `findOne()`, `findById()`, `findOneAndUpdate()` ,`findByIdAndUpdate()`

 `remove()`, `deleteOne()` ,`deleteMany()` 