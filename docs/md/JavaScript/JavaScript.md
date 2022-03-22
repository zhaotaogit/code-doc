# JavaScript基础语法

## 一、写js的方式

### 1.行内式

```javascript
<input  type="button" value="唐伯虎" onclick="alert('秋香姐')">
```

### 2.内嵌式

```javascript
 <script>
        alert('沙漠骆驼')
    </script>
```

### 3.外部引入试

```javascript
// 创建一个js文件如my.js,写入一条js语句
alert('如果我是DJ，你会爱我吗？')
// 然后在html文件中引入
<script src="my.js"></script>
```

## 二、js的注释方式

```javascript
// 单行注释			// 单行注释
/* 多行注释 */   //多行注释
```

## 三、js的输入输出语句

```javascript
// 这是一个输入框
prompt('请输入你的年龄')
//alert 弹出警示框 输出的 展示给用户的
alert('计算的结果是')
// console 控制台输出 给程序员测试用的
console.log('我是程序员能看到的')
```

## 四、变量的使用

### 1.声明变量

```javascript
var age; //声明一个名称为age的变量
```

- **var** 是一个 JS关键字，用来声明变量( variable 变量的意思 )。使用该关键字声明变量后，计算机会自动为变量分配 内存空间，不需要程序员管 
-  age 是程序员定义的变量名，我们要通过变量名来访问内存中分配的空间

### 2.赋值

```javascript
 age = 10; // 给 age 这个变量赋值为 10 
```

- **= **用来把右边的值赋给左边的变量空间中 此处代表赋值的意思
- 变量值是程序员保存到变量空间里的值

### 3.变量的初始化

```js
var age = 18;	// 声明变量的同时给变量赋值
```

### 4.变量案例1 - 初始化变量并输出

```js
var myname = '卡卡西';
var address = '火影村';
var age = 30;
var email = 'kaka@kaka.com';
var gz = 2000;
console.log(myname)
console.log(address)
console.log(age)
console.log(email)
console.log(gz)
```

### 5.变量案例2 -用户输入变量并输出

```js
// 1.用户输入用户名 存储到一个变量里
var myname = prompt('请输入用户名');
// 2.输出这个用户名
alert("你的用户名是:" + myname)
```

### 6.更新变量

> 一个变量被重新复赋值后，它原有的值就会被覆盖，变量值将以最后一次赋的值为准.

```js
var age = 18;
age = 81; // 最后的结果就是81因为18 被覆盖掉了
```

### 7.同时声明多个变量

> 同时声明多个变量时，只需要写一个 var，多个变量名之间使用英文逗号隔开。

```js
var age = 10, name = 'zs', sex = 2;
```

### 8.声明变量特殊情况

| 情况                       |                        |           |
| -------------------------- | ---------------------- | --------- |
| var age;console.log(age);  | 只声明 不赋值          | undefined |
| console.log(age)           | 不声明 不赋值 直接使用 | 报错      |
| age = 10;console.log(age); | 不声明 只赋值          | 10        |

### 9.变量的命名规范

- 由字母(A-Za-z)、数字(0-9)、下划线(_)、美元符号( $ )组成，如：usrAge, num01, _name 

- 严格区分大小写。var app; 和 var App; 是两个变量 

- 不能 以数字开头。 18age 是错误的 

- 不能 是关键字、保留字。例如：var、for、while 

-  变量名必须有意义。 MMD BBD nl → age  

-  遵守驼峰命名法。首字母小写，后面单词的首字母需要大写。 myFirstName 

- 推荐翻译网站： 有道 爱词霸 

### 10.两个变量的交换

```js
var temp;
var red = '红';
var green = '绿'
console.log(red,green)
temp = red;
red = green;
green = temp;
console.log(red,green)
```

### 11.变量小结

- 为什么需要变量？
  - 因为一些数据需要保存，所以需要变量
-  变量是什么？
	- 变量就是一个容器，用来存放数据的。方便我们以后使用里面的数据 
- 变量的本质是什么?
  -  变量是内存里的一块空间，用来存储数据。
- 变量怎么使用的？
  - 使用变量的时候，一定要声明变量，然后赋值
  - 声明变量本质是去内存申请空间。
- 什么是变量的初始化？
  - 声明变量并赋值我们称之为变量的初始化
- 变量命名规范有哪些？
  - 变量名尽量要规范，见名知意——驼峰命名法
- 交换2个变量值的思路
  - 区分哪些变量名不合法
  - 学会交换2个变

## 四、数据类型

>  变量是用来存储值的所在处，它们有名字和数据类型。变量的数据类型决定了如何将代表这些值的位存储到计算机的 内存中。**JavaScript 是一种弱类型或者说动态语言**。这意味着不用提前声明变量的类型，在程序运行过程中，类型会 被自动确定。

```js
var age = 10; // 这是一个数字型
var areYouOk = '是的'; // 这是一个字符串
```

> 在代码运行时，变量的数据类型是由 JS引擎 **根据 = 右边变量值的数据类型来判断** 的，运行完毕之后， 变量就确定了数据类型。 **JavaScript 拥有动态类型，同时也意味着相同的变量可用作不同的类型**：

```js
var x = 6; // x 为数字
var x = "Bill"; // x 为字符串 
```

### 1.简单数据类型

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/JS基础学习/20210913182148.png"/>

#### 1.数字型

> 最常见的进制有二进制、八进制、十进制、十六进制。

```js
// 1.八进制数字序列范围：0~7
var num1 = 07; 		// 对应十进制的7
var num2 = 019; 	// 对应十进制的19
var num3 = 08; 		// 对应十进制的8
 // 2.十六进制数字序列范围：0~9以及A~F
var num = 0xA; 
```

- JavaScript中数值的最大和最小值

  ```js
  alert(Number.MAX_VALUE); 	// 1.7976931348623157e+308
  alert(Number.MIN_VALUE); 	// 5e-324
  ```

  -  最大值：Number.MAX_VALUE，这个值为： 1.7976931348623157e+308 
  -  最小值：Number.MIN_VALUE，这个值为：5e-32

- 数字型的三个特殊值

  ```js
  alert(Infinity); 	// Infinity
  alert(-Infinity); 	// -Infinity
  alert(NaN); 		// NaN
  ```

  - Infinity ，代表无穷大，大于任何数值 
  - -Infinity ，代表无穷小，小于任何数值 
  - NaN ，Not a number，代表一个非数值

- isNaN方法

  > 用来判断一个变量是否非数字类型

  <img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/JS基础学习/20210913184112.png"/>

```js
var usrAge = 21;
var isOk = isNaN(userAge);
console.log(isNum); // false ，21 不是一个非数字
var usrName = "andy";
console.log(isNaN(userName)); // true ，"andy"是一个非数字
```

#### 2.字符串类型String

> 字符串型可以是引号中的任意文本，其语法为 双引号 "" 和 单引号''

```js
var strMsg = "我爱北京天安门~"; // 使用双引号表示字符串
var strMsg2 = '我爱吃猪蹄~'; // 使用单引号表示字符串
// 常见错误
var strMsg3 = 我爱大肘子; // 报错，没使用引号，会被认为是js代码，但js没有这些语法
```

- 因为 HTML 标签里面的属性使用的是双引号，JS 这里我们更推荐使用单引号。

##### 1.字符串嵌套

