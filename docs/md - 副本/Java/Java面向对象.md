

# Java 面向对象

## 一、方法

访问修饰符:

- 定义格式中三个修饰符的意义：
  1. static：表示该方法是静态方法，可以有类直接调用

  2. final：表示该方法不能被子类重写。

  3. abstract：表示该方法是一个抽象方法。

![image-20210621202503634](Linux%E5%9F%BA%E7%A1%80_imgs/image-20210621202503634.png)

- public/private/protected的具体区别

  1、public：public表明该数据成员、成员函数是对所有用户开放的，所有用户都可以直接进行调用
  2、private：private表示私有，私有的意思就是除了class自己之外，任何人都不可以直接使用。
  3、protected：protected对于子女、朋友来说，就是public的，可以自由使用，没有任何限制，而对于其他的外部class，protected就变成private。

### 2.值传递与引用传递

#### 1.值传递

```java
package 面向对象.值传递与引用传递;

public class 值传递 {
    public static void main(String[] args) {
        int a = 3;
        int b ;
        b = a;
        System.out.println(a);
        System.out.println(b);
        b = 5;
        System.out.println(a);
        System.out.println(b);
    }
}
```

#### 2.引用传递

- 示例1

  ```java
  package 面向对象.值传递与引用传递;
  
  public class 引用传递 {
      public static void main(String[] args) {
  
          Student student1 = new Student();
          student1.setName("琴静");
          System.out.println("student1的name："+student1.getName());
          Student student2 = new Student();
          student2.setName("张俊");
          System.out.println("student2的name："+student2.getName());
          student2.setName(student1.getName());
          System.out.println("student1的name："+student1.getName());
          System.out.println("student2的name："+student2.getName());
          // 运行之后发现当修改了student2的name值后,student1的name也会变
      }
  }
  class Student{
      String strName;
      public String getName(){
          return strName;
      }
      public void setName(String name){
          strName = name;
      }
  }
  ```


- 示例2

  ```java
  package 面向对象.值传递与引用传递;
  
  public class 引用传递1 {
      public static void main(String[] args) {
          int a[] = {1,2,3};
          int b[] = new int[3];
          b = a;
          System.out.println(b[0]);
          a[0] = 5;
          System.out.println(b[0]);
      }
  }
  ```

  

### 4.静态方法

![image-20210621155958463](Linux%E5%9F%BA%E7%A1%80_imgs/image-20210621155958463.png)

```python
package 面向对象;

public class 静态方法 {
    // 用static修饰定义一个静态方法
    public static void helloWorld(){
        System.out.println("这是一个静态方法！");
    }
    public static void main(String[] args) {
        // 直接用类名调用静态方法
        静态方法.helloWorld();
    }
}
```

### 5.方法重载

```java
package 面向对象.方法;

public class 方法重载 {
    public void method(int x){
        System.out.println(x);
    }
    public void method(int x,int y){
        System.out.printf("%s,%s",x,y);
    }

    public static void main(String[] args) {
        方法重载 a = new 方法重载();
        a.method(5);
        a.method(10,15);
    }
    // 可以看到定义了两个方法，但是参数数量不一样。后面定义了一个对象，调用方法，可以发现传入的参数不同，返回结果也是不同的
}
```

## 二、常用的类库

### 1.日期类-Data

![image-20210621183232942](Linux%E5%9F%BA%E7%A1%80_imgs/image-20210621183232942.png)

```java
package 面向对象.常用的类库.日期类;

import java.util.Date;

public class 日期类 {
    public static void main(String[] args) {
        Date date1 = new Date();    // 获取当前时间
        Date date2 = new Date(System.currentTimeMillis()+12345);    // 当前时间+12345ms
        System.out.println(date1);
        System.out.println(date2);
        System.out.println("时间戳:"+date2.getTime()+"ms");
        System.out.println(date1.compareTo(date2)); // 判断date1和date2是否相同，相同返回0，小返回-1，大返回1
        System.out.println(date1.before(date2));    // 判断date1是否比date2早
    }
}
```

