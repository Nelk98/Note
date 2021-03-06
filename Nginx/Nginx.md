# Nginx 基本认识

## 1.	服务器集群

- 多台服务器组成的响应大并发、高数据量访问的架构体系。
- 特点：
  - 成本高。
  - ==能够降低单台服务器的压力，使流量平均分配到多台服务器。==
  - 网站服务器更加稳定。



## 2.	WEB服务器软件

- apache	功能多，稳定
- nginx  轻量，并发高 web服务器 代理服务器 网络接口服务



## 3.	反向代理

- ==正向代理== 通过代理服务器访问

<img src=".\media\Snipaste_2020-03-24_16-49-56.jpg" style="zoom: 50%;" />



- ==反向代理==

  - 直接访问 反向代理服务器 转发到真实的服务器上
  - ==对外暴露的服务器== ==转发== 到 真实的服务器

  ![](.\media\Snipaste_2020-03-24_16-56-42.jpg)





## 4.	负载均衡

- 请求数量高，单个服务器压力大
- 增加服务器数量，将原先集中的请求分发到各个服务器上

![](.\media\Snipaste_2020-03-24_17-10-51.jpg)





## 5.	动静分离

- 为了加快解析速度，将动态页面和静态页面用不同服务器来解析
- 降低原来单个服务器压力





# Nginx 使用

==必须进入nginx 目录，xxx/nginx/sbin/==

## 1.	基本命令

- ./nginx	启动

- ./nginx -s stop    关闭

- ./nginx -s reload    重新加载
  - 不需要重启nginx 服务器，会重新加载配置



# Nginx配置



## 1.	全局快

- ==从配置文件开头到events块的内容==
- 主要设置一些影响nginx服务器整体运行的命令
- worker_process 1;  值越大，支持的并发量越大



## 2.	events块

- 主要配置与用户的网络连接
- worker_connecton 1024; 支持最大连接数

## 3.	http块  *

- 代理、缓存、日志定义、和绝大多数的功能以及第三方模块
- ==http块 包含 http全局快、server块==



## 4.配置实例-反向代理

- 效果：浏览器输入 `www.nelk.xyz` 跳转到自定义页面中
- ![](.\media\Snipaste_2020-03-24_18-28-59.jpg)
- 修改 windows 本地host 配置域名使其访问nginx而非访问网络dns域名 ==C:\Windows\System32\drivers\etc\hosts==
- ![](.\media\Snipaste_2020-03-24_18-52-01.jpg)





















