# Vue学习笔记

## 17.生命周期

### 1.引出生命周期

生命周期
	a 又名生命周期回调函数、生命周期函数、生命周期钩子
	b 是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数
	c 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的
	d 生命周期函数中的 this 指向是vm或组件实例对象

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>引出生命周期</title>
		<script src="../js/vue.js"></script>
	</head>
	<!-- 
	 生命周期
	 a. 又名生命周期回调函数、生命周期函数、生命周期钩子
	 b. 是什么： Vue 在关键时刻帮我们调用的一些特殊名称的函数
	 c. 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的
	 d. 生命周期函数中的 this 指向是 vm 或 组件实例对象
-->
	<body>
		<div id="root">
			<h2 v-if="a">你好啊</h2>
			<h2 :style="{opacity}">欢迎学习Vue</h2>
		</div>
		<script>
			Vue.config.productionTip = false
			const vm = new Vue({
				el: '#root',
				data: {
					opacity: 0.5,
					a: false
				},
				// Vue完成模板的解析并把初始的真实dom元素放入页面后(挂载完毕)调用mounted
				mounted() {
					console.log('mounted');
					setInterval(() => {
						this.opacity -= 0.1
						if (this.opacity <= 0) {
							this.opacity = 1
						}
					}, 16)
				}

			})
			// 通过外部的定时器实现(不推荐)
			// setInterval(()=>{
			// 	vm.opacity -=0.1
			// 	if (vm.opacity<=0) {
			// 		vm.opacity = 1
			// 	}
			// })
		</script>
	</body>
</html>
```

![CPT2204232016-152x28](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204232017246.gif)

### 2.分析生命周期

![生命周期.png](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204232036425.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>分析生命周期</title>
	<script src="../js/vue.js"></script>
</head>

<body>
	<div id="root">
		<h2>当前的n值是:{{n}}</h2>
		<button @click="add">点我n+1</button>
		<button @click="bye">点我销毁vm</button>
	</div>
	<script>
		Vue.config.productionTip = false
		const vm = new Vue({
			el: '#root',
			// template:
			// `<div>
			// 	<h2>当前的n值是:{{n}}</h2>
			// 	<button @click="add">点我n+1</button>
			// </div>`,
			data: {
				n: 1
			},
			methods: {
				add() {
					this.n++
				},
				bye(){
					console.log("bye");
					// 销毁
					this.$destroy()
				}
			},
			beforeCreate() {
				console.log('beforeCreate')
				// console.log(this); 
				// debugger;
			},
			created() {
				console.log('created')
				// console.log(this); 
				// debugger;
			},
			beforeMount() {
				console.log('beforeMount')
				// console.log(this);
				// debugger;
			},
			mounted() {
				console.log('mounted')
				// console.log(this);
				// debugger;
			},
			beforeUpdate() {
				console.log('beforeUpdate')
				// console.log(this.n);
				// debugger;
			},
			updated() {
				console.log('updated');
				// console.log(this.n);
				// debugger;
			},
			beforeDestroy() {
				console.log(this.n);
				this.add()  // 不会触发
			},
			destroyed() {
				console.log('destroyed')
			},
		})	
	</script>
</body>

</html>
```

### 3.总结生命周期

```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>总结生命周期</title>
	<script src="../js/vue.js"></script>
</head>
<!-- 
	总结
	常用的生命周期钩子
	a. mounted 发送 ajax 请求、启动定时器、绑定自定义事件、订阅消息等初始化操作
	b. beforeDestroy 清除定时器、解绑自定义事件、取消订阅消息等收尾工作
	关于销毁 Vue 实例
	a. 销毁后借助 Vue 开发者工具看不到任何信息
	b. 销毁后自定义事件会失效，但原生 DOM 事件依然有效
	c. 一般不会在 beforeDestroy 操作数据，因为即便操作数据，也不会再触发更新流程了

 -->
<body>
		<div id="root">
			<h2 :style="{opacity}">欢迎学习Vue</h2>
			<button @click="stop">点我停止变换</button>
		</div>
	<script>
		Vue.config.productionTip = false
		const vm = new Vue({
				el: '#root',
				data: {
					opacity: 0.5,
				},
				methods: {
					stop(){
						// 进行销毁vm
						this.$destroy();
					}
				},
				// Vue完成模板的解析并把初始的真实dom元素放入页面后(挂载完毕)调用mounted
				mounted() {
					console.log('mounted');
					this.timer = setInterval(() => {
						this.opacity -= 0.1
						if (this.opacity <= 0) {
							this.opacity = 1
						}
					}, 16)
				},
				// 销毁前执行
				beforeDestroy() {
					clearInterval(this.timer)
					console.log('vm凉凉了');
				},

			})
	</script>