### 2.日期格式化类

![image-20210621184438667](Linux%E5%9F%BA%E7%A1%80_imgs/image-20210621184438667.png)

```java
package 面向对象.常用的类库;

import java.text.SimpleDateFormat;
import java.util.Date;

public class 日期格式化类 {
    public static void main(String[] args) {
        // 创建格式化格式
        String format1 = "yyyy年MM月dd日 HH:mm:ss E";
        String format2 = "yyyy年MM月dd日 HH时mm分ss秒SSS E";
        // 创建sdf对象，并传入格式
        SimpleDateFormat sdf1 = new SimpleDateFormat(format1);
        SimpleDateFormat sdf2 = new SimpleDateFormat(format2);
        // 格式化当前日期
        String date1 = sdf1.format(new Date());
        String date2 = sdf2.format(new Date());
        System.out.println(date1);
        System.out.println(date2);
    }
}
```



```java
package 面向对象.常用的类库;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class 日期格式化类1 {
    public static void main(String[] args) {
        String strDate = "2012-09-08 13:56:35.321";		//  日期
        String format = "yyyy-MM-dd HH:mm:ss.SSS";		// 指定要格式化的日期格式
        SimpleDateFormat sdf = new SimpleDateFormat(format);	// 创建sdf对象，并传入指定格式化格式
        Date date = null;	# 创建Date类型
        try {
            date = sdf.parse(strDate);	# 用parse方法转换
        } catch (ParseException e) {
            e.printStackTrace();
        }
        System.out.println(date);
        }
}
```

### 3. 随机类

```java
package 面向对象.常用的类库.随机类;

import java.util.Random;

public class 随机类 {
    public static void main(String[] args) {
        int num;
        Random random = new Random();
        for(int i=0;i<19;i++){
            num = random.nextInt(6)+1;
            System.out.println(num);
        }
        // 利用随机类Random随机产生1-6的20个随机数
    }
}
```

### 4.字符类

```java
package 面向对象.常用的类库;

public class 字符类 {
    public static void main(String[] args) {
        // 创建String对象
        String  string = new String("Hello World!");
        System.out.println(string);
        // 比较字符串
        String string1 = new String("Hello World!");
        System.out.println(string==string1);    // 判断地址是否相同
        System.out.println(string.equals(string1)); // 判断内容是否相同
        // String的length，charAt和getChars方法
        System.out.println(string.length());
        System.out.println(string.charAt(2));
        char arr[] = new char[5];
        // 取string的下标0-1的数放进arr数组中，从arr[0]开始。
        string.getChars(0,2,arr,0);
        System.out.println(arr[0]);
        System.out.println(arr);
    }
}
```

## 三、

### 1.构造方法

```java
package 面向对象;

public class 构造方法 {
    public static void main(String[] args) {
        Person person = new Person(20,"赵涛涛");
        person.say();
    }
}
class Person{
    int age;
    String name;
    // 创建了一个构造方法
    public Person(int age,String name){
        this.age=age;
        this.name=name;
    }
    public void say(){
        System.out.println("我的年龄是"+this.age+",我叫"+this.name);
    }
}
```



### 2.构造方法重载

```java
package 面向对象;

public class 构造方法重载 {
    public static void main(String[] args) {
        Student stu1 = new Student("赵涛涛");
        System.out.println(stu1.name);
        Student stu2 = new Student("周杰伦",20);
        System.out.printf("%s   %s",stu2.name,stu2.age);
    }
}
class Student{
    String name;
    int age;
    public Student(String name) {
        this.name = name;
    }
    public Student(String name,int age){
        this.name = name;
        this.age = age;
    }
}
```



















## 1.类定义的语法形式：

```java
public class 类名｛
    //定义类属性
    属性1类型:属性1名;
    属性2类型:属性2名;
    …
    //定义方法
    方法1定义
    方法2定义
    …
｝
```

现在创建一个Student类:

