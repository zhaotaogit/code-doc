# 安装MySql

首先去官网下载安装包，这里下载的是压缩包：https://dev.mysql.com/downloads/mysql/

![image-20211123225352387](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123225352387.png)

![image-20211123225404726](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123225404726.png)

将下载好的压缩包解压：

![image-20211123225457070](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123225457070.png)

创建一个my.ini文件，内容为：

![image-20211123230034510](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123230034510.png)

```mysql
[mysqld]
# 设置3306端口
port=3306
# 设置mysql的安装目录
basedir=D:\\MySql
# 设置mysql数据库的数据的存放目录
datadir=D:\\MySql\\data
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
[client]
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8
```

![image-20211123225913321](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123225913321.png)

配置环境变量

![image-20211123231631119](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123231631119.png)

![image-20211123231653347](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123231653347.png)

CMD执行`mysqld --initialize --console`命令。

执行过后找到A temporary password is generated for root@localhost: 这句，localhost后面就是自己的初始化密码。

![image-20211123231806228](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123231806228.png)

执行`mysqld --install`,要以管理员方式打开CMD，不然可能报错。

启动服务输入`net start mysql`

修改密码`mysql -u root -p`

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';







**cmd进入mysql:mysql -h localhost -u root  -p**

其中-h表示服务器名，localhost表示本地；-u为数据库用户名，root是mysql默认用户名；-p为密码，如果设置了密码，可直接在-p后链接输入，如：-p 123456，用户没有设置密码，直接Enter。