</body>

</html>
```

## 18.组件化编程

### 1.模块与组件、模块化与组件化

模块
	a. 理解：向外提供特定功能的 js 程序，一般就是一个 js 文件
	b. 为什么：js 文件很多很复杂
	c. 作用：复用、简化 js 的编写，提高 js 运行效率
组件
	a. 定义：用来实现局部功能的代码和资源的集合（html/css/js/image…）
	b. 为什么：一个界面的功能很复杂
	c. 作用：复用编码，简化项目编码，提高运行效率
模块化
	当应用中的 js 都以模块来编写的，那这个应用就是一个模块化的应用
组件化
	当应用中的功能都是多组件的方式来编写的，那这个应用就是一个组件化的应用

![image.png](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204241431985.png)

![image.png](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204241431166.png)



### 2.非单文件组件

非单文件组件：一个文件中包含有 n 个组件
单文件组件：一个文件中只包含有 1 个组件

### 3.基本使用

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>组件的基本使用</title>
    <script src="../js/vue.js"></script>
</head>


<!-- 
    2.2.1. 基本使用
    Vue中使用组件的三大步骤 
    定义组件
    使用Vue.extend(options)创建，其中options和new Vue(options)时传入的options几乎一样，但也有点区别
    el不要写，因为最终所有的组件都要经过一个vm的管理，由vm中的el才决定服务哪个容器
    data必须写成函数，避免组件被复用时，数据存在引用关系
    注册组件
    局部注册：new Vue()的时候options传入components选项
    全局注册：Vue.component('组件名',组件)
    使用组件
    编写组件标签如 <school></school> 
 -->
<body>
    <div id="root">
        <!-- <h2>学校名称:{{schoolName}}</h2>
        <h2>学校地址:{{address}}</h2>
        <hr>
        <h2>学生姓名:{{studentName}}</h2>
        <h2>学生年龄:{{Age}}</h2> -->
        <!-- 第三步:编写组件标签 -->
        <school></school>
        <hr>
        <!-- 第三步:编写组件标签 -->
        <student></student>
        <hr>
        <hello></hello>
        <hr>
    </div>

    <div id="root2">
        <hello></hello>
    </div>
    <script>

        Vue.config.productionTip = false
        // 第一步：创建school的组件
        const school = Vue.extend({
            template: `
            <div>
                <h2>学校名称:{{schoolName}}</h2>
                <h2>学校地址:{{address}}</h2>
                <button @click="showNmae">点我显示学校名</button>
            </div>
            `,
            data() {
                return {
                    schoolName: '尚硅谷',
                    address: '北京昌平'
                }
            },
            methods: {
                showNmae() {
                    alert(this.schoolName)
                }
            },
        })
        // 第一步：创建student的组件
        const student = Vue.extend({
            template: `
            <div>
                <h2>学生名称:{{studentName}}</h2>
                <h2>学校地址:{{Age}}</h2>
            </div>
            `,
            data() {
                return {
                    studentName: '张三',
                    Age: 18
                }
            }
        })



        const hello = Vue.extend({
            template: `
            <div>
                <h2>你好啊{{name}}！</h2>
                </div>
            `,
            data() {
                return {
                    name: '张三'
                }
            }
        })



        Vue.component('hello', hello)

        var vm = new Vue({
            el: '#root',
            // 第二步:注册组件
            components: {
                school,
                student
            }
        })

        new Vue({
            el: '#root2',
        })
    </script>
</body>

</html>
```



![image-20220424143920629](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204241439677.png)

### 4.几个注意点

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>几个注意点</title>
    <script src="../js/vue.js"></script>
</head>
<!-- 
    关于组件名
    一个单词组成
    第一种写法（首字母小写）：school
    第二种写法（首字母大写）：School
    多个单词组成
    第一种写法（kebab-case 命名）：my-school
    第二种写法（CamelCase 命名）：MySchool（需要 Vue 脚手架支持）
    备注
    组件名尽可能回避 HTML 中已有的元素名称，例如：h2、H2都不行
    可以使用 name 配置项指定组件在开发者工具中呈现的名字
    关于组件标签
    第一种写法： <school></school>
    第二种写法： <school/> （需要 Vue 脚手架支持）
    备注：不使用脚手架时， <school/> 会导致后续组件不能渲染
    一个简写方式： const school = Vue.extend(options) 可简写为 const school = options ，因为父组件 components 引入的时候会自动创建
 -->
