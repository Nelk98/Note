# HTML 

[toc]







## img

```html
<img scr="" alt="当图片无法加载用于替换图片的文字" title="鼠标经过会显示的文字" />
```





## a

```html
<a href="" target="_self"></a> 			在本窗口打开
<a href="" target="_blank"></a> 		在新窗口打开

<a href="文件路径"></a>			下载压缩文件 .exe .zip 等等

<a href="#hello"></a>				锚点跳转
<div id="hello">HELLO WORLD</div>
```





## 转义字符

```html
&nbsp;  半角空格
&emsp;  全角空格
&lt;		< 小于
&gt;		> 大于
&yen;		￥¥
```







## 表格table

### 1. 基本使用

```html
<table>
  <thead>
  	<tr>
    	<th>姓名</th>
    	<th>性别</th>
    	<th>年龄</th>
  	</tr>
  </thead>
  <tbody>
  	<tr>
  		<td>Nelk</td>
  		<td>男</td>
  		<td>18</td>
  	</tr>
  	<tr>
  		<td>Mike</td>
  		<td>男</td>
  		<td>19</td>
  	</tr>
  </tbody>
  
</table>
```

**th 是表头 默认 字体 居中加粗**

**把table 划分 为 thead 和 tbody**

![](media\table.jpg)



### 2. 合并单元格

1. 从左到右 colspan = “2”，从上到下 rowspan = "2"

2. 删除被合并的空格

   ![](media\table2.jpg)

## 列表

### 1. ul ol 之间只允许插入 li 标签



### 2. 自定义列表

```html
<dl>
  <!-- dd 用于围绕 dt，一个 dt 对应多个 dd -->
  <dt>关于我们</dt>
  <dd>xxx</dd>
  <dd>xxx</dd>
  <dd>xxx</dd>
</dl>
```







## 表单

### input表单

- 作用域

```html
<form action="提交的目标" method="GET/POST" name="作用域名字" ></form>
```

#### 1. input 的 type 属性

![](media\input.jpg)

#### 2. name 属性

- 可以用于区分表单提交数据
- 单选和复选之间用于确定联系

#### 3. value 属性

- 表单提交时的值
- 输入框的value默认为空
- placholder 为占位符
- outline-style ： none 可以取消表单输入时的轮廓线

#### 4. checked

- 首次加载时被选中 常用于 单选复选

#### 5. maxlength 

- 输入范围的最大值

#### 6. label 标签

- **点击文字就可以选中对应的input**

```html
<label for="boy">男</label><input type="radio" name="gender" id="boy" />
<label for="girl">女</label><input type="radio" name="gender" id="girl" />
```





### 下拉列表 select

```html
<form>
  <select>
    <option selected>xxx</option> <!--默认选中状态-->
    <option>xxx</option>
    <option>xxx</option>
  </select>
</form>
```

### 文本域 textarea 







---



# CSS



## 样式表

### 1.	行内样式表

`<div style="xxx"></div>`

### 2.	内部样式表

```css
<style>

</style>
```

### 3.	外部样式表

```html
<link rel="stylesheet" href="xxx.css">
```





## CSS属性顺序（建议）

- ![](media\rules.jpg)





## 三大特性

### 层叠性 (样式冲突)

- 就近原则 后来居上

### 继承性 (子承父业)

- inherited  from xxx     继承自xxx的样式
- 只有部分样式可以被基础

### 优先级 (样式冲突)

- 优先级高的覆盖优先级低的样式

- 符合选择器的权重 先相加 再比较 0,0,0,1+ 0,1,0,0 = 0,1,0,1 > 0,0,999,999

- 权重相加不会有进位

- |       选择器        |    权重    |
  | :-----------------: | :--------: |
  |       继承、*       | 0，0，0，0 |
  |     元素选择器      | 0，0，0，1 |
  |   类选择器、伪类    | 0，0，1，0 |
  |      id选择器       | 0，1，0，0 |
  | 行内样式style=“xxx” | 1，0，0，0 |
  |     ！important     |    max     |

  

