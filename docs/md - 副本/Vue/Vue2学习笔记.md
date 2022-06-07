# Vue2学习笔记

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

## 28.组件的自定义事件

> 1. 一种组件间通信的方式，适用于：<strong style="color:red">子组件 ===> 父组件</strong>
>
> 2. 使用场景：A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（<span style="color:red">事件的回调在A中</span>）。
>
> 3. 绑定自定义事件：
>
>    1. 第一种方式，在父组件中：```<Demo @atguigu="test"/>```  或 ```<Demo v-on:atguigu="test"/>```
>
>    2. 第二种方式，在父组件中：
>
>       ```js
>       <Demo ref="demo"/>
>       ......
>       mounted(){
>          this.$refs.xxx.$on('atguigu',this.test)
>       }
>       ```
>
>    3. 若想让自定义事件只能触发一次，可以使用```once```修饰符，或```$once```方法。
>
> 4. 触发自定义事件：```this.$emit('atguigu',数据)```
>
> 5. 解绑自定义事件```this.$off('atguigu')```
>
> 6. 组件上也可以绑定原生DOM事件，需要使用```native```修饰符。
>
> 7. 注意：通过```this.$refs.xxx.$on('atguigu',回调)```绑定自定义事件时，回调<span style="color:red">要么配置在methods中</span>，<span style="color:red">要么用箭头函数</span>，否则this指向会出问题！

App.vue

```vue
<template>
  <div class="app">
    <h1>{{ msg }}，学生姓名是{{ studentname }}</h1>
    <!-- 通过父组件给子组件传递函数类型的props实现：子给父传递数据 -->
    <School :getSchoolName="getSchoolName"></School>
    <hr />
    <!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据  第一种写法：v-on或@符-->
    <!-- <Student v-on:atguigu="getStudentName" @demo="m1"></Student> -->
    <!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据  第二种写法：ref  (更灵活)-->
    <!-- native不当作自定义指令 -->
    <Student ref="student" @click.native="show"></Student>
  </div>
</template>

<script>
// 引入School组件
import School from "./components/School.vue";
import Student from "./components/Student.vue";

export default {
  name: "App",
  components: { Student, School },
  data() {
    return {
      msg: "你好啊！",
      studentname: "",
    };
  },
  methods: {
    getSchoolName(name) {
      console.log("app收到了学校名", name);
    },
    getStudentName(name) {
      console.log("app收到了学生名", name);
      this.studentname = name;
    },
    m1() {
      console.log("demo事件被触发了");
    },
    show(){
        alert(123)
    }
  },
  mounted() {
    //   绑定自定义事件
    this.$refs.student.$on("atguigu", this.getStudentName);
    // 如果不自定义函数getStudentName，第二个参数可以一试一个函数，但必须是箭头函数，不推荐
    // this.$refs.student.$on("atguigu", (name) => {
    //   this.getStudentName(name);
    // });
    // 只触发一次
    // this.$refs.student.$once("atguigu", this.getStudentName);
  },
};
</script>

<style>
.app {
  background-color: gray;
  padding: 5px;
}
</style>
```

Student.vue

```vue
<template>
  <div class="student">
    <h2>学生名称:{{ name }}</h2>
    <h2>学生性别:{{ sex }}</h2>
    <h2>当前number为：{{ number }}</h2>
    <button @click="add">点我number++</button>
    <button @click="sendStudentName">将学生名称传给App</button>
    <button @click="unbind">解绑atguigu事件</button>
    <button @click="death">点我销毁当前Student实例</button>
  </div>
</template>

<script>
export default {
  name: "Student",

  data() {
    return {
      name: "张三",
      sex: "男",
      number: 0,
    };
  },
  methods: {
    add() {
      console.log("add被调用了");
      this.number++;
    },
    sendStudentName() {
      //   触发Student组件的atguigu事件
      this.$emit("atguigu", this.name);
      //   this.$emit("demo");
      this.$emit("click");
    },
    unbind() {
      //   解绑atguigu,只试用解绑一个自定义事件
      this.$off("atguigu");
      // 解绑多个自定义事件
      //   this.$off(["atguigu", "demo"]);
      // 所有事件都解绑
      //   this.$off();
    },
    death() {
      this.$destroy(); // 销毁了当前Student组件的实例，销毁后所有Student实例的自定义事件全都不奏效
    },
  },
};
</script>

<style lang="less">
.student {
  background-color: orange;
  padding: 5px;
  margin-top: 30px;
}
</style>
```

## 29.TodoList组件自定义事件版本

App.vue

```vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader @addTodo="addTodo" />
        <MyList
          :todos="todos"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        />
        <MyFooter
          @checkedAll="checkedAll"
          :todos="todos"
          @deleteAllTodo="deleteAllTodo"
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
      todos: JSON.parse(localStorage.getItem("todos")) || [
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
      this.todos = this.todos.filter((todo) => !todo.done);
    },
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
      // this.addTodo(todoObj)
      // 组件自定义方法实现
      this.$emit('addTodo', todoObj);
      // 清空输入框
      this.title = ''
    }
  },
  // props:['addTodo']
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
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ["todos"],
  methods: {
    handleCheckAll(e) {
      this.checkedAll(e.target.checked);
    },
    clearAll(){
      this.$emit('deleteAllTodo');
    }
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
        // return this.checkedAll(value);
        return this.$emit('checkedAll',value);
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

## 30.全局事件总线

> 1. 一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。
>
> 2. 安装全局事件总线：
>
>    ```js
>    new Vue({
>    	......
>    	beforeCreate() {
>    		Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm
>    	},
>        ......
>    }) 
>    ```
>
> 3. 使用事件总线：
>
>    1. 接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的<span style="color:red">回调留在A组件自身。</span>
>
>       ```js
>       methods(){
>         demo(data){......}
>       }
>       ......
>       mounted() {
>         this.$bus.$on('xxxx',this.demo)
>       }
>       ```
>
>    2. 提供数据：```this.$bus.$emit('xxxx',数据)```
>
> 4. 最好在beforeDestroy钩子中，用$off去解绑<span style="color:red">当前组件所用到的</span>事件。

main.js

```js
// 引入vue
import Vue from "vue"
// 引入App
import App from "./App.vue"
// 关闭生产提示
Vue.config.productionTip = false