<body>
    <div id="root">
        <h1>{{msg}}</h1>
        <!-- <School></School> -->
        <my-school></my-school>
        <my-school />
        <!-- <schoolName></schoolName> -->
    </div>
    <script>
        Vue.config.productionTip = false;

        const school = Vue.extend({
            // name:'schoolName',
            template: `
            <div>
                <h2>学校名称:{{schoolName}}</h2>
                <h2>学校地址:{{address}}</h2>
                <button @click="showNmae">点我显示学校名</button>
            </div>
            `,
            data() {
                return {
                    schoolName: '尚硅谷',
                    address: '北京昌平'
                }
            },
            methods: {
                showNmae() {
                    alert(this.schoolName)
                }
            },
        })
        new Vue({
            el: '#root',
            data: {
                msg: '欢迎学习Vue'
            },
            components: {
                // 1.单个单词建议首字母大写
                // School: school
                // 2.多个单词写法
                'my-school': school
            }
        })
    </script>
</body>

</html>
```

### 5.组件嵌套

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>组件的嵌套</title>
    <script src="../js/vue.js"></script>
</head>

<body>
    <div id="root">
        <!-- <app></app> -->
    </div>
    <script>
        Vue.config.productionTip = false;
        // 创建student组件
        const student = Vue.extend({
            template:
                `
            <div>
                <h2>学生姓名:{{studentName}}</h2>
                <h2>学生年龄:{{Age}}</h2>
            </div>
                `,
            data() {
                return {
                    studentName: '张三',
                    Age: 18
                }
            }
        })

        // 定义school组件
        const school = Vue.extend({
            template:
                `
                <div>
                    <h2>学校名称:{{schoolName}}</h2>
                    <h2>学校地址:{{address}}</h2>
                    <student></student>
                    </div>
                `,
            data() {
                return {
                    schoolName: '尚硅谷',
                    address: '北京昌平'
                }
            },
            components: {
                student
            }
        })
        // 定义school组件
        const hello = Vue.extend({
            template:
                `
                <div>
                    <h2>{{msg}}</h2>
                </div>
                `,
                data(){
                    return {
                        msg: 'hello欢迎你来学习'
                    }
                }
        })

        //  定义app组件
        const app = Vue.extend({
            template:`
            <div>
                <hello></hello>
                <school></school>
                </div>
            `,
            components:{
                school,
                hello
            }
        })
        new Vue({
            template:`<app></app>`,
            el: '#root',
            components: {
                app
            }
        })
    </script>
</body>

</html>
```

![image-20220424191908188](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204241919251.png)

![img](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204241517235.png)

### 6.VueComponent

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VueComponent</title>
    <script src="../js/vue.js"></script>
</head>
<!-- 
    关于 VueComponent
        1. school 组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，而是 Vue.extend() 生成的 
        2.我们只需要写 <school/> 或 <school></school>，Vue 解析时会帮我们创建 school 组件的实例对象，即Vue帮我们执行的new VueComponent(options) 
        3.每次调用Vue.extend，返回的都是一个全新的VueComponent，即不同组件是不同的对象
        4.关于 this 指向 
            a. 组件配置中
                data函数、methods中的函数、watch中的函数、computed中的函数 它们的 this 均是 VueComponent实例对象
            b. new Vue(options)配置中：
                data函数、methods中的函数、watch中的函数、computed中的函数 它们的 this 均是 Vue实例对象
        5.VueComponent的实例对象，以后简称vc（组件实例对象）Vue的实例对象，以后简称vm  
 -->
<body>
    <div id="root">
        <school></school>
        <hello></hello>
    </div>
    <script>
        Vue.config.productionTip = false;
        const school = Vue.extend({
            template:
                `
                <div>
                    <h2>学校名称:{{schoolName}}</h2>
                    <h2>学校地址:{{address}}</h2>
                    <button @click="showName">点我显示学校名称</button>
                    </div>
                `,
            data() {
                return {
                    schoolName: '尚硅谷',
                    address: '北京昌平'
                }
            },
            methods: {
                showName() {
                    console.log(this);
                    alert(this.schoolName);
                }
            },
        })


        const test = Vue.extend({
            template:'<span>张三</span>'
        })

        const hello = Vue.extend({
            template:
                `
                <div>
                    <h2>{{msg}}</h2>
                    <test></test>
                </div>`,
            data() {
                return {
                    msg: 'hello，欢迎学习Vue'
                }
            },
            components:{
                test
            }
        })
       
        new Vue({
            el: '#root',
            components: {
                school,
                hello
            }
        })

        console.log('@', school);
        console.log('#', hello);
        console.log(school == hello);
    </script>
</body>

