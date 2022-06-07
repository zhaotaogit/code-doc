
# MySql安装与测试

## 安装非常简单，只需要三个命令

1.安装服务端 

sudo apt-get install mysql-server 

2.安装客户端

sudo apt-get install mysql-client

3.安装程序编译时链接的库

sudo apt-get install libmysqlclient-dev

## 测试

### 1.检测有没有安装成功

sudo netstat -tap | grep mysql

如果出现mysql 的socket处于 listen 状态则表示安装成功

执行sudo netstat -tap | grep mysql如果提示netstat:找不到命令，说明未安装网络工具没有安装要执行：

sudo apt-get install net-tools

### 2.连接

使用命令mysql -u root -p123456进行连接

### 3.卸载
1.删除MySQL服务器：sudo apt-get remove mysql-server

2.删除随MySQL服务器自动安装的任何其他软件：sudo apt-get autoremove

3.查看从MySQL APT存储库安装的软件包列表：dpkg -l | grep mysql | grep ii

记住这几个软件包

4.卸载这些：sudo apt-get remove <<package-name>>

### 4.进入数据库

mysql -uroot -pmysql

-u+用户名，-p+用户密码

