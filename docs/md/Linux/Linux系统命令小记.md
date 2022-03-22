

# Linux系统命令小记

- pwd：查看当前路径

  ```shell
  [root@localhost ~]# pwd
  /root
  ```

- date：查看当前日期

  ```shell
  [root@localhost ~]# date
  2021年 09月 09日 星期四 09:46:12 CST
  ```

- ls：查看当前路径下的文件

  ```shell
  [root@localhost ~]# ls
  anaconda-ks.cfg  initial-setup-ks.cfg  公共  模板  视频  图片  文档  下载  音乐  桌面
  ```

  

- cal：日历命令

  ```shell
  [root@localhost ~]# cal
        九月 2021     
  日 一 二 三 四 五 六
            1  2  3  4
   5  6  7  8  9 10 11
  12 13 14 15 16 17 18
  19 20 21 22 23 24 25
  26 27 28 29 30
  [root@localhost ~]# cal 2021	# 显示2021年的日历
                                 2021                               
  
          一月                   二月                   三月        
  日 一 二 三 四 五 六   日 一 二 三 四 五 六   日 一 二 三 四 五 六
                  1  2       1  2  3  4  5  6       1  2  3  4  5  6
   3  4  5  6  7  8  9    7  8  9 10 11 12 13    7  8  9 10 11 12 13
  10 11 12 13 14 15 16   14 15 16 17 18 19 20   14 15 16 17 18 19 20
  17 18 19 20 21 22 23   21 22 23 24 25 26 27   21 22 23 24 25 26 27
  24 25 26 27 28 29 30   28                     28 29 30 31
  31
          四月                   五月                   六月        
  日 一 二 三 四 五 六   日 一 二 三 四 五 六   日 一 二 三 四 五 六
               1  2  3                      1          1  2  3  4  5
   4  5  6  7  8  9 10    2  3  4  5  6  7  8    6  7  8  9 10 11 12
  11 12 13 14 15 16 17    9 10 11 12 13 14 15   13 14 15 16 17 18 19
  18 19 20 21 22 23 24   16 17 18 19 20 21 22   20 21 22 23 24 25 26
  25 26 27 28 29 30      23 24 25 26 27 28 29   27 28 29 30
                         30 31
          七月                   八月                   九月        
  日 一 二 三 四 五 六   日 一 二 三 四 五 六   日 一 二 三 四 五 六
               1  2  3    1  2  3  4  5  6  7             1  2  3  4
   4  5  6  7  8  9 10    8  9 10 11 12 13 14    5  6  7  8  9 10 11
  11 12 13 14 15 16 17   15 16 17 18 19 20 21   12 13 14 15 16 17 18
  18 19 20 21 22 23 24   22 23 24 25 26 27 28   19 20 21 22 23 24 25
  25 26 27 28 29 30 31   29 30 31               26 27 28 29 30
  
          十月                  十一月                 十二月       
  日 一 二 三 四 五 六   日 一 二 三 四 五 六   日 一 二 三 四 五 六
                  1  2       1  2  3  4  5  6             1  2  3  4
   3  4  5  6  7  8  9    7  8  9 10 11 12 13    5  6  7  8  9 10 11
  10 11 12 13 14 15 16   14 15 16 17 18 19 20   12 13 14 15 16 17 18
  17 18 19 20 21 22 23   21 22 23 24 25 26 27   19 20 21 22 23 24 25
  24 25 26 27 28 29 30   28 29 30               26 27 28 29 30 31
  31
  
  
  ```

- who：列出在线用户

  ```shell
  [root@localhost ~]# who
  root     :0           2021-09-09 09:45 (:0)
  root     pts/0        2021-09-09 09:46 (:0)
  
  ```

- uname：系统信息命令

  ```shell
  [root@localhost ~]# uname
  Linux
  [root@localhost ~]# uname -r
  3.10.0-514.el7.x86_64
  [root@localhost ~]# uname -m
  x86_64
  [root@localhost ~]# uname -i
  x86_64
  [root@localhost ~]# uname -v
  #1 SMP Tue Nov 22 16:42:41 UTC 2016
  ```

- clear：清屏

- su zjiet：切换当前用户为zjiet

  ```shell
  [root@localhost ~]# su zjiet
  [zjiet@localhost root]$
  ```

- cd：进入到某个目录

  ```shell
  [zjiet@localhost home]$ cd /home/
  [zjiet@localhost home]$ pwd
  /home
  ```