</html>
```

### 7.一个重要的内置关系

1.  一个重要的内置关系：VueComponent.prototype.__proto__ === Vue.prototype

2. 为什么要有这个关系：让组件实例对象vc可以访问到 Vue原型上的属性、方法

![image.png](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204242055362.png)

### 8.单文件组件

School.vue

```vue
<template>
  <!-- 组件的结构 -->
  <div class="demo">
    <h2>学校名称:{{ name }}</h2>
    <h2>学校地址:{{ address }}</h2>
    <button @click="showNmae">点我显示学校名称</button>
  </div>
</template>

<script>
// 组件交互相关的代码
export default {
  name:'School',
  // 定义组件的data属性
  data() {
    return {
      name: '清华大学',
      address: '北京市海淀区'
    }
  },
  // 定义组件的methods属性
  methods: {
    showNmae() {
      this.schoolName = '清华大学'
    }
  }
}
</script>

<style>
/* 组件的格式 */
.demo {
  background-color: orange;
}
</style>

```

Student.vue

```vue
<template>
  <!-- 组件的结构 -->
  <div>
    <h2>学生姓名:{{ name }}</h2>
    <h2>学生年龄:{{ age }}</h2>
  </div>
</template>

<script>
// 组件交互相关的代码
export default {
  name: "Student",
  // 定义组件的data属性
  data() {
    return {
      name: "张三",
      age: 18,
    };
  },
};
</script>

```

App.vue

```vue
<template>
  <div>
    <School></School>
    <Student></Student>
  </div>
</template>

<script>
import School from "./School.vue";
import Student from "./Student.vue";
export default {
  name: "App",
  components: {
    School,
    Student,
  },
};
</script>

<style></style>
```

main.js

```js
import App from './App.vue'


new Vue({
    el:'#root',
    template:`<App></App>`,
    components:{
        App
    }
})
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>练习单文件语法</title>
</head>
<body>
    <div id="root">
        <script src="../js/vue.js"></script>
        <script src="./main.js"></script>
    </div>
</body>
</html>
```

到目前为止是无法看到运行效果的，需要借助Vue脚手架。

## 19.Vue脚手架

### 1.安装脚手架

```shell
# 设置淘宝源
npm config set registry http://registry.npm.taobao.org
# 安装脚手架
npm install -g @vue/cli
```

在demo目录下执行如下命令

![image-20220424215552398](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204242155464.png)

选择Vue2然后回车，结果如下：

![image-20220424215655095](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204242156163.png)

然后执行

```shell
cd vue_test
npm run serve
```

结果如下:

![image-20220424220006607](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204242200667.png)

然后在浏览器中输入http://localhost:8080/ :

![image-20220424220103095](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204242201222.png)



### 2.将之前单文件组件写的内容用脚手架来运行

目录结构:

![image-20220424223039602](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204242230664.png)

App.vue

```vue
<template>
  <div>
    <img src="./assets/logo.png" alt="" />
    <School></School>
    <Student></Student>
  </div>
</template>

<script>
import School from "./components/School.vue";
import Student from "./components/Student.vue";
export default {
  name: "App",
  components: {
    School,
    Student,
  },
};
</script>

<style></style>

```

main.js

```js

/*
  该文件是整个项目的入口文件
*/
// 引入Vue
import Vue from 'vue'
// 引入App组件，他是所有组件的父组件
import App from './App.vue'
// 关闭VUe的生产提示
Vue.config.productionTip = false
// 创建Vue实例对象
new Vue({
  // 将App组件放入容器中
  render: h => h(App),
}).$mount('#app')
```

index.html

```html
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
    <!-- 针对ie浏览器的特殊配置，含义是：让ie浏览器以最高的渲染级别渲染页面 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!-- 开启移动端的理想视口 -->
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <!--配置页面图标   <%= BASE_URL %>就是public目录  -->
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
    <!-- 配置网页标题 <%= htmlWebpackPlugin.options.title %>就是package.json中的title   -->
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
    <!-- 若浏览器不支持js，以下内容就会出现在浏览器页面上 -->
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <!-- 容器 -->
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>