```java
public class Student {
    String stuName;
    int stuAge;
    int stuSex;
    int stuGrade;
    public void learn() {
        System.out.println(stuName + "正在认真听课！");
    }

    public String doHomework(int hour) {
        return "现在是北京时间：" + hour + "点，" + stuName + "正在写作业!";
    }

}
```

需要注意的是，这个类里面没有 `main` 方法，所以只能编译，不能运行。

定义好 `Student` 类后，就可以根据这个类创建（实例化）对象了。类就相当于一个模板，可以创建多个对象。创建对象的语法形式如下。

```java
类名 对象名 = new 类名();
```

创建对象时，要使用 new 关键字，后面要跟着类名（构造方法名），类名后的括号内可传递构造参数。

根据上面创建对象的语法，创建王云这个学生对象的代码如下。

```java
Student wangYun = new Student();
```

这里，只创建了 wangYun 这个对象，并没有对这个对象的属性赋值，考虑到每个对象的属性值不一样，所以通常在创建对象后给对象的属性赋值。在 Java 语言中，通过 `.` 操作符来引用对象的属性和方法，具体的语法形式如下。

```java
对象名.属性 ;
对象名.方法() ;
```

通过上面的语法形式，可以给对象的属性赋值，也可以更改对象属性的值或者调用对象的方法，具体的代码如下。

```java
wangYun.stuName ="王云";
wangYun.stuAge = 22;
wangYun.stuSex = 1;            //1代表男，2代表女
wangYun.stuGrade = 4;        //4代表大学四年级
wangYun.learn();            //调用学生听课的方法
wangYun.doHomework(22);        //调用学生写作业的方法，输入值22代表现在是22点
```

接下来通过创建一个测试类 `TestStudent`（这个测试类需要和之前编译过的 `Student` 类在同一个目录），来测试 `Student` 类的创建和使用，程序如下。

```java
public class TestStudent {
    public static void main(String[] args) {
        Student wangYun = new Student();
        wangYun.stuName = "王云";
        wangYun.stuAge = 22;
        wangYun.stuSex = 1;
        wangYun.stuGrade = 4;
        wangYun.learn();
        String restring = wangYun.doHomework(22);
        System.out.println(restring);
    }
}
```

![image-20211121130608150](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121130608150.png)

这个程序虽然非常简单，但却是我们第一次使用两个类来完成程序。其中 `TestStudent` 类是测试类，测试类中包含 `main` 方法，提供程序运行的入口。在 `main` 方法内，创建 `Student` 类的对象并给对象属性赋值，然后调用对象的方法。

这个程序有两个 Java 文件，每个 Java 文件中编写了一个 Java 类，编译完成后形成 2 个 class 文件。也可以将两个 Java 类写在一个 Java 文件里，但其中只能有一个类用 public 修饰，并且这个 Java 文件的名称必须用这个 public 类的类名命名，详见以下程序。

```java
public class TestStudent2 {
    public static void main(String[] args) {
        Student2 wangYun = new Student2();
        wangYun.stuName = "王云";
        wangYun.stuAge = 22;
        wangYun.stuSex = 1;
        wangYun.stuGrade = 4;
        wangYun.learn();
        String rstString = wangYun.doHomework(22);
        System.out.println(rstString);
    }
}

class Student2 {
    String stuName;
    int stuAge;
    int stuSex;
    int stuGrade;
    public void learn() {
        System.out.println(stuName + "正在认真听课！");
    }

    public String doHomework(int hour) {
        return "现在是北京时间：" + hour + "点，" + stuName + "正在写作业！";
    }
}
```

![image-20211121131213212](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121131213212.png)

在上面的例子中，对对象的属性都是先赋值后使用，如果没有赋值就直接使用对象的属性，会有什么样的结果呢？

下面将 `TestStudent` 测试类的代码修改成下面的代码。

