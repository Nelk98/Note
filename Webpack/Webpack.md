# 一.	初识

## 1.1	打包工具

## 1.2	和 grunt/gulp 的区别

### 1.2.1	gulp

- gulp 核心是 Task 任务流
- 定义一系列的 task 之后让 gulp 依次 执行 task
- 自动化流程
- 也称为 自动化任务管理工具
- ==没有模块化概念==
- ==更强调任务流==



### 1.2.2	Webpack

- ==前端模块化打包工具==

- ==更强调模块化==
- 处理模块之间的依赖



## 1.3	依赖 node.js 环境



# 二.	安装使用

## 2.1	npm 安装

- ==webpack依赖 node 环境==

- ==全局安装：==

- npm install webpack@版本号 -g
- 局部安装： ==开发时依赖==
- npm install webpack@版本号 --save-dev



## 2.2	打包

- 只会打包 以main.js为顶部的依赖树上 的文件

- ==dist、src、配置 都放在项目根目录==

- ==dist文件夹==：用于存放打包后的文件（自动创建）
- ==src文件夹==：用于存放项目的源文件
  - ==main.js : 项目的入口==
  - mathUtils.js : 定义了数学函数
  - ==index.html : 浏览器显示的默认页面==
  - package.json : 依赖信息
- ==在 package.json 里 配置 scripts 脚本==
- ==会先从 项目本地模块查找是否有存在该模块==
- ==本地没有才会到全局查找==



# 三.	配置

## 3.1	webpack.config.js

- ==放在项目根目录==
- ==__==dirname 获取当前文件的绝对路径
- ==_ _==是两个下划线

```javascript
const path = require('path') //node的内置模块用于动态获取路径

module.exports = {
  entry: './src/main.js', //入口
  output: {			//打包出口
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    reles: [
      test: /\.css$/,				//正则表达式匹配文件
      use: ['style-loader','css-loader']	
    			//用什么处理,使用多个loader顺序从后到前使用
    ]
  }
}
```



## 3.2	loader

- webpack ==默认用来处理 js 文件==
- 解析打包其他类型文件需要使用 loader
- 不同文件用不同的 loader
- test: /正则表达式/
- use: ['xxx', 'xxx', 'xxx']
- use : [{loader: 'xxx', option:{ }}]



### 3.2.1	css-loader

- 只负责加载css 不负责解析



### 3.2.2	style-loader 

- 解析css 并把 样式 添加到 html



### 3.2.3	url-loader

- ==解析文件== 图片等等...
- ==limit：8192==    小于8192字节 8kb 的文件直接用base64字符串格式显示图片
- name: 'img/[name].[hash:8].[ext]]'
  - img/ 文件要打包的路径 ==默认是在 dist 文件夹下==
  - ==[name] 取到原文件的名字==
  - ==[hash:8] 把原始32位的hash值截取到8位==
  - ==[ext] 使用原来的拓展名==

```javascript
rules: [
  {
    test: /\.(png|jpg|jpeg|gif)$/,
    use: [
      {
        loader: 'url-loader',
        options: {
          limit: 8192,  // 
          name: 'img/[name.[hash:8].[ext]]' //hash默认32位 这里截取8位
        }
      }
    ]
  }
]
```





## 3.3	babel

- es6语法转化成es5语法
- 安装：npm install babel-loader@7 babel-core babel-preset-es2015 --save-dev
- babel-loader、babel-core、babel-preset-es2015

```javascript
rules: [
  {
    test: /\.js$/,
    exclude: /(node_modules|bower_components)/,	//排除
    include: xxx.js,	//包含	
    use: [
      {
        loader: 'babel-loader',
        options: {
          preset: ['es2015']
        }
      }
    ]
  }
]
```





## 3.4	resolve

### 3.4.1	alias 别名

```javascript
resolve: {
  alias: {
    'components': 'src/components',
    'vue$': 'vue/dist/vue.esm.js'
  }
}
```





## 3.5	plugins

- import xxx from 'xxx插件'
- plugins: [ new xxx( ), new xxx( ) ]



### 3.5.1 html-webpack-plugin

- 将打包的js文件自动加入html



### 3.5.2	uglifyjs-webpack-plugin

- ==js 文件压缩==
- 去掉空格
- 变量换名、函数换名





## 3.6	搭建本地服务器

### 3.6.1	安装 webpack-dev-server

- 安装 npm i webpack-dev-server --save-dev

- 编译的文件==缓存到内存里==
- build 之后才 存储到硬盘里



### 3.6.2	配置

```javascript
//webpack.config.js
devServer: {
  contentBase: './dist',
  inline: true
}

//package.json
{
  "script": {
    "dev": "webpack-dev-server"    //npm run dev
    "dev": "webpack-dev-server --open --config ./xxx.config.js"  //手动指定配置文件
    
  }
}
```





## 3.7	配置文件分离



- ==base.config.js 公共配置==
- ==dev.config.js  开发时配置==
- ==prod.config.js 打包发布时配置==



- 使用 webpack-merge 合并 两个 js 文件

```javascript
const webpackMerge = require('webpack-merge')
webpackMerge(xxx, xxx)
```