```



在控制台输入

```shell
npm run serve
```

如果报如下错误：![image-20220424223213938](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204242232996.png)

解决方法1：

修改vue.config.js

![image-20220424223258549](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204242232599.png)

解决方法2：

- 更改组件名(这个比较麻烦),也就是重新起个组件名,使其符合命名规范,如: StudentName 或者 student-name



运行结果：

![image-20220424223351141](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204242233267.png)

###  3.render函数

```js
/*
  该文件是整个项目的入口文件
*/
// 引入Vue
// import Vue from "vue/dist/vue";
import Vue from "vue";
// 引入App组件，他是所有组件的父组件
import App from "./App.vue";
// 关闭VUe的生产提示
Vue.config.productionTip = false;
// 创建Vue实例对象
new Vue({
  el: "#app",
  // 将App组件放入容器中
  // render: (h) => h(App),
  // 完整形式
  // render(createElement) {
  //   return createElement("h1", "你好啊");
  // },

  render:(createElement) => createElement(App),
  // template:`<h1>你好啊!</h1>`
});

```

### 4.修改默认配置

```markdown
## 脚手架文件结构

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
│   │── main.js: 入口文件
├── .gitignore: git版本管制忽略的配置
├── babel.config.js: babel的配置文件
├── package.json: 应用包配置文件 
├── README.md: 应用描述文件
├── package-lock.json：包版本控制文件

## 关于不同版本的Vue

1. vue.js与vue.runtime.xxx.js的区别：
1. vue.js是完整版的Vue，包含：核心功能 + 模板解析器。
2. vue.runtime.xxx.js是运行版的Vue，只包含：核心功能；没有模板解析器。
2. 因为vue.runtime.xxx.js没有模板解析器，所以不能使用template这个配置项，需要使用render函数接收到的createElement函数去指定具体内容。

## vue.config.js配置文件

1. 使用vue inspect > output.js可以查看到Vue脚手架的默认配置。
2. 使用vue.config.js可以对脚手架进行个性化定制，详情见：https://cli.vuejs.org/zh

```

vue.config.js

```
const { defineConfig } = require("@vue/cli-service");
module.exports = defineConfig({
  transpileDependencies: true,
  // 关闭语法检查
  lintOnSave: false,
  // 
  pages: {
    index: {
      // 入口
      entry: "src/main.js",
    },
  },
});

```

## 20.ref属性

> 1. 被用来给元素或子组件注册引用信息（id的替代者）
> 2. 应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象（vc）
> 3. 使用方式：
>    1. 打标识：```<h1 ref="xxx">.....</h1>``` 或 ```<School ref="xxx"></School>```
>    2. 获取：```this.$refs.xxx```

App.vue

```vue
<template>
    <div>
        <h1 v-text="msg" ref="title"></h1>
        <button ref="btn" @click="showDom">点我输出上方的dom元素</button>
        <school ref="school" id="school" />
    </div>
</template>

<script>
// 引入School组件
import School from './components/School.vue'

export default {
    name: 'App',

    data() {
        return {
            msg:'欢迎学习Vue'
        };
    },

    mounted() {
        
    },

    methods: {
        showDom(){
            console.log(this.$refs.title);  // 真实DOM元素
            console.log(this.$refs.btn);    // 真实DOM元素
            console.log(this.$refs.school); // School组件的实例对象（vc）
            console.log(document.getElementById('school')); // School组件的真实DOM元素
        }
    },
    components:{School}
};
</script>

<style>

</style>
```

![image-20220425211427237](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204252114370.png)

## 21.props

> ## props配置项
>
> 1. 功能：让组件接收外部传过来的数据
>
> 2. 传递数据：```<Demo name="xxx"/>```
>
> 3. 接收数据：
>
>    1. 第一种方式（只接收）：```props:['name'] ```
>    2. 第二种方式（限制类型）：```props:{name:String}```
>    3. 第三种方式（限制类型、限制必要性、指定默认值）：
>
>    ```js
>    props:{
>        name:{
>            type:String, //类型
>                required:true, //必要性
>                    default:'老王' //默认值
>        }
>    }
>    ```
>    
>    > 备注：props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据。

Student.vue

```vue
<template>
    <div>
        <h1>{{msg}}</h1>
        <h2>学生名称:{{name}}</h2>
        <h2>学生性别:{{sex}}</h2>
        <h2>学生年龄:{{myAge+1}}</h2>
        <button @click="changeAge">尝试修改收到的年龄</button>
    </div>
</template>

<script>
export default {
    name: 'Student',

    data() {
        return {
            msg:'我是一个学生',
            // 后续可能修改年龄
            myAge:this.age
        };
    },
    // 简单声明接收
    // props:['name','sex','age']
    // 接收提示对数据进行类型限制。
    // props:{
    //     name:String,
    //     sex:String,
    //     age:Number
    // }
    // 接收的同时对数据，进行类型限制+默认值限定+必要性的限制
    props:{
        name:{
            type:String,  // name的类型是字符串
            required:true,  // name是必要的
        },
        age:{
            type:Number,
            default:18,  // age的默认值是18
        },
        sex:{
            type:String,
            required:true
        }
    },
    methods: {
        changeAge(){
            this.myAge ++
        }
    },
};
</script>

