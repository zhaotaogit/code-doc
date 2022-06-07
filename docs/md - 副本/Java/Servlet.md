# Servlet

## 1.使用注解方式配置

> 这种方法不与web.xml冲突。

@WebServlet()注解常用解释：

> ![image-20220225193754815](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220225193754815.png)

例：

```java
package com.example.webprojet;

import com.sun.org.apache.xalan.internal.xsltc.cmdline.getopt.GetOpt;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Zhtao
 * @date 2022/2/25 19:35
 */
@WebServlet(value = {"/bs","/bss"})
public class BasicServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("这是get");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("这是post");
    }
}
```

此时访问/bs和/bss都可以。

## 2.request对象

### 1.request主要方法

| 方法名                                    | 说明                         |
| ----------------------------------------- | ---------------------------- |
| String getParameter(String name)          | 根据表单组件名称获取提交数据 |
| void setCharacterEncoding(String charset) | 指定每个请求的编码           |

### 2.request应用

#### 1.Get()请求

```java
package com.qf.servlet2;

import com.sun.javaws.HtmlOptions;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.security.SecureRandom;

/**
 * @author Zhtao
 * @date 2022/2/25 19:56
 */
@WebServlet(value = "/rs")
public class RegisterServlet extends HttpServlet {
//    1.获取用户请求发送的数据
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println("用户提交的数据:" + username + "\t" + password);
    }
}
```

![image-20220225200231690](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220225200231690.png)

![image-20220225200251318](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220225200251318.png)

![image-20220225200313042](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220225200313042.png)

#### 2.Post()请求

```java
package com.qf.servlet2;

import com.sun.javaws.HtmlOptions;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.security.SecureRandom;

/**
 * @author Zhtao
 * @date 2022/2/25 19:56
 */
@WebServlet(value = "/rs")
public class RegisterServlet extends HttpServlet {
//    1.获取用户请求发送的数据

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println("用户提交的数据:" + username + "\t" + password);
    }
}
```

![image-20220225200646459](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220225200646459.png)

![image-20220225200638007](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220225200638007.png)

#### 3.解决中文乱码

> req.setCharacterEncoding("UTF-8");

```java
package com.qf.servlet2;

import com.sun.javaws.HtmlOptions;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.security.SecureRandom;

/**
 * @author Zhtao
 * @date 2022/2/25 19:56
 */
@WebServlet(value = "/rs")
public class RegisterServlet extends HttpServlet {


    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//    对request请求对象设置统一编码
        req.setCharacterEncoding("UTF-8");
//    1.获取用户请求发送的数据
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println("用户提交的数据:" + username + "\t" + password);
    }
}
```

### 3.response响应数据

#### 1.response主要方法

| 方法名称                    | 作用                               |
| --------------------------- | ---------------------------------- |
| setHeader(name,value)       | 设置响应信息头                     |
| setContenType(String)       | 设置响应文件数据、响应式的编码格式 |
| setCharacterEncoding(Sting) | 设置服务端响应内容编码格式         |
| getWriter()                 | 获取字符输出流                     |

**例:**用户注册后，返回注册成功！

```java
package com.qf.servlet2;

import com.sun.javaws.HtmlOptions;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.security.SecureRandom;

/**
 * @author Zhtao
 * @date 2022/2/25 19:56
 */
@WebServlet(value = "/rs")
public class RegisterServlet extends HttpServlet {


    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //    对request请求对象设置统一编码
        req.setCharacterEncoding("UTF-8");
//    1.获取用户请求发送的数据
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println("用户提交的数据:" + username + "\t" + password);
//    2.响应数据给客户端
        PrintWriter printWriter = resp.getWriter();
        printWriter.println("Register Success!");
    }
}
```

![image-20220225201638203](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220225201638203.png)

#### 2.解决返回中文乱码

方法1（不推荐）：

```java
resp.setCharacterEncoding("utf-8"); // 设置服务器端编码格式
resp.setHeader("Content-Type","text/html;charset=utf-8");   // 设置客户端编码方式
```

方法2：

放到PrintWriter printWriter = resp.getWriter();后面

```java
resp.setContentType("text/html;charset=UTF-8");
```

