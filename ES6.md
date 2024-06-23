# ES6



[TOC]













> [ES6从入门到精通](https://www.bilibili.com/video/BV1Bh4y1q73A)

## 1.什么是ECMAScript？

​     主流浏览器都支持ES6～ES13

## 4.数据类型

```javascript
/*对象*/
let boy = {
    name: "David",
    age: 28,
    weight: 70.5
}
console.log("boy", boy)
```

## 5.函数

###### 函数定义默认值

```js
/*默认值*/
function getPage(page = 1) {
    return page
}
console.log("getPage - 默认值", getPage())
console.log("getPage", getPage(6))
```

###### 箭头函数

```js
/*箭头函数 [箭头函数是一种匿名函数]*/ = (a, b) => a + b
console.lo
let plus = (a, b) => { //省略 function 添加 =>
    return a + b
}
console.log("plus", plus(5, 10));

/*隐式返回 [在函数体内只有一个表达式的情况下, 可以省略花括号 {} 和 return 关键字]*/
let plus2 = (a, b) => a + b
console.log("plus2", plus2(10, 20))
```

## 6.数组

######   数字排序

```js
/*数组中的元素按照数字排序*/
let arr3 = [5, 20, 13, 1, 4]
//arr3.sort() //默认情况下 sort() 方法使用字符串排序, 导致并没有按照数字大小排序
/*
    比较函数 (a, b) => a - b 接收两个参数 a 和 b, 用于比较这两个元素的大小, 返回 a - b 的结果决定了 sort() 方法的排序顺序
    若 a < b, 则 a - b 是一个负数, 表示 a 应该在 b 前面
    若 a = b, 则 a - b 是 0, 位置保持不变
    若 a > b, 则 a - b 是一个正数, 表示 a 应该在 b 后面
*/
arr3.sort((a, b) => a - b)
```

###### 数组筛选，返回数组

```javascript
//筛选符合条件的元素, 返回一个新的数组
let arr4 = [10, 11, 12, 13, 14, 15]
let newArr = arr4.filter((value, index) => {
    return value > 12
})
console.log("newArr", newArr) //[13, 14, 15]
```

###### 数组遍历

```javascript
//使用for...of循环遍历数组
let arr6 = ["邓瑞", "dengruicode.com", 100]
/*数组可以包含不同的数据类型*/
for (let item of arr6) {
    console.log("for...of", item)
}

//使用forEach方法来遍历数组
arr6.forEach((value,index) => {
    console.log("forEach", value,"index", index)
})
```

## 7.Set集合、扩展运算符

###### set基本操作

- add()
- delete()
- has()

###### 扩展运算符

```javascript
//使用扩展运算符将 Set集合 转换为 数组
let arr2 = [...fruits]
console.log("arr2", arr2)

//扩展运算符是用于展开可迭代对象(如数组、字符串等)
//let web = 'dengruicode.com'
let web = '邓瑞编程'
let webArr = [...web] //使用扩展运算符将 字符串 转换为 数组
console.log("webArr", webArr) //['邓', '瑞', '编', '程']
```

###### 数组集合转换

```javascript
//将 数组 转换为 Set集合 实现数组去重
let numberArr = [1, 2, 3, 3, 2, 1]
let numberSet = new Set(numberArr)
console.log(numberSet)
```

## 8.Map 集合

###### map基本操作

- set()
- delete()
- has()

###### map集合转换

```javascript
//创建Map集合
//let person = new Map() //创建一个空的Map集合
let person = new Map([
    ["name", "邓瑞"],
    ["gender", "男"],
    ["web", "dengruicode.com"]
])
//将Map集合转换为数组
let arr = Array.from(person)
console.log("arr", arr)

//使用扩展运算符将 Map集合 转换为 数组
let arr2 = [...person]
console.log("arr2", arr2)

```

###### map解构

```javascript
//使用for...of循环遍历Map集合
//解构可以从数组或对象中提取值并赋给变量
//[key, value] 就是一种解构语法, 用于将 Map 集合中的键值对解构为 key 和 value 两个变量
for (let [key, value] of person) {
    console.log("for...of", key, value)
}

//不使用解构，使用forEach方法遍历Map集合的键值对
person.forEach((value, key) => {
    console.log("forEach", key, value)
})
```

## 9.对象

###### 添加属性

```js
let person = {
    name: "邓瑞",
    gender: "男",
    web: "dengruicode.com",
}

//向对象中添加新的属性
person.height = 175
```

###### 删除数据

```js
//删除属性
delete person.gender
console.log("person", person)
```

###### 检查属性有没有包含

```js
//检查对象是否包含指定属性
let has = "gender" in person
console.log("has", has)
```

###### 获取对象属性数量

```js
//获取对象的属性数量
console.log("keysArr", Object.keys(person)) //Object.keys() 用于获取对象属性名的数组
console.log("length", Object.keys(person).length)
```

###### 遍历

```js
//使用for...in循环遍历对象 
//for...of 用于遍历可迭代对象[如数组、Set、Map、字符串等]
//for...in 用于遍历对象的可枚举属性
for (let key in person) {
    console.log("for...in", key, person[key])
}

//使用forEach方法遍历对象的属性和值
Object.entries(person).forEach(([key, value]) => {
   console.log("forEach", key, value)
})
```

清空对象

```js
//清空对象
person = {}
console.log("length", Object.keys(person).length)
```

## 13.解构

###### 取出最后一个元素

###### 扩展运算符

###### 默认值

###### 两数字交换

###### 对象解构

###### 重命名

###### 默认值

```javascript
//取出最后一个元素
let [, , c] = [10, 20, 30]
console.log("c:", c)

//扩展运算符
let [A, ...B] = [1, 2, 3, 4, 5, 6]
console.log("A:", A, "B:", B)

let [x2, y2 = 200] = [100] //默认值
console.log("x2:", x2, "y2:", y2)

//两数交换
let x3 = 10
let y3 = 20; //不加分号会报错
[x3, y3] = [y3, x3]
console.log("x3:", x3, "y3:", y3)

//--- 对象解构
let person = {
    name: '邓瑞',
    gender: '男',
    web: 'dengruicode.com'
}

let { name } = person
console.log("name:", name)

//重命名
let { name: userName, gender, web } = person
console.log("userName:", userName, "gender:", gender, "web:", web)

//默认值
let { address = "安徽" } = person
console.log("address:", address)
```



## 15.Promise

`Promise` 表示承诺在未来的某个时刻可能会完成并返回结果

对于某些需要时间来处理结果的操作, 如**用户登录**、读取文件等, 可以使用Promise 对象来执行**异步操作**。

`Promise` 对象有三种状态 `pending`(待处理)、`fulfilled`(已履行)、`rejected`(被驳回)

当创建一个 `Promise` 对象时, 它的初始状态为 pending, 表示异步执行还未完成

当异步执行成功时, 会调用 resolve 函数把 Promise 对象的状态改变为 fulfilled, 可通过 then 方法来获取异步操作的结果。

当异步执行异常时, 会调用 reject 函数把 Promise 对象的状态更改为 rejected, 可通过 catch 方法来处理错误

注：异步操作是指在程序执行过程中, 某个操作不会立即返回结果, 而是需要一段时间的等待

```javascript
let promise = new Promise((resolve, reject) => {
    //resolve("邮件发送成功")
    reject("邮件发送失败")
}).then(result => {
    console.log("result:", result)
}).catch(error => {
    console.log("error:", error)
}).finally(() => {
    console.log("异步执行结束")
})
```

## 16.Fetch

`fetch` 是基于 `Promise` 的 api, 它可以发送`http`请求并接收服务器返回的响应数据。

`fetch` 返回的是一个 `Promise` 对象

```javascript
//get请求
fetch('http://127.0.0.1/get').then(response => {
    //返回的解析后的json数据会传递给下一个 then() 方法中的回调函数作为参数,这个参数就是 data
    return response.json() //response.json() 用于将响应数据解析为json格式的数据
}).then(data => { //data 解析后的json数据
    console.log("get.data:", data)
}).catch(error => {
    console.log("get.error:", error.message)
}).finally(() => {
    console.log("get.finally")
})

//post请求 post
fetch('http://127.0.0.1/post', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded'
    },            
    body: new URLSearchParams({
        //URLSearchParams 用于处理键值对类型的数据,
        //并将其编码为url查询字符串
        name: '邓瑞',
        web: 'dengruicode.com',
    }),
}).then(response => {
    return response.json()
}).then(data => {
    console.log("post.data:", data)
}).catch(error => {
    console.log("post.error:", error.message)
}).finally(() => {
    console.log("post.finally")
})

//post请求 postJson
fetch('http://127.0.0.1/postJson', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
    },
    body: JSON.stringify({
        //JSON.stringify 用于将对象转换为json字符串
        name: '邓瑞编程',
        web: 'www.dengruicode.com',
    }),
}).then(response => {
    return response.json()
}).then(data => {
    console.log("postJson.data:", data)
}).catch(error => {
    console.log("postJson.error:", error.message)
}).finally(() => {
    console.log("postJson.finally")
})
```

## 17.安装和配置Node.js

###### 下载地址

[nodejs.org](https://nodejs.org/)

###### 查看安装的版本

node -v

npm -v



###### 查看当前镜像源

npm get registry



###### 设置淘宝镜像源

npm config set registry https://registry.npmmirror.com/



> Node.js是一个开源的JavaScript运行时环境, 用于在服务器端运行JavaScript代码
>
> npm(Node Package Manager)是Node.js包管理器, 用来安装各种库、框架和工具
>
> 比如: npm install axios
>
> `<script src="https://unpkg.com/axios/dist/axios.min.js"></script>`

## 18.Axios

Axios 是基于 Promise 的网络请求库, 它可以发送http请求并接收服务器返回的响应数据

Axios 返回的是一个 Promise 对象

Axios 不仅可以用于浏览器, 也可以用于 Node.js, 而 Fetch 主要用于浏览器

```javascript
//get请求
axios.get('http://127.0.0.1/get').then(response => {
    console.log("get.data:", response.data)
}).catch(error => {
    console.log("get.error:", error)
}).finally(() => {
    console.log("get.finally")
})

//post请求 post
let data = { //参数
    name: '邓瑞',
    web: 'dengruicode.com',
}

axios.post('http://127.0.0.1/post', data, {
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded'
    }
}).then(response => {
    console.log("post.data:", response.data)
}).catch(error => {
    console.log("post.error:", error)
}).finally(() => {
    console.log("post.finally")
})

//post请求 postJson [axios 的默认请求头是 application/json]
axios.post('http://127.0.0.1/postJson', data).then(response => {
    console.log("postJson.data:", response.data)
}).catch(error => {
    console.log("postJson.error:", error)
}).finally(() => {
    console.log("postJson.finally")
})
```

## 19.模块化开发

```javascript
模块化开发是指将复杂的代码拆分为独立的模块,每个模块负责完成特定的功能,
不同的模块之间可以通过使用export关键字将代码导出为模块,其他模块可以使用import关键字导入该模块

------ import、export
//index.js
let title = "邓瑞编程"
let web = "dengruicode.com"

/*
let getWeb = () => {
    return "www.dengruicode.com"
}
*/
let getWeb = () => "www.dengruicode.com"

export { title, web, getWeb } //将多个变量或函数分别导出

<script type="module">
    //从 index.js 文件中导入 title、web、getWeb 变量/函数
    import { title as webTitle, web, getWeb } from './index.js'

    console.log(webTitle)
    console.log(web)
    console.log(getWeb())
</script>

------ default
//index.js
let title = "邓瑞编程"
let web = "dengruicode.com"

let getWeb = () => "www.dengruicode.com"

//将一个对象作为整体导出, 导出的对象包含 title、web、getWeb 三个属性
export default { title, web, getWeb }

<script type="module">
    import obj from "./index.js"

    console.log(obj.title)
    console.log(obj.web)
    console.log(obj.getWeb())
</script>

------ as
//index.js
let title = "邓瑞编程"
let web = "dengruicode.com"
let getWeb = () => "www.dengruicode.com"
export { title, web, getWeb } //将多个变量或函数分别导出

<script type="module">
    import * as obj from "./index.js"

    console.log(obj.title)
    console.log(obj.web)
    console.log(obj.getWeb())
</script>
```

注

  import * as obj 用于避免命名冲突

  VSCode扩展: Live Server

## 20.async、await 使用同步的方式编写异步代码

### 同步

   代码按照编写顺序逐行执行,后续的代码必须等待当前正在执行的代码完成之后才能执行

   当遇到耗时的操作(如网络请求等)时,主线程会被阻塞,直到该操作完成



   举例

   在单车道路段上发生交通事故导致交通堵塞, 只有拖走事故车辆后, 后续车辆才能继续行驶



### 异步

   当遇到耗时的操作发生时, 主线程不会被阻塞, 主线程会继续执行后续的代码, 而非等待耗时操作完成



   举例

   在具有多车道的高速公路上, 发生交通事故后, 可以走其他车道继续行驶



### async

   当一个函数被标记为 async 后, 该函数会返回一个 Promise 对象

### await

   只能在 async 函数内部使用, 加上 await 关键字后, 会在执行到这一行时暂停函数的剩余部分，

   等待网络请求完成,然后继续执行并获取到请求返回的数据



```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script src="axios/dist/axios.min.js"></script>
</head>

<body>
  <script>

    //回调地狱是指过度使用嵌套的回调函数,导致代码难以阅读和维护
    //get请求
    axios.get('http://127.0.0.1/get').then(response => {
      console.log("get.data:", response.data)
      if (response.data.data.web == "dengruicode.com") {

        //get请求2
        return axios.get('http://127.0.0.1/article/get/id/1').then(response2 => {
          console.log("get2.data:", response2.data)
          if (response2.data.data.name == "邓瑞") {

            //get请求3
            return axios.get('http://127.0.0.1/article/get/search/title/入门').then(response3 => {
              console.log("get3.data:", response3.data)
            })
          }
        })
      }
    }).catch(error => {
      console.log("get.error:", error)
    }).finally(() => {
      console.log("get.finally")
    })

    //async/await 使用同步的方式编写异步代码, 避免回调地狱
    //优势 在处理多个异步操作的情况下, 可以使代码更简洁易读
    const getData = async () => {
      try {
        //get请求
        const response = await axios.get('http://127.0.0.1/get')
        console.log("async.get.data:", response.data)
        if (response.data.data.web === "dengruicode.com") {

          //get请求2
          const response2 = await axios.get('http://127.0.0.1/article/get/id/1')
          console.log("async.get2.data:", response2.data)
          if (response2.data.data.name === "邓瑞") {

            //get请求3
            const response3 = await axios.get('http://127.0.0.1/article/get/search/title/入门')
            console.log("async.get3.data:", response3.data)
          }
        }

      } catch (error) {
        console.log("async.get.error:", error)
      } finally {
        console.log("async.get.finally")
      }
    }

    getData()

  </script>
</body>

</html>
```