# 1.Linux

**小记**

>Linux下测试网速
>
>```python
>>curl -s https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py | python
>```

## 一、vi编辑器

### 1.1Vi编辑器的模式

* ####  插入模式：文字数据的输入，按Esc键可以回到编辑模式

* #### 编辑模式：进入Vi的默认模式，主要功能是控制光标的移动、删除字符、区段复制等。

* ####  命令模式：保存文件、退出Vi,以及其他的设置，例如查找或替换字符串等。

## 1.2 Vi编辑器模式的切换

- 编辑模式-->插入模式

  按a键：从当前光标所在位置的下一个字符开始输入

  按i键：从光标所在位置插入新输入的字符

  按o键：新增加一行，并将光标移动到下一行的开头

  注意：在编辑模式下输入命令时，如a、i、o字符并不会显示出来。

  

- 插入模式-->编辑模式

  ​	按下Esc键

  <img src="Linux%E5%9F%BA%E7%A1%80_imgs/Linux%E5%9F%BA%E7%A1%80image-20201219144839599.png"/>

- 编辑模式-->命令模式

  输入":"键即可

- 命令模式-->编辑模式

  输入命令后回车即可

  #### 编辑模式中常用命令

  >i:在光标前插入文本
  >
  >a：在光标后插入文本
  >
  >I：在当前的前端插入文本
  >
  >A：在当前行的末端插入文本
  >
  >O：在当前行前插入一行
  >
  >o：在当前行后插入一行

  #### 命令模式和编辑模式下的操作

  <img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20201219145615577.png"/>

## 二、文件操作

1. li显示目录文件  语法：ls 选项[-alF] [文件或目录]

   * -a 显示所有文件，包括隐藏文件
   * -l 使用长格式显示
   * -F 附加文件类别，符号在文件名最后

   <img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110135615077.png"/>

2. cp 复制文件 语法：cp  选项[-afp] [源文件或目录] [目的文件或目录]

   * -a 复制所有目录并包含子目录
   * -f 强制复制文件
   * -p 保留源文件的日期

   <img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110135811752.png"/>

   <img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110140404827.png"/>

3. cat 显示文件内容 语法: cat [文件名]

<img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110135855215.png"/>

1. more 分页显示文件内容 语法：more [文件名]

   * f或空格：显示下一页
   * Enter 显示下一行
   * q或Q 退出more

2. rm 删除文件 语法：rm 选项[-irf] [文件目录]

   * -i 交互方式，询问是否删除
   * -r 递归删除目录
   * -f 强制删除，不需询问

   <img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110140003294.png"/>

3. rmdir 删空目录 语法rmdir 目录名

   <img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110144648731.png"/>

4. mv 移动文件 语法:mv 文件名 目录地址

   <img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110144840955.png"/>

5. tar 解压缩文件 语法

   压缩：

   <img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110145202459.png"/>

   解压：

   ​	           <img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110145243347.png"/>

6. touch 创建文件 语法 touch 文件名.后缀

   <img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110145413167.png"/>

7.修改日志保存未知步骤

```linux
touch /var/log/test2.log 创建要保存日志的文件
pwd 查看此文件的目录
vi /etc/rsyslog.conf 修改日志系统
					### 在# Save boot messages also to boot.log
					###local7.* 行下编辑
*.*														/var/log/test2.log

systemctl restart rsyslog.service 重启日志系统
cat /var/log/test2.log  查看test2.log的文件内容

```

<img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110151224600.png"/>

<img src="Linux%E5%9F%BA%E7%A1%80_imgs/image-20210110151059479.png"/>















