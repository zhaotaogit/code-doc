# Vue3

## 1.Vue3简介

- 2020年9月18日，Vue.js发布3.0版本，代号：One Piece（海贼王）
- 耗时2年多、[2600+次提交](https://github.com/vuejs/vue-next/graphs/commit-activity)、[30+个RFC](https://github.com/vuejs/rfcs/tree/master/active-rfcs)、[600+次PR](https://github.com/vuejs/vue-next/pulls?q=is%3Apr+is%3Amerged+-author%3Aapp%2Fdependabot-preview+)、[99位贡献者](https://github.com/vuejs/vue-next/graphs/contributors)
- github上的tags地址：https://github.com/vuejs/vue-next/releases/tag/v3.0.0

## 2.Vue3带来了什么

### 1.性能的提升

- 打包大小减少41%

- 初次渲染快55%, 更新渲染快133%

- 内存减少54%

  ......

### 2.源码的升级

- 使用Proxy代替defineProperty实现响应式

- 重写虚拟DOM的实现和Tree-Shaking

  ......

### 3.拥抱TypeScript

- Vue3可以更好的支持TypeScript

### 4.新的特性

1. Composition API（组合API）

    - setup配置
    - ref与reactive
    - watch与watchEffect
    - provide与inject
    - ......
2. 新的内置组件
    - Fragment
    - Teleport
    - Suspense
3. 其他改变

    - 新的生命周期钩子
    - data 选项应始终被声明为一个函数
    - 移除keyCode支持作为 v-on 的修饰符
    - ......

## 3.创建Vue3工程

### 1.使用 vue-cli 创建

官方文档：https://cli.vuejs.org/zh/guide/installation.html

```bash
## 查看@vue/cli版本，确保@vue/cli版本在4.5.0以上
vue --version
## 安装或者升级你的@vue/cli
npm install -g @vue/cli
## 创建
vue create vue_test
## 启动
cd vue_test
npm run serve
```

### 2.使用 vite 创建

官方文档：https://v3.cn.vuejs.org/guide/installation.html#vite

vite官网：https://vitejs.cn

- 什么是vite？—— 新一代前端构建工具。
- 优势如下：
   - 开发环境中，无需打包操作，可快速的冷启动。
   - 轻量快速的热重载（HMR）。
   - 真正的按需编译，不再等待整个应用编译完成。
- 传统构建 与 vite构建对比图

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202205051649122.png" style="width:500px;height:280px;float:left" /><img src="https://cn.vitejs.dev/assets/esm.3070012d.png" style="width:480px;height:280px" />

```bash
## 创建工程
npm init vite@latest
## 进入工程目录
cd <project-name>
## 安装依赖
npm install
## 运行
npm run dev
```

## 二、常用 Composition API

官方文档: https://v3.cn.vuejs.org/guide/composition-api-introduction.html

## 1.拉开序幕的setup

1. 理解：Vue3.0中一个新的配置项，值为一个函数。
2. setup是所有<strong style="color:#DD5145">Composition API（组合API）</strong><i style="color:gray;font-weight:bold">“ 表演的舞台 ”</i>。
3. 组件中所用到的：数据、方法等等，均要配置在setup中。
5. setup函数的两种返回值：
    1. 若返回一个对象，则对象中的属性、方法, 在模板中均可以直接使用。（重点关注！）
    2. <span style="color:#aad">若返回一个渲染函数：则可以自定义渲染内容。（了解）</span>
6. 注意点：
    1. 尽量不要与Vue2.x配置混用
        - Vue2.x配置（data、methos、computed...）中<strong style="color:#DD5145">可以访问到</strong>setup中的属性、方法。
        - 但在setup中<strong style="color:#DD5145">不能访问到</strong>Vue2.x配置（data、methos、computed...）。
        - 如果有重名, setup优先。
    2. setup不能是一个async函数，因为返回值不再是return的对象, 而是promise, 模板看不到return对象中的属性。（后期也可以返回一个Promise实例，但需要Suspense和异步组件的配合）

App.vue

```vue
<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h2>性别：{{sex}}</h2>
  <h2>a的值为：{{a}}</h2>
  <button @click="sayHello">说话(Vue3配置的)</button>
  <br><br>
  <button @click="sayWelcome">说话(vue2配置的)</button>
  <br><br>
  <button @click="test1">测试以下在vue2配置中读取Vue3中的数据</button>
  <br><br>
  <button @click="test2">测试以下在vue3配置中读取Vue2中的数据</button>
</template>

<script>
// import { h } from "vue";
export default {
  name: "App",
  data() {
    return {
      sex: "男",
      a:100
    };
  },
  methods: {
    sayWelcome() {
      alert("欢迎学习Vue")
    },
    test1(){
      console.log(this.name);
      console.log(this.age);
      console.log(this.sex);
      console.log(this.sayWelcome);
    }
  },
  // 此处不考虑响应式
  setup() {
    // 数据
    let name = "张三";
    let age = 18;
    let a = 200;
    // 方法
    function sayHello() {
      alert(`我叫${name}，今年${age}岁,你好啊！`);
    }
    function test2() {
      console.log(name);
      console.log(age);
      console.log(this.sex);
      console.log(this.sayHello);
    }
    // 返回一个对象(常用)
    return {
      name,
      age,
      a,
      sayHello,
      test2
    };
    // 返回一个函数(不常用)
    // return ()=> h('h1','尚硅谷')
  },
};
</script>

<style></style>

```

###  2.ref函数

- 作用: 定义一个响应式的数据
- 语法: ```const xxx = ref(initValue)```
    - 创建一个包含响应式数据的<strong style="color:#DD5145">引用对象（reference对象，简称ref对象）</strong>。
    - JS中操作数据： ```xxx.value```
    - 模板中读取数据: 不需要.value，直接：```<div>{{xxx}}</div>```
- 备注：
    - 接收的数据可以是：基本类型、也可以是对象类型。
    - 基本类型的数据：响应式依然是靠``Object.defineProperty()``的```get```与```set```完成的。
    - 对象类型的数据：内部 <i style="color:gray;font-weight:bold">“ 求助 ”</i> 了Vue3.0中的一个新函数—— ```reactive```函数。

App.vue

```vue
<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h3>工作种类:{{job.type}}</h3>
  <h3>工作薪水:{{job.salary}}</h3>
  <button @click="changeInfo">修改人的信息</button>
</template>

<script>
import {ref} from 'vue'
export default {
  name: "App",
  setup() {
    // 数据
    let name = ref("张三");
    let age = ref(18);
    let job = ref({
      type:'前端',
      salary:'30K'
    })

    function changeInfo() {
      name.value = "李四";
      age.value = 15;
      job.value.type = 'UI设计师'
      job.value.salary = '60K'
      console.log(name,age);
    }
    // 返回一个对象(常用)
    return {
      name,
      age,
      job,
      changeInfo,
    };
  },
};
</script>

<style></style>
```

### 3.reactive函数

- 作用: 定义一个<strong style="color:#DD5145">对象类型</strong>的响应式数据（基本类型不要用它，要用```ref```函数）
- 语法：```const 代理对象= reactive(源对象)```接收一个对象（或数组），返回一个<strong style="color:#DD5145">代理对象（Proxy的实例对象，简称proxy对象）</strong>
- reactive定义的响应式数据是“深层次的”。
- 内部基于 ES6 的 Proxy 实现，通过代理对象操作源对象内部数据进行操作。

App.vue

```vue
<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{ person.name }}</h2>
  <h2>年龄：{{ person.age }}</h2>
  <h3>工作种类:{{ person.job.type }}</h3>
  <h3>工作薪水:{{ person.job.salary }}</h3>
  <h3>爱好:{{ person.hobby }}</h3>
  <h3>测试的数据:{{ person.job.a.b.c }}</h3>
  <button @click="changeInfo">修改人的信息</button>
</template>

<script>
import {reactive } from "vue";
export default {
  name: "App",
  setup() {
    // 数据
    const person = reactive({
      name: "张三",
      age: 18,
      job: {
        type: "前端",
        salary: "30K",
        a: {
          b: {
            c: 666,
          },
        },
      },
      hobby: ["抽烟", "喝酒", "烫头"],
    })
    // 方法 
    function changeInfo() {
      person.name = "李四";
      person.age = 15;
      person.job.type = "UI设计师";
      person.job.salary = "60K";
      person.job.a.b.c = 999;
      person.hobby[0] = "学习";
    }
    // 返回一个对象(常用)
    return {
      person,
      changeInfo,
    };
  },
};
</script>

<style></style>
```

### 4.Vue3.0中的响应式原理

#### vue2.x的响应式

- 实现原理：
    - 对象类型：通过```Object.defineProperty()```对属性的读取、修改进行拦截（数据劫持）。

    - 数组类型：通过重写更新数组的一系列方法来实现拦截。（对数组的变更方法进行了包裹）。

      ```js
      Object.defineProperty(data, 'count', {
          get () {}, 
          set () {}
      })
      ```

- 存在问题：
    - 新增属性、删除属性, 界面不会更新。
    - 直接通过下标修改数组, 界面不会自动更新。

#### Vue3.0的响应式

- 实现原理:
    - 通过Proxy（代理）:  拦截对象中任意属性的变化, 包括：属性值的读写、属性的添加、属性的删除等。
    - 通过Reflect（反射）:  对源对象的属性进行操作。
    - MDN文档中描述的Proxy与Reflect：
        - Proxy：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy

        - Reflect：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect

          ```js
          new Proxy(data, {
              // 拦截读取属性值
              get (target, prop) {
                  return Reflect.get(target, prop)
              },
              // 拦截设置属性值或添加新属性
              set (target, prop, value) {
                  return Reflect.set(target, prop, value)
              },
              // 拦截删除属性
              deleteProperty (target, prop) {
                  return Reflect.deleteProperty(target, prop)
              }
          })
          
          proxy.name = 'tom'   

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue3的响应式原理</title>
</head>

<body>
    <script>
        // 元数据
        let person = {
            name: '张三',
            age: 18
        }
        // 模拟Vue2中的实现响应式原理
        // let p = {}
        // Object.defineProperty(p, 'name', {
        //     // 有人读取name时调用
        //     get() {
        //         return person.name
        //     },
        //     set(value) {
        //         console.log('有人修改了name属性，我发现了，我要去更新界面。');
        //         person.name = value
        //     }
        // })
        // Object.defineProperty(p, 'age', {
        //     // 有人读取name时调用
        //     get() {
        //         return person.age
        //     },
        //     set(value) {
        //         console.log('有人修改了name属性，我发现了，我要去更新界面。');
        //         person.age = value
        //     }
        // })
    

        // 模拟Vue3中实现响应式
        const p = new Proxy(person, {
            // 有人读取p的某个属性时调用
            get(target, propName) {
                console.log(target, propName);
                console.log('有人读取了' + propName + '属性，我发现了，我要去更新界面。');
                // return target[propName]
                return Reflect.get(target,propName)
            },
            // 有人修改p的某个属性、或给p追加某个属性时调用
            set(target,propName,value){
                console.log(target, propName, value);
                console.log('有人修改了' + propName + '属性，我发现了，我要去更新界面。');
                // target[propName] = value
                Reflect.set(target,propName,value)
            },
            // 有人删除p的某个属性时调用
            defineProperty(target, propName) {
                console.log(target, propName);
                console.log('有人删除了' + propName + '属性，我发现了，我要去更新界面。');
                // return delete target[propName]
                return Reflect.defineProperty(target,propName)
            }
        })



        // let obj = {a:1,b:2}
        // 通过Object.defineProperty操作
        // Object.defineProperty(obj,'c',{
        //     get(){
        //         return 3
        //     }
        // })


        // 通过Reflect.defineProperty反射对象操作
        // const x1 = Reflect.defineProperty(obj,'c',{
        //     get(){
        //         return 3
        //     }
        // })
        // const x2 = Reflect.defineProperty(obj,'c',{
        //     get(){
        //         return 4
        //     }
        // })
    </script>
</body>

</html>
```

### 5.reactive对比ref

-  从定义数据角度对比：
    -  ref用来定义：<strong style="color:#DD5145">基本类型数据</strong>。
    -  reactive用来定义：<strong style="color:#DD5145">对象（或数组）类型数据</strong>。
    -  备注：ref也可以用来定义<strong style="color:#DD5145">对象（或数组）类型数据</strong>, 它内部会自动通过```reactive```转为<strong style="color:#DD5145">代理对象</strong>。
-  从原理角度对比：
    -  ref通过``Object.defineProperty()``的```get```与```set```来实现响应式（数据劫持）。
    -  reactive通过使用<strong style="color:#DD5145">Proxy</strong>来实现响应式（数据劫持）, 并通过<strong style="color:#DD5145">Reflect</strong>操作<strong style="color:orange">源对象</strong>内部的数据。
-  从使用角度对比：
    -  ref定义的数据：操作数据<strong style="color:#DD5145">需要</strong>```.value```，读取数据时模板中直接读取<strong style="color:#DD5145">不需要</strong>```.value```。
    -  reactive定义的数据：操作数据与读取数据：<strong style="color:#DD5145">均不需要</strong>```.value```。

### 6.setup的两个注意点

- setup执行的时机
    - 在beforeCreate之前执行一次，this是undefined。
- setup的参数
    - props：值为对象，包含：组件外部传递过来，且组件内部声明接收了的属性。
    - context：上下文对象
        - attrs: 值为对象，包含：组件外部传递过来，但没有在props配置中声明的属性, 相当于 ```this.$attrs```。
        - slots: 收到的插槽内容, 相当于 ```this.$slots```。
        - emit: 分发自定义事件的函数, 相当于 ```this.$emit```。

App.vue

```vue
<template>
  <Demo @hello="showHelloMsg" msg="你好啊" school="尚硅谷">
    <template v-slot:qwe>
      <span>尚硅谷</span>
    </template>
  </Demo>
</template>

<script>
import Demo from "./component/Demo.vue";
export default {
  name: "App",
  components: {
    Demo,
  },
  setup() {
    function showHelloMsg(value) {
      alert("你好啊，你触发了hello事件，我收到的参数是:" + value);
    }
    return {
      showHelloMsg,
    };
  },
};
</script>
```

Demo.vue

```vue
<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{ person.name }}</h2>
  <h2>年龄：{{ person.age }}</h2>
  <button @click="test">测试触发以下Demo组件的Hello事件</button>
</template>

<script>
import { reactive } from "vue";
export default {
  name: "Demo",
  beforeCreate() {
    console.log("-----beforeCreate");
  },
  props: ["msg", "school"],
  emits: ["hello"],
  setup(props, context) {
    console.log(props, context);
    //   console.log(props,context.$attrs); // 详单与vue2中的$arrts
    //   console.log(props,context.emit); // 触发自定义事件
    console.log(context.slots); // 插槽
    console.log("----setup------");
    // 数据
    const person = reactive({
      name: "张三",
      age: 18,
    });
    function test() {
      console.log("测试触发以下Demo组件的Hello事件");
      context.emit("hello", 666);
    }
    return {
      person,
      test,
    };
  },
};
</script>
```

## 7.计算属性与监视

### 1.computed函数

- 与Vue2.x中computed配置功能一致

- 写法

  ```js
  import {computed} from 'vue'
  
  setup(){
      ...
  	//计算属性——简写
      let fullName = computed(()=>{
          return person.firstName + '-' + person.lastName
      })
      //计算属性——完整
      let fullName = computed({
          get(){
              return person.firstName + '-' + person.lastName
          },
          set(value){
              const nameArr = value.split('-')
              person.firstName = nameArr[0]
              person.lastName = nameArr[1]
          }
      })
  }
  ```

### 2.watch函数

- 与Vue2.x中watch配置功能一致

- 两个小“坑”：

    - 监视reactive定义的响应式数据时：oldValue无法正确获取、强制开启了深度监视（deep配置失效）。
    - 监视reactive定义的响应式数据中某个属性时：deep配置有效。

  ```js
  //情况一：监视ref定义的响应式数据
  watch(sum,(newValue,oldValue)=>{
  	console.log('sum变化了',newValue,oldValue)
  },{immediate:true})
  
  //情况二：监视多个ref定义的响应式数据
  watch([sum,msg],(newValue,oldValue)=>{
  	console.log('sum或msg变化了',newValue,oldValue)
  }) 
  
  /* 情况三：监视reactive定义的响应式数据
  			若watch监视的是reactive定义的响应式数据，则无法正确获得oldValue！！
  			若watch监视的是reactive定义的响应式数据，则强制开启了深度监视 
  */
  watch(person,(newValue,oldValue)=>{
  	console.log('person变化了',newValue,oldValue)
  },{immediate:true,deep:false}) //此处的deep配置不再奏效
  
  //情况四：监视reactive定义的响应式数据中的某个属性
  watch(()=>person.job,(newValue,oldValue)=>{
  	console.log('person的job变化了',newValue,oldValue)
  },{immediate:true,deep:true}) 
  
  //情况五：监视reactive定义的响应式数据中的某些属性
  watch([()=>person.job,()=>person.name],(newValue,oldValue)=>{
  	console.log('person的job变化了',newValue,oldValue)
  },{immediate:true,deep:true})
  
  //特殊情况
  watch(()=>person.job,(newValue,oldValue)=>{
      console.log('person的job变化了',newValue,oldValue)
  },{deep:true}) //此处由于监视的是reactive素定义的对象中的某个属性，所以deep配置有效
  ```

Demo1.vue
```vue
<template>
  <h2>当前求和为:{{ sum }}</h2>
  <button @click="sum++">点我+1</button>
  <hr />
  <h2>当前的信息为：{{ msg }}</h2>
  <button @click="msg += '!'">修改信息</button>
  <hr />
  <h2>姓名：{{ person.name }}</h2>
  <h2>年龄：{{ person.age }}</h2>
  <h2>薪资：{{ person.job.j1.salary }}k</h2>
  <button @click="person.name += '~'">修改姓名</button>
  <button @click="person.age++">增长年龄</button>
  <button @click="person.job.j1.salary++">涨薪</button>
</template>

<script>
import { reactive, ref, watch } from "vue";
export default {
  name: "Demo",
  // watch:{
  // 简写方式
  // sum(newValue, oldValue){
  //   console.log('sum的值变化了',newValue, oldValue);
  // }
  // 完整写法
  //   sum:{
  //     deep:true,  // 深度监视
  //     immediate:true, // 立即执行
  //     handler(newValue, oldValue){
  //       console.log('sum的值变化了',newValue, oldValue);
  //     }
  //   }
  // },
  setup() {
    let sum = ref(0);
    let msg = ref("你好啊");

    let person = reactive({
      name: "张三",
      age: 18,
      job: {
        j1: {
          salary: 20,
        },
      },
    });
    // 情况1：监视ref所定义的一个响应式数据
    // watch(sum,(newValue,oldValue)=>{
    //   console.log('sum的值变化了',newValue,oldValue);
    // })
    // 情况2：监视ref所定义的多个响应式数据
    // watch(
    //   sum,
    //   (newValue, oldValue) => {
    //     console.log("sum变化了", newValue, oldValue);
    //   },
    //   { immediate: true }
    // );
    // watch(
    //   [msg, watch],
    //   (newValue, oldValue) => {
    //     console.log("sum或msg变了", newValue, oldValue);
    //   },
    //   { immediate: true }
    // );
    /*
      情况3：监视reactive所定义的一个响应式数据
      1.注意：此处无法正确获取oldvalue
      2.注意：强制开启了深度监视(deep配置无效)
      */
    // watch(person, (newValue, oldValue) => {
    //   console.log("person变化了", newValue, oldValue);
    // },{deep:false}); // 此处的deep配置无效
    // 情况4：监视reactive所定义的一个响应式数据中的某个属性
    // watch(
    //   () => person.name,
    //   (newValue, oldValue) => {
    //     console.log("person.name变化了", newValue, oldValue);
    //   }
    // );
    // 情况5：监视reactive所定义的一个响应式数据中的某些属性
    watch([() => person.age, () => person.name], (newValue, oldValue) => {
      console.log("person.age或person.name变化了", newValue, oldValue);
    });
    // 特殊情况
    watch(()=>person.job,(newValue,oldValue)=>{
      console.log('person.job发生变化了',newValue,oldValue);
    },{deep:true});
    return {
      sum,
      msg,
      person,
    };
  },
};
</script>
```

Demo2.vue

```vue
<template>
  <h2>当前求和为:{{ sum }}</h2>
  <button @click="sum++">点我+1</button>
  <hr />
  <h2>当前的信息为：{{ msg }}</h2>
  <button @click="msg += '!'">修改信息</button>
  <hr />
  <h2>姓名：{{ person.name }}</h2>
  <h2>年龄：{{ person.age }}</h2>
  <h2>薪资：{{ person.job.j1.salary }}k</h2>
  <button @click="person.name += '~'">修改姓名</button>
  <button @click="person.age++">增长年龄</button>
  <button @click="person.job.j1.salary++">涨薪</button>
</template>

<script>
import { reactive, ref, watch } from "vue";
export default {
  name: "Demo",
  // watch:{
  // 简写方式
  // sum(newValue, oldValue){
  //   console.log('sum的值变化了',newValue, oldValue);
  // }
  // 完整写法
  //   sum:{
  //     deep:true,  // 深度监视
  //     immediate:true, // 立即执行
  //     handler(newValue, oldValue){
  //       console.log('sum的值变化了',newValue, oldValue);
  //     }
  //   }
  // },
  setup() {
    let sum = ref(0);
    let msg = ref("你好啊");
    // 用ref定义对象
    let person = ref({
      name: "张三",
      age: 18,
      job: {
        j1: {
          salary: 20,
        },
      },
    });
    console.log(sum, msg, person);
    watch(sum, (newValue, oldValue) => {
      console.log("sum的值变化了", newValue, oldValue);
    });
    // 直接监视person对象是不行的，得写person.value或deep:true。。ref()包裹的对象，最终还是用reactive。person.value用的就是reactive的person

    watch(
      person,
      (newValue, oldValue) => {
        console.log("person的值变化了", newValue, oldValue);
      },
      { deep: true }
    );
    return {
      sum,
      msg,
      person,
    };
  },
};
</script>
```



### 3.watchEffect函数

- watch的套路是：既要指明监视的属性，也要指明监视的回调。

- watchEffect的套路是：不用指明监视哪个属性，监视的回调中用到哪个属性，那就监视哪个属性。

- watchEffect有点像computed：

    - 但computed注重的计算出来的值（回调函数的返回值），所以必须要写返回值。
    - 而watchEffect更注重的是过程（回调函数的函数体），所以不用写返回值。

  ```js
  //watchEffect所指定的回调中用到的数据只要发生变化，则直接重新执行回调。
  watchEffect(()=>{
      const x1 = sum.value
      const x2 = person.age
      console.log('watchEffect配置的回调执行了')
  })
  ```

Demo.vue

```vue
<template>
  <h2>当前求和为:{{ sum }}</h2>
  <button @click="sum++">点我+1</button>
  <hr />
  <h2>当前的信息为：{{ msg }}</h2>
  <button @click="msg += '!'">修改信息</button>
  <hr />
  <h2>姓名：{{ person.name }}</h2>
  <h2>年龄：{{ person.age }}</h2>
  <h2>薪资：{{ person.job.j1.salary }}k</h2>
  <button @click="person.name += '~'">修改姓名</button>
  <button @click="person.age++">增长年龄</button>
  <button @click="person.job.j1.salary++">涨薪</button>
</template>

<script>
import { reactive, ref, watch,watchEffect } from "vue";
export default {
  name: "Demo",
  setup() {
    let sum = ref(0);
    let msg = ref("你好啊");
  // 用ref定义对象
    let person = reactive({
      name: "张三",
      age: 18,
      job: {
        j1: {
          salary: 20,
        },
      },
    });
    // watch写法
    // watch(sum, (newValue, oldValue) => {
    //   console.log("sum的值变化了", newValue, oldValue);
    // },{immediate:true});


    watchEffect(()=>{
      const x1 = sum.value
      const x2 = person.job.j1.salary
      console.log('watchEffect所指定的回调执行了');
    })
    return {
      sum,
      msg,
      person,
    };
  },
};
</script>
```

### 8.生命周期

![](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202205062309456.png)

<img src="https://v3.cn.vuejs.org/images/lifecycle.svg" alt="lifecycle_2" style="zoom:33%;width:2500px" />



- Vue3.0中可以继续使用Vue2.x中的生命周期钩子，但有有两个被更名：
    - ```beforeDestroy```改名为 ```beforeUnmount```
    - ```destroyed```改名为 ```unmounted```
- Vue3.0也提供了 Composition API 形式的生命周期钩子，与Vue2.x中钩子对应关系如下：
    - `beforeCreate`===>`setup()`
    - `created`=======>`setup()`
    - `beforeMount` ===>`onBeforeMount`
    - `mounted`=======>`onMounted`
    - `beforeUpdate`===>`onBeforeUpdate`
    - `updated` =======>`onUpdated`
    - `beforeUnmount` ==>`onBeforeUnmount`
    - `unmounted` =====>`onUnmounted`

### 9.自定义hook函数

- 什么是hook？—— 本质是一个函数，把setup函数中使用的Composition API进行了封装。

- 类似于vue2.x中的mixin。

- 自定义hook的优势: 复用代码, 让setup中的逻辑更清楚易懂。

src/hooks/userPoint.js

```js
import {reactive, onMounted, onBeforeUnmount } from "vue";
export default function () {
  // 实现鼠标坐标获取的数据
  const point = reactive({
    X: 0,
    Y: 0,
  });
  // 定义获取鼠标坐标的函数
  function savePoint(e) {
    point.X = e.pageX;
    point.Y = e.pageY;
    console.log(e);
  }
  //   实现获取鼠标坐标生命周期
  // 挂载时
  onMounted(() => {
    addEventListener("click", savePoint);
  });
  // 卸载前
  onBeforeUnmount(() => {
    removeEventListener("click", savePoint);
  });
  return point
}
```

src/component/Test.vue

```vue
<template>
  <h2>当前点击时鼠标的坐标为:x:{{ point.X }},y:{{ point.Y }}</h2>
</template>

<script>
import usePoint from "../hooks/usePoint";
export default {
  name: "Test",
  setup() {
    let point = usePoint();
    return {
      point,
    };
  },
};
</script>
```

App.vue

```vue
<template>
<button @click="isShowDemo = !isShowDemo">切换隐藏/显示</button>
  <Demo v-if="isShowDemo"></Demo>
  <hr>
  <Test />
</template>

<script>
import Demo from "./component/Demo.vue";
import Test from './component/Test.vue';
import {ref} from 'vue'
export default {
  name: "App",
  components: {
    Demo,
    Test
  },
  setup() {
    let isShowDemo = ref(true);
    return {
      isShowDemo,
    };
  },
};
</script>
```

![image-20220507155847674](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202205071558798.png)

### 10.toRef

- 作用：创建一个 ref 对象，其value值指向另一个对象中的某个属性。
- 语法：```const name = toRef(person,'name')```
- 应用:   要将响应式对象中的某个属性单独提供给外部使用时。


- 扩展：```toRefs``` 与```toRef```功能一致，但可以批量创建多个 ref 对象，语法：```toRefs(person)```

Demo.vue

```vue
<template>
<h4>{{person}}</h4>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h2>薪资：{{ job.j1.salary }}k</h2>
  <button @click="name += '~'">修改姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="job.j1.salary++">涨薪</button>
</template>

<script>
import { reactive,toRef,toRefs } from "vue";
export default {
  name: "Demo",
  setup() {
    // 用ref定义对象
    let person = reactive({
      name: "张三",
      age: 18,
      job: {
        j1: {
          salary: 20,
        },
      },
    });

    // const name1 = person.name
    // console.log('@@@@@@',name1)

    // const name2 = toRef(person, 'name')
    // console.log('######',name2);

    // const x = toRefs(person)
    // console.log(x);
    return {
      person,
      // name:toRef(person,'name'),
      // age:toRef(person,'age'),
      // salary:toRef(person.job.j1,'salary'),
      ...toRefs(person)
    };
  },
};
</script>
```

## 三、其它 Composition API

### 1.shallowReactive 与 shallowRef

- shallowReactive：只处理对象最外层属性的响应式（浅响应式）。
- shallowRef：只处理基本数据类型的响应式, 不进行对象的响应式处理。

- 什么时候使用?
    -  如果有一个对象数据，结构比较深, 但变化时只是外层属性变化 ===> shallowReactive。
    -  如果有一个对象数据，后续功能不会修改该对象中的属性，而是生新的对象来替换 ===> shallowRef。

Demo.vue

```vue
<template>
  <h4>当前x值是:{{ x.y }}</h4>
  <button @click="x.y++">x++</button>
  <hr />
  <h4>{{ person }}</h4>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h2>薪资：{{ job.j1.salary }}k</h2>
  <button @click="name += '~'">修改姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="job.j1.salary++">涨薪</button>
</template>

<script>
import { reactive, shallowReactive, shallowRef, toRefs, ref } from "vue";
export default {
  name: "Demo",
  setup() {
    // let person = shallowReactive({  // 只考虑第一层的响应式
    let person = reactive({
      name: "张三",
      age: 18,
      job: {
        j1: {
          salary: 20,
        },
      },
    });

    let x = shallowRef({ y: 0 });
    console.log(x);
    return {
      x,
      person,
      ...toRefs(person),
    };
  },
};
</script>

```

### 2.readonly 与 shallowReadonly

- readonly: 让一个响应式数据变为只读的（深只读）。
- shallowReadonly：让一个响应式数据变为只读的（浅只读）。
- 应用场景: 不希望数据(尤其是这个数据是来自与其他组件时)被修改时。

Demo.vue

```vue
<template>
  <h4>当前求和为:{{ sum }}</h4>
  <button @click="sum++">点我++++</button>
  <hr />
  <h4>{{ person }}</h4>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h2>薪资：{{ job.j1.salary }}k</h2>
  <button @click="name += '~'">修改姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="job.j1.salary++">涨薪</button>
</template>

<script>
import {
  reactive,
  shallowReactive,
  shallowRef,
  toRefs,
  ref,
  readonly,
  shallowReadonly,
} from "vue";
export default {
  name: "Demo",
  setup() {
    let sum = ref(0);
    let person = reactive({
      name: "张三",
      age: 18,
      job: {
        j1: {
          salary: 20,
        },
      },
    });

    // person = readonly(person);
    person = shallowReadonly(person);
    return {
      sum,
      person,
      ...toRefs(person),
    };
  },
};
</script>
```

### 3.toRaw 与 markRaw

- toRaw：
    - 作用：将一个由```reactive```生成的<strong style="color:orange">响应式对象</strong>转为<strong style="color:orange">普通对象</strong>。
    - 使用场景：用于读取响应式对象对应的普通对象，对这个普通对象的所有操作，不会引起页面更新。
- markRaw：
    - 作用：标记一个对象，使其永远不会再成为响应式对象。
    - 应用场景:
        1. 有些值不应被设置为响应式的，例如复杂的第三方类库等。
        2. 当渲染具有不可变数据源的大列表时，跳过响应式转换可以提高性能。

Demo.vue

```vue
<template>
  <h4>当前求和为:{{ sum }}</h4>
  <button @click="sum++">点我++++</button>
  <hr />
  <!-- <h4>{{ person }}</h4> -->
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h2>薪资：{{ job.j1.salary }}k</h2>
  <h2 v-if="person.car">汽车品牌：{{ person.car.name }}</h2>
  <h2 v-if="person.car">汽车价格：{{ person.car.price }}</h2>
  <button @click="name += '~'">修改姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="job.j1.salary++">涨薪</button>
  <button @click="showRaw">输出最原始的person</button>
  <button @click="addCar">添加一台车</button>
  <button @click="person.car.name+='!'">换车名</button>
  <button @click="person.car.price='50w'">换价格</button>
</template>

<script>
import {
  reactive,
  toRefs,
  ref,
  markRaw,
  toRaw
} from "vue";
export default {
  name: "Demo",
  setup() {
    let sum = ref(0);
    let person = reactive({
      name: "张三",
      age: 18,
      job: {
        j1: {
          salary: 20,
        },
      },
    });


    function showRaw(){
      const p = toRaw(person);
      console.log(p);

      const sum = toRaw(sum);
      console.log(sum);
    }

    function addCar(){
      let car = {name:'奔驰',price:'40W'}
      person.car = markRaw(car)
    }
    return {
      sum,
      person,
      ...toRefs(person),
      showRaw,
      addCar
    };
  },
};
</script>
```

### 4.customRef

- 作用：创建一个自定义的 ref，并对其依赖项跟踪和更新触发进行显式控制。

- 实现防抖效果：

  ```vue
  <template>
  	<input type="text" v-model="keyword">
  	<h3>{{keyword}}</h3>
  </template>
  
  <script>
  	import {ref,customRef} from 'vue'
  	export default {
  		name:'Demo',
  		setup(){
  			// let keyword = ref('hello') //使用Vue准备好的内置ref
  			//自定义一个myRef
  			function myRef(value,delay){
  				let timer
  				//通过customRef去实现自定义
  				return customRef((track,trigger)=>{
  					return{
  						get(){
  							track() //告诉Vue这个value值是需要被“追踪”的
  							return value
  						},
  						set(newValue){
  							clearTimeout(timer)
  							timer = setTimeout(()=>{
  								value = newValue
  								trigger() //告诉Vue去更新界面
  							},delay)
  						}
  					}
  				})
  			}
  			let keyword = myRef('hello',500) //使用程序员自定义的ref
  			return {
  				keyword
  			}
  		}
  	}
  </script>
  ```

### 5.provide 与 inject

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202205072325541.png" style="width:300px" />

- 作用：实现<strong style="color:#DD5145">祖与后代组件间</strong>通信

- 套路：父组件有一个 `provide` 选项来提供数据，后代组件有一个 `inject` 选项来开始使用这些数据

- 具体写法：

    1. 祖组件中：

       ```js
       setup(){
           ......
           let car = reactive({name:'奔驰',price:'40万'})
           provide('car',car)
           ......
       }
       ```

    2. 后代组件中：

       ```js
       setup(props,context){
           ......
           const car = inject('car')
           return {car}
           ......
       }
       ```

### 6.响应式数据的判断

- isRef: 检查一个值是否为一个 ref 对象
- isReactive: 检查一个对象是否是由 `reactive` 创建的响应式代理
- isReadonly: 检查一个对象是否是由 `readonly` 创建的只读代理
- isProxy: 检查一个对象是否是由 `reactive` 或者 `readonly` 方法创建的代理  

App.vue

```vue
<template>
  <h2>app(祖)</h2>
</template>

<script setup>
import {ref, reactive,toRefs,isRef,isReactive,isProxy,readonly,isReadonly } from "vue";
name: "App";
let car = reactive({
  name: "奔驰",
  price: '40W',
});
let sum = ref(0)
let car2 = readonly(car)
console.log(isRef(sum));
console.log(isReactive(car));
console.log(isReadonly(car2));
console.log(isProxy(car2));

</script>
```



## 四、Composition API 的优势

### 1.Options API 存在的问题

使用传统OptionsAPI中，新增或者修改一个需求，就需要分别在data，methods，computed里修改 。

<div style="width:600px;height:370px;overflow:hidden;float:left">
    <img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f84e4e2c02424d9a99862ade0a2e4114~tplv-k3u1fbpfcp-watermark.image" style="width:600px;float:left" />
</div>
<div style="width:300px;height:370px;overflow:hidden;float:left">
    <img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e5ac7e20d1784887a826f6360768a368~tplv-k3u1fbpfcp-watermark.image" style="zoom:50%;width:560px;left" /> 
</div>










### 2.Composition API 的优势

我们可以更加优雅的组织我们的代码，函数。让相关功能的代码更加有序的组织在一起。

<div style="width:500px;height:340px;overflow:hidden;float:left">
    <img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bc0be8211fc54b6c941c036791ba4efe~tplv-k3u1fbpfcp-watermark.image"style="height:360px"/>
</div>
<div style="width:430px;height:340px;overflow:hidden;float:left">
    <img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6cc55165c0e34069a75fe36f8712eb80~tplv-k3u1fbpfcp-watermark.image"style="height:360px"/>
</div>




## 五、新的组件

### 1.Fragment

- 在Vue2中: 组件必须有一个根标签
- 在Vue3中: 组件可以没有根标签, 内部会将多个标签包含在一个Fragment虚拟元素中
- 好处: 减少标签层级, 减小内存占用

### 2.Teleport

- 什么是Teleport？—— `Teleport` 是一种能够将我们的<strong style="color:#DD5145">组件html结构</strong>移动到指定位置的技术。

  ```vue
  <teleport to="移动位置">
  	<div v-if="isShow" class="mask">
  		<div class="dialog">
  			<h3>我是一个弹窗</h3>
  			<button @click="isShow = false">关闭弹窗</button>
  		</div>
  	</div>
  </teleport>
  ```

Dialog.vue

```vue
<template>
  <div>
    <button @click="isShow = true">点我弹个窗</button>
    <teleport to="body">
      <div v-if="isShow" class="mask">
        <div class="dialog">
          <h3>我是一个弹窗</h3>
          <h4>一些内容</h4>
          <h4>一些内容</h4>
          <h4>一些内容</h4>
          <h4>一些内容</h4>
          <button @click="isShow = !isShow">关闭弹窗</button>
        </div>
      </div>
    </teleport>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "Dialog",
  setup() {
    let isShow = ref(false);
    return { isShow };
  },
};
</script>

<style>
.mask {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
}
.dialog {
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  width: 300px;
  height: 300px;
  background-color: green;
}
</style>
```

![image-20220508000223413](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202205080002517.png)

![image-20220508000233241](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/202205080002358.png)

### 3.Suspense

- 等待异步组件时渲染一些额外内容，让应用有更好的用户体验

- 使用步骤：

    - 异步引入组件

      ```js
      import {defineAsyncComponent} from 'vue'
      const Child = defineAsyncComponent(()=>import('./components/Child.vue'))
      ```

    - 使用```Suspense```包裹组件，并配置好```default``` 与 ```fallback```

      ```vue
      <template>
          <div class="app">
              <h3>我是App组件</h3>
              <Suspense>
                  <template v-slot:default>
                      <Child/>
                  </template>
                  <template v-slot:fallback>
                      <h3>加载中.....</h3>
                  </template>
              </Suspense>
          </div>
      </template>
      ```

App,vue

```vue
<template>
  <div class="app">
    <h2>app(祖)</h2>
    <!-- 正常显示v-slot:default的内容 -->
    <Suspense>
      <template  v-slot:default>
      <Child /></template>
    
    <!-- 若网络出现问题，导致组件加载不出来，就会显示下面的内容代替 -->
    <template v-slot:fallback>
      <h3>稍等,加载中....</h3>
    </template>
    </Suspense>
  </div>

</template>

<script>
import { defineAsyncComponent } from "vue";
const Child = defineAsyncComponent(() => import("./components/Child.vue"));
export default {
  name: "App",
  components: { Child },
};
</script>

<style>
.app {
  background: grey;
  padding: 10px;
}
</style>
```

## 六、其他

### 1.全局API的转移

- Vue 2.x 有许多全局 API 和配置。

    - 例如：注册全局组件、注册全局指令等。

      ```js
      //注册全局组件
      Vue.component('MyButton', {
        data: () => ({
          count: 0
        }),
        template: '<button @click="count++">Clicked {{ count }} times.</button>'
      })
      
      //注册全局指令
      Vue.directive('focus', {
        inserted: el => el.focus()
      }
      ```

- Vue3.0中对这些API做出了调整：

    - 将全局的API，即：```Vue.xxx```调整到应用实例（```app```）上

      | 2.x 全局 API（```Vue```） | 3.x 实例 API (`app`)                        |
      | ------------------------- | ------------------------------------------- |
      | Vue.config.xxxx           | app.config.xxxx                             |
      | Vue.config.productionTip  | <strong style="color:#DD5145">移除</strong> |
      | Vue.component             | app.component                               |
      | Vue.directive             | app.directive                               |
      | Vue.mixin                 | app.mixin                                   |
      | Vue.use                   | app.use                                     |
      | Vue.prototype             | app.config.globalProperties                 |

### 2.其他改变

- data选项应始终被声明为一个函数。

- 过度类名的更改：

    - Vue2.x写法

      ```css
      .v-enter,
      .v-leave-to {
        opacity: 0;
      }
      .v-leave,
      .v-enter-to {
        opacity: 1;
      }
      ```

    - Vue3.x写法

      ```css
      .v-enter-from,
      .v-leave-to {
        opacity: 0;
      }
      
      .v-leave-from,
      .v-enter-to {
        opacity: 1;
      }
      ```

- <strong style="color:#DD5145">移除</strong>keyCode作为 v-on 的修饰符，同时也不再支持```config.keyCodes```

- <strong style="color:#DD5145">移除</strong>```v-on.native```修饰符

    - 父组件中绑定事件

      ```vue
      <my-component
        v-on:close="handleComponentEvent"
        v-on:click="handleNativeClickEvent"
      />
      ```

    - 子组件中声明自定义事件

      ```vue
      <script>
        export default {
          emits: ['close']
        }
      </script>
      ```

- <strong style="color:#DD5145">移除</strong>过滤器（filter）

  > 过滤器虽然这看起来很方便，但它需要一个自定义语法，打破大括号内表达式是 “只是 JavaScript” 的假设，这不仅有学习成本，而且有实现成本！建议用方法调用或计算属性去替换过滤器。

- ......