```

## 22.mixin混入

![image-20220425220344958](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204252203014.png)

School.vue

```vue
<template>
    <div>
        <h2 @click="showName">学校名称:{{name}}</h2>
        <h2>学校地址:{{address}}</h2>
    </div>
</template>

<script>
// 引入混合
// import {hunhe,hunhe2} from '../mixin'
export default {
    name: 'School',

    data() {
        return {
            name:'尚硅谷',
            address:'北京',
            x:666
        };
    },
    // mixins:[hunhe,hunhe2],
    // mounted() {
    //     console.log('你好啊！！！！！！！！');
    // },
};
</script>

```

Student.vue

```vue
<template>
    <div>
        <h2 @click="showName">学生名称:{{name}}</h2>
        <h2>学生性别:{{sex}}</h2>
    </div>
</template>

<script>
// import {hunhe,hunhe2} from '../mixin.js'
export default {
    name: 'Student',

    data() {
        return {
            name:'张三',
            sex:'男'
        };
    },
    // mixins:[hunhe,hunhe2]
};
</script>

```

mixin.js

```js
export const hunhe = {
  methods: {
    showName() {
      alert(this.name);
    },
  },
  mounted() {
    console.log("你好啊");
  },
};

export const hunhe2 = {
  data(){
    return {
        x:100,
        y:200
    }
  }
};

```

main.js

```js
// 引入vue
import Vue from "vue"
// 引入App
import App from "./App.vue"

import {hunhe,hunhe2} from './mixin'
// 关闭生产提示
Vue.config.productionTip = false
// 全局引入mixin
Vue.mixin(hunhe);
Vue.mixin(hunhe2)

new Vue({
    el: "#app",
    render: (h) => h(App)
})
```



![image-20220425220222292](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204252202387.png)

## 23.插件

目录结构：

![image-20220426125542271](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204261255418.png)

main.js

```js
// 引入vue
import Vue from "vue"
// 引入App
import App from "./App.vue"

// 引入插件
import plugins from './plugins'
// 关闭生产提示
Vue.config.productionTip = false
// 应用插件
Vue.use(plugins)
new Vue({
    el: "#app",
    render: (h) => h(App)
})
```

plugins.js

```js
export default {
  install(Vue) {
    console.log("@@@install", Vue);
    // 全局过滤器
    Vue.filter("mySlice", function (value) {
      return value.slice(0, 4);
    });
    // 全局自定义指令
    Vue.directive("fbind", {
      bind(el, binding) {
        el.value = binding.value;
      },
      inserted(el, binding) {
        el.value = binding.value;
        el.focus();
      },
      update(el, binding) {
        el.value = binding.value;
      },
    });
    // 定义混入
    Vue.mixin({
      data() {
        return {
          x: 100,
          y: 200,
        };
      },
    });
    // 给vue原型上添加一个方法(vm和vc就都能用了)
    Vue.prototype.hello = () => alert("你好啊");
  },
};

```

School.vue

```vue
<template>
    <div>
        <h2>学校名称:{{name | mySlice}}</h2>
        <h2>学校地址:{{address}}</h2>
        <input v-fbind:value="name" type="text">
        <button @click="hello">点我测试一下hello</button>
    </div>
</template>

<script>
export default {
    name: 'School',
    data() {
        return {
            name:'尚硅谷123444',
            address:'北京',
        };
    },
};
</script>

```

![image-20220426125555130](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204261255226.png)

## 24.scoped样式

> 1. 作用：让样式在局部生效，防止冲突。
> 2. 写法：```<style scoped>```

School.vue

```vue
<template>
    <div class="demo">
        <h2 class="title">学校名称:{{name}}</h2>
        <h2>学校地址:{{address}}</h2>
    </div>
</template>

<script>
export default {
    name: 'School',
    data() {
        return {
            name:'尚硅谷',
            address:'北京',
        };
    },
};
</script>

<style scoped>
    .demo{
        background-color: skyblue;
    }
</style>
```

Student.vue

```vue
<template>
    <div class="demo">
        <h2 class="title">学生名称:{{name}}</h2>
        <h2 class="qwe">学生性别:{{sex}}</h2>
    </div>
</template>

<script>
export default {
    name: 'Student',

    data() {
        return {
            name:'张三',
            sex:'男'
        };
    },
};
</script>

<style lang="less">
    .demo {
        background-color: orange;
        .qwe{
            font-size: 40px;
        }
    }
