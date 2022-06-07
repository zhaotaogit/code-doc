# Flask 命令小记

## 1. form.hidden_tag()

form.hidden_tag() 模板参数将被替换为一个隐藏字段，用来是实现在配置中激活的 CSRF 保护。如果你已经激活了 CSRF，这个字段需要出现在你所有的表单中。

## 2.{{form.name(size=8)}}

{{form.name(size=8)}}要求表单生成一个 8 个字符宽度的 name 字段。



## 2. config:

```python
CSRF_ENABLED = True
SECRET_KEY = 'shi-yan-lou'
```

1. Flaks-WTF 扩展只需要两个配置。CSRF_ENABLED 配置是为了激活跨站点请求伪造保护。在大多数情况下，你需要激活该配置使得你的应用程序更安全些。

2. SECRET_KEY 配置仅仅当 CSRF 激活的时候才需要，它是用来建立一个加密的令牌，用于验证一个表单。当你编写自己的应用程序的时候，请务必设置很难被猜测到密钥。



在初始化文件(__init__.py)中，加上一行

```
app.config.from_object('Config')	
```

来读取和使用配置文件。



## 3. User.query.delete()

- User.query.delete()将User类中创建的所有数据删除

## 4.Flask-WTF添加样式

![image-20210626184113062](Linux%E5%9F%BA%E7%A1%80_imgs/image-20210626184113062.png)