```java
public class TestStudent {
    public static void main(String[] args) {
        Student wangYun = new Student();
        System.out.println("未赋值前的学生姓名为:" + wangYun.stuName);
        System.out.println("未赋值前的学生年龄为:" + wangYun.stuAge);
        System.out.println("未赋值前的学生性别数值为:" + wangYun.stuSex);
        System.out.println("未赋值前的学生年纪为:" + wangYun.stuGrade);
        wangYun.stuName = "王云";
        wangYun.stuAge = 22;
        wangYun.stuSex = 1;
        wangYun.stuGrade = 4;
        System.out.println("赋值后的学生姓名为：" + wangYun.stuName);
        System.out.println("赋值后的学生年龄为：" + wangYun.stuAge);
        System.out.println("赋值后的学生性别数值为：" + wangYun.stuSex);
        System.out.println("赋值后的学生年级为：" + wangYun.stuGrade);
    }
}
```

![image-20211121131510640](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121131510640.png)

从程序运行结果可以看出，在未给对象属性赋值前使用属性时，属性使用的都是对应数据类型的默认值，即如果该属性为引用数据类型，其初始默认值为 null，如果该属性是 int 型，其初始默认值为 0。

```java
import java.util.Scanner;

public class TestStuTea {
    static Scanner input = new Scanner(System.in);

    public static void main(String[] args) {
        Teacher[] tea = new Teacher[2];
        Student[] stu = new Student[4];
        for (int i = 0; i < tea.length; i++) {
            System.out.println("请创建并输入第" + (i + 1) + "个老师的基本信息");
            tea[i] = createTeacher();
        }
        for (int i = 0; i < stu.length; i++) {
            System.out.println("请创建并输入第" + (i + 1) + "个学生的基本信息");
            stu[i] = createStudent();
        }
        tea[0].teach();
        for (int j = 0; j < stu.length; j++) {
            stu[j].learn();
        }
        for (int j = 0; j < stu.length; j++) {
            String tempStr = stu[j].doHomework(20);
            System.out.println(tempStr);
        }
        for (int j = 0; j < stu.length; j++) {
            tea[1].checkHomework(stu[j]);
        }
    }

    public static Teacher createTeacher() {
        Teacher tea = new Teacher();
        System.out.print("请输入老师的姓名：");
        tea.teaName = input.next();
        System.out.print("请输入老师的专业：");
        tea.teaSpecialty = input.next();
        System.out.print("请输入老师的所讲授的课程：");
        tea.teaCourse = input.next();
        System.out.print("请输入老师的教龄：");
        tea.teaYears = input.nextInt();
        return tea;
    }

    public static Student createStudent() {
        Student stu = new Student();
        System.out.print("请输入学生姓名：");
        stu.stuName = input.next();
        System.out.print("请输入学生年龄：");
        stu.stuAge = input.nextInt();
        System.out.print("请输入学生性别数值（1代表男、2代表女）：");
        stu.stuSex = input.nextInt();
        System.out.print("请输入学生年级：");
        stu.stuGrade = input.nextInt();
        return stu;

    }


}


class Teacher {
    String teaName;
    String teaSpecialty;
    String teaCourse;
    int teaYears;

    public void teach() {
        System.out.println(teaName + "正在辛苦讲:" + teaCourse + "课程！");
    }

    public void checkHomework(Student stu) {
        System.out.println("讲授:" + teaCourse + "课程的老师:" + teaName + "已经批改完毕:" + stu.stuName + "的作业！");
    }
}

class Student {
    String stuName;
    int stuAge;
    int stuSex;
    int stuGrade;

    public void learn() {
        System.out.println(stuName + "正在认真听课！");
    }

    public String doHomework(int hour) {
        return "现在是北京时间：" + hour + "点" + stuName + "正在写作业！";
    }
}
```

![image-20211121134200542](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121134200542.png)

![image-20211121134217478](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121134217478.png)

### 2.初识封装

封装的目的是简化编程和增强安全性。