## 选择器

### 1.	标签选择器

### 2.	类选择器  .

### 3.	id选择器  #id

### 4.	通配符选择器 * 

### 5. 	后代选择器

```css
div sppan {}  中间用空格隔开
```

### 6.	子元素选择器

```css
div>span {}		只会选择div里最近一级的span
```

### 7.	并集选择器

```css
div,	         可以选择多个
span,
p {
  xxxx
}
```

### 8.	伪类选择器

#### 链接伪类选择器 ：

- :link	未被访问

- :visited	被访问

- :hover	鼠标悬停

- :active	鼠标按下未释放

#### 其他伪类选择器 :focus

- :focus		选取焦点
- :checked       选中

#### 结构伪类选择器

- :not(s)         匹配不含s选择器的元素
- :frist-child      父元素的第一个元素
- :last-child      父元素的最后一个元素
- :only-child      父元素的唯一一个元素
- nth-child(n)    父元素中第n个孩子 
  - odd奇数 
  - even偶数
- first-of-type    和 child 类似 但不会匹配选择的标签是否一致

### 9. 伪元素选择器(content属性)

- ::before
- ::after
- 不是真正意义的html元素在文档结构上无法找到
- ==必须有content属性==
- ==权重和标签选择器一样==
- xxx:hover::before { display: block }

### 10.	属性选择器

```css
div[xxx] {}  				只选择有xxx属性的div
div[xxx=1]{}  		只选择 xxx = 1 的 div
div[xxx^=hello] 	xxx值以hello开头
div[xxx$=hello]		xxx值以hello结尾
div[xxx*=hello]		xxx值包含hello
```









## font-family

- 有空格的字体名称用 单引号包含
- 多个字体之间用 逗号 隔开，优先检查第一个字体再系统中是否存在 再依次 往后



## font-style

- normal 		不显示斜体   常用于 <em> 标签 让他不斜体
- italic	          显示斜体



## text-decoration

- none				无效果
- underline        下划线
- overline           上划线
- line-through   删除线



## text-indent

- 单位常用em 
- 1em 就是当前的 字体大小
- 缩进2字符就是 2em



## line-height

- 行高 = 盒子高度  => 文字垂直居中

![](media\linheight.jpg)





## emmet语法 

```html
div*3
<div></div>
<div></div>
<div></div>

ul>li*2
<ul>
  <li></li>
  <li></li>
</ul>

div+span
<div></div>
<span></span>

.xxx
<div class="xxx"></div>

#xxx
<div id="xxx"></div>

自增符 $
.hello$*3
<div class="hello1"></div>
<div class="hello2"></div>
<div class="hello3"></div>

内容符 {}
.ul>li{$}*5
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
</ul>

```

```css
xxx {
  w100 => width: 100px;
}
```



## display

- block 块元素 、显示
- inline 行内元素
- inline-block 行内块元素
- none   隐藏、同时占用的位置消失

![](media\display.jpg)





## background

### 连写

```css
background: 背景颜色 背景图片 repeat 滚动 位置
```

![](media\bg.jpg)

### backgroun-color

- transparent 默认为透明
- #000、red、rgba

### background-img

- none 默认
- url(xxxxx.xx)

### background-repeat

- no-repeat 不平铺
- repeat       平铺
- repeat-x    横向平铺
- repeat-y    纵向平铺

### background-position

- x  y  数值
- 方位名词 top、bottom、center、left、right
- top left 为默认情况 相对于 （0，0）
- 只写一个方位名词的时候 另一个默认为center
- 混合单位   20px center  =>    （x，y）  

### background-attachment

- scroll 背景图片随着滚动条滚动
- fixed 背景固定在相对屏幕的位置



## 元素水平居中