> JS 可以用单引号嵌套双引号 ，或者用双引号嵌套单引号 (外双内单，外单内双)

```js
var strMsg = '我是"高帅富"程序猿'; // 可以用''包含""
var strMsg2 = "我是'高帅富'程序猿"; // 也可以用"" 包含'' // 常见错误
var badQuotes = 'What on earth?"; // 报错，不能 单双引号搭
```

##### 2.字符串转义字符

> 类似HTML里面的特殊字符，字符串中也有特殊字符，我们称之为转义符。 转义符都是 \ 开头的，常用的转义符及其说明如下：

| 转义符 | 解释说明                |
| ------ | ----------------------- |
| \n     | 换行符,n是newline的意思 |
| \\\    | 斜杠\                   |
| \\'    | ‘单引号                 |
| \\"    | “双引号                 |
| \t     | tab缩进                 |
| \b     | 空格,b是blank的意思     |

##### 3.字符串长度

> 字符串是由若干字符组成的，这些字符的数量就是字符串的长度。通过字符串的 length 属性可以获取整个字符 串的长度。

```js
var strMsg = "我是帅气多金的程序猿！";
alert(strMsg.length); // 显示 11
```

##### 4.字符串拼接

-  多个字符串之间可以使用 **+** 进行拼接，其拼接方式为 字符串 + 任何类型 = 拼接之后的新字符串 
- 拼接前会把与字符串相加的任何类型转成字符串，再拼接成一个新的字符串

```js
// 1.1 字符串 "相加" 
alert('hello' + ' ' + 'world'); // hello world
//1.2 数值字符串 "相加" 
alert('100' + '100'); // 100100
//1.3 数值字符串 + 数值
alert('11' + 12); // 1112 
```

- **\+ **号总结口诀：数值相加 ，字符相连

##### 5.字符串拼接加强

```js
console.log('pink老师' + 18); // 只要有字符就会相连
var age = 18;
// console.log('pink老师age岁啦'); // 这样不行哦
console.log('pink老师' + age); // pink老师18
console.log('pink老师' + age + '岁啦'); // pink老师18岁啦
```

- 我们经常会将字符串和变量来拼接，因为变量可以很方便地修改里面的值 

- 变量是不能添加引号的，因为加引号的变量会变成字符串 

- 如果变量两侧都有字符串拼接，口诀“引引加加 ”，删掉数字，变量写加中间

#### 3.布尔类型

> 布尔类型有两个值：true 和 false ，其中 true 表示真（对），而 false 表示假（错）。 布尔型和数字型相加的时候， true 的值为 1 ，false 的值为 0

```js
console.log(true + 1); 		// 2
console.log(false + 1); 	// 1
```

##### 1.Undefined 和 Null

> 一个声明后没有被赋值的变量会有一个默认值 undefined ( 如果进行相连或者相加时，注意结果

```js
var variable;
console.log(variable); // undefined
console.log('你好' + variable); // 你好undefined
console.log(11 + variable); // NaN
console.log(true + variable); // NaN
```

> 一个声明变量给 null 值，里面存的值为空（学习对象时，我们继续研究null)

```js
var vari = null;
console.log('你好' + vari); // 你好null
console.log(11 + vari); // 11
console.log(true + vari); // 1
```

### 4.获取变量数据类型

#### 1.获取检测变量的数据类型

```js
var num = 18;
console.log(typeof num) // 结果 number 
```

不同类型的返回值

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/JS基础学习/20210913213511.png"/>

```js
var num = 10;
console.log(typeof num);    // number
var str = '哈哈哈'
console.log(typeof str);    // string
var bool = true;
console.log(typeof bool);   // boolean
var vari = undefined;
console.log(typeof vari);   // undefined
var timer = null;
console.log(typeof timer);  // object

var age = prompt('请输入你的年龄:')
console.log(age);    // 18
console.log(typeof age);    // string
```

#### 2.字面量

> 字面量是在源代码中一个固定值的表示法，通俗来说，就是字面量表示如何表达这个值。   

- 数字字面量：8, 9, 10 

- 字符串字面量：'黑马程序员', "大前端" 

- 布尔字面量：true，false

### 5.数据类型转换

#### 1.什么是数据类型转换

> 使用表单、prompt 获取过来的数据默认是字符串类型的，此时就不能直接简单的进行加法运算，而需要转换变 量的数据类型。通俗来说，就是把一种数据类型的变量转换成另外一种数据类型。

 我们通常会实现3种方式的转换：

- 转换为字符串类型 
-  转换为数字型 
-  转换为布尔型

#### 2.转为字符串

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/JS基础学习/20210913220636.png"/>

- oString() 和 String() 使用方式不一样。 
-  三种转换方式，我们更喜欢用第三种加号拼接字符串转换方式， 这一种方式也称之为隐式转换

```js
// 1.把数字型转换为字符串型 变量.toString()
var num = 10;
var str = num.toString();
console.log(str);   // 10
console.log(typeof str);    // string
// 2.利用String()
var str1 = String(num);
console.log(str1);  // 10
console.log(typeof(str1));  // string
```

#### 3.转换为数字型

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/JS基础学习/20210913221613.png"/>

- parseInt 和 parseFloat 单词的大小写，这2个是重点 
-  隐式转换是我们在进行算数运算的时候，JS 自动转换了数据类型

```js
var age = prompt('请输入你的年龄：');
console.log(age);   
console.log(typeof(age));   // string
// 1.利用parseInt变量)将字符型转换成数字型，但是得到的是整数
var num = parseInt(age);
console.log(num);
console.log(typeof(num));   // number
console.log(parseInt(3.14)) // 3
console.log(parseInt(3.94)) // 3,没有四色五入
console.log(parseInt('120px'))  // 120,会去掉px
console.log(parseInt('rem120px'))  // NaN
// 2.利用parseFloat变量)将字符型转换成数字型，但是得到的是浮点数
console.log(parseFloat(3));  // 3.14
console.log(parseFloat(3.14));  // 3.14
        // 3.利用Number(变量)转换
        console.log(Number('123'));
        console.log(typeof(Number('123')))  // number
        // 4.利用算数运算 - * / 隐式转换
        console.log('12' - 0);  // 12
        console.log(typeof('12'-0));    // number
        console.log('123' - '120');     // 3
        console.log(typeof(('123' - '120')));   // number
```

#### 4.计算年龄案例

```js
var year = prompt('请输入的你出生年份：');
var age = 2021 - year;
alert('你今年的年龄为:' + age);
```

#### 5.简单加法器

```js
var num1 = prompt('请输入第一个值:') - 0;
var num2 = prompt('请输入第二个值:') - 0;
alert('两个值的和为：' +  (num1+num2)) ;
```

#### 6.转换为布尔类型

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/JS基础学习/20210913224441.png"/>

-  代表空、否定的值会被转换为 false ，如 ''、0、NaN、null、undefined  
-  其余值都会被转换为 true

```js
console.log(Boolean('')); // false
console.log(Boolean(0)); // false
console.log(Boolean(NaN)); // false
console.log(Boolean(null)); // false
console.log(Boolean(undefined)); // false
console.log(Boolean('小白')); // true
console.log(Boolean(12)); // true
```

## 五、运算符

### 1.算数运算符

