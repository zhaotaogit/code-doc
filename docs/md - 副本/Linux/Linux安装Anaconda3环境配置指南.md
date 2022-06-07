# Linux安装Anaconda3环境配置指南

## 1.添加jupyter环境变量

```shell
find -name jupyter		找jupyter的位置

vim /etc/profile		编辑文件

根据找到的位置,在最后一行添加,PATH后面跟的路径自行改变：
export PATH=$PATH:/root/anaconda3/bin 

source  /etc/profile/		 执行配置
```

## 2.修改配置文件

```linux
jupyter notebook --generate-config		生成配置文件

vim  /root/.jupyter/jupyter_notebook_config.py 		编辑配置文件

添加代码：
c.NotebookApp.ip = '*'		配置可以访问的ip为所有ip
c.NotebookApp.open_browser = False		配置不自动打开浏览器
c.NotebookApp.port = 8888		配置服务端口为888

jupyter notebook --allow-root&  开启服务，root用户需要加--allow-root，&代表在后台运行
```

## 3.让服务在后台运行

1. 后台运行
    在云服务器中搭建好jupyter并运行后, 发现它会占用当前终端, 于是研究了一下怎么让它在后台运行.
    1.入门级: jupyter notebook --allow-root > jupyter.log 2>&1 &
    2.进阶版: nohup jupyter notebook --allow-root > jupyter.log 2>&1 &

- 解释: 1. 用&让命令后台运行, 并把标准输出写入jupyter.log中

- nohup表示no hang up, 就是不挂起, 于是这个命令执行后即使终端退出, 也不会停止运行.

2. 终止进程

   执行上面第2条命令, 可以发现关闭终端重新打开后, 用jobs找不到jupyter这个进程了, 于是要用ps -a, 可以显示这个进程的pid.
   kill -9 pid 终止进程