- 块级元素   给定宽高 margin：xx  auto
- 行内元素 行内块元素  => 给父盒子添加 text-align：center



## 解决外边距合并

- 设置边框
- 设置内边距
- overflow：hidden





## box-shadow

```css
box-shadow: x y blur spread color (inset)
```

## text-shadow

```css
text-shadow: x y blur color
```





## 浮动

- 浮动之后具有行内块元素特点

- 脱离标准流

- 一浮全浮

- 浮动不能超越标准流

- 浮动不会压住标准流的文字

- 触发BFC

- 清除浮动

- ```css
  .clearfix:after,
  .clearfix:before{
          content: "";
          display: table;
      }
      .clearfix:after{
          clear: both;
      }
      .clearfix{
          *zoom: 1;
      }
  ```

- 





## 定位 position

### z-index

- 使用定位开启 z-index
- 默认为auto 、0
- 数值大的能遮盖数值低的



### static 静态定位

- 默认的定位，遵循标准流规则
- 没有偏移量



### relative 相对定位

- 默认位置为标准流位置。
- 偏移量以自身左上角为中心偏移
- 偏移前的位置仍占用，不脱标。



### absolute 绝对定位

- 脱离标准流
- 相对于父元素偏移（父元素需要定位 => 子绝父相）
- 父元素没有定位的情况下，会根据document进行偏移



### fixed

- 脱标
- 根据浏览器位置偏移
- 不会根据页面的滚动而滚动



### sticky

- 以窗口为参照偏移
- 占有原来的位置不脱标
- 必须使用 偏移 的其中一个
- （吸顶灯案例）





## visibility 显示与隐藏

- visible 显示
- hidden 隐藏  仍占用原来的位置 和 display：none 不一样





## overflow 溢出

- visible  默认不剪切内容也不隐藏 

- hidden  隐藏超出的内容
- scroll  用滚动条显示超出内容 默认有滚动条，即使没有超出
- auto   溢出才显示滚动条，否则不显示





## cursor 鼠标

- default
- pointer
- move
- text
- not-allowed



## vertical-align （可解决图片底部缝隙）

- 只适用于 行内元素 和 行内块元素
- 是与父元素的《文字》对齐方式
- baseline  默认 放置在父元素的基线上
- top  把元素的顶端和行中最高的元素顶端对齐
- middle 把元素放在父元素的中部
- bottom  .......
- 缝隙原因是图片底部默认和基线对齐。





## 单行溢出

```css
/*强制不换行*/
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```

## 多行溢出

```css
overflow: hidden;
text-overflow: ellipsis;
/*弹性伸缩盒子模型显示*/
display: -webkit-box;
/*限制行数*/
-webkit-line-clamp: 2;
/*设置或检索伸缩盒模型的子元素的排列方式*/
-webkit-box-orient: vertical;
```





# HTML5



## HTML5 新增标签 

- ie9 需要 转成 块级元素

- header 头部标签
- nav   导航标签
- article  内容标签
- section  定义文档某个区域
- aside  侧边标签栏
- footer  尾部标签
- ![](media\newtag.png)





## HTML5 多媒体标签

### video 视频

- ==autoplay="autoplay" ————自动播放==
- controls="conttrols"————显示播放控件
- width = "...px" 
- height = "...px"
- ==loop = "loop" ————播放结束继续循环==
- preload 
  - auto  预先加载视频
  - none 不预先加载
  - autoplay的情况下 该属性默认为 auto
- src ————视频路径
- poster————加载视频时的等待图片
- ==muted————静音播放==

```html
<video width="320" height="240" src="xxx.mp4" controls">

<!-- 依次往下查找能播放的视频格式，如果都不能播放则显示文字内容 -->
<video width="320" height="240" controls">
	<source src="xxx.mp4" type="video/mp4">                                
	<source src="xxx.webm" type="video/webm">                                
	<source src="xxx.ogg" type="video/ogg">
  您的浏览器不支持视频播放，请更换浏览器
</video>
```



