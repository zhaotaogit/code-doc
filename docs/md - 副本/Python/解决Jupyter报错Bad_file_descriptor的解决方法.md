# 解决Jupyter报错:Bad file descriptor的解决方法

 jupyter 依赖的是 pyzmq==19.0.2 版本的。于是解决步骤如下：

1.卸载pyzmq：pip uninstall pyzmq
2.安装指定版本的库：pip install pyzmq==19.0.2
3.重新启动jupyter即可

