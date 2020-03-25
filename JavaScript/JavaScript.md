# 一.	运算

## 1.1	逻辑中断

### 1.1.1	逻辑与短路

- x1 && x2
- x1= ture return x2
- x1 = false return x1



### 1.1.2	逻辑或短路

- x1 || x2 || x3
- x1  true  return x1



## 1.2排序

### 1.2.1	冒泡排序

原理：从第一个元素开始，把当前元素和下一个索引元素进行比较。如果当前元素大，那么就交换位置，重复操作直到比较到最后一个元素

```javascript
    for (let i = 0; i < arr.length - 1; i++) {
            for (let j = i + 1; j < arr.length; j++) {
                if (arr[i] > arr[j]) {
                    let temp = arr[i]
                    arr[i] = arr[j]
                    arr[j] = temp
                }
            }
        }
```

### 1.2.2	选择排序

原理：遍历数组，设置最小值的索引为 0，如果取出的值比当前最小值小，就替换最小值索引，遍历完成后，将第一个元素和最小值索引上的值交换。如上操作后，第一个元素就是数组中的最小值，下次遍历就可以从索引 1 开始重复上述操作。

![img](.\img\sort2.gif)

```
    function selectSort(arr) {
      if (Array.isArray(arr)) {
        for (var i = 0; i < arr.length - 1; i++) {
          var minIdex = i;
          for (var j = i + 1; j < arr.length; j++) {
            minIdex = arr[j] < arr[minIdex] ? j : minIdex;
          }
          [arr[i], arr[minIdex]] = [arr[minIdex], arr[i]];
        }
        return arr;
      }
    }
```



### 1.2.3	插入排序

原理：第一个元素默认是已排序元素，取出下一个元素和当前元素比较，如果当前元素大就交换位置。那么此时第一个元素就是当前的最小数，所以下次取出操作从第三个元素开始，向前对比，重复之前的操作。

![img](.\img\sort3.gif)

```
    function insertSort(arr) {
      if (Array.isArray(arr)) {
        for (var i = 1; i < arr.length; i++) {
          var preIndex = i - 1;
          var current = arr[i]
          while (preIndex >= 0 && arr[preIndex] > c) {
            arr[preIndex + 1] = arr[preIndex];
            preIndex--;
          }
          arr[preIndex + 1] = current;
        }
        return arr;
      }
    }
```



### 1.2.4	快速排序

原理：在数据集之中，找一个基准点，建立两个数组，分别存储左边和右边的数组，利用递归进行下次比较。

![img](.\img\sort4.gif)

```
    function quickSort(arr) {
      if (!Array.isArray(arr)) return;
      if (arr.length <= 1) return arr;
      var left = [], right = [];
      var num = Math.floor(arr.length / 2);
      var numValue = arr.splice(num, 1)[0];
      for (var i = 0; i < arr.length; i++) {
        if (arr[i] > numValue) {
          right.push(arr[i]);
        } else {
          left.push(arr[i]);
        }
      }
      return [...quickSort(left), numValue, ...quickSort(right)]
    }
```



### 1.2.5	希尔排序

原理：

选择一个增量序列 t1，t2，……，tk，其中 ti > tj, tk = 1；

按增量序列个数 k，对序列进行 k 趟排序；

每趟排序，根据对应的增量 ti，将待排序列分割成若干长度为 m 的子序列，分别对各子表进行直接插入排序。仅增量因子为 1 时，整个序列作为一个表来处理，表长度即为整个序列的长度。

![img](.\img\sort5.jpg)

 

```
    function shellSort(arr) {
      var len = arr.length,
        temp,
        gap = 1;
      // 动态定义间隔序列，也可以手动定义，如 gap = 5；
      while (gap < len / 5) {
        gap = gap * 5 + 1;
      }
      for (gap; gap > 0; gap = Math.floor(gap / 5)) {
        for (var i = gap; i < len; i++) {
          temp = arr[i];
          for (var j = i - gap; j >= 0 && arr[j] > temp; j -= gap) {
            arr[j + gap] = arr[j];
          }
          arr[j + gap] = temp;
        }
      }
      return arr;
    }
```