</style>
```

App.vue

```vue
<template>
    <div>
        <School></School>
        <hr>
        <Student></Student>
    </div>
</template>

<script>
// 引入School组件
import School from './components/School.vue'
import Student from './components/Student.vue'

export default {
    name: 'App',
    components:{Student,School}
};
</script>

<style>
    .title {
        color: red;
    }
</style>
```

![image-20220426131605315](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204261316431.png)

## 25.TodoList案例

>1. 组件化编码流程：
>
>   	(1).拆分静态组件：组件要按照功能点拆分，命名不要与html元素冲突。
>	  	
>   	(2).实现动态组件：考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用：
>	  	
>   			1).一个组件在用：放在组件自身即可。
>	  	
>   			2). 一些组件在用：放在他们共同的父组件上（<span style="color:red">状态提升</span>）。
>	  	
>   	(3).实现交互：从绑定事件开始。
>
>2. props适用于：
>
>   	(1).父组件 ==> 子组件 通信
>	  	
>   	(2).子组件 ==> 父组件 通信（要求父先给子一个函数）
>
>3. 使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为props是不可以修改的！
>
>4. props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做。

目录结构:

![image-20220426211934351](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204262119435.png)

App.vue

```vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo" />
        <MyList
          :todos="todos"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        />
        <MyFooter 
        :checkedAll="checkedAll" 
        :todos="todos" 
        :deleteAllTodo="deleteAllTodo"
        />
      </div>
    </div>
  </div>
</template>

<script>
// 引入组件
import MyHeader from "./components/MyHeader.vue";
import MyList from "./components/MyList.vue";
import MyFooter from "./components/MyFooter.vue";
export default {
  name: "App",
  components: { MyHeader, MyList, MyFooter },
  data() {
    return {
      todos: [
        {
          id: "001",
          title: "抽烟",
          done: true,
        },
        {
          id: "002",
          title: "喝酒",
          done: true,
        },
        {
          id: "003",
          title: "开车",
          done: true,
        },
      ],
    };
  },
  methods: {
    // 添加一个todo
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    // 勾选or取消勾选一个todo
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          todo.done = !todo.done;
        }
      });
    },
    // 删除一个todo
    deleteTodo(id) {
      // 方法一
      // this.todos.forEach((todo,index) => {
      //   if (todo.id === id) {
      //     this.todos.splice(index,1)
      //   }
      // }
      // );
      // 方法二
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    // 全选or全不选
    checkedAll(checked) {
      this.todos.forEach((todo) => {
        todo.done = checked;
      });
    },
    // 清除所有已完成的todo
    deleteAllTodo() {
      this.todos = this.todos.filter((todo) => !todo.done );
    },
  },
};
</script>

<style>
/*base*/
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
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
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
```

MyHeader.vue

```vue
<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add" />
  </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {
  name: "MyHeader",
  data() {
    return {
      title: '',
    };
  },
  methods: {
    add() {
      // 校验数据
      if (!this.title.trim())  return alert('输入不能为空！')
      // 将用户的输入包装成一个todo对象
      const todoObj = {id:nanoid(),title:this.title,done:false}
      // 通知App组件添加一个todo对象
      this.addTodo(todoObj)
      // 清空输入框
      this.title = ''
    }
  },
  props:['addTodo']
};
</script>

<style scoped>
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>

```

MyList.vue

```vue
<template>
  <ul class="todo-main">
    <MyItem v-for="todoObj in todos" 
      :key="todoObj.id" 
      :todo="todoObj" 
      :checkTodo="checkTodo" 
      :deleteTodo="deleteTodo"
    />
  </ul>
</template>

<script>
import MyItem from "./MyItem.vue";
export default {
  name: "MyList",
  components: { MyItem },
  props:['todos','checkTodo','deleteTodo'],
};
</script>

<style scoped>
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>

```

MyItem.vue

```vue
<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="todo.done"
        @change="handleCheck(todo.id)"
      />
      <!-- 如下代码也能实现功能，但是不太推荐，因为有点违反原则，因为修改了props -->
      <!-- <input type="checkbox" v-model="todo.done" /> -->
      <span>{{ todo.title }}</span>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  // 声明接收todo对象
  props: ["todo", "checkTodo",'deleteTodo'],
  methods: {
    handleCheck(id) {
      // 通知App组件done取反
      this.checkTodo(id);
    },
    handleDelete(id){
      // 通知App组件删除
      if(confirm('确定要删除吗？')){
        this.deleteTodo(id);
      }
    }
  },
};
</script>

