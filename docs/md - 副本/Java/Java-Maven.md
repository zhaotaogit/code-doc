# Java-Maven

## 1.下载安装

首先到Maven观望下载Maven安装包:

官网地址:https://maven.apache.org/download.cgi#

windowns的话下载图中箭头所指位置:

![image-20220304212702482](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304212702482.png)

下载完成后将压缩包解压到你想放的位置，比如D盘。	

![image-20220304212809615](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304212809615.png)

然后配置系统环境变量:

先创建一个MAVEN_HOME：

![image-20220304212914735](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304212914735.png)

然后在系统变量的path中添加:

![image-20220304212948176](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304212948176.png)

最后测试一下是否安装成功:

![image-20220304213009835](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304213009835.png)

## 2.修改仓库位置和配置阿里云镜像源

### 1.配置仓库

打开maven安装目录下的conf/settings.xml文件:

![image-20220304213113890](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304213113890.png)

配置仓库：

![image-20220304213140214](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304213140214.png)

图中的D:/apache-maven-3.8.4/repository是仓库的地址，需要自己创建一个repository文件夹用来存放jar包。

![image-20220304213247493](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304213247493.png)

当你的maven项目需要jar包时，如果jar包不在repository中，就会下载，并存放在repository目录中。

### 2.配置阿里云镜像源

因为jar包大多都是存放在国外服务器，导致下载很慢，所以我们配置成阿里云的镜像源，可以提高下载jar包的速度。

还是打开maven安装目录下的conf/settings.xml文件：

![image-20220304213505446](C:\Users\Oxygen\AppData\Roaming\Typora\typora-user-images\image-20220304213505446.png)

图中框选的位置就是我们要配置的代码:

```xml
    <mirror>
        <id>aliyunmaven</id>
        <mirrorOf>central</mirrorOf>
        <name>aliyun maven</name>
        <url>https://maven.aliyun.com/repository/central</url>
    </mirror>
```

## 3.项目的编译与运行

我们随便创建一个测试项目，目录结构如下:

![image-20220304213638535](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304213638535.png)

![image-20220304213658498](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304213658498.png)

pom.xml文件内容为:

![image-20220304214019132](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304214019132.png)

```xml
<?xml version="1.0" encoding="utf-8" ?>
<project xmlns = "http://maven.apache.org/POM/4.0.0"
         xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation = "http://maven.apache.org/POM/4.0.0
    http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <!-- 模型版本 -->
    <modelVersion>4.0.0</modelVersion>
    <!-- 公司或者组织的唯一标志，并且配置时生成的路径也是由此生成， 如com.companyname.project-group，maven会将该项目打成的jar包放本地路径：/com/companyname/project-group -->
    <groupId>com.companyname.project-group</groupId>

    <!-- 项目的唯一ID，一个groupId下面可能多个项目，就是靠artifactId来区分的 -->
    <artifactId>maven01</artifactId>

    <!-- 版本号 -->
    <version>1.0</version>
    <packaging>jar</packaging>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



src/main/com/xxx/下的demo.java文件内容为：

```java
package com.xxx.demo;

public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello Maven!");
    }
}

```

然后来到项目根目录下，打开cmd执行:

```shel
mvn compile	// 编译
```

然后就会下载项目所需的jar包。

![image-20220304213835483](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304213835483.png)

![image-20220304213902768](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304213902768.png)

出现BUILD SUCCESS即为编译成功！

然后继续执行:

```java
mvn exec:java -Dexec.mainClass="com.xxx.demo.Hello"  // 执行main方法
```

![image-20220304214447587](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304214447587.png)

可以看到成功打印了Hello Maven!.

## 4.Maven命令

Maven命令格式如下:

```shell
mvn [plugin-name]:[goal-name]
```

命令代表的含义：执行`plugin-name`插件的`goal-name`目标

| 命令                   | 描述                                                    |
| ---------------------- | ------------------------------------------------------- |
| mvn -version           | 显示版本信息                                            |
| mvn clean              | 清理项目产生的临时文件，一般是模块下的target目录        |
| mvn compile            | 编译源代码，一般编译模块下的src/main/java目录           |
| mvn package            | 项目打包工具，会在模块下的target目录生成jar或war等文件  |
| mvn test               | 测试命令，或执行src/test/java下junit的测试用例          |
| mvn install            | 将打包的jar/war文件复制到你的本地仓库中，供其他模块使用 |
| mvn deploy             | 将打包的文件发布到远程参考，提供其他人员进行下载依赖    |
| mvn site               | 生产项目相关信息的网站                                  |
| mvn eclipse:eclipse    | 将项目转化为Eclipse项目                                 |
| mvn dependency:tree    | 打印出项目的整个依赖树                                  |
| mvn archetype:generate | 创建Maven的普通java项目                                 |
| mvn tomcat7:run        | 在tomcat容器中运行web应用                               |
| mvn jetty:run          | 调用Jetty插件的Run目标在Jetty Servlet容器中启动web应用  |

## 5.Idea集成Maven环境

进入Idea设置:

![image-20220304220306155](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304220306155.png)

搜索maven：

![image-20220304220333965](C:\Users\Oxygen\AppData\Roaming\Typora\typora-user-images\image-20220304220333965.png)

Maven主路径:maven解压的路径。

用户设置文件:maven路径下conf/settings.xml文件。

记得勾上重写。

## 6.Idea创建Maven项目

打开Idea选择新建项目：

![image-20220304220634850](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304220634850.png)

选择java版本，以及选择模板:

![image-20220304220725802](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304220725802.png)

然后设置项目名称:

![image-20220304220904990](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304220904990.png)

然后选择Maven:

![image-20220304220949213](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304220949213.png)

然后项目就创建好了，idea会自动下载pom中所需的jar包。

然后点击：

![image-20220304222342365](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304222342365.png)

点击+号，选择Maven：

![image-20220304222405753](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220304222405753.png)

配置如图：

![image-20220304222419202](C:\Users\Oxygen\AppData\Roaming\Typora\typora-user-images\image-20220304222419202.png)