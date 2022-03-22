# Cnda创建python环境

# 1 列出当前存在的环境

可以用以下命令罗列出当前已经创建的python虚拟环境

```cpp
conda env list
```

罗列结果如下所示:

![img](https://upload-images.jianshu.io/upload_images/12538199-ff94199c7100b189.png?imageMogr2/auto-orient/strip|imageView2/2/w/680/format/webp)

左边是虚拟环境的名称，右边是其所在路径，带星号的表示是默认环境。

# 2 创建虚拟环境

可以用如下命令创建一个名字为my_py_env，python版本为3.6.2的虚拟环境。

```undefined
conda create -n my_py_env python=3.6.2
```

该方式创建的环境在默认路径下，可以通过以下方式指定路径：

```swift
conda create --prefix="D:\\my_python\\envs\\my_py_env"  python=3.6.3
```

其中"D:\my_python\envs\"是路径名，"my_py_env" 是环境名.

# 3 进入环境

```undefined
activate my_py_env
```

在windows系统cmd下通过以上命令即可进入my_py_env环境，如果在linux系统下，需要使用：

```bash
source activate my_py_env
```

# 4 退出环境

windows:

```undefined
deactivate
```

linux：

```bash
source deactivate
```

# 5 使用conda管理包

```undefined
conda install -n my_py_env package_name
conda uninstall -n my_py_env package_name
```

只需要在conda命令中通过 -n 显示指定python环境即可

# 6 删除环境

```csharp
conda remove -n my_py_env --all
```