```js
console.log(1 + 1); // 2
console.log(1 - 1); // 0
console.log(1 * 1); // 1
console.log(1 / 1); // 1
// 1.取余%
console.log(3 % 2); // 1
console.log(5 % 3); // 2
console.log(3 % 5 ); // 3
// 2.浮点数 算数运算会有问题
console.log(0.1 + 0.2);     // 0.30000000000000004
console.log(0.07 * 100);    // 7.000000000000001
// 3. 不能直接用浮点数进行数值比较
var num = 0.1 + 0.3;
console.log(0.3 == num);    // false
```

### 2.表达式与返回值

> 表达式是由数字、运算符、变量等组成的式子 我们称为表达式

```js
// 表达式是由数字、运算符、变量等组成的式子 我们称为表达式
console.log(1 + 1); // 2 就是返回值
```

--------------------------------------------------------------------------------------------------------------------------------------------------------

**关于运算符的跳过!**

## 六、流程控制

### 1.if语句

if语法结构

```js
// 1.if的语法结构
        if (条件表达式){
            // 执行语句
        }
```

### 2.进入网吧案例

> 用户打开网页，提示用户输入年龄，如果用户年龄大于等于18岁，就给出提示。

```js
var age = prompt('请输入您的年龄:');
if (age >= 18){
    alert('我想带你去网吧偷耳机!');
}
```

### 3.if-else双分支语句

```js
// 语法结构
if(条件表达式){
    // 语法语句1
}else{
    // 执行语句2
}
```

```js
var age = prompt('请输入您的年龄:');
if (age >= 18){
    alert('我带你去网吧偷耳机!');
}else{
    alert('滚，回家做作业去！');
}
```

### 4. 判断闰年

```js
var year = prompt('请输入一个年份:');
if (year % 4 ==0 && year % 100 != 0 || year % 400 == 0){
    alert(year + '是闰年');
}else{
    alert(year + '不是闰年');
}
```

### 5.if-else-if多分支语句

```js
if (条件语句1){
    // 执行语句 1
}else if(条件语句2){
    // 执行语句2
}else if (条件语句3){
    // 执行语句3
}else{
    // 执行语句4
}
```

### 6.三元表达式

```js
// 条件表达式 ? 表达式1 : 表达式2
var num = 5;
num > 6 ? alert('True') : alert('False')
```

### 3.for循环

```js
for(初始化变量;条件表达式;操作表达式){
    // 循环体
}
for(var i = 1;i <= 100;i++){
    console.log(i)
}
```

> 打印九九乘法表

```js
for(var i = 1;i<=9;i++){
            var str = '';
            for(var j = 1;j<=i;j++){
                str += j + '*' + i  + '=' + i*j + '\t\t';
            }
            console.log(str);
        }
```

### 4.while循环

```js
var num = 1;
while(num <= 100){
    console.log(num);
    num ++;
}
```

### 5.do-while循环

```js
var num = 1;
do{
    console.log('张亚龙' + '*' + num);
    num ++;
} while(num<=100);
```

### 6.简易ATM机

```js
var money = 100;
var num = prompt('请输入你要的操作:' + '\n' + '1.存钱' + '\n' + '2.取钱' + '\n' + '3.显示余额' + '\n' + '4.退出');
while (true){
    if (num == 1){
        money += parseFloat(prompt('请输入你要存入钱数:'));
    }else if(num == 2){
        money -= parseFloat(prompt('请输入你要取出钱数:'));
    }else if(num == 3){
        alert('当前余额为：' + money + '元.');
    }else{
        break;
    }
    var num = prompt('请输入你要的操作:' + '\n' + '1.存钱' + '\n' + '2.取钱' + '\n' + '3.显示余额' + '\n' + '4.退出');     
}
```

## 七、数组

### 1.创建数组

```js
// 普通的一个变量只能存储一个值;
var num = 10;
// 一个数组可以存储多个值；
var arr = [1,2,3,4,5];
// 1.利用new创建数组
var arr1 = new Array();
// 2.利用数组字面量创建数组 []
var arr2 = ['red','blue','green'] 
console.log(arr2);
```

### 2.获取数组元素

```js
var arr = ['red','green','black','blue']
console.log(arr[0]);    // red
console.log(arr[3]);    // blue
console.log(arr[4]);    // 因为没有4这个索引，所以结果是undefined
```

### 3.遍历数组与获取数组长度

```js
var arr = ['red','green','blue'];
        console.log(arr.length);
        for (var i =0;i<arr.length;i++) {
            console.log(arr[i]);
        }
```

### 4.数组新增元素

```js
// 1.通过数组的length修改
var arr = ['red','blue','green'];
arr.length = 5;
console.log(arr);
console.log(arr.length);    // 5
console.log(arr[3]);    // undefined
console.log(arr[4]);    // undefined

// 2.通过数组索引
var arr1 = ['red','blue','green'];
arr1[3] = 'yellow';
console.log(arr1.length);
console.log(arr1);
```



## 八、函数

### 1.函数的使用

```js
// 1.声明函数
// function 函数名() {
//     // 函数体
// }
function sayhi() {
    console.log('Hello World！');
}
// 2.调用函数
sayhi();
```

### 2.函数形参实参个数匹配

```js
function getnum(num1,num2) {
    console.log(num1,num2);
}
getnum(1,2);    // 1 2
getnum(1);  // 1 undefined
getnum(1,2,3);  // 1 2
```

### 3.arguments的使用

```js
function fn() {
    console.log(arguments);
    console.log(arguments.length);
    console.log(arguments[2]);
    for (var i=0;i<arguments.length;i++) {
        console.log(arguments[i]);
    }
}   

fn(1,2,3);
```

### 4.函数声明的两种方式

```js
// 1.利用函数关键是自定义函数
function func() {
    // 函数体
}
// 调用方式
func();
// 2.函数表达式
var func1 = function() {
    console.log('hello');
}
//调用方式
func1()
```



### 5.预解析

#### 1.预解析基本使用

```js
// console.log(num); //  报错 num is not defined
// 1
// console.log(num);   // undefined
// var num = 10;
// 相当于执行了
var num;
console.log(num);
num = 10;
// 2
fun();  // Hello
function fun() {
    console.log('Hello');
}
// 3
// func()  // 报错 func is not a function
// var func = function() {
//     console.log('World');
// }

// 相当于执行了
var func;
func();
func = function() {
    console.log('World');
}
```

#### 2.预解析案例

```js
function func() {
    var a=b=c=9;
    console.log(a);
    console.log(b);
    console.log(c);
}
func()
console.log(b);
console.log(c);
console.log(a);

// 相当于执行
function func() {
    var a=9;b=9;c=9;
    console.log(a);
    console.log(b);
    console.log(c);
}
func()
console.log(b);
console.log(c);
console.log(a);
```

## 九、对象

### 1.利用字面量创建对象

```js
// 利用字面量创建对象
var obj = {};   // 创建了一个空对象
var obj1 = {
    uname: '张三丰',
    age: 18,
    sex: '男',
    sayHi: function() {
        console.log('Hi');
    }
}
// 调用对象
console.log(obj1.uname);
console.log(obj1['age']);
console.log(obj1.sex);
obj1.sayHi();
```

### 2.利用new Object创建对象

```js
// 利用new Object创建对象
var obj = new Object(); // 创建了一个空对象
obj.uanme = '男';
obj.age = 18;
obj.sex = '男';
obj.sayHi = function() {
    console.log('Hi');
}

// 调用对象
console.log(obj.uanme);
console.log(obj['age']);
obj.sayHi();
```