### audio 音频

- 格式 mp3 > wav > ogg

- autoplay   ==谷歌浏览器默认禁止自动播放==
- controls
- loop
- muted
- preload
- src



## input 新增类型

| 属性值     | 说明                |
| ---------- | ------------------- |
| ==email==  | 只允许输入email类型 |
| url        | 只允许输入URL类型   |
| time       | 只允许输入time类型  |
| date       | 只允许输入date类型  |
| month      | 只允许输入month类型 |
| week       | 只允许输入week类型  |
| ==number== | 只允许输入数字类型  |
| ==tel==    | 只允许输入手机号码  |
| search     | 搜索框              |
| color      | 生成取色盘          |



## input 新增属性

| 属性         | 值         | 说明                 |
| ------------ | ---------- | -------------------- |
| ==required== | required   | 必填                 |
| placeholder  | 文本       | 占位符               |
| autofocus    | autofocus  | 加载后自动聚焦       |
| autocomplate | ==off==/on | 自动提示之前输入的值 |
| multiple     | multiple   | 选择多文件提交       |



## box-sizing

- content-box 默认
- border-box  内边距、边框不会撑开盒子



## filter 图片处理

- filter：blur（..px） 模糊



## calc盒子尺寸计算函数

```css
div{
  width: calc(100vw - 50px);
  height: calc(100% - 20px);
}
```





## transition 过渡

- ==经常和 :hover一起使用==

- ```css
  div {
    transition: css属性 time timing-fn delay
  }
  /*多属性 , 分隔*/
  div {
    transition: xxx 0.5s, xxx .8s
  }
  ```

- 属性：需要过渡的css属性 （所有属性 all）

  - width、height、transform 等等

- time：变化所需时间 （必须写单位秒s）

- timing-function：运动曲线 默认 ease 可以省略

  - linear 匀速
  - ease 逐渐减速==默认==
  - ease-in 加速
  - ease-out 减速
  - ease-in-out 加速再减速

- delay：延迟执行开始的时间 一般不需要



## transform 2D变形



- 连写 transform：==translate放最前==  rotate  scale

- translate 移动 不会影响其他元素
  - ==对行内元素无效==
  - translate（x, y）
  - translateX（x）
  - translateY（y）
- rotate(360deg) 旋转
- scale  缩放
  - ==不会影响其他盒子==
  - scale(2) 宽高同时设置
  - scale(w, h) ==宽高分别设置==
- transform-origin：旋转点
  - x  y => ==默认为 50%  50%==
  - 方位
    - top
    - bottom
    - center
    - left
    - right



## animation 动画

- delay 延迟 ==默认为0==

- timing-function 运动曲线
  - ==steps(n) 把动画等分成 n 份 会有一种卡顿的感觉==
  - 其他 和 transition 一样
- interation-count 播放次数：n | ==infinte无限循环==
- direction 是否反向播放：normal | ==alternate反向播放==

==定义动画==

```css

@keyframe name {
  from {xxx} /*等同于 0% 到 100% */
  to {xxx}
}

@keyframe name {
  0% {xxx}
  ·····
  ·····
  50% {xxx}
  ·····
  ·····
  100% {xxx}
}
```

==调用动画==

```css
div {
  animation: name | duration | timing-fn | delay | count | 
}
```

![](media\animation.png)





## transform 3D 变形

==坐标轴z轴单位最好只用 px==

![](media\3d.jpg)



- ==perspective 透视（视距）==
- 透视越小，相当于视距越小，物体会变大
- ==透视写在被观察元素的父盒子上==
- translate3D(x, y, z) 
- rotate3D(x, y, z , deg) ==旋转轴为原点到xyz向量方向==



- transform-style: flat ==3D变形时子元素默认不开启3D空间==
- ==transform-style: preserve-3D 子元素保持3D空间==