# Python小记

## 1.生成requestment.txt文件

第一种 适用于 **单虚拟环境的情况：** ：

```shell
pip freeze > requirements.txt
```

为什么只适用于单虚拟环境？因为这种方式，会将环境中的依赖包全都加入，如果使用的全局环境，则下载的所有包都会在里面，不管是不时当前项目依赖的，如下图

当然这种情况并不是我们想要的，当我们使用的是全局环境时，可以使用第二种方法。

第二种 **(推荐)** 使用 `pipreqs` ，github地址为： https://github.com/bndr/pipreqs

```shell
# 安装
pip install pipreqs
# 在当前目录生成
pipreqs . --encoding=utf8 --force
```



注意 `--encoding=utf8` 为使用utf8编码，不然可能会报UnicodeDecodeError: 'gbk' codec can't decode byte 0xae in position 406: illegal multibyte sequence 的错误。

`--force` 强制执行，当 生成目录下的requirements.txt存在时覆盖。

使用requirements.txt安装依赖的方式：

```shell
pip install -r requirements.txt
```