### 3.利用构造函数创建对象

```js
// 利用构造函数创建对象
function Star(uname,age,sex) {
    this.name = uname;
    this.age = age;
    this.sex = sex;
    this.song = function(sang) {
        console.log(sang);
    }
}
var obj = new Star('张亚龙',18,'男')
console.log(obj['name']);
obj.song('冰雨')
```

# JS-Dom

### 1.[getElementById](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementById)获取元素

> 此方法是根据元素ID来获取元素

```html
 <div id="time">2021-10-09</div>
```

```js
var element = document.getElementById('time');
console.log(element);   // <div id="time">2021-10-09</div>
console.log(typeof element);    // object
console.dir(element);   // div#time 表示是div标签下id为time的元素
```

### 2.getElementsByTagName获取某类标签元素

> 此方法是根据标签名来获取元素

```html
<ul>
        <li>呵呵哈哈哈1</li>
        <li>呵呵哈哈哈2</li>
        <li>呵呵哈哈哈3</li>
        <li>呵呵哈哈哈4</li>
        <li>呵呵哈哈哈5</li>
        <li>呵呵哈哈哈6</li>
    </ul>
```

```js
// 返回的是获取对象的集合，伪数组
var lis = document.getElementsByTagName('li');
console.log(lis);
console.log(lis[0]);    // 输入第一个结果
// 遍历打印结果
for (var i = 0; i < lis.length; i++) {
    console.log(lis[i]);
}

// 获取某元素下的元素
var uls = document.getElementsByTagName('ul');
console.log(uls[0].getElementsByTagName('li'));
```

### 3.getElementsByClassName获取元素

> 此方法是根据类名来获取元素

```html
<div class="box">盒子1</div>
<div class="box">盒子2</div>
<div class="nav">
    <ul>
        <li>首页</li>
        <li>产品</li>
    </ul>
</div>
```

```js
var box = document.getElementsByClassName('box');
    console.log(box);
```

### 4..querySelector获取元素

> 此方法是根据指定的选择器返回第一个元素

```html
<div class="box">盒子1</div>
<div class="box">盒子2</div>
<div class="nav">
    <ul>
        <li>首页</li>
        <li>产品</li>
    </ul>
</div>
```

```js
    // querySelector是返回匹配结果的第一个
    var firstbox = document.querySelector('.box');
    console.log(firstbox);  // <div class="box">盒子1</div>
    var firstnav = document.querySelector('#nav');	// 结果为下面的注释
    /*
    <div id="nav">
        <ul>
            <li>首页</li>
            <li>产品</li>
        </ul>
    </div>
    */
    console.log(firstnav);
    var firstli = document.querySelector('li');
    console.log(firstli);   // <li>首页</li>
    // querySelectorAll是返回所有符合结果的元素的集合
    console.log(document.querySelectorAll('li'));
```

### 5.获取body元素和html元素

```js
// 1.获取body标签
var body = document.body;
console.log(body);
console.dir(body);
// 2.获取html元素
var html = document.documentElement;
console.log(html);
console.dir(html);
```

### 6.修改元素内容

```html
<button>按钮</button>
<div>-------------</div>
```

```js
var btn = document.querySelector('button');
var div = document.querySelector('div');
btn.onclick = function () {
    div.innerText = '点击按钮修改内容';
}
```

### 7.innerText和innerHTML区别

```html
<div></div>
<p>
    Hello
    <span>今天是2021-10-9</span>
</p>
```

```js
// innerText不识别HTML标签
var div = document.querySelector('div');
div.innerText = '<strong>今天是周六</strong>';
// innerHTML识别HTML标签
var div = document.querySelector('div');
div.innerHTML = '<strong>今天是周六</strong>';

var p = document.querySelector('p');
console.log(p.innerText);
console.log(p.innerHTML);
```

### 8.点击按钮切换图片

```html
<button id="zxy">张学友</button>
<button id="ldh">刘德华</button>
</br>
<img id="img"
     src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fdingyue.nosdn.127.net%2F3WKmSi9G2oCkRdfU004xJEtTbc%3DPbkZFzLgi08W%3DAr0CR1499226607542.jpg&refer=http%3A%2F%2Fdingyue.nosdn.127.net&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1635426519&t=432cc8238fd6531efd83b2ff1a73f662">
```

```js
var zxy = document.getElementById('zxy');
var ldh = document.getElementById('ldh');
var img = document.getElementById('img');
zxy.onclick = function () {
    img.src = 'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fdingyue.nosdn.127.net%2F3WKmSi9G2oCkRdfU004xJEtTbc%3DPbkZFzLgi08W%3DAr0CR1499226607542.jpg&refer=http%3A%2F%2Fdingyue.nosdn.127.net&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1635426519&t=432cc8238fd6531efd83b2ff1a73f662';
}
ldh.onclick = function () {
    img.src = 'https://img1.baidu.com/it/u=2117656796,1247674614&fm=253&fmt=auto&app=120&f=JPEG?w=690&h=362';
}
```

### 9.操作元素值表单属性设置

```html
<button>按钮</button>
<input type="text" value="输入内容">
```

```js
// 获取元素
var btn = document.querySelector('button');
var input = document.querySelector('input');
// 注册事件，处理程序
btn.onclick = function () {
    input.value = '按钮被点击了!';
    btn.disabled = true;
}
```

### 10.通过className修改元素样式

> 通过js修改元素得class属性。会覆盖原有类名,若想保留原有类名，可以原类名+空格+新类名。

```javascript
element.style	 行内样式操作
element.className	类名样式操作
```

例:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: red;
        }
        .change {
            background-color: green;
            color: white;
            font-size: 25px;
            margin-top: 100px;
        }
    </style>
</head>

<body>
    <div>文本</div>
    <script>
        // 1.使用element.style修改元素样式,如果样式比较少，或者功能简单得情况下使用。
        // var test = document.querySelector('div')
        // test.onclick = function() {
        //     this.style.backgroundColor = 'green'
        //     this.style.color = 'white'
        //     this.style.fontSize = '25px'
        //     this.style.marginTop = '100px'
        // }
        // 2. 使用className修改元素样式
        var test = document.querySelector('div')
        test.onclick = function () {
            this.className = 'change';
        }
    </script>
</body>

</html>
```

###  11.仿新浪注册页面

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            width: 600px;
            height: 200px;
        }

        .message {
            display: inline-block;
            font-size: 15px;
            color: #999;
            background: url('./images/mess.png') no-repeat left center;
            padding-left: 20px;
        }
        .wrong {
            color: red;
            background-image: url('./images/wrong.png');
        }
        .right {
            color: green;
            background-image: url('images/right.png');
        }
    </style>
</head>

<body>
    <div>
        <input type="password" class="ipt">
        <p class="message">请输入6-16为密码</p>
    </div>
    <script>
        //首先判断的事件是表单失去焦点 onblur
        //如果输入正确则提示正确的信息颜色为绿色小图标变化
        //如果输入不是6到16位，则提示错误信息颜色为红色小图标变化
        //因为里面变化样式较多，我们采取className修改样式
        // 1.获取元素
        var ipt = document.querySelector('.ipt')
        var message = document.querySelector('.message')
        // 注册事件，失去焦点
        ipt.onblur = function () {
            // 根据表单里面值得长度判断ipt.value.length
            if (this.value.length<6 || this.value.length>16) {
                message.className = 'message wrong'
                message.innerHTML = '输入得位数部署6-16位，请重新输入！'
            } else {
                message.className = 'message right'
                message.innerHTML = '输入符合要求正确！'
            }
        }
    </script>
</body>

</html>
```