1. 简化编程是指，封装可以让使用者不必了解具体类的内部实现细节，而只是要通过提供给外部访问的方法来访问类中的属性和方法。例如 Java API 中的 `Arrays.sort()`方法，该方法可以用于给数组进行排序操作，开发者只需要将待排序的数组名放到 `Arrays.sort()`方法的参数中，该方法就会自动的将数组排好序。可见，开发者根本不需要了解 `Arrays.sort()`方法的底层逻辑，只需要简单的将数组名传递给方法即可实现排序。
2. 增强安全性是指，封装可以使某个属性只能被当前类使用，从而避免被其他类或对象进行误操作。例如在 `Student.java` 的程序中，`Student` 的 `stuAge` 属性是 `public` 的形式体现的，但这样做实际存在着安全隐患：`TestStudent` 类（或在访问修饰符可见范围内的其他类）完全可以随意的对 `stuAge` 进行修改，如以下程序。

```java
public class TestStudent {
    public static void main(String[] args) {
        Student wangYun = new Student();
        wangYun.stuAge = -10;
        ...
    }
}
```

如上，给 `stuAge` 赋了一个不符合逻辑的值，但语法是却正确的。因此这种做法，实际就给程序造成了安全问题。如何避免此类问题呢？使用 `private` 修饰符来修饰 `stuAge` 属性，以此禁止 `Student` 以外的类对 `stuAge` 属性的修改。但这么做未免显得“过犹不及”，为了保证安全，也不至于让其他类无法访问吧！有没有一种办法，既能让其他类可以访问 `Student` 类中的 `stuAge` 属性，又能保证其他类始终是在安全的数值范围内修改 `stuAge` 值呢？有，先用 `private` 修饰 `stuAge` 属性，然后再给该属性提供两个 `public` 修饰的、保证属性安全的访问方法（`setter` 方法和 `getter` 方法），即：

1. 用 `private` 禁止其他类直接访问属性；
2. 给 1 中的属性新增两个 `public` 修饰的 `setter` 和 `getter` 方法，供其他类安全的访问。

`setter` 方法用于给属性赋值，而 `getter` 访问用于获取属性的值。并且一般而言，`setter` 方法的名字通常是 `set+属性名`，`getter` 方法的名字通常是 `get+属性名`。

根据以上描述，先用 `private` 修饰 `stuAge`，禁止 `TestStudent` 类对 `stuAge` 的直接访问，以此保证 `stuAge` 安全性；然后新增 `setStuAge()`和 `getStuAge()`方法，一方面供 `TestStudent` 类间接的访问 `stuAge` 属性，另一方面也保证了 `stuAge` 的数据安全，详见以下程序。

```java
public class StudentPrivate {
    private int stuAge;

    public int getStuAge() {
        return stuAge;
    }

    public void setStuAge(int age) {
        if (age > 0 && age < 110)
            stuAge = age;
        else
            age = 0;
    }
}
```
后续，其他类只需要调用 setStuAge()和 getStuAge()方法，就能对 stuAge 属性进行安全的赋值或取值，代码如下。
```java
public class TestStudent3 {
    public static void main(String[] args) {
        StudentPrivate wangYun = new StudentPrivate();
        wangYun.setStuAge(-10);
        int age = wangYun.getStuAge();
        System.out.println(age);
        wangYun.setStuAge(22);
        age = wangYun.getStuAge();
        System.out.println(age);

    }
}
```

![image-20211121135113210](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121135113210.png)

实际上，使用 setter 和 getter 的解决方案用到了一个程序设计的基本原则：逻辑代码不能写在变量中，而必须写在方法或代码块中。

### 3.构造方法基本语法

构造方法不同于普通方法，普通方法代表对象的行为，而构造方法是提供给系统用于创建对象的方法。

构造方法（也称为构造函数）是一种特殊的方法，它具有以下特点。

- 构造方法的方法名必须与类名相同。
- 构造方法没有返回类型，在方法名前不声明返回类型（包括 void）。

构造方法的语法形式如下。

```java
[访问修饰符] 类名([参数列表]) ;
```

虽然构造方法在语法形式上没有返回类型，但其实构造方法是有返回值的，返回的是刚刚被初始化完成的当前对象的引用。既然构造方法返回被初始化对象的引用，为什么不写返回值类型呢？例如 Student 类构造方法为什么不写成 `public Student Student（参数列表）｛…｝`呢？