new Vue({
    el: "#app",
    render: (h) => h(App),
    beforeCreate() {
        // 安装全局事件总线
        Vue.prototype.$bus = this
    }
})
```

School.vue

```vue
<template>
  <div class="school">
    <h2>学校名称:{{ name }}</h2>
    <h2>学校地址:{{ address }}</h2>
    <button @click="sendSchoolName">点我测试</button>
  </div>
</template>

<script>
export default {
  name: "School",
  data() {
    return {
      name: "尚硅谷",
      address: "北京",
    };
  },
  methods:{
    sendSchoolName(){
      this.$bus.$emit('hello',this.name)
    }
  },
  mounted(){
    // console.log('School',this.x);
    this.$bus.$on('hello',(data)=>{
      console.log(this.name,'我是School,我收到了Student传来的数据：',data);
    })
  },
  // 在组件中销毁之前解绑事件
  beforeDestroy(){
    this.$bus.$off('hello')
  }
};
</script>

<style scoped>
.school {
  background-color: skyblue;
  padding: 5px;
}
</style>

```

Student.vue

```vue
<template>
  <div class="student">
    <h2>学生名称:{{ name }}</h2>
    <h2>学生性别:{{ sex }}</h2>
    <button @click="sendStudentName">点我将学生姓名传给School</button>
  </div>
</template>

<script>
export default {
  name: "Student",

  data() {
    return {
      name: "张三",
      sex: "男",
    };
  },
  methods:{
    sendStudentName(){
      this.$bus.$emit('hello',this.name)
    }
  }
};
</script>

<style lang="less">
.student {
  background-color: orange;
  padding: 5px;
  margin-top: 30px;
}
</style>

```

![image-20220428171231720](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204281712874.png)

### TodoList案例应用全局事件总线

main.js

```js
// 引入vue
import Vue from "vue"
// 引入App
import App from "./App.vue"
// 关闭生产提示
Vue.config.productionTip = false
new Vue({
    el: "#app",
    render: (h) => h(App),
    beforeCreate() {
        Vue.prototype.$bus = this
    }
})
```

App.vue

```vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader @addTodo="addTodo" />
        <MyList
          :todos="todos"
        />
        <MyFooter
          @checkedAll="checkedAll"
          :todos="todos"
          @deleteAllTodo="deleteAllTodo"
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
      todos: JSON.parse(localStorage.getItem("todos")) || [
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
      this.todos = this.todos.filter((todo) => !todo.done);
    },
  },
  watch: {
    todos: {
      deep:true,
      handler(value) {
        localStorage.setItem("todos", JSON.stringify(value));
      },
    },
  },
  mounted(){
    // 挂载事件
    this.$bus.$on('checkTodo',this.checkTodo);
    this.$bus.$on('deleteTodo',this.deleteTodo);
  },
  // 销毁前解绑事件
  beforeDestroy(){
    this.$bus.$off('checkTodo');
    this.$bus.$off('deleteTodo');
  }
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

MyItem.vue

``` vue
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
  props: ["todo"],
  methods: {
    handleCheck(id) {
      // 通知App组件done取反
      this.$bus.$emit("checkTodo", id);
      // this.checkTodo(id);
    },
    handleDelete(id){
      // 通知App组件删除
      if(confirm('确定要删除吗？')){
        // this.deleteTodo(id);
        this.$bus.$emit("deleteTodo", id);
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

![image-20220428172724872](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204281727969.png)

## 31.消息订阅与发布

> 1. 一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。
>
> 2. 使用步骤：
>
>    1. 安装pubsub：```npm i pubsub-js```
>
>    2. 引入: ```import pubsub from 'pubsub-js'```
>
>    3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的<span style="color:red">回调留在A组件自身。</span>
>
>       ```js
>       methods(){
>         demo(data){......}
>       }
>       ......
>       mounted() {
>         this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息
>       }
>       ```
>
>    4. 提供数据：```pubsub.publish('xxx',数据)```
>
>    5. 最好在beforeDestroy钩子中，用```PubSub.unsubscribe(pid)```去<span style="color:red">取消订阅。</span>

School.vue

```vue
<template>
  <div class="school">
    <h2>学校名称:{{ name }}</h2>
    <h2>学校地址:{{ address }}</h2>
  </div>
</template>

<script>
// 引入消息订阅与发布库
import pubsub from "pubsub-js";
export default {
  name: "School",
  data() {
    return {
      name: "尚硅谷",
      address: "北京",
    };
  },
  mounted() {
    // console.log('School',this.x);
    // this.$bus.$on('hello',(data)=>{
    //   console.log(this.name,'我是School,我收到了Student传来的数据：',data);
    // })
    // 订阅消息
    this.pubId = pubsub.subscribe("hello", (msgName, data) => {
      console.log("有人发布了hello消息,hello消息的回调执行了", msgName, data);
    });
  },
  // 在组件中销毁之前解绑事件
  beforeDestroy() {
    // this.$bus.$off('hello')
    // 取消订阅消息
    pubsub.unsubscribe(this.pubId);
  },
};
</script>

