#  一.	Vue初识 

## 1.1	渐进式

## 1.2	Model ViewModel View

- ViewModel 作为桥梁 为 Model 和 View 进行通信
- Vue充当的角色就是ViewModel
- ![](media\mvvm.jpg)
- 操作一：数据绑定（model数据进行解析绑定到DOM）
- 操作二：对DOM进行监听数据变化
- ![](media\mvvm2.jpg)



## 1.3	虚拟DOM

- Vue在进行DOM的渲染时，会在内存创建一个虚拟DOM
- 再重新渲染的时候，虚拟DOM会先看看内部是否有同样的DOM元素存在，有直接==复用==该DOM元素，没有才会重新创建
- 不希望复用就绑定一个 key ，就不会复用。常用于v-for
- ==diff算法==    绑定key以更好的复用 ==高效更新虚拟DOM==
  - 没有key时，往中间插入新值，会把序号依次往后位移
  - 有key时，会先对比key对应的东西是否有变化，没有则直接复用，最后才会创建新的结点将元素插入
  - ==key不能绑定index，因为数据数量变化，index也会变==

![](media\diff.jpg)



## 1.4	Vue的 options

### 1.4.1	el

- 决定了这个Vue实例用于管理哪一个DOM

- el: string | element
- 字符串 => 自动调用 document.querySelector(  ) 得到dom元素再传入
- dom元素 => 直接传入



### 1.4.2	data

- Vue实例的对象可以是 Object | function
- ==组件的 data 必须是 一个函数==，函数有自己的作用域，因为组件复用，避免数据耦合



### 1.4.3	methods

- 是一个对象

- 每个属性都必须是方法

  ```javascript
  methods: {
    fn1: function() {
      ......
    },
    fn2() {  <!--es6对象解构写法-->
      ......
    }
  }
  ```



## 1.5变量作用域



## 1.6	runtime-only	*

- ==代码中不能使用template==

## 1.7	runtime-complier

- ==代码中可以包含 template==
- 有 complier 可以 编译 template



# 二.	生命周期

- new Vue( )创建实例时 就开始进行生命周期
- 生命周期每个过程都会对vue实例进行回调

![](media\life.png)



##  2.1	created( )

- ==一般网络请求在created实现==



## 2.2	mounted( )

- 当vue实例被挂载到DOM上回调





# 三.	基本语法

## 3.1	mustache语法