因为 Java 设计人员把这种方法名（类名）和返回类型的类名相同的方法看成一个普通方法，只是名称“碰巧”相同罢了，编译器识别时也会认为它是一个方法。为了和普通方法进行区别，Java 设计人员规定构造方法不写返回值，编译器通过这一规定识别构造方法，而不是说构造方法真的没有返回值。

将 `Student` 类的代码改为下面的形式：

```java
private String stuName;
private int stuAge;
private int stuSex;
private int stuGrade;

public StudentInit (String name,int age,int sex,int grade) {
    stuName = name;
    stuAge = age;
    stuSex = sex;
    stuGrade = grade;
}
public void learn() {
    System.out.println(stuName + "正在认真听课！");
}

public String doHomework(int hour) {
    return "现在是北京时间：" + hour + "点" + stuName + "正在写作业！";
}
```

测试类 `TestStudent1.java` 的代码如下所示。

```java
public class TestStudent1 {
    public static void main(String[] args) {
        StudentInit wangYun = new StudentInit("王云",22,1,4);
        wangYun.learn();
        String rstString = wangYun.doHomework(22);
        System.out.println(rstString);
    }
}

```

![image-20211121141633416](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121141633416.png)

### 4.this关键字

`this` 是 Java 的一个关键字，它表示“指向当前对象的引用（后文简称为‘当前对象’）”。举个例子，在前面小节中给 `stuAge` 属性赋值的语句是`wangYun.setStuAge(22);`，这条语句中的当前对象就是 wangYun，因此在 `setStuAge()`方法中 `this` 就是 wangYun。

在实际开发时，this 通常用于以下两个场景。

1. 区分成员变量和局部变量，避免命名的烦恼。
2. 调用其他构造方法。

先看一下如何使用 this 区分成员变量和局部变量。在前面一小节中，我们是通过以下代码给 stuAge 赋值的。

```java
private int stuAge ;
...
public void setStuAge(int age) {
...
stuAge = age ;
}
```

是否可以将参数 `age`，和成员变量 `stuAge` 设置为相同的名称，如下所示。

```java
private int age ;
...
public void setAge(int age) {
...
age = age ;
}
```

显然，编译器将无法区分`age = age`这句代码中哪个变量是成员变量，哪个变量是参数，因此我们之前就只能通过不同的变量名来区分。而现在，我们就可以通过 this 来区分不同的 age，如下所示。

```java
private int age ;
...
public void setAge(int age) {
...
this.age = age ;
}
```

在`this.age = age ;`这句代码中，因为 this 代表着当前对象，因此`this.age`就代表了当前对象的 age 属性；而`age`没有 this 修饰，就会根据变量的作用域，默认为方法参数中的 age。

再看一下如何使用 this 调用其他构造方法。

在构造方法中，还可以使用 this 调用类中的其他构造方法，但这种`this()`语句必须写在构造方法的一行，如下所示。

```java
public Student() {
    //调用有一个String参数的构造方法
    this(" WangYun" );
}

public Student(String name) {
    //调用有两个参数的构造方法
    this(name,23);
}

public Student(String name, int age) {
    ...
}
```

需要注意的是，所有的构造方法之间不能循环调用，否则会出现类似“死循环”的现象。例如以上代码，如果在最后一个构造方法的第一行也加上`this()`，那么三个构造方法就会无限制的彼此调用。

例：

构造方法的主要作用是完成对象的初始化工作，它能够把定义对象时的参数传给对象。一个类可以定义多个构造方法，但需要根据参数的个数、类型或排列顺序来区分不同的构造方法，详见以下程序。

新建一个 `Student1.java` 文件，并输入以下代码。