### 1.2.6	归并排序

原理：

（1） 把长度为n的输入序列分成两个长度为n/2的子序列；

（2）对这两个子序列分别采用归并排序；

（3） 将两个排序好的子序列合并成一个最终的排序序列。

![img](.\img\sort6.gif)



```
    function mergeSort(arr) {  //采用自上而下的递归方法
      var len = arr.length;
      if (len < 2) {
        return arr;
      }
      var middle = Math.floor(len / 2),
        left = arr.slice(0, middle),
        right = arr.slice(middle);
      return merge(mergeSort(left), mergeSort(right));
    }

    function merge(left, right) {
      var result = [];
      while (left.length && right.length) {
        // 不断比较left和right数组的第一项，小的取出存入res
        left[0] < right[0] ? result.push(left.shift()) : result.push(right.shift());
      }
      return result.concat(left, right);
    }
```



# 二.	函数



## 2.1	函数的声明

### 2.1.1	直接声明

```javascript
function fn() {
  
}
```

### 2.2.2	表达式声明

```javascript
var fn = function() {
  
}
```

### 2.2.3	构造器声明

```javascript
var fn = new Function() {
  //自动调用构造函数
}
```



## 2.2	函数返回 return

- return 的值作为 函数调用的返回值
- ==return 中断函数不会继续执行后面的运算==
- ==每个函数都有返回值== 没有return则返回 ==undefind==



## 2.3	内置参数arguments

- 每一个函数都内置 arguments参数
- ==arguments 用于保存所有实参==
- ==arguments是一个伪数组==，不能使用数组的内置方法

```javascript
function fn() {
  console.log(arguments[0])		=> 1
  console.log(arguments[1])		=> 3
  console.log(arguments[2])		=> 5
}

fn(1, 3, 5)
```



## 2.4	作用域链

- 内部函数可以调用外部函数的数据
- 调用方式为链式调用，逐层往外找，就近原则

```javascript
var num =  10
function fn1() {
  var num = 20
  function fn2() {
    console.log(num)  => 20
  }
}
```



## 2.5	预解析

### 2.5.1	变量预解析（变量提升）

- 将变量名提升到作用域最前
- 并没有将赋值提升
- ==表达式声明的函数也同理==

```javascript
console.log(num)  => undefind
var num = 10

/*-------------------------------*/

var num
console.log(num)
num = 10
```



### 2.5.2	函数预解析（函数提升）

- ==直接声明函数==

```javascript
fn()
function fn() {
  ...
}
  
/*-------------------------------*/
  
function fn() {
  ...
}
fn()
```



# 三.	对象

## 3.1 函数和方法的区别

- 函数：单独存放的 function
- 方法：存放在某个对象里的函数 



## 3.2	创建对象

### 3.2.1	字面量

==var obj = { }==

```javascript
var obj = {
  name: 'Nelk',
  age: 18,
  gender: 'boy',
  say: function() { console.log('hello') }
}
```

### 3.2.2	new Object( )

==var obj = new Object( )==

```javascript
var obj = new Object()
obj.name = 'Nelk'
obj.age = 18
obj.say = function() { console.log('hello') }
```

### 3.2.3	构造函数创建对象

- ==构造函数名开头大写==
- 不需要return 会自动返回 一个 实例对象

```javascript
function Me(name, age) {
  this.name = name,
  this.age = age,
  this.say = function() { console.log('hello') }
}
var me = new Me('Nelk', 18)
```



## 3.3	遍历对象 for in

```javascript
var obj = {
  name: 'Nelk',
  age: 18,
  gender: 'boy',
  say: function() { console.log('hello') }
}

for(var k in obj) {
  console.log(k)          =>  键（属性名）
  console.log(obj[k])    	=>	值（属性值）
}
```





# 四.	内置对象、方法

## 4.1	Math

### 4.1.1	圆周率 Math.PI

```javascript
Math.PI = 3.1415926 · · ·
```



### 4.1.2	向下取整 ceil( )