### 12.百度换肤效果

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        body {
            background: url('images/1.jpg') no-repeat center top;
        }
        li {
            list-style: none;
        }
        .baidu {
            overflow: hidden;
            margin: 100px auto;
            background-color: #fff;
            width: 410px;
            padding-top: 3px
        }
        .baidu li {
            float: left;
            margin: 0 1px;
            cursor: pointer;
        }
        .baidu img {
            width: 100px;
        }
    </style>
</head>

<body>
    <ul class="baidu">
        <li><img src="./Images/1.jpg" alt=""></li>
        <li><img src="./Images/2.jpg" alt=""></li>
        <li><img src="./Images/3.jpg" alt=""></li>
        <li><img src="./Images/4.jpg" alt=""></li>
    </ul>
    <script>
        var imgs = document.getElementsByTagName('img');
        for (var i=0;i< imgs.length;i++) {
            imgs[i].onclick = function() {
                console.log(imgs);
                document.body.style.backgroundImage = 'url(' + this.src +')'
            }
        }
    </script>
</body>

</html>
```

### 13.表格隔行变色效果

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        table {
            width: 800px;
            margin: 100px auto;
            text-align: center;
            border-collapse: collapse;
            font-size: 14px;
        }

        thead tr {
            height: 30px;
            background-color: skyblue;
        }

        tbody tr {
            height: 30px;
        }

        tbody td {
            border-bottom: 1px solid #d7d7d7;
            font-size: 12px;
            color: blue;
        }

        .bg {
            background-color: pink;
        }
    </style>
</head>

<body>
    <table>
        <thead>
            <tr>
                <th>代码</th>
                <th>名称</th>
                <th>最新公布净值</th>
                <th>累计净值</th>
                <th>前单位净值</th>
                <th>净值增长率</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>003526</td>
                <td>农银金穗3个月定期开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
        </tbody>
    </table>
    <script>
        var obj = document.querySelector('tbody').querySelectorAll('tr');
        for (var i = 0; i < obj.length; i++) {
            obj[i].onmouseover = function () {
                this.className = 'bg'
            }
            obj[i].onmouseout = function () {
                this.className = '';
            }
        }
    </script>
</body>

</html>
```

### 14.表格全选取消全选

```html
<!DOCTYPE html>
<html>

<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        .wrap {
            width: 300px;
            margin: 100px auto 0;
        }

        table {
            border-collapse: collapse;
            border-spacing: 0;
            border: 1px solid #c0c0c0;
            width: 300px;
        }

        th,
        td {
            border: 1px solid #d0d0d0;
            color: #404060;
            padding: 10px;
        }

        th {
            background-color: #09c;
            font: bold 16px "微软雅黑";
            color: #fff;
        }

        td {
            font: 14px "微软雅黑";
        }

        tbody tr {
            background-color: #f0f0f0;
        }

        tbody tr:hover {
            cursor: pointer;
            background-color: #fafafa;
        }
    </style>

</head>

<body>
    <div class="wrap">
        <table>
            <thead>
                <tr>
                    <th>
                        <input type="checkbox" id="j_cbAll" />
                    </th>
                    <th>商品</th>
                    <th>价钱</th>
                </tr>
            </thead>
            <tbody id="j_tb">
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>iPhone8</td>
                    <td>8000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>iPad Pro</td>
                    <td>5000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>iPad Air</td>
                    <td>2000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>Apple Watch</td>
                    <td>2000</td>
                </tr>

            </tbody>
        </table>
    </div>
    <script>
        // 获取全选按钮
        var j_cbAll = document.getElementById('j_cbAll')
        // 获取其他多选框
        var j_tb = document.getElementById('j_tb').getElementsByTagName('input')
        // 实现全部多选
        j_cbAll.onclick = function () {
            for (var i = 0; i < j_tb.length; i++) {
                j_tb[i].checked = this.checked
            }
        }
        // 单个多选框实现选择
        for (var i = 0; i < j_tb.length; i++) {
            j_tb[i].onclick = function () {
                var flag = true;
                for (var j = 0; j < j_tb.length; j++) {
                    if (!j_tb[j].checked) {
                        flag = false
                        break
                    }
                }
                j_cbAll.checked = flag
            }
        }

    </script>
</body>

</html>
```

### 15.自定义属性操作

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="demo1" index="1"></div>
    <script>
        var div = document.querySelector('#demo1')
        // 1.获取元素得值
        // element.属性名
        console.log(div.id);
        // element.getAttribute('属性'),主要用来获取自己定义得一些属性
        console.log(div.getAttribute('id'));
        // 2.设置元素属性值
        // element.属性 = '值'
        div.id = 'test'
        console.log(div.id);
        // element.setAttribute('属性','值')
        div.setAttribute('id','test1')
        console.log(div.id);
    </script>
</body>
</html>
```

### 16.tab栏切换布局

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    .tab {
        margin: 100px auto;
    }

    .tab_list {
        height: 39px;
        background-color: #f1f1f1;
        border: 1px solid #ccc;
    }

    .tab_list li {
        float: left;
        height: 39px;
        line-height: 39px;
        padding: 0 10px;
        text-align: center;
        cursor: pointer;
    }

    li {
        list-style-type: none;
    }

    .tab_list .current {
        background-color: #c81623;
        color: white;
    }

    .item {
        display: none;
    }

    .iteminfo {
        display: block;
    }
</style>

<body>


    <div class="tab">
        <div class="tab_list">
            <ul>
                <li class="current">商品介绍</li>
                <li>规格与包装</li>
                <li>售后保障</li>
                <li>商品评价（50000）</li>
                <li>手机社区</li>
            </ul>
        </div>
        <div class="tab_con">
            <div class="item">商品介绍模块</div>
            <div class="item">规格与包装模块</div>
            <div class="item">售后保障模块</div>
            <div class="item">商品评价（50000）模块</div>
            <div class="item">手机社区模块</div>
        </div>
    </div>
    <script>
        var lis = document.querySelectorAll('li')
        var items = document.querySelectorAll('.item')
        for (var i = 0; i < lis.length; i++) {
            lis[i].onclick = function () {
                for (var j = 0; j < lis.length; j++) {
                    lis[j].className = ''
                }
                this.setAttribute('class', 'current')
                for (var i = 0; i < lis.length; i++) {
                    if (lis[i].className == 'current') {
                        items[i].className = 'iteminfo'
                    } else {
                        items[i].className = 'item'
                    }
                }
            }
            
        }
    </script>
</body>

</html>
```