- runlevel：查看当前运行级别

  | 运行级别0 | **系统停机状态，系统默认运行级别不能设为0，否则不能正常启动** |
  | --------- | :----------------------------------------------------------: |
  | 运行级别1 |     单用户工作状态，root权限，用于系统维护，禁止远程登陆     |
  | 运行级别2 |                     多用户状态(没有NFS)                      |
  | 运行级别3 |     完全的多用户状态(有NFS)，登陆后进入控制台命令行模式      |
  | 运行级别4 |                       系统未使用，保留                       |
  | 运行级别5 |               X11控制台，登陆后进入图形GUI模式               |
  | 运行级别6 | 系统正常关闭并重启，默认运行级别不能设为6，否则不能正常启动  |

  ```shell
  [zjiet@localhost home]$ runlevel 
  N 5
  ```

- init 3：切换运行级别为3

  ```shell
  init 3
  ```

  运行之后，如果当前是图形界面就会切换到纯文本界面。

- shutdown [选项] [参数]：关机/重启

  选项：-h(关机) -r(重启)

  参数：mm:ss(某个时刻);+n(n分钟后)

  ```shell
  [zjiet@localhost home]$ shutdown -h 10:00	# 10点关机
  [zjiet@localhost home]$ shutdown -h +5	# 5分钟后关机
  [zjiet@localhost home]$ shutdown -h now	# 立即关机
  [zjiet@localhost home]$ shutdown -r now # 立即重启
  ```

- man：在线帮助命令

  ```shell
  [zjiet@localhost home]$ man who # 查看who的帮助命令
  ```

- history：查看用户在命令行操作中输入过的所有命令

  用户在命令行操作中输入的所有命令，系统都会将其自动记录到用户宿主机主目录下的一个文件中(~/.bash_history),记录的多少由用户环境变量中的HISTSIZE决定。

  ```shell
  [root@localhost ~]# history 
      1  ifconfig
      2  shutdown now
      3  ifconfig
      4  pwd
      5  date
      6  cal 2021
      7  cal
      8  who
  [root@localhost ~]# !5	# 执行历史中第5条语句
  date
  2021年 09月 09日 星期四 11:08:34 CST
  ```

- wc：统计命令

  wc命令用来统计给定文件的行数、字数和字符数

  格式为：

  ​	wc [ -lw] [ -c] 文件名

  ​	l为统计行数

  ​	w为统计字数

  ​	c为统计字节数

  ```shell
  [root@localhost ~]# vi helloworld.py
  [root@localhost ~]# cat helloworld.py 
  print('Hello World!')
  [root@localhost ~]# wc helloworld.py 
   1  2 22 helloworld.py
  ```

  

- Shell的重定向:

  "\>" 将输入的信息直接写入，">>"将输入的信息以追加的方式写入:

  ```shell
  [root@localhost ~]# ls
  anaconda-ks.cfg  initial-setup-ks.cfg  公共  模板  视频  图片  文档  下载  音乐  桌面
  [root@localhost ~]# ls >test
  [root@localhost ~]# cat test 
  anaconda-ks.cfg
  initial-setup-ks.cfg
  test
  公共
  模板
  视频
  图片
  文档
  下载
  音乐
  桌面
  [root@localhost ~]# cal >> test
  [root@localhost ~]# cat test 
  anaconda-ks.cfg
  initial-setup-ks.cfg
  test
  公共
  模板
  视频
  图片
  文档
  下载
  音乐
  桌面
        九月 2021     
  日 一 二 三 四 五 六
            1  2  3  4
   5  6  7  8  9 10 11
  12 13 14 15 16 17 18
  19 20 21 22 23 24 25
  26 27 28 29 30
  
  [root@localhost ~]#
  ```

- Shell的管道操作

  管道线"|"可以将多个简单的命令集合在一起，用以完成较复杂的功能。管道先"|"前面命令的输出是管道线"|"的输入。格式为：

  ```shell
  命令1 | 命令2 | 命令3| ··· | 命令n
  ```

  例：

  ```shell
  [root@localhost ~]# cal
        九月 2021     
  日 一 二 三 四 五 六
            1  2  3  4
   5  6  7  8  9 10 11
  12 13 14 15 16 17 18
  19 20 21 22 23 24 25
  26 27 28 29 30
  
  [root@localhost ~]# cal | wc
        8      39     151
  ```

  