```javascript
Math.ceil(1.9) = 1
```



### 4.1.3	向上取整 floor( )

```javascript
Math.floor(1.1) = 2
```



### 4.1.4	四舍五入 round( )

==注意负数的取舍==

```javascript
Math.round(-3.4) = -3
Math.round(-3.5) = -3
Math.round(-3.7) = -4
```



### 4.1.5	绝对值 abs( )

```javascript
Math.abs(-100) = 100
```



### 4.1.6	最大最小 max( ) min( )

```javascript
Math.max(1,2,3,4,5) = 5 
Math.min(1,2,3,4,5) = 1 
```



### 4.1.7	随机数 random( )

- 返回随机浮点数 [0, 1)
- ==两个数之间随机整数 并可以取到这两个数==

```javascript
Math.floor(Math.random() * (max - min + 1) ) + min
```



## 4.2 Date



### 4.2.1	参数

```javascript
view plainnew Date("month dd,yyyy hh:mm:ss");
new Date("month dd,yyyy");
new Date(yyyy,mth,dd,hh,mm,ss);
new Date(yyyy,mth,dd);

时间戳作为参数
new Date(ms);
```

```
month:用英文表示月份名称，从January到December
month:用整数表示月份，0-11 （1月-12月）
dd:表示一个月中的第几天，从1到31
yyyy:四位数表示的年份
hh:小时数，0 ~ 23
mm:分钟数，从0到59的整数
ss:秒数，从0到59的整数
ms:毫秒数，为大于等于0的整数，表示的是需要创建的时间和GMT时间1970年1月1日之间相差的毫秒数。
```



### 4.2.2 get方法

| 方法                   | 说明     |
| ---------------------- | -------- |
| getFullYear( )         | 完整年份 |
| getMonth( )            | 月份     |
| getDate( )             | 日期     |
| getDay( )              | 星期     |
| getHours( )            | 小时     |
| getMinutes( )          | 分钟     |
| getSeconds( )          | 秒       |
| getTime( )、valueOf( ) | 时间戳   |

### 4.2.3	时间戳 毫秒

==var time = +new Date(...)==

```javascript
var date = new Date()
date.valueOf() => 时间戳
date.getTime() => 时间戳

var time = +new Date() => 时间戳

Date.now() => 时间戳  H5新增
```





# 五.	数组

## 5.1	indexOf

- indexOf( item, start )
- 返回数组中某个指定元素的位置 （下标）
- item 为查找的内容
- start 不是必须的 不填则从头开始查找
- 找到返回下标，==没有找到返回 -1==

```javascript
let arr = [43, 23, 46, 13, 78, 95]
arr.indexOf(13) = 2
arr.indexOf(100) = -1
```





## 5.2	slice

- slice( start, end )

- 对数组的部分截取，并返回一个数组副本

- ==不会影响原数组==

- ==返回值是新的数组==

- start 为开始截取的位置

- 正数从前往后，负数从后往前

  ![](C:\Users\Nelk\Desktop\笔记\img\JavaScript\slice.png)

```javascript
let arr = [43, 23, 46, 13, 78, 95]
arr.slice(1) = [23, 46, 13, 78, 95]
arr.slice(-2) = [78, 95]
arr.slice(1,3) = [23, 46]
/* 本质就是从start到end 之间的 元素 */
```



## 5.3	splice

- splice( start, n, new )
- start 为 开始删除的位置
- n 为删除个数，不写则从start后删完
- ==n为0则不删除，可用于插入==
- new 为 删除后替换的元素
- ==会影响原数组，直接从原数组删除==
- ==返回被删元素==

```javascript
let arr = [43, 23, 46, 13, 78, 95]

arr.splice(1) = [23, 46, 13, 78, 95]
//arr = [43]

arr.splice(1,3) = [23, 46, 13]
//arr = [43, 78, 95]

arr.splice(1,2,100) = [23, 46]
//arr = [43, 100, 13, 78, 95]
```



## 5.4	for in 遍历

```javascript
for(let n in arr) {
  console.log(arr[n])
}
```