```java
public class Student1 {
    private String name;
    private int age;
    private int sex;
    private int grade;

    public Student1(String name, int age, int sex, int grade) {
        this(name, age, sex);
        this.grade = 4;
    }

    public Student1(String name, int age, int sex) {
        this(name, sex);
        this.age = age;
        this.grade = 4;
    }

    public Student1(String name, int sex) {
        this.sex = sex;
        this.name = name;
        this.age = 22;
        this.grade = 4;
    }

    public Student1(String name) {
        this.name = name;
        this.age = 22;
        this.grade = 4;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public void setSex(int sex) {
        this.sex = sex;
    }

    public int getGrade() {
        return grade;
    }
    public void setAge(int age) {
        if (age > 0 && age <110) {
            this.age = age;
        } else {
            this.age = 0;
        }
    }
    public void learn() {
        System.out.println(name + "正在认真听课！");
    }
    public String doHomework(int hour) {
        return "现在是北京时间：" + hour + "点," + name + "正在写作业！";
    }
}
```

新建测试类 `TestStudent3`，其代码如下。

```java
public class TestStudent4 {
    public static void main(String[] args) {
        Student1 wangYun = new Student1("王云",22,1,4);
        Student1 liuJT = new Student1("刘静涛",21,2);
        Student1 nanTH = new Student1("南天华");
        nanTH.setSex(1);

        wangYun.learn();
        String rstString = wangYun.doHomework(22);
        System.out.println(rstString);

        liuJT.learn();
        System.out.println(liuJT.getName() + "正在读大学" + liuJT.getGrade() + "年级");
        System.out.println(nanTH.doHomework(23));
    }
}

```

![image-20211121143637588](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121143637588.png)

构造方法有一个约定：如果在定义类时没有定义构造方法，编译系统会自动插入一个无参数的默认构造方法，这个构造方法不执行任何代码。如果在定义类时定义了有参的构造方法，没有显式地定义无参的构造方法，那么在使用构造方法创建类对象时，则不能使用默认的无参构造方法。

例如，在 `TestStudent3` 程序的 `main` 方法内添加一行语句`Student leiJing = new Student();`，编译器会报错，提示没有找到无参的构造方法。

### 5.对象的初始化过程

对象的初始化，实际就是先在堆内存中申请一块用于存放对象属性值的空间，然后再给这些属性值赋上默认值、程序员期望的数据或者用户指定的数据。当堆内存中的这块空间有了值以后，再在栈空间中申请一块空间并存放引用变量，然后用栈中的引用变量指向堆中的对象，最终就可以通过栈中的引用变量访问或者修改堆中的对象了，如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/a52bd58b463cfe98caf9b39735b00a2a-0)

下面我们结合代码，分析对象初始化过程中内存演变的细节。

本次在堆中存放的对象是由 `Student` 类生成的，并且 `Student` 类通过初始化块给属性赋了值（初始化块会在本节的后续分析内存演变时讲解），详见以下程序。

```java
public class Student2 {
    private String name = "";
    private int age = -1;
    private int sex = -1;
    private int grade = -1;
    {
        System.out.println("使用初始化快初始化");
        this.name = "雷静";
        this.age = 22;
        this.sex = 2;
        this.grade = 4;
    }
    public Student2() {
        System.out.println("使用无参构造函数初始化");
    }

    public Student2(String name,int age,int sex,int grade) {
        System.out.println("使用有参构造函数初始化");
        this.name = name;
        this.age = age;
        this.sex = sex;
        this.grade = grade;
    }
    public void setSex(int sex) {
        this.sex = sex;
    }
    public int getGrade() {
        return grade;
    }
    public String getName() {
        return name;
    }
}
```

新建测试类 `TestStudent5.java`，其代码如下。

```java
public class TestStudent5 {
    public static void main(String[] args) {
        Student2 temp = new Student2();
        System.out.println(temp.getName() + "正在读大学" + temp.getGrade() + "年级");
        Student2 wangYun = new Student2("王云",22,1,4);
        System.out.println(wangYun.getName() + "正在读大学" + wangYun.getGrade() + "年级");
    }
}
```

对象初始化时的内存演变过程如下。