<style scoped>
.school {
  background-color: skyblue;
  padding: 5px;
}
</style>

```

Student.vue

```vue
<template>
  <div class="student">
    <h2>学生名称:{{ name }}</h2>
    <h2>学生性别:{{ sex }}</h2>
    <button @click="sendStudentName">点我将学生姓名传给School</button>
  </div>
</template>

<script>
// 引入消息订阅与发布库
import pubsub from "pubsub-js";
export default {
  name: "Student",

  data() {
    return {
      name: "张三",
      sex: "男",
    };
  },
  methods: {
    sendStudentName() {
      //   this.$bus.$emit('hello',this.name)
      // 发布hello消息，内容为666
      pubsub.publish("hello", 666);
    },
  },
};
</script>

<style lang="less">
.student {
  background-color: orange;
  padding: 5px;
  margin-top: 30px;
}
</style>

```

### 订阅消息完成TodoList的todo的删除

App.vue

```vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader @addTodo="addTodo" />
        <MyList
          :todos="todos"
        />
        <MyFooter
          @checkedAll="checkedAll"
          :todos="todos"
          @deleteAllTodo="deleteAllTodo"
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

import pubsub from 'pubsub-js'
export default {
  name: "App",
  components: { MyHeader, MyList, MyFooter },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || [
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
    deleteTodo(_,id) {
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
      this.todos = this.todos.filter((todo) => !todo.done);
    },
  },
  watch: {
    todos: {
      deep:true,
      handler(value) {
        localStorage.setItem("todos", JSON.stringify(value));
      },
    },
  },
  mounted(){
    // 挂载事件
    this.$bus.$on('checkTodo',this.checkTodo);
    // this.$bus.$on('deleteTodo',this.deleteTodo);
    this.pubId = pubsub.subscribe('deleteTodo',this.deleteTodo);
    
  },
  // 销毁前解绑事件
  beforeDestroy(){
    this.$bus.$off('checkTodo');
    // this.$bus.$off('deleteTodo');
    // 取消消息订阅
    pubsub.unsubscribe(pubId);
  }
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
import pubsub from 'pubsub-js'
export default {
  name: "MyItem",
  // 声明接收todo对象
  props: ["todo"],
  methods: {
    handleCheck(id) {
      // 通知App组件done取反
      this.$bus.$emit("checkTodo", id);
      // this.checkTodo(id);
    },
    handleDelete(id){
      // 通知App组件删除
      if(confirm('确定要删除吗？')){
        // this.deleteTodo(id);
        // this.$bus.$emit("deleteTodo", id);
        pubsub.publish('deleteTodo', id);
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

## 32.$nextTick

> 1. 语法：```this.$nextTick(回调函数)```
> 2. 作用：在下一次 DOM 更新结束后执行其指定的回调。
> 3. 什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。

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
      <input
        type="text"
        @blur="handleBlur(todo,$event)"
        v-show="todo.isEdit"
        :value="todo.title"
        ref="inputTitle"
      />
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    <button
      class="btn btn-edit"
      v-show="!todo.isEdit"
      @click="handleEdit(todo)"
    >
      编辑
    </button>
    <button
      class="btn btn-edit"
      v-show="todo.isEdit"
      @click="handleSave(todo)"
    >
      确认
    </button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  // 声明接收todo对象
  props: ["todo"],
  methods: {
    handleCheck(id) {
      // 通知App组件done取反
      this.$bus.$emit("checkTodo", id);
      // this.checkTodo(id);
    },
    handleDelete(id) {
      // 通知App组件删除
      if (confirm("确定要删除吗？")) {
        this.deleteTodo(id);
        this.$bus.$emit("deleteTodo", id);
      }
    },
    handleEdit(todo) {
      // 给todo对象添加isEdit属性
      // 判断todo是否有isEdit属性
      if (todo.hasOwnProperty("isEdit")) {
        todo.isEdit = true;
      } else {
        this.$set(todo, "isEdit", true);
      }
      // input框获取焦点
      this.$nextTick(() => {
        this.$refs.inputTitle.focus();
      });
    },
    handleBlur(todo,e) {
      todo.isEdit = false;
      if (!e.target.value.trim()) return alert('输入不能为空')
      this.$bus.$emit('updateTodo',todo.id,e.target.value);
    },
    // 点击确定按钮
    handleSave(todo){
      todo.isEdit = false;
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

## 33.过渡与动画

> 1. 作用：在插入、更新或移除 DOM元素时，在合适的时候给元素添加样式类名。
>
> 2. 图示：<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204292200202.png" style="width:60%" />
>
> 3. 写法：
>
>    1. 准备好样式：
>
>       - 元素进入的样式：
>          1. v-enter：进入的起点
>          2. v-enter-active：进入过程中
>          3. v-enter-to：进入的终点
>       - 元素离开的样式：
>          1. v-leave：离开的起点
>          2. v-leave-active：离开过程中
>          3. v-leave-to：离开的终点
>
>    2. 使用```<transition>```包裹要过度的元素，并配置name属性,注意如果配置了appear属性的话就代表一开始挂载真实dom的时候就开启动画的效果：
>
>       ```vue
>       <transition name="hello" appear>
>       	<h1 v-show="isShow">你好啊！</h1>
>       </transition>
>       ```
>
>    3. 备注：若有多个元素需要过度，则需要使用：```<transition-group>```，且每个元素都要指定```key```值。

App.vue

```vue
<template>
  <div id="root">
    <Test />
    <Test2 />
    <Test3 />
  </div>
</template>

<script>
import Test from './components/Test.vue' 
import Test2 from './components/Test2.vue' 
import Test3 from './components/Test3.vue' 
export default {
  name: "App",
  components: { Test,Test2,Test3 },
};
</script>
```

Test.vue

```vue
<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <!-- appear初始就有动画 -->
    <transition name="hello" appear>
        <h1 v-show="isShow">你好啊！</h1>
    </transition>

  </div>
</template>

<script>
export default {
  name: "Test",

  data() {
    return {
      isShow: true,
    };
  },

  mounted() {},

  methods: {},
};
</script>

<style scoped>
h1 {
  background-color: orange;
}
.hello-enter-active {
    animation: atguigu 0.5s;
}
.hello-leave-active {
    animation: atguigu 0.5s reverse;
}

@keyframes atguigu{
    /* 0%{
        background-color: orange;
    }
    50%{
        background-color: red;
    }
    100%{
        background-color: orange;
    } */
    from {
        transform: translateX(-100%);
    }to{
        transform: translateX(0%);
    }
}
</style>
```

Test2.vue

```vue
<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <!-- appear初始就有动画 -->
    <transition-group name="hello" appear>
      <h1 v-show="!isShow" :key="1">你好啊！</h1>
      <h1 v-show="isShow" :key="2">Vue！</h1>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: "Test",

  data() {
    return {
      isShow: true,
    };
  },
};
</script>

<style scoped>
h1 {
  background-color: orange;
}
/* 进入的起点,离开的终点*/
.hello-enter,
.hello-leave-to {
  transform: translateX(-100%);
}
.hello-enter-active,
.hello-leave-active {
  transition: 0.5s linear;
}
/* 进入的终点，离开的起点 */
.hello-enter-to,
.hello-leave {
  transform: translateX(0);
}
</style>

```

Test3.vue

``` vue
<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <!-- appear初始就有动画 -->
    <transition-group 
      name="animate__animated animate__bounce"
      enter-active-class="animate__fadeInDownBig"
      leave-active-class="animate__fadeOutTopRight"
      appear>
      <h1 v-show="isShow" :key="1">你好啊！</h1>
      <!-- <h1 v-show="isShow" :key="2">Vue！</h1> -->
    </transition-group>
  </div>
</template>

<script>
import 'animate.css'
export default {
  name: "Test",

  data() {
    return {
      isShow: true,
    };
  },
};
</script>

<style scoped>
h1 {
  background-color: orange;
}
</style>

```

![image-20220429220203267](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204292202331.png)

## 34.配置代理

> ### 方法一
>
> 	在vue.config.js中添加如下配置：
>
> ```js
> devServer:{
>   proxy:"http://localhost:5000"
> }
> ```
>
> 说明：
>
> 1. 优点：配置简单，请求资源时直接发给前端（8080）即可。
> 2. 缺点：不能配置多个代理，不能灵活的控制请求是否走代理。
> 3. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器 （优先匹配前端资源）
>
> ### 方法二
>
> 	编写vue.config.js配置具体代理规则：
>
> ```js
> module.exports = {
> 	devServer: {
>       proxy: {
>       '/api1': {// 匹配所有以 '/api1'开头的请求路径
>         target: 'http://localhost:5000',// 代理目标的基础路径
>         changeOrigin: true,
>         pathRewrite: {'^/api1': ''}
>       },
>       '/api2': {// 匹配所有以 '/api2'开头的请求路径
>         target: 'http://localhost:5001',// 代理目标的基础路径
>         changeOrigin: true,
>         pathRewrite: {'^/api2': ''}
>       }
>     }
>   }
> }
> /*
>    changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
>    changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:8080
>    changeOrigin默认值为true
> */
> ```
>
> 说明：
>
> 1. 优点：可以配置多个代理，且可以灵活的控制请求是否走代理。
> 2. 缺点：配置略微繁琐，请求资源时必须加前缀。
>

vue.config.js

```js
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
  // 开启代理服务器(方式1)
  // devServer: {
  //   proxy: "http://localhost:3000",
  // },
  // 开启代理服务器端(方式2)
  devServer: {
    proxy: {
      // 请求前缀
      "/atguigu": {
        target: "http://localhost:3000",
        // 重写路径，匹配开头为/atguigu的请求,替换为控
        pathRewrite: { "^/atguigu": "" },
        // ws代表：websocket，用于支持webSocket
        // ws: true,
        // 跨域伪造。false就是真实ip+端口，true就是traget的值...用于空值请求头中的host值
        changeOrigin: true,
      },
      "/demo": {
        target: "http://localhost:3001",
        // 重写路径，匹配开头为/atguigu的请求,替换为控
        pathRewrite: { "^/demo": "" },
        // ws代表：websocket，用于支持webSocket
        // ws: true,
        // 跨域伪造。false就是真实ip+端口，true就是traget的值...用于空值请求头中的host值
        changeOrigin: true,
      },
    },
  },
});

```

App.vue

```vue
<template>
  <div>
    <button @click="getStudents">获取学生信息</button>
    <button @click="getCar">获取汽车信息</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {};
  },
  methods: {
    getStudents() {
      axios.get("http://localhost:8081/atguigu/students").then(
        (res) => {
          console.log("请求成功了", res.data);
        },
        (error) => {
          console.log("请求失败了", error.message);
        }
      );
    },
    getCar(){
      axios.get("http://localhost:8081/demo/car").then(
        (res) => {
          console.log("请求成功了", res.data);
        },
        (error) => {
          console.log("请求失败了", error.message);
        }
      );
    }
  },
};
</script>
```

![image-20220430222341623](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202204302223733.png)

## 35.Github案例

App.vue

```vue
<template>
  <div id="app">
    <div class="container-md">
      <Search />
      <List />
    </div>
  </div>
</template>

<script>

import Search from "./components/Search.vue";
import List from "./components/List.vue";
export default {
  name: "App",
  data() {
    return {};
  },
  components: { Search, List },
};
</script>
```

List.vue

```vue
<template>
  <div class="row">
      <!-- 展示用户列表 -->
    <div class="card" v-for="user in info.users" :key="user.node_id" v-show="info.users.length">
      <a :href="user.html_url" target="_blank">
        <img :src="user.avatar_url" style="width: 100px" />
      </a>
      <p class="card-text">{{user.login}}</p>
    </div>
    <!-- 展示欢迎词 -->
    <h1 v-show="info.isFirst">欢迎使用</h1>
    <!-- 展示加载中 -->
    <h1 v-show="info.isLoading">加载中...</h1>
    <!-- 展示错误信息 -->
    <h1 v-show="info.errMsg">{{info.errMsg}}</h1>
  </div>
</template>

<script>
export default {
  name: "List",
  data() {
    return {
        info:{
            isFirst:true,
            isLoading:false,
            errMsg:'',
            users:[]
        }
    };
  },
  mounted() {
    this.$bus.$on('updateListData', (data) => {
        // 合并
      this.info = {...this.info,...data};
    });
  },

  methods: {},
};
</script>

<style lang="css" scope>
.album {
  min-height: 50rem;
  padding-top: 3rem;
  padding-bottom: 3rem;
  background-color: #f7f7f7;
}

.card {
  float: left;
  width: 33.333%;
  padding: 0.75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}

.card > img {
  margin-bottom: 0.75rem;
  border-radius: 100px;
}

.card-text {
  font-size: 85%;
}
</style>

```

Search.vue

```vue
<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input
        class="form-control"
        type="text"
        placeholder="enter the name you search"
        v-model="keyWord"
      />
    </div>
    <button style="margin-top:10px" class="btn btn-primary" @click="searchUsers">Search</button>
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

  mounted() {},

  methods: {
    searchUsers() {
      this.$bus.$emit("updateListData", {
        isFirst: false,
        isLoading: true,
        errMsg: "",
        users: [],
      });
      axios.get("https://api.github.com/search/users?q=" + this.keyWord).then(
        (res) => {
          this.$bus.$emit("updateListData", {
            isLoading: false,
            errMsg: "",
            users: res.data.items,
          });
        },
        (error) => {
          console.log(error.message);
          this.$bus.$emit("updateListData", {
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
    <!-- 引入第三方bootstrap -->
    <!-- <link rel="stylesheet" href="<%= BASE_URL %>css/bootstrap.css"> -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.1/dist/css/bootstrap.min.css">
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

![image-20220501152009511](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202205011520529.png)

## 36.vue-resource

> vue-resource插件可以替代axios完成请求

修改Search.vue

```vue
<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input
        class="form-control"
        type="text"
        placeholder="enter the name you search"
        v-model="keyWord"
      />
    </div>
    <button style="margin-top:10px" class="btn btn-primary" @click="searchUsers">Search</button>
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

  mounted() {},

  methods: {
    searchUsers() {
      this.$bus.$emit("updateListData", {
        isFirst: false,
        isLoading: true,
        errMsg: "",
        users: [],
      });
      this.$http.get("https://api.github.com/search/users?q=" + this.keyWord).then(
        (res) => {
          this.$bus.$emit("updateListData", {
            isLoading: false,
            errMsg: "",
            users: res.data.items,
          });
        },
        (error) => {
          console.log(error.message,1);
          this.$bus.$emit("updateListData", {
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
```

### 37.slot插槽

### 1.默认插槽

Category.vue

```vue
<template>
  <div class="category">
    <h3>{{title}}分类</h3>
    <!-- 插槽 -->
    <slot>我是一些默认值，当使用者没有传递具体结构时，我会出现</slot>
  </div>
</template>

<script>
export default {
  name: "Category",
  data() {
    return {};
  },
  props:['title'],
};
</script>

<style scoped>
.category {
  background-color: skyblue;
  width: 200px;
  height: 300px;
}
h3 {
  background-color: orange;
  text-align: center;
}
</style>
```

App.vue

```vue
<template>
  <div class="container">
    <Category title="美食" :listData="foods">
      <img src="https://s3.ax1x.com/2021/01/16/srJlq0.jpg" alt="" />
    </Category>
    <Category title="游戏" :listData="games">
      <li v-for="(g, index) in games" :key="index">{{ g }}</li>
    </Category>
    <Category title="电影" :listData="films">
      <video
        controls
        src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"
      ></video>
    </Category>
  </div>
</template>

<script>
import Category from "./components/Category.vue";
export default {
  name: "App",
  data() {
    return {
      foods: ["火锅", "烧烤", "小龙虾", "牛排"],
      games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"],
      films: ["《教父》", "《拆弹专家》", "《你好李焕英》", "《尚硅谷》"],
    };
  },
  components: { Category },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-around;
}
img {
  width: 100%;
}
video {
  width: 100%;
}
</style>
```

![image-20220501160435567](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202205011604706.png)

### 2.具名插槽

App.vue

```vue
<template>
  <div class="container">
    <Category title="美食" :listData="foods">
        
      <img
        slot="center"
        src="https://s3.ax1x.com/2021/01/16/srJlq0.jpg"
        alt=""
      />
      <a slot="footer" href="www.baidu.com">更多美食</a>
    </Category>
    <Category title="游戏" :listData="games">
      <li slot="center" v-for="(g, index) in games" :key="index">{{ g }}</li>
      <div class="foot" slot="footer">
        <a href="www.baidu.com">网络游戏</a>
        <a href="www.baidu.com">单机游戏</a>
      </div>
    </Category>
    <Category title="电影" :listData="films">
      <video
        slot="center" 
        controls
        src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"
      ></video>
      <!-- template可以使用v-slot:footer,其他形式则不行 -->
      <template  v-slot:footer >
        <div class="foot">
        <a href="www.baidu.com">经典</a>
        <a href="www.baidu.com">热门</a>
        <a href="www.baidu.com">推荐</a>
      </div>
       <h4 class="foot" slot="footer">欢迎前来观影</h4>
      </template>
      
     
    </Category>
  </div>
</template>

<script>
import Category from "./components/Category.vue";
export default {
  name: "App",
  data() {
    return {
      foods: ["火锅", "烧烤", "小龙虾", "牛排"],
      games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"],
      films: ["《教父》", "《拆弹专家》", "《你好李焕英》", "《尚硅谷》"],
    };
  },
  components: { Category },
};
</script>

<style scoped>
.container,.foot {
  display: flex;
  justify-content: space-around;
}
img {
  width: 100%;
}
video {
  width: 100%;
}
</style>
```

Category.vue

```vue
<template>
  <div class="category">
    <h3>{{title}}分类</h3>
    <!-- 具名插槽，指定名字 -->
    <slot name="center">我是一些默认值，当使用者没有传递具体结构时，我会出现1</slot>
    <slot name="footer">我是一些默认值，当使用者没有传递具体结构时，我会出现2</slot>
  </div>
</template>

<script>
export default {
  name: "Category",
  data() {
    return {};
  },
  props:['title'],
};
</script>

<style scoped>
.category {
  background-color: skyblue;
  width: 200px;
  height: 300px;
}
h3 {
  background-color: orange;
  text-align: center;
}
</style>

```

### 3.作用域插槽

App.vue

```vue
<template>
  <div class="container">
    <Category title="游戏">
        <!-- 接受games命名为atguigu -->
      <template scope="atguigu">
        <ul>
          <li v-for="(g,index) in atguigu.games" :key="index">{{g}}</li>
        </ul>
      </template>
    </Category>
    <Category title="游戏">
      <template scope="atguigu">
        <ol>
          <li style="color:red" v-for="(g,index) in atguigu.games" :key="index">{{g}}</li>
        </ol>
      </template>
    </Category>
  </div>
</template>

<script>
import Category from "./components/Category.vue";
export default {
  name: "App",

  components: { Category },
};
</script>

<style scoped>
.container,
.foot {
  display: flex;
  justify-content: space-around;
}
img {
  width: 100%;
}
video {
  width: 100%;
}
</style>

```

Category.vue

```vue
<template>
  <div class="category">
    <h3>{{title}}分类</h3>
    <!-- 插槽,传入games -->
    <slot :games="games">我是默认的一些内容</slot>
  </div>
</template>

<script>
export default {
  name: "Category",
  data() {
    return {
      games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"],
    };
  },
  props:['title'],
};
</script>

<style scoped>
.category {
  background-color: skyblue;
  width: 200px;
  height: 300px;
}
h3 {
  background-color: orange;
  text-align: center;
}
</style>
```

> 1. 作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于 <strong style="color:red">父组件 ===> 子组件</strong> 。
>
> 2. 分类：默认插槽、具名插槽、作用域插槽
>
> 3. 使用方式：
>
>    1. 默认插槽：
>
>       ```vue
>       父组件中：
>               <Category>
>                  <div>html结构1</div>
>               </Category>
>       子组件中：
>               <template>
>                   <div>
>                      <!-- 定义插槽 -->
>                      <slot>插槽默认内容...</slot>
>                   </div>
>               </template>
>       ```
>
>    2. 具名插槽：
>
>       ```vue
>       父组件中：
>               <Category>
>                   <template slot="center">
>                     <div>html结构1</div>
>                   </template>
>       
>                   <template v-slot:footer>
>                      <div>html结构2</div>
>                   </template>
>               </Category>
>       子组件中：
>               <template>
>                   <div>
>                      <!-- 定义插槽 -->
>                      <slot name="center">插槽默认内容...</slot>
>                      <slot name="footer">插槽默认内容...</slot>
>                   </div>
>               </template>
>       ```
>
>    3. 作用域插槽：
>
>       1. 理解：<span style="color:red">数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。</span>（games数据在Category组件中，但使用数据所遍历出来的结构由App组件决定）
>
>       2. 具体编码：
>
>          ```vue
>          父组件中：
>          		<Category>
>          			<template scope="scopeData">
>          				<!-- 生成的是ul列表 -->
>          				<ul>
>          					<li v-for="g in scopeData.games" :key="g">{{g}}</li>
>          				</ul>
>          			</template>
>          		</Category>
>                                                       
>          		<Category>
>          			<template slot-scope="scopeData">
>          				<!-- 生成的是h4标题 -->
>          				<h4 v-for="g in scopeData.games" :key="g">{{g}}</h4>
>          			</template>
>          		</Category>
>          子组件中：
>                  <template>
>                      <div>
>                          <slot :games="games"></slot>
>                      </div>
>                  </template>
>          		                                             
>                  <script>
>                      export default {
>                          name:'Category',
>                          props:['title'],
>                          //数据在子组件自身
>                          data() {
>                              return {
>                                  games:['红色警戒','穿越火线','劲舞团','超级玛丽']
>                              }
>                          },
>                      }
>                  </script>
>          ```

## 37.Vuex

### 1.概念

> ​	在Vue中实现集中式状态（数据）管理的一个Vue插件，对vue应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。

### 2.何时使用？

多个组件需要共享数据时

### 3.搭建Vuex环境

1. 创建文件：```src/store/index.js```

   ```js
   //引入Vue核心库
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //应用Vuex插件
   Vue.use(Vuex)
   
   //准备actions对象——响应组件中用户的动作
   const actions = {}
   //准备mutations对象——修改state中的数据
   const mutations = {}
   //准备state对象——保存具体的数据
   const state = {}
   
   //创建并暴露store
   export default new Vuex.Store({
   	actions,
   	mutations,
   	state
   })
   ```

2. 在```main.js```中创建vm时传入```store```配置项

   ```js
   ......
   //引入store
   import store from './store'
   ......
   
   //创建vm
   new Vue({
   	el:'#app',
   	render: h => h(App),
   	store
   })
   ```

###    4.基本使用

1. 初始化数据、配置```actions```、配置```mutations```，操作文件```store.js```

   ```js
   //引入Vue核心库
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //引用Vuex
   Vue.use(Vuex)
   
   const actions = {
       //响应组件中加的动作
   	jia(context,value){
   		// console.log('actions中的jia被调用了',miniStore,value)
   		context.commit('JIA',value)
   	},
   }
   
   const mutations = {
       //执行加
   	JIA(state,value){
   		// console.log('mutations中的JIA被调用了',state,value)
   		state.sum += value
   	}
   }
   
   //初始化数据
   const state = {
      sum:0
   }
   
   //创建并暴露store
   export default new Vuex.Store({
   	actions,
   	mutations,
   	state,
   })
   ```

2. 组件中读取vuex中的数据：```$store.state.sum```

3. 组件中修改vuex中的数据：```$store.dispatch('action中的方法名',数据)``` 或 ```$store.commit('mutations中的方法名',数据)```

   >  备注：若没有网络请求或其他业务逻辑，组件中也可以越过actions，即不写```dispatch```，直接编写```commit```

### 5.getters的使用

1. 概念：当state中的数据需要经过加工后再使用时，可以使用getters加工。

2. 在```store.js```中追加```getters```配置

   ```js
   ......
   
   const getters = {
       bigSum(state){
           return state.sum * 10
       }
   }
   
   //创建并暴露store
   export default new Vuex.Store({
       ......
       getters
   })
   ```

3. 组件中读取数据：```$store.getters.bigSum```

### 6.四个map方法的使用



1. <strong>mapState方法：</strong>用于帮助我们映射```state```中的数据为计算属性

   ```js
   computed: {
       //借助mapState生成计算属性：sum、school、subject（对象写法）
        ...mapState({sum:'sum',school:'school',subject:'subject'}),
            
       //借助mapState生成计算属性：sum、school、subject（数组写法）
       ...mapState(['sum','school','subject']),
   },
   ```

2. <strong>mapGetters方法：</strong>用于帮助我们映射```getters```中的数据为计算属性

   ```js
   computed: {
       //借助mapGetters生成计算属性：bigSum（对象写法）
       ...mapGetters({bigSum:'bigSum'}),
   
       //借助mapGetters生成计算属性：bigSum（数组写法）
       ...mapGetters(['bigSum'])
   },
   ```

4. <strong>mapMutations方法：</strong>用于帮助我们生成与```mutations```对话的方法，即：包含```$store.commit(xxx)```的函数

   ```js
   methods:{
       //靠mapActions生成：increment、decrement（对象形式）
       ...mapMutations({increment:'JIA',decrement:'JIAN'}),
       
       //靠mapMutations生成：JIA、JIAN（对象形式）
       ...mapMutations(['JIA','JIAN']),
   }
   ```

> 备注：mapActions与mapMutations使用时，若需要传递参数需要：在模板中绑定事件时传递好参数，否则参数是事件对象。

### 7.模块化+命名空间

1. 目的：让代码更好维护，让多种数据分类更加明确。

2. 修改```store.js```

   ```javascript
   const countAbout = {
     namespaced:true,//开启命名空间
     state:{x:1},
     mutations: { ... },
     actions: { ... },
     getters: {
       bigSum(state){
          return state.sum * 10
       }
     }
   }
   
   const personAbout = {
     namespaced:true,//开启命名空间
     state:{ ... },
     mutations: { ... },
     actions: { ... }
   }
   
   const store = new Vuex.Store({
     modules: {
       countAbout,
       personAbout
     }
   })
   ```

3. 开启命名空间后，组件中读取state数据：

   ```js
   //方式一：自己直接读取
   this.$store.state.personAbout.list
   //方式二：借助mapState读取：
   ...mapState('countAbout',['sum','school','subject']),
   ```

4. 开启命名空间后，组件中读取getters数据：

   ```js
   //方式一：自己直接读取
   this.$store.getters['personAbout/firstPersonName']
   //方式二：借助mapGetters读取：
   ...mapGetters('countAbout',['bigSum'])
   ```

5. 开启命名空间后，组件中调用dispatch

   ```js
   //方式一：自己直接dispatch
   this.$store.dispatch('personAbout/addPersonWang',person)
   //方式二：借助mapActions：
   ...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   ```

6. 开启命名空间后，组件中调用commit

   ```js
   //方式一：自己直接commit
   this.$store.commit('personAbout/ADD_PERSON',person)
   //方式二：借助mapMutations：
   ...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
   ```

## 38.路由

1. 理解： 一个路由（route）就是一组映射关系（key - value），多个路由需要路由器（router）进行管理。
2. 前端路由：key是路径，value是组件。

### 1.基本使用

1. 安装vue-router，命令：```npm i vue-router```

2. 应用插件：```Vue.use(VueRouter)```

3. 编写router配置项:

   ```js
   //引入VueRouter
   import VueRouter from 'vue-router'
   //引入Luyou 组件
   import About from '../components/About'
   import Home from '../components/Home'
   
   //创建router实例对象，去管理一组一组的路由规则
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
   
   //暴露router
   export default router
   ```

4. 实现切换（active-class可配置高亮样式）

   ```vue
   <router-link active-class="active" to="/about">About</router-link>
   ```

5. 指定展示位置

   ```vue
   <router-view></router-view>

### 2.几个注意点

1. 路由组件通常存放在```pages```文件夹，一般组件通常存放在```components```文件夹。
2. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载。
3. 每个组件都有自己的```$route```属性，里面存储着自己的路由信息。
4. 整个应用只有一个router，可以通过组件的```$router```属性获取到。

### 3.多级路由（多级路由）

1. 配置路由规则，使用children配置项：

   ```js
   routes:[
   	{
   		path:'/about',
   		component:About,
   	},
   	{
   		path:'/home',
   		component:Home,
   		children:[ //通过children配置子级路由
   			{
   				path:'news', //此处一定不要写：/news
   				component:News
   			},
   			{
   				path:'message',//此处一定不要写：/message
   				component:Message
   			}
   		]
   	}
   ]
   ```

2. 跳转（要写完整路径）：

   ```vue
   <router-link to="/home/news">News</router-link>
   ```

### 4.路由的query参数

1. 传递参数

   ```vue
   <!-- 跳转并携带query参数，to的字符串写法 -->
   <router-link :to="/home/message/detail?id=666&title=你好">跳转</router-link>
   				
   <!-- 跳转并携带query参数，to的对象写法 -->
   <router-link 
   	:to="{
   		path:'/home/message/detail',
   		query:{
   		   id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

2. 接收参数：

   ```js
   $route.query.id
   $route.query.title
   ```

### 5.命名路由

1. 作用：可以简化路由的跳转。

2. 如何使用

   1. 给路由命名：

      ```js
      {
      	path:'/demo',
      	component:Demo,
      	children:[
      		{
      			path:'test',
      			component:Test,
      			children:[
      				{
                            name:'hello' //给路由命名
      					path:'welcome',
      					component:Hello,
      				}
      			]
      		}
      	]
      }
      ```

   2. 简化跳转：

      ```vue
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
      ```

### 6.路由的params参数

1. 配置路由，声明接收params参数

   ```js
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
   					path:'detail/:id/:title', //使用占位符声明接收params参数
   					component:Detail
   				}
   			]
   		}
   	]
   }
   ```

2. 传递参数

   ```vue
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
   ```

   > 特别注意：路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置！



### 7.路由的props配置

	作用：让路由组件更方便的收到参数

```js
{
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,

	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
	// props:{a:900}

	//第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数通过props传给Detail组件
	// props:true
	
	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
	props(route){
		return {
			id:route.query.id,
			title:route.query.title
		}
	}
}
```

### 8.```<router-link>```的replace属性

1. 作用：控制路由跳转时操作浏览器历史记录的模式
2. 浏览器的历史记录有两种写入方式：分别为```push```和```replace```，```push```是追加历史记录，```replace```是替换当前记录。路由跳转时候默认为```push```
3. 如何开启```replace```模式：```<router-link replace .......>News</router-link>```

### 9.编程式路由导航

1. 作用：不借助```<router-link> ```实现路由跳转，让路由跳转更加灵活

2. 具体编码：

   ```js
   //$router的两个API
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
   this.$router.forward() //前进
   this.$router.back() //后退
   this.$router.go() //可前进也可后退 参数是number类型(正数为前进的步数,负数为后退的部署)
   ```

### 10.缓存路由组件

1. 作用：让不展示的路由组件保持挂载，不被销毁。

2. 具体编码：

   ```vue
   <keep-alive include="News"> 
       <router-view></router-view>
   </keep-alive>
   ```

### 11.两个新的生命周期钩子

1. 作用：路由组件所独有的两个钩子，用于捕获路由组件的激活状态。
2. 具体名字：
   1. ```activated```路由组件被激活时触发。
   2. ```deactivated```路由组件失活时触发。

### 12.路由守卫

1. 作用：对路由进行权限控制

2. 分类：全局守卫、独享守卫、组件内守卫

3. 全局守卫:

   ```js
   //全局前置守卫：初始化时执行、每次路由切换前执行
   router.beforeEach((to,from,next)=>{
   	console.log('beforeEach',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
   		if(localStorage.getItem('school') === 'atguigu'){ //权限控制的具体规则
   			next() //放行
   		}else{
   			alert('暂无权限查看')
   			// next({name:'guanyu'})
   		}
   	}else{
   		next() //放行
   	}
   })
   
   //全局后置守卫：初始化时执行、每次路由切换后执行
   router.afterEach((to,from)=>{
   	console.log('afterEach',to,from)
   	if(to.meta.title){ 
   		document.title = to.meta.title //修改网页的title
   	}else{
   		document.title = 'vue_test'
   	}
   })
   ```

### 13.路由器的两种工作模式


1. 对于一个url来说，什么是hash值？—— #及其后面的内容就是hash值。
2. hash值不会包含在 HTTP 请求中，即：hash值不会带给服务器。
3. hash模式：
   1. 地址中永远带着#号，不美观 。
   2. 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。
   3. 兼容性较好。
4. history模式：
   1. 地址干净，美观 。
   2. 兼容性和hash模式相比略差。
   3. 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。