## 5.5	push

- 尾部增加
- 可以增加一个==或者多个==
- ==返回新数组的长度==

```javascript
let arr = [1, 3, 5, 7]
arr.push(100)
//arr = [1, 3, 5, 7, 100]
```



## 5.6	pop

- ==删除最后一个==
- ==返回被删除的元素==

```javascript
let arr = [1, 3, 5, 7]
arr.pop()
//arr = [1, 3, 5]
```



## 5.7	unshift

- 头部增加
- 可以增加一个==或者多个==
- ==返回新数组的长度==

```javascript
let arr = [1, 3, 5, 7]
arr.push(99, 100)
//arr = [99, 100, 1, 3, 5, 7, 100]
```



## 5.8	shift

- ==删除第一个==
- ==返回被删除的元素==

```javascript
let arr = [1, 3, 5, 7]
arr.shift()
//arr = [3, 5, 7]
```



## 5.9	concat 数组拼接

- ==不会影响原数组==
- ==返回拼接的新数组==

```javascript
let arr1 = [1, 3, 5]
let arr2 = [2, 4, 6]
console.log(arr1.concat(arr2))
//[1, 3, 5, 2, 4, 6]
```



## 5.10	(...array)数组拼接

- ...代表可变参数，会把数组元素逐一取出来push
- ==在原来的数组上拼接==

```javascript
let arr1 = [1, 3, 5]
let arr2 = [2, 4, 6]
arr1.push(...arr2)
//arr1 = [1, 3, 5, 2, 4, 6]
```



## 5.11	join

- 把所有元素拼接成字符串
- 不指定分隔符，默认用 逗号 分割
- ==不影响原数组，返回拼接的字符串==

```javascript
let arr = [i, love, you]
arr.join()		// i,love,you
arr.join('-') // i-love-you
arr.join(' ') // i love you
```



## 5.12	sort 还没理解





# 六.	字符串

## 6.1	indexOf

- indexOf( 'item', start )
- 返回第一次查询结果的位置
- ==字符串位置从0开始==
- 每个字符（包括标点符号）都占1位

```javascript
let str = '你好，我是Nelk，我18岁。'
str.indexOf('我') = 3
str.indexOf('我', 5) = 10
```



## 6.2	slice

- slice( start, end )
- 支持负数位置
- ==不会影响原字符串，返回截取的字符串==
- ==按位截取==
- substing( ) 不支持负数

![](.\img\JavaScript\slice2.png)

```javascript
let str = '你好，我是Nelk，我18岁。'
str.slice(1, 5)
// 好，我是
```



## 6.3	substr

- substr( start, length )
- 截取字符串，无指定长度默认截取到末尾
- ==不会影响原字符串，返回截取字符串==
- ==按长度截取==

```javascript
let str = '你好，我是Nelk，我18岁。'
str.substr(1, 5)
// 好，我是N
```



## 6.4	split

- split( separator, limit )
- 分割字符串转成数组
- separator：可以是字符串、正则表达式
- limit：限制分割片段数量
- ==用于分割的内容不会加入数组元素==
- 不会影响原字符串，==返回数组==

```javascript
let str = '你好，我是Nelk，我18岁。'
var arr = str.split('，')
// arr= ['你好', '我是Nelk', '我18岁']
```



## 6.5	charAt

- charAt( index )

- 返回指定位置的字符

  ```javascript
  let str = '你好，我是Nelk，我18岁。'
  str.charAt(0) = '你'
  str.charAt(10) = '我'
  ```



## 6.6	replace

- replace( separator, str )
- separator：可以是字符串、正则表达式
- str：替换内容
- 不会影响原字符串，==返回新字符串==

```javascript
let str = '你好，我是Nelk，我18岁。'
str.replace('，', '--')
//你好--我是Nelk--我18岁。
```



## 6.7	toUpperCase 

- 全部改成大写
- 不会影响原字符串，==返回新字符串==



## 6.8	toLowerCase

- 全部改成小写
- 不会影响原字符串，==返回新字符串==