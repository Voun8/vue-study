# Vue

MVVM

M (model) 模型 data数据

V (view) 试图	代码模板

VM	(ViewModel)    试图模型  vue实例

# 两种模板语法

1.插值语法

~~~js
<div id="root">
  {{name}}
</div>

script
new vue({
  el:'#root'
  name:'1111'
})
~~~

2.**指令语法** 

~~~js
<div id="root">
  <a v-bind:href="url">
</div>

//还有一种写法
<a :href="url">
  
new vue({
  el:'#root',
  url:"http://baidu.com"
})
~~~



#  **数据绑定**

### 单向绑定（v-bind）

即从数据流向页面

### 双向绑定（v-model）

从数据流向页面，然后页面修改数据同时也会修改

双向绑定只能在`input上应用，即表单控件`

<input><select><textarea>

也可以写为

~~~js
<input type="text" v-module='name'>
~~~

# **el 与 data 的两种写法**

el有两种写法

​	1.创建vue实例的时候直接写el

​	2.创建vue实例时不写el，创建实例给一个变量，然后常量的$mount（）方法指定el，挂载上去

data的两种写法

​	1.对象型，直接写`data{}`

​	2.函数型，`data(){}`

​	函数型不能写成箭头函数，否则箭头函数指向window



# 数据代理



Object.defineproperty方法

示例

~~~js
let number=18
let person={
  name:"张三",
  sex:"男",
}


Object.defineProperty(peroson,'age',{
  get(){
    return number
  }
 set(value){
  age=value
}
})
~~~

数据代理就是通过一个对象对另一个对象属性值的操作

~~~js
let obj={x:100}
let obj2={y:100}

Object.defineProperty(obj2,'x',{
  get(){
    return obj.x
  },
  set(value){
    obj.x=value
  }
})
~~~