### 18.节点操作

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="div1">我是div</div>
    <span>我是span</span>
    <ul>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
    </ul>
    <div class="box">
        <div class="erweima"></div>
    </div>
    <ul id="ul1">

    </ul>
    <ul class="remove">
        <li>熊大</li>
        <li>熊二</li>
        <li>光头强</li>
    </ul>
    <button id="submit_remove">删除</button>
    <ul class="clone">
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
    <script>
        // 1.父节点
        var erweima = document.querySelector('.erweima')
        // 得到的是离得最近的父节点
        console.log(erweima.parentElement);
        // 2.子节点,包含所有节点，文字节点，元素节点。
        // 元素节点nodetype是1，文字节点nodetype是2
        var ul = document.querySelector('ul')
        console.log(ul.childNodes);
        for (var i = 0; i < ul.childNodes.length; i++) {
            if (ul.childNodes[i].nodeType == 1) {
                console.log(ul.childNodes[i]);
            }
        }
        // 3.子节点,只包含元素节点
        console.log(ul.children);
        // 4.获取第一个元素和最后一个元素（包含元素节点和文本节点）
        console.log(ul.firstChild);
        console.log(ul.lastChild);
        // 5.获取第一个元素和最后一个元素(只包含元素节点)
        console.log(ul.firstElementChild);
        console.log(ul.lastElementChild);
        // 6.兄弟节点nextSibling,包含下一个节点，包含文本节点和元素节点
        var div = document.querySelector('#div1')
        console.log(div.nextSibling);
        console.log(div.previousSibling);
        // 7.兄弟节点只包含元素节点,找不到返回null
        console.log(div.nextElementSibling);
        console.log(div.previousElementSibling);
        // 8.创建节点
        var li = document.createElement('li')
        // 9.添加节点 node.appendChild(child) node父级，child子级   追加
        var ul = document.querySelector('#ul1')
        li.innerHTML = '<h1>这是添加的li</li>'
        ul.appendChild(li)
        console.log(ul.children[0]);
        // 10.在某个元素前面添加元素
        var li1 = document.createElement('li')
        li1.innerHTML = '<h1>这是添加的li1</li>'
        ul.insertBefore(li1, ul.children[0])
        // 11.删除节点
        var ul = document.querySelector('.remove')
        // 删除第一个
        ul.removeChild(ul.children[0])
        // 12.用按钮依次删除
        var btn = document.querySelector('#submit_remove')
        btn.onclick = function () {
            if (ul.children.length == 0) {
                this.disabled = true
            } else {
                ul.removeChild(ul.children[0])
            }
        }
        // 13.克隆节点
        var ulclone = document.querySelector('.clone')
        ulclone.appendChild(ulclone.children[0].cloneNode(true))
    </script>
</body>

</html>
```

### 19.新浪下拉菜单

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        li {
            list-style-type: none;
        }

        a {
            text-decoration: none;
            font-size: 14px;
        }

        .nav {
            margin: 100px;
        }

        .nav>li {
            position: relative;
            float: left;
            width: 80px;
            height: 41px;
            text-align: center;
        }

        .nav li a {
            display: block;
            width: 100%;
            height: 100%;
            line-height: 41px;
            color: #333;
        }

        .nav>li>a:hover {
            background-color: #eee;
        }

        .nav ul {
            display: none;
            position: absolute;
            top: 41px;
            left: 0;
            width: 100%;
            border-left: 1px solid #FECC5B;
            border-right: 1px solid #FECC5B;
        }

        .nav ul li {
            border-bottom: 1px solid #FECC5B;
        }

        .nav ul li a:hover {
            background-color: #FFF5DA;
        }
    </style>
</head>

<body>
    <ul class="nav">
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
    </ul>
    <script>
        var lis = document.querySelector('.nav').children
        for (var i = 0; i < lis.length; i++) {
            lis[i].onmouseover = function () {
                console.log(this.children[1]);
                this.children[1].style.display = 'block'
            }
            lis[i].onmouseout = function () {
                this.children[1].style.display = 'none'
            }
        }
    </script>
</body>

</html>
```

### 20.简单版发布留言板案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        li {
            color: red;
            background-color: pink;
            width: 100px;
            height: 30px;
            line-height: 30px;
        }
    </style>
</head>

<body>
    <textarea rows="20" cols="20" maxlength="100"></textarea>
    <input type="submit" name="submit" id="submit">
    <ul>

    </ul>
    <script>
        var submit = document.querySelector('#submit')
        var ul = document.querySelector('ul')
        var textarea = document.querySelector('textarea')
        submit.onclick = function () {
            if (textarea.value == '') {
                alert("不可为空！")
            } else {
                var li = document.createElement('li')
                li.innerText = textarea.value
                ul.insertBefore(li, ul.children[0])
            }

        }
    </script>
</body>

</html>
```

### 21.删除留言案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
             margin: 0;
             padding: 0;
        }
        textarea {
            margin: 10px 0px 0px 20px;;
        }
        li {
            margin-left: 10px;
            color: red;
            background-color: pink;
            width: 300px;
            height: 30px;
            line-height: 30px;
        }
        ul li a{
            float: right;
        }
    </style>
</head>

<body>
    <textarea rows="20" cols="20" maxlength="100"></textarea>
    <input type="submit" name="submit" id="submit">
    <ul>

    </ul>
    <script>
        var submit = document.querySelector('#submit')
        var ul = document.querySelector('ul')
        var textarea = document.querySelector('textarea')
        submit.onclick = function () {
            if (textarea.value == '') {
                alert("不可为空！")
            } else {
                var li = document.createElement('li')
                li.innerHTML = textarea.value + "<a href='javascript:;' style='float=right;'>删除</a>"
                ul.insertBefore(li, ul.children[0])
                var as = document.querySelectorAll('a')
                for (var i=0;i<as.length;i++) {
                    as[i].onclick = function() {
                        // console.log(this.parentNode)
                        ul.removeChild(this.parentNode)
                    }
                }
            }

        }
    </script>
</body>

</html>
```

### 22.动态生成表格

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        table {
            width: 500px;
            margin: 100px auto;
            border-collapse: collapse;
            text-align: center;
        }

        td,
        th {
            border: 1px solid #333;
        }

        thead tr {
            height: 40px;
            background-color: #ccc;
        }
    </style>
</head>

<body>
    <table cellspacing="0">
        <thead>
            <tr>
                <th>姓名</th>
                <th>科目</th>
                <th>成绩</th>
                <th>操作</th>
            </tr>
        </thead>
        <tbody>

        </tbody>
    </table>
    <script>
        var datas = [{
            name: '卫英络',
            subject: 'javascript',
            score: 100
        }, {
            name: '宏利',
            subject: 'javascript',
            score: 98
        }, {
            name: '傅亨',
            subject: 'javascript',
            score: 99
        }, {
            name: '明宇',
            subject: 'javascript',
            score: 88
        },]
        var tbody = document.querySelector('tbody')
        for (var i = 0; i < datas.length; i++) {
            // 创建行
            var tr = document.createElement('tr')
            tbody.appendChild(tr)
            // 行里面创建单元格
            for (var k in datas[i]) {
                var td = document.createElement('td')
                td.innerText = datas[i][k]
                tr.appendChild(td)
            }
            var td = document.createElement('td')
            td.innerHTML = "<a href='javascript:;'>删除</a>"
            tr.appendChild(td)

        }
        var as = document.querySelectorAll('a')
        for (var i = 0; i < as.length; i++) {
            as[i].onclick = function () {
                tbody.removeChild(this.parentNode.parentNode)
            }
        }
    </script>
</body>