- =={{ 表达式 }}== // 加减乘除调用方法等等
- {{ data }}  匹配data的值
- {{ #data }} {{name}} {{/data}}  = {{data.name}}  定义代码块
- {{^data}} {{/data}}  => 当 data为null、underline、false 才渲染
- {{ . }}  可以遍历整个数组 {{#data}} {{ . }} {{/data}}
- {{>data}} 作为子模块
- {{{data}}} 作为文本 不作为变量
- {{ ! 注释 }} 不会渲染出来



## 3.2	v-once

- ==只会渲染一次，不会响应数据变化==

```html
<div v-once >{{ msg }}</div>
```



## 3.3	v-html

- 会把数据以html标签进行解析
- 一般当数据有html标签才使用
- ==会把标签中间所有内容覆盖==

```html
<div v-html="url">
  
</div>
```

```javascript
new Vue({
  el:'#app',
  data: {
    url: '<a url="#">点我</a>'
  }
})
```



## 3.4	v-text

- 把数据以字符串进行渲染
- 和mustache语法基本一样
- ==一般不用，因为会把标签中间的所有内容覆盖掉==



## 3.5	v-pre

- 原封不动将内容渲染出来
- 不会解析 {{ }} 语法

```html
<h1 v-pre> {{hello}} </h1>
```





## 3.6	v-cloak

- 斗篷(一般也用不到)
- 浏览器解析 {{ }} 语法时先 显示 {{xxx}} 再解析替换
- 如果当前网页卡顿时候就会显示出 {{xxx}} 再闪现成 真正内容，这样对用户体验不友好
- 在vue解析之后会自动将 v-cloak 删除

```html
<style>
[v-cloak] {
	display: none
}
</style>


<h2 v-cloak>{{data}}</h2>
```



## 3.7	v-bind *

- ==动态绑定属性==
- v-bind:属性名="xxx"
- ==语法糖 :属性名="xxx"==

```html
<img src="xxx.jpg"/> 直接把xxx.jpg 作为 字符串绑定
<img v-bind:src="img"/>	解析img变量的值绑定到src
<img :src="img?/>
```

### 3.7.1	v-bind 绑定 class

-  :class="{key: boolean}"

- ==用变量来决定Boolean值==
- 多类名之间逗号隔开
- ==class 和 :class 会进行合并，不会覆盖==
- 对象语法：

```html
<div :class="{xxx1: true, xxx2: false}">
  <!-- 此处添加了xxx1，没有xxx2 -->
</div>

<div class="xxx1" :class="getClass()">
  <!-- 此处添加了xxx1,2,3 进行合并-->
</div>
```

```javascript
methods:{
  getClass() {
  	return {xxx1: true, xxx2: true}
	}
} 
```

- ==数组语法：一般不用==

```html
<div :class="[class1, class2]">
  <!-- 作为变量解析 -->
</div>

<div :class="['class1', 'class2']">
  <!-- 作为字符串解析 -->
</div>
```



### 3.7.2	v-bind 绑定 style

- 对象语法
- 多个值以逗号分隔

```html

<div :class="{font-size: '50px', color: 'red'}">
  <!-- 需要注意值是字符串，不是变量 -->
</div>

  <!-- 一般动态样式使用变量 -->
<div :style="fontSize: fs + 'px' ">
  <!-- 属性可以是驼峰写法 -->
</div>

<script>
export default {
  data() {
    return {
      fs: 100	
    }
  }
}
</script>
  
```



## 3.8 v-for	*

- ==遍历数组==
- v-for="(item,index) in  data"

```html
<ul>
	<li v-for="(item,index) in  data">{{item}}</li>
</ul>

```

- ==遍历对象==
-  v-for="(value,key,index) in  data"
- index 可以取得索引，但几乎不使用

```html
<ul>
  <li v-for="(value, key) in  data">{{value}}</li>
</ul>
```

- ==添加key==

```html
<!--  -->
```





## 3.8	v-on

### 3.8.1	基本使用

- v-on:监听方法=" "
- 语法糖 @监听方法=" "

```html
<button v-on:click="num++">加1</button>
<button @click="num--">减1</button>
<!-- 此处的num是一个变量 -->
```



### 3.8.2	事件对象

- 调用 通过methods 定义的方法
- 调用方法时用 ==$event== 传入 事件对象
- ==没有参数可以不加（）==会自动把==事件对象==传到函数里

````html
<button v-on:click="increasement">加1</button>
<button @click="decreasement(5)">减5</button>

<script>
export default {
  data() {
    return {
      num: 0
    }
  },
  methods: {
    increasement(event) { 		//事件对象自动传入
      console.log(event) 
      this.num++
    },
    decreasement(n) {				//
      this.num -= n
    }
  }
}
</script>
````



### 3.8.3	修饰符

- v-on:监听方法.修饰符="xxx"

- ==.stop==	调用event.stopPropagation( ) ==阻止冒泡==
- ==.prevent==.    调用event.preventDefault( )  ==阻止默认行为==
- ==.native==    监听==组件根元素==的原生事件
- ==.once==    只触发一次回调（只监听一次）
- ==.[asciicode | alias ]== 监听某个键盘按键 可以直接写别名
- .capture    捕获事件 从==最外层==的父元素开始执行
- .self    只会执行本身的函数
- 修饰符串联：==有先后顺序==，可能出错

```html
<input type="submit" value="提交" v-on:click.prevent.once />
```





## 3.9	v-if、v-else

- ==v-if="true/false"==
- v-else-if="true/false"    用得不多
- ==v-else==
- 通过控制boolean值控制是否渲染

```html
<h2 v-if="true">我会被渲染</h2>
<h2 v-else>我不会被渲染</h2>

<h2 v-if="false">我不会被渲染</h2>
<h2 v-else>我会被渲染</h2>

<!--不建议使用else-if，复杂操作用计算属性 -->

<h2 v-if="score>=90">优秀</h2>
<h2 v-else-if="score>=80">良好</h2>
<h2 v-else-if="score>=70">一般</h2>
<h2 v-else-if="score>=60">及格</h2>
<h2 v-else>不及格</h2>
```



## 3.10	v-show

- ==必定渲染==
- 通过控制boolean值来决定是否显示
- 显示和隐藏 display：none、block
- ==需要频繁切换显示隐藏，使用v-show==  性能更高
- ==只有一次切换使用 v-if== 隐藏则从dom上删除





## 3.11	v-model 

### 3.11.1 基本使用

- ==表单控件==双向绑定 input、selector、textarea、button...
- ==复选框定义为一个空数组==
- ==下拉框绑定到 selector==
- 多选下拉框，定义为数组，selector添加multiple属性
- ==多选表单值绑定==，不要写死数据，应该动态获取 再v-bind绑定

```html
<input v-model="msg" />

<script>
export default {
  data() {
    return {
      msg: 'hhh'
    }
  }
}
</script>
```

- ==实现原理 绑定变量，监听input方法==

```html
<input :value="msg" @input="change" />

<script>
export default {
  data() {
    return {
      msg: 'hhh'
    }
  },
  methods: {
    change(event) {
      this.msg = event.target.value
    }
  }
}
</script>
```



### 3.11.2	selector的使用

### 3.11.3	textarea的使用

### 3.11.4	修饰符

- ==.lazy==	输入框失去焦点或者按回车才会更新数据
- ==.number==   v-model给变量赋值默认都是string类型
- ==.trim==    自动删除输入框两边的空格





## 3.12	v-slot

### 3.12.1	匿名插槽基本使用

- 在组件中使用 slot 标签预留插槽
- slot 标签中可以预留默认内容
- 无放置插槽则显示默认内容，有放置则覆盖默认内容
- 父组件使用 子组件的标签中 使用 template标签来替换插槽

```html
<!-- 父组件 -->
<div>
  <cpn>
  	<template>我是替换的内容</template>
  </cpn>
</div>

<!-- 子组件 -->
<div>
  <slot>
  	我是默认内容
  </slot>
</div>
```





### 3.12.2	具名插槽

- slot 标签 加上 name 属性
- template 标签 使用 v-slot 绑定具名插槽

```html
<!-- 父组件 -->
<div>
  <cpn>
  	<template v-slot:name>我是替换姓名的内容</template>
  	<template v-slot:age>我是替换年龄的内容</template>
  </cpn>
</div>

<!-- 子组件 -->
<div>
  <slot name="name">姓名</slot>
  <slot name="age">年龄</slot>
</div>
```



### 3.13.2	作用域插槽

- 子组件通过 slot 标签 将数据传到父组件

- 父组件 通过 v-slot:xxx="xxx" 接收

  ```html
  <!-- 父组件 -->
  <div>
    <cpn>
    	<template v-slot:name="slotProps">
        {{slotProps.userName}}  <!-- Nelk -->
      </template>
    </cpn>
  </div>
  
  <!-- 子组件 -->
  <div>
    <slot name="name" :userName="Nelk">姓名</slot>
  </div>
  ```

  







# 四.	选项

## 4.1	name



## 4.2	data

### 4.2.1	为什么必须是函数

- 不可以访问Vue实例的数据 （顶层的data）
- ==组件有属于自己的数据==
- 考虑到组件的复用，data是函数可以有自己的作用域
- 这样不会造成数据==耦合==。
- ==否则每个组件对应的数据都是指向同一个数据对象==





## 4.x	watch

## 4.x	computed 计算属性

- ==对于数据进行某种复杂变换==
- 是一个对象
- 元素都是函数，函数名一般不加动词==(不完整)==
- getFullName  => fullName ==不当成函数==而是当成==属性==
-  在 {{ fullName }} 不需要加（）调用
- 同一个==计算属性只会调用一次==，然后把结果加入==缓存==，相比函数每次调用都重新执行，==提高了性能==

```html
<h2>{{fullName}}</h2>

<script>
export default {
  data() {
    return {
      firstName: 'Nelk',
      lastName: 'Lin'
    }
  },
  computed: {
    fullName() {
      return this.firstName + ' ' + this.lastName
    }
  }
}
</script>
```

- ==完整的计算属性 是 一个对象==
- 解析时会自动调用 get 方法 
- 几乎不使用set方法，==作为只读属性==

```html
<h2>{{ fullName }}</h2>

<script>
export default {
  computed: {
    fullName: {
      getter() {		//get方法
        ......
      },
      setter() {		//set方法，一般不使用
        ......
      }
    }
  }
}
</script>
```



## 	filters

- 过滤器，对象
- 元素是函数，需返回值
- 无需调用，看作一个属性，会自动把需要过滤的数据传入

```html
<h2>{{ price | finalPrice }}</h2>
<!-- ¥20.00 -->

<script>
export default {
  data:() {
  	return {
  		price: 20
		}
}
  dilters: {
    finalPrice(n) {
      return ¥ + n.toFixed(2) 
    }
  }
}
</script>
```





# 五.	组件通信

## 5.1	props 父传子

- 父组件在子组件标签里 通过 ==v-bind:xxx="data"==
- 没有通过v-bind 会直接把字符串传过去
- 子组件可以在自己的选项中用==props接收==
- ==发送的属性名和接收的属性名必须一致==
- 可以使用驼峰命名（:my-name）=> myName
- props：['xxx', 'xxx', 'xxx'] 不能指定类型和默认值、required必须
- props：{'xxx': {type: Array, default(){return [ ] } } }
- 类型是 Object | Array 的default必须是一个函数的return值
- String、Number、Boolean、Array、Object、Date、Function、Symbol

```html
<!-- 父组件 -->
<div>
  <cpn :name="Nelk"></cpn>
</div>

<!-- 子组件 -->
<h2>{{name}}</h2>

<script>
export default {
  props: {
    name: {
      type: String,
      default: ''
    }
  }
}
</script>
```



## 5.2	$emit 子传父

- 子组件发生了什么事件，发送给父组件，可以传递数据
- ==this.$emit('xxxx', ...args)==
- 子组件发送 xxx 事件
- 父组件在子组件标签内 用 v-on监听xxx事件

```html
<!-- 子组件 -->
<button @click="itemClick"></button>

<script>
export default {
	methods: {
    itemClick() {
      this.$emit('iClick', 'hello')
    }
  }
}
</script>

<!-- 父组件 -->
<div>
  <cpn @iClick="cpnClick"></cpn>
</div>
<script>
export default {
	methods: {
    cpnClick(msg) {
      console.log(msg)
    }
  }
}
</script>
```



## 5.3	$refs	*

- this.$refs="xxx" 访问 ==ref 属性===为xxx子组件
- 访问子组件对象
- ref = reference 引用

```html
<div>
  <cpn ref="child"></cpn>
</div>

<script>
console.log(this.$refs.child)
</script>
```



## 5.4	$children

- this.$children 选择所有子组件 ==伪数组== 通过索引获取
- 一般不用，因为索引可能会变，不适合复用



### 5.5	$parent

- 访问父组件对象
- 一般也不用、耦合度高



### 5.6	$root

- ==访问根组件 顶层的 Vue实例对象==

# n.	响应式

## 哪些数组操作方法是响应式的

- ==通过索引修改数组不是响应式的== 但数组已经发送变化

- push
- pop
- unshift
- shift
- slice
- splice
- ==Vue.set ( target, key, value)==