1. `Student2 temp= new Student2();`执行时，首先需要在堆内存中申请空间，用于存放对象的实例，这片空间上成员变量的值全部为默认值：name 的值是 null、age 的值是 0……，如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/3b1d455c641443828bc109ede4544c83-0)

1. 紧接着，执行声明初始化（由设计该类的开发者指定），例如在 `Student2` 类中`private int age = -1;`代表程序员希望 age 属性用值-1 覆盖默认值，如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/280c2be5a7e237b5ec4f52079256dcba-0)

3.初始化块初始化。

初始化块就是在类的下一级（与成员变量和成员方法同级）用一对大括号括起来的代码块，语法形式如下：

```java
{
    代码块
}
```

初始化块可以用来覆盖类的成员变量的值，初始化块的执行时机是发生在“声明初始化”之后，在“构造器初始化”之前。例如，如下的初始化代码，就用于给成员变量再次赋值，如图所示。

```java
{
    this.name = "雷静";
    this.age = 22;
    this.sex = 2;
}
```

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/1b9536540928bd247b6911a4f0207daa-0)

执行程序后，运行结果如图所示。大家可以通过运行结果，分析刚才说的初始化块的执行时机。

![image-20211121151010497](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121151010497.png)

1. 构造器初始化，例如`Student2 temp = new Student2("王云", 22, 1, 4);`，在默认初始化，声明初始化，初始化块之后，再此用构造器覆盖各个属性的值，如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/a1eadb542a26b2ff6252e679101ed970-0)

### 6.重载基本语法

在同一个类中，可以有两个或两个以上的方法具有相同的方法名，但它们的参数列表不同。这种形式被称为重载（overload）。所谓参数列表不同包括以下三种情形。

- 参数的数量不同。
- 参数的类型不同。
- 参数的顺序不同。

必须注意的是，仅返回值不同不能视为方法重载，还会得到一个语法错误。而且重载的方法之间只是“碰巧”名称相同罢了，不具备连带效应。既然方法名称相同，在使用相同的名称调用方法时，编译器怎么确定调用哪个方法呢？这就要靠传入参数的不同确定具体调用哪个方法。

注意，一个类的多个构造方法被视为重载，因为多个构造方法的方法名相同，而参数列表不同，符合重载的定义。

看以下程序中的代码，其中的重点是 `learn` 方法的重载。

```java
public class Student3 {
    private String name;
    private int age;

    public Student3(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public void read(String bookName, String bookAuthor, double bookPrice) {
        if (bookName != null && bookAuthor == null && bookPrice != 0.0) {
            System.out.println(this.name + "正在读《" + bookName + "》，书价：" + bookPrice);
        }
        //当bookPrice使用的是默认值时
        if (bookName != null && bookAuthor != null && bookPrice == 0.0) {
            System.out.println(this.name + "正在读《" + bookName + "》，作者：" + bookAuthor);
        }

        //当全部的参数都使用的是默认值时
        if (bookName == null && bookAuthor == null && bookPrice == 0.0) {
            System.out.println(this.name + "正在读书");
        }

        //当全部的参数都使用的不是默认值时
        if (bookName != null && bookAuthor != null && bookPrice != 0.0) {
            System.out.println(this.name + "正在读《" + bookName + "》，作者：" + bookAuthor
                    + "，书价：" + bookPrice);
        }
    }

    public void read(String bookName, String bookAuthor) {
        this.read(bookName, bookAuthor, 0.0);
    }

    public void read(String bookName, double bookPrice) {
        this.read(bookName, null, bookPrice);
    }

    public void read(String bookName) {
        this.read(bookName, null, 0.0);
    }

    public void read() {
        this.read(null, null, 0.0);
    }

}

```

测试类 `TestStudent6.java` 文件代码如下。

```java
public class TestStudent6 {
    public static void main(String[] args) {
        Student3 stu = new Student3("王云",22);
        stu.read("Java编程思想","埃克尔",108.0);
        stu.read("Java编程思想","埃克尔");
        stu.read("Java编程思想",108.0);
        stu.read();
    }
}
```

![image-20211121152059252](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121152059252.png)