</html>
```

### 23.注册事件的2种方式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button>传统注册方式</button>
    <button>方法监听注册方式</button>
    <script>
        // 1.传统方式：一个元素创建两个事件会只执行一个(最后一个)
        var btns = document.querySelectorAll('button')
        btns[0].onclick = function() {
            alert('test1')
        }
        btns[0].onclick = function() {
            alert('test2')
        }
        // 2.事件监听注册方式
        // eventTarget.addEventListener(type,listener[,useCapture])
        // 该方法将只当的监听器注册到eventTarget(目标对象上),当该对象触发指定的事件时，就会执行事件处理函数。
        // type 事件类型字符串，比如click，mouseover
        // listener 事件处理函数，事件发生时，会调用该监听函数
        // useCapture 可选参数，是一个布尔值，默认false
        btns[1].addEventListener('click',function() {
            alert('test3')
        })
        btns[1].addEventListener('click',function() {
            alert('test4')
        })
    </script>
</body>
</html>
```

### 24.删除事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            height: 100px;
            width: 100px;
            background-color: pink;
        }
    </style>
</head>
<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <script>
        // 1.传统方式
        var divs = document.querySelectorAll('div')
        divs[0].onclick = function() {
            alert(123)
            divs[0].onclick = null
        }
        // 2.监听方式
        function fn() {
            alert(456)
            divs[1].removeEventListener('click', fn)
        }
        divs[1].addEventListener('click',fn)
        
    </script>
</body>
</html>
```

### 25.事件对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div>123</div>
    <script>
        var div = document.querySelector('div')
        div.onclick = function(event){
            console.log(event);
        }
        // 1. event就是一个事件对象，当作形参来看
        // 2. 事件对象只有有了事件才会存在，他是系统给我们创建的，不需要我们传递参数
        // 3. 事件对象 是我们事件的一些列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标等。
    </script>
</body>
</html>
```

### 26.常见事件对象的属性和方法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div>112</div>
    <ul>
        <li>abc</li>
        <li>abc</li>
        <li>abc</li>
    </ul>
    <a href="http://wwwbaidu.com">百度</a>
    <form action="http://www.baidu.com">
        <input type="submit" name="提交" id="sub">
    </form>
    <script>
        var div = document.querySelector('div')
        div.addEventListener('click',function(e) {
            // 返回触发事件的对象
            // 1.e.target返回的是触发事件的对象
            console.log(e.target);
            // 2.this返回的是绑定事件的对象
            console.log(this);
            // 3.e.type返回事件类型
            console.log(e.type);
        })
        var ul = document.querySelector('ul')
        ul.addEventListener('click',function(e){
            console.log(e.target);
            console.log(this);
        })
        // 4.阻止默认行为，让连接不跳转 或者让提交按钮不提交
        var a = document.querySelector('a')
        a.addEventListener('click',function(e){
            e.preventDefault()
        })
    </script>
</body>
</html>
```

### 27.阻止冒泡

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .outer {
            overflow: hidden;
            width: 300px;
            height: 300px;
            background-color: pink;
            margin: 0 auto;
        }
        .inner {
            margin: 50px;
            width: 200px;
            height: 200px;
            line-height: 200px;
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="outer">
        <div class="inner"></div>
    </div>
    <script>
        var outer = document.querySelector('.outer')
        outer.addEventListener('click',function(e){
            alert(123)
        })
        var inner = document.querySelector('.inner')
            inner.addEventListener('click', function (e) {
                alert(456)
                // 阻止事件冒泡
                e.stopPropagation()
            })
        
    </script>
</body>
</html>
```

### 28.常用鼠标事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            height: 3000px;
        }
    </style>
</head>
<body>
    哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈
    <script>
        // 1.禁用右键菜单contextmenu
        document.addEventListener('contextmenu',function(e){
            e.preventDefault()
        })
        // 2.禁止选中文字selectstart
        document.addEventListener('selectstart',function(e){
            e.preventDefault()
        })
        // 3.获取鼠标x和y坐标，相对于浏览器窗口可视区域
        document.addEventListener('click',function(e){
            console.log(e.clientX);
            console.log(e.clientY);
            console.log("-------------------------");
        })
        // 4.获取鼠标x和y坐标，相对于页面
        document.addEventListener('click',function(e){
            console.log(e.pageX);
            console.log(e.pageY);
            console.log("-------------------------");
        })
        // 5.反会鼠标相对于电脑屏幕的x和y坐标
        document.addEventListener('click',function(e){
            console.log(e.screenX);
            console.log(e.screenY);
        })
    </script>
</body>
</html>
```

### 29.跟随鼠标的天使

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        img {
            position: absolute;
        }
    </style>
</head>
<body>
    <img src="./Images/angel.gif">
    <script>
        var img = document.querySelector('img')
        document.addEventListener('mousemove',function(e){
            // mousemove只要鼠标移动了1px，就触发这个事件
            var x = e.pageX
            var y = e.pageY
            console.log(img.width);
            img.style.left = x - img.width/4 + 'px'
            img.style.top = y  - img.height/2 + 'px'
        })
    </script>
</body>
</html>
```

### 30.键盘常用事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        // 1.keyup键盘按下弹起时触发
        document.onkeyup  = function() {
            console.log("我弹起了");
        }
        // 2.keydown键盘按下时触发  ，闭keypress优先触发
        document.onkeydown = function() {
            console.log("我按下了");
        }
        // 3.keypress键盘按下时触发，但不识别功能键，如ctrl，shift 箭头等。
        document.onkeypress = function() {
            console.log("我按下了111");
        }
    </script>
</body>
</html>
```

### 31.键盘事件之keyCode事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        // keyup打印ascll码，不区分大小写
        document.addEventListener('keyup',function(e){
            console.log(e.keyCode);
        })
        // keyup打印ascll码，不区分大小写
        document.addEventListener('keypress',function(e){
            console.log(e.keyCode);
        })
</script>
</body>
</html>
```

### 32.模拟京东按键输入内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <input type="text" name="" id="">
    <script>
        var search = document.querySelector('input')
        document.addEventListener('keyup',function(e){
            console.log(e.keyCode);
            if (e.keyCode == 83) {
                search.focus()
            }
        })
    </script>
</body>
</html>
```

### 33.模拟京东快读查询

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .search {
            position: relative;
            width: 178px;
            margin: 100px;
        }

        .con {
            display: none;
            position: absolute;
            top: -40px;
            width: 171px;
            border: 1px solid rgba(0, 0, 0, .2);
            box-shadow: 0 2px 4px rgba(0, 0, 0, .2);
            padding: 5px 0;
            font-size: 18px;
            line-height: 20px;
            color: #333;
        }

        .con::before {
            content: '';
            width: 0;
            height: 0;
            position: absolute;
            top: 28px;
            left: 18px;
            border: 8px solid #000;
            border-style: solid dashed dashed;
            border-color: #fff transparent transparent;
        }
    </style>
</head>

<body>
    <div class="search">
        <div class="con">123</div>
        <input type="text" placeholder="请输入您的快递单号" class="jd">
    </div>
    <script>
        var con = document.querySelector('.con')
        var inp = document.querySelector('input')
        inp.addEventListener('keyup', function () {
            if (inp.value == '') {
                con.style.display = 'none'
            } else {
                con.style.display = 'block'
                con.innerText = this.value
            }
            inp.addEventListener('blur',function() {
                con.style.display = 'none'
            })
            inp.addEventListener('focus',function(){
                if (inp.value!=''){
                    con.style.display = 'block'
                }
            })
        })
    </script>
</body>
```