<style scoped>
/*item*/
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
  background-color: #ccc;
}
li:hover button {
  display: block;
}
</style>
```

MyFooter.vue

```vue
<template>
  <div class="todo-footer">
    <label>
      <!-- <input type="checkbox" @change="handleCheckAll" :checked="isAll" /> -->
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="deleteAllTodo">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ["checkedAll", "todos",'deleteAllTodo'],
  methods: {
    handleCheckAll(e) {
      this.checkedAll(e.target.checked);
    },
  },
  // 计算属性
  computed: {
    // todos总个数
    total() {
      return this.todos.length;
    },
    // 已完成todos个数
    doneTotal() {
      return this.todos.filter((todo) => todo.done).length;
    },
    // 方法1
    // isAll() {
    //   return this.doneTotal === this.total && this.total>0 ;
    // },
    // 方法2
    isAll: {
      get() {
        return this.doneTotal === this.total && this.total > 0;
      },
      set(value) {
        return this.checkedAll(value);
      },
    },
  },
};
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
```

![image-20220426212133455](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204262121552.png)

## 26.浏览器本地存储WebStorage

> 1. 存储内容大小一般支持5MB左右（不同浏览器可能还不一样）
>
> 2. 浏览器端通过 Window.sessionStorage 和 Window.localStorage 属性来实现本地存储机制。
>
> 3. 相关API：
>
>    1. ```xxxxxStorage.setItem('key', 'value');```
>       该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值。
>
>    2. ```xxxxxStorage.getItem('person');```
>
>       		该方法接受一个键名作为参数，返回键名对应的值。
>
>    3. ```xxxxxStorage.removeItem('key');```
>
>       		该方法接受一个键名作为参数，并把该键名从存储中删除。
>
>    4. ``` xxxxxStorage.clear()```
>
>       		该方法会清空存储中的所有数据。
>
> 4. 备注：
>
>    1. SessionStorage存储的内容会随着浏览器窗口关闭而消失。
>    2. LocalStorage存储的内容，需要手动清除才会消失。
>    3. ```xxxxxStorage.getItem(xxx)```如果xxx对应的value获取不到，那么getItem的返回值是null。
>    4. ```JSON.parse(null)```的结果依然是null。

localStorage.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>localStorage</title>
</head>

<body>
    <h2>localStorage</h2>
    <button onclick="saveData()">点我保存一个数据</button>
    <button onclick="readData()">点我读取一个数据</button>
    <button onclick="deleteData()">点我删除一个数据</button>
    <button onclick="deleteAllData()">点我清空一个数据</button>
    <script>
        let p = {name:'张三',age:18}
        function saveData() {
            localStorage.setItem('msg', 'hello');
            localStorage.setItem('person', JSON.stringify(p));
        }
        function readData() {
            console.log(localStorage.getItem('msg'));
            const result = localStorage.getItem('person');
            console.log(JSON.parse(result));
            console.log(localStorage.getItem('msg5')); // null

        }
        function deleteData() {
            localStorage.removeItem('msg');
            localStorage.removeItem('person');
        }
        function deleteAllData() {
            localStorage.clear();
        }
    </script>
</body>

</html>
```

session.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>sessionStorage</title>
</head>

<body>
    <h2>sessionStorage</h2>
    <button onclick="saveData()">点我保存一个数据</button>
    <button onclick="readData()">点我读取一个数据</button>
    <button onclick="deleteData()">点我删除一个数据</button>
    <button onclick="deleteAllData()">点我清空一个数据</button>
    <script>
        let p = { name: '张三', age: 18 }
        function saveData() {
            sessionStorage.setItem('msg', 'hello');
            sessionStorage.setItem('person', JSON.stringify(p));
        }
        function readData() {
            console.log(sessionStorage.getItem('msg'));
            const result = sessionStorage.getItem('person');
            console.log(JSON.parse(result));
            console.log(sessionStorage.getItem('msg5')); // null

        }
        function deleteData() {
            sessionStorage.removeItem('msg');
            sessionStorage.removeItem('person');
        }
        function deleteAllData() {
            sessionStorage.clear();
        }
    </script>
</body>

</html>
```

## 27.TodoList浏览器本地存储版本

App.vue

```vue
<template>
  <div id="root">
  </div>
</template>

<script>
// 引入组件
import MyHeader from "./components/MyHeader.vue";
import MyList from "./components/MyList.vue";
import MyFooter from "./components/MyFooter.vue";
export default {
  name: "App",
  components: { MyHeader, MyList, MyFooter },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || [],
    };
  },
  watch: {
    todos: {
      deep:true,
      handler(value) {
        localStorage.setItem("todos", JSON.stringify(value));
      },
    },
  },
};
</script>
```