# 3.Js-Bom

> BOM(Browser Object Model)即浏览器对象模型，它提供了独立于内容而与浏览器窗口进行交互的对象，其核心是window

### 1.BOM顶级对象window

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var num = 10
        console.log(num);
        console.log(window.num);
        function fn() {
            console.log(11);
        }
        window.fn()
        console.log(window);
    </script>
</body>
</html>
```

### 2.BOM常见事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        // onload是窗口加载事件，当文档内容全部加载完才会执行此事件。多个onload，以最后一个为准
        // window.onload = function () {
        //     var button = document.querySelector('button')
        //     button.addEventListener('click', function () {
        //         alert('点击我')
        //     })
        // }
        window.addEventListener('load',function(){
            var button = document.querySelector('button')
            button.addEventListener('click', function () {
                alert('点击我')
            })
        })
        window.addEventListener('load',function(){
            alert(2222)
        })
        // DOMContentLoaded等待所有DOM加载完毕，不包含图片，flash等。加载速度闭load快
        document.addEventListener('DOMContentLoaded',function() {
            alert(3333)
        })
    </script>
    <button>点击</button>
</body>
</html>
```

### 3.调整窗口大小事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>
<body>
    <div></div>
    <script>
        // 1.窗口大小发生变化触发
        // 如果窗口宽度小于900就隐藏div
        var div = document.querySelector('div')
        window.addEventListener('resize',function(){
            console.log("变化了");
            // window.innerWidth获取窗口宽度
            if (window.innerWidth <900) {
                div.style.display = 'none'
            }else {
                div.style.display = 'block'
            }
        })
    </script>
</body>
</html>
```

### 4.定时器

> windows.setTimeout(调用函数，[延迟毫秒数])

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=s, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        // 1.setTimeout(调用函数,[延迟毫秒数]),时间可以省略，默认为0
        // 语法规范:window.setTimeout(调用函数,[延迟毫秒数])
        // window可以省略
        // 写法1
        setTimeout(function(){
            alert('时间到了')
        },2000)
        // 写法2
        function func() {
            alert('时间到')
        }
        setTimeout(func,500)
    </script>
</body>
</html>
```

### 5.5秒钟自动关闭广告

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <img src="./images/1.jpg" alt="">
    <script>
        var img = document.querySelector('img')
        setTimeout(function () {
            img.style.display = 'none'
        }, 5000)
    </script>
</body>

</html>
```



### 6.停止定时器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button>点击停止计时</button>
    <script>
        // window.clearTimeout(timeId)
        var btn = document.querySelector('button')
        var time = setTimeout(function(){
            alert('计时结束')
        },5000)
        btn.addEventListener('click',function(){
            clearTimeout(time)
        })
    </script>
</body>
</html>
```

### 7.定时器之setInterval

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        // 每隔一定秒数就执行某个函数
        setInterval(function(){console.log('正在输出');},2000)
    </script>
</body>
</html>
```

### 8.倒计时效果

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div>
        <div class="hour">1</div>
        <div class="minute">2</div>
        <div class="second">3</div>
    </div>
    <script>
        var hour = document.querySelector('.hour')
        var minute = document.querySelector('.minute')
        var second = document.querySelector('.second')
        var inputtime = new Date('2022-03-29 20:00:00')
        timeout()
        setInterval(timeout,1000)
        function timeout() {
            var newtime = new Date()
            var time = (inputtime - newtime) / 1000
            var h = parseInt(time / 60 / 60 % 24)
            h = h < 10 ? '0' + h : h
            var m = parseInt(time / 60 % 60)
            m = m < 10 ? '0' + m : m
            var s = parseInt(time % 60)
            s = s < 10 ? '0' + s : s
            hour.innerHTML = h
            minute.innerHTML = m
            second.innerHTML = s

        }
    </script>
</body>

</html>
```

### 9.清除setInterval定时器

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div>
        <div class="hour">1</div>
        <div class="minute">2</div>
        <div class="second">3</div>
    </div>
    <script>
        var hour = document.querySelector('.hour')
        var minute = document.querySelector('.minute')
        var second = document.querySelector('.second')
        var inputtime = new Date('2022-03-29 20:00:00')
        timeout()
        setInterval(timeout,1000)
        function timeout() {
            var newtime = new Date()
            var time = (inputtime - newtime) / 1000
            var h = parseInt(time / 60 / 60 % 24)
            h = h < 10 ? '0' + h : h
            var m = parseInt(time / 60 % 60)
            m = m < 10 ? '0' + m : m
            var s = parseInt(time % 60)
            s = s < 10 ? '0' + s : s
            hour.innerHTML = h
            minute.innerHTML = m
            second.innerHTML = s

        }
    </script>
</body>

</html>
```

### 11.发送短信案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <input type="text" name="" id="">
    <button>发送</button>
    <script>
        var input = document.querySelector('input')
        var button = document.querySelector('button')
        var time = null;
        button.addEventListener('click', function () {
            button.disabled = 'true'
            time = 5
            var timer = setInterval(function () {
                button.innerHTML = '还剩' + --time + '秒后可以点击'
                if (time < 0) {
                    clearInterval(timer)
                    button.innerHTML = '发送'
                    button.disabled = !button.disabled
                }
            }, 1000)

        })
    </script>
</body>

</html>
```

### 11.this指向问题

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        // this一般情况下指向的都是调用者
        // 1.在全局作用域或普通函数中this指向的是window，定时器也指向window
        console.log(this);
        function fn() {
            console.log(this);
        }
        fn()
        // 2.方法中this的指向是对象本身o
        o = {
            sayhi:function() {
                console.log(this);
            }
        }
        o.sayhi()
    </script>
</body>
</html>
```

### 12.5秒钟之后跳转页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button>点击</button>
    <script>
        var btn = document.querySelector('button')
        btn.addEventListener('click',function(){
            // 查看当前地址
            console.log(location.href);
            setTimeout(function(){
                location.href = 'http://www.baidu.com'
            },5000)
        })
    </script>
</body>
</html>
```

### 13.location常见方法

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <button class="btn1">assign点击1</button>
    <button class="btn2">replace点击2</button>
    <button class="btn3">reload点击3</button>
    <script>
        var button = document.querySelector('.btn1')
        button.addEventListener('click', function () {
            // 1.记录浏览历史，可以实现前进后退
            // 跟href一样，可以实现页面跳转(也成为重定向页面)
            location.assign('http://www.baidu.com')
        })
        var button = document.querySelector('.btn2')
        button.addEventListener('click', function () {
            // 2.replace替换当前页面，不记录历史，不可前进后退
            location.replace('http://www.baidu.com')
        })
        var button = document.querySelector('.btn3')
        button.addEventListener('click', function () {
            // 3.重新加载页面，相当于f5,如果参数为true，为强制刷新ctrl+f5
            location.reload()
        })
    </script>
</body>

</html>
```

### 14.navigator对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <script>
        // mavigator包含很多浏览器对象信息，比如user-agent
        console.log(navigator);
    </script>
</body>
</html>
```

### 15.history对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        // 前进
        // history.forward()
        // 后退
        // history.back()
        // history.go(1)  前进1步  -1 后退1步
    </script>
</body>
</html>
```

# Pc网页动效

