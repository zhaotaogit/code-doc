# Python-一些命令笔记-持续更新

> 生成requments文件:
>
> pip freeze > requirements.txt

## 1.[python的u,r,b分别什么意思？](https://www.cnblogs.com/young233/p/11195577.html)

我们经常在python当中看到以下内容：

```python
print(u'hi\thi\thi')
print(b'hi\thi\thi')
print(r'hi\thi\thi')
```

在其他语言里没见过类似的，所以特此记录：

### u: 表示unicode字符串，默认模式，里边的特殊字符会被识别。

```python
print(u'hi\thi\thi')
```

执行之后：
**hi hi hi**

### b: 表示二进制字符串，括号内的内容原样输出。

```python
print(b'hi\thi\thi')
```

执行之后：
**b'hi\thi\thi'**

### r：不转义字符串，要输出的内容原样输出。

```python
print(r'hi\thi\thi')
```

执行之后：
**hi\thi\thi**

解决编码问题：

在python2中，默认的编码格式是ascll编码，有中文字符必须加u,为了解决这个问题，可以在代码中添加下面的代码

```python
# 解决编码问题
import sys
reload(sys)
sys.setdefaultencoding("utf-8")
```

## 2.Pandas时间序列——date_range方法

- ### 功能

  date_range()方法主要用于生成一系列特定的时间，我们可以自己设定开始、结束、周期数、时间间隔、时区等等。

  ### 语法

  ```python
  import pandas
  
  pandas.date_range(start=None, end=None, periods=None, freq='D', tz=None, normalize=False, name=None, closed=None, **kwargs)
  ```

  ### 参数说明

  - start、end

  开始时间、结束时间，可以是str格式，也可以是datetime对象或None。

  - periods

  生成的周期数，可以是整数或None。

  ```python
  In [54]: pd.date_range(start='1/1/2018', end='1/08/2018')
  Out[54]:
  DatetimeIndex(['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04',
                 '2018-01-05', '2018-01-06', '2018-01-07', '2018-01-08'],
                dtype='datetime64[ns]', freq='D')
   
  In [55]: pd.date_range(start='1/1/2018', periods=8)
  Out[55]:
  DatetimeIndex(['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04',
                 '2018-01-05', '2018-01-06', '2018-01-07', '2018-01-08'],
                dtype='datetime64[ns]', freq='D')
   
  In [56]: pd.date_range(end='1/1/2018', periods=8)
  Out[56]:
  DatetimeIndex(['2017-12-25', '2017-12-26', '2017-12-27', '2017-12-28',
                 '2017-12-29', '2017-12-30', '2017-12-31', '2018-01-01'],
                dtype='datetime64[ns]', freq='D')
   
  In [57]: pd.date_range(start='2018-04-24', end='2018-04-27', periods=3)
  Out[57]:
  DatetimeIndex(['2018-04-24 00:00:00', '2018-04-25 12:00:00',
                 '2018-04-27 00:00:00'],
                dtype='datetime64[ns]', freq=None)
   
  In [58]: pd.date_range(start='2018-04-24', end='2018-04-27', periods=4)
  Out[58]: DatetimeIndex(['2018-04-24', '2018-04-25', '2018-04-26', '2018-04-27'], dtype='datetime64[ns]', freq=None)
   
  In [59]: pd.date_range(start='2018-04-24', end='2018-04-27', periods=2)
  Out[59]: DatetimeIndex(['2018-04-24', '2018-04-27'], dtype='datetime64[ns]', freq=None)
   
  In [60]: pd.date_range(start='2018-04-24', end='2018-04-27', periods=5)
  Out[60]:
  DatetimeIndex(['2018-04-24 00:00:00', '2018-04-24 18:00:00',
                 '2018-04-25 12:00:00', '2018-04-26 06:00:00',
                 '2018-04-27 00:00:00'],
                dtype='datetime64[ns]', freq=None)
  ```

  - freq

  日期偏移量，即相邻时间的间隔，可以是str形式或DateOffset，默认为’D‘。

  ```python
  In [66]: pd.date_range(start='1/1/2018', periods=5, freq='5D')
  Out[66]:
  DatetimeIndex(['2018-01-01', '2018-01-06', '2018-01-11', '2018-01-16',
                 '2018-01-21'],
                dtype='datetime64[ns]', freq='5D')
   
  In [67]: pd.date_range(start='1/1/2018', periods=5, freq='M')
  Out[67]:
  DatetimeIndex(['2018-01-31', '2018-02-28', '2018-03-31', '2018-04-30',
                 '2018-05-31'],
                dtype='datetime64[ns]', freq='M')
   
  In [68]: pd.date_range(start='1/1/2018', periods=5, freq='H')
  Out[68]:
  DatetimeIndex(['2018-01-01 00:00:00', '2018-01-01 01:00:00',
                 '2018-01-01 02:00:00', '2018-01-01 03:00:00',
                 '2018-01-01 04:00:00'],
                dtype='datetime64[ns]', freq='H')
   
  In [69]: pd.date_range(start='1/1/2018', periods=5, freq=pd.offsets.MonthEnd(3))
  Out[69]:
  DatetimeIndex(['2018-01-31', '2018-04-30', '2018-07-31', '2018-10-31',
                 '2019-01-31'],
                dtype='datetime64[ns]', freq='3M')
  ```

  - tz

  设定时区，可以为str格式或tz fo。

  ```python
  In [70]: pd.date_range(start='1/1/2018', periods=5, tz='Asia/Tokyo')
  Out[70]:
  DatetimeIndex(['2018-01-01 00:00:00+09:00', '2018-01-02 00:00:00+09:00',
                 '2018-01-03 00:00:00+09:00', '2018-01-04 00:00:00+09:00',
                 '2018-01-05 00:00:00+09:00'],
                dtype='datetime64[ns, Asia/Tokyo]', freq='D')
   
  In [71]: pd.date_range(start='1/1/2018', periods=5, tz='Asia/Shanghai')
  Out[71]:
  DatetimeIndex(['2018-01-01 00:00:00+08:00', '2018-01-02 00:00:00+08:00',
                 '2018-01-03 00:00:00+08:00', '2018-01-04 00:00:00+08:00',
                 '2018-01-05 00:00:00+08:00'],
                dtype='datetime64[ns, Asia/Shanghai]', freq='D')
  ```

  - normalize

  布尔值，默认为False，若参数为True表示将start、end参数值正则化到午夜时间戳；

  ```python
  In [83]: pd.date_range(start='1/1/2018 14:00:00', periods=5,normalize=False)
  Out[83]:
  DatetimeIndex(['2018-01-01 14:00:00', '2018-01-02 14:00:00',
                 '2018-01-03 14:00:00', '2018-01-04 14:00:00',
                 '2018-01-05 14:00:00'],
                dtype='datetime64[ns]', freq='D')
   
  In [84]: pd.date_range(start='1/1/2018 14:00:00', periods=5,normalize=True)
  Out[84]:
  DatetimeIndex(['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04',
                 '2018-01-05'],
                dtype='datetime64[ns]', freq='D')
  ```

  - name

  生成时间索引对象的名称，取值为str g或None；

  ```python
  In [79]: pd.date_range(start='2017-01-01', end='2017-01-04', closed=None,freq='2D',name='xiaowoniu')
  Out[79]: DatetimeIndex(['2017-01-01', '2017-01-03'], dtype='datetime64[ns]', name=u'xiaowoniu', freq='2D')
  ```

  - closed

  若closed=’left’表示在返回的结果基础上，再取左闭右开的结果，若closed=’right’表示在返回的结果基础上，再取左开右闭的结果。当freq参数不为‘D’时，始终去掉的是为‘D‘时最左或最有的日期。

  ```python
  In [72]: pd.date_range(start='2017-01-01', end='2017-01-04', closed=None)
  Out[72]: DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03', '2017-01-04'], dtype='datetime64[ns]', freq='D')
   
  In [73]: pd.date_range(start='2017-01-01', end='2017-01-04', closed='left')
  Out[73]: DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03'], dtype='datetime64[ns]', freq='D')
   
  In [74]: pd.date_range(start='2017-01-01', end='2017-01-04', closed='right')
  Out[74]: DatetimeIndex(['2017-01-02', '2017-01-03', '2017-01-04'], dtype='datetime64[ns]', freq='D')
   
  In [75]: pd.date_range(start='2017-01-01', end='2017-01-04', closed='right',freq='2D')
  Out[75]: DatetimeIndex(['2017-01-03'], dtype='datetime64[ns]', freq='2D')
   
  In [76]: pd.date_range(start='2017-01-01', end='2017-01-04', closed='left',freq='2D')
  Out[76]: DatetimeIndex(['2017-01-01', '2017-01-03'], dtype='datetime64[ns]', freq='2D')
   
  In [77]: pd.date_range(start='2017-01-01', end='2017-01-04', closed=None,freq='2D')
  Out[77]: DatetimeIndex(['2017-01-01', '2017-01-03'], dtype='datetime64[ns]', freq='2D')
  ```


# 3.Pandas中常用操作

###### 1、创建一个空的DataFrame



```undefined
a = pd.DataFrame()
```

###### 2、txt、csv、excel、数据库 数据读取



```python
1、读取txt文件
【方法一】
df = pd.read_table("F:/datafrog/2-PYTHON/CDNOW_master.txt",names = ['user_id','order_dt','order_products','order_amount'],sep = '\s+')
【方法二】
columns = ['user_id','order_dt','order_products','order_amount']
df = pd.read_table("CDNOW_master.txt",names = columns,sep = '\s+')

#因为原始数据不包含表头，所以需要赋予"names"。字符串是空格分割，用"\s+"表示匹配任意空白符。

2、读取CSV文件
df = pd.read_csv("F:/datafrog/2-PYTHON/链家二手房.csv",sep = ',',engine = 'python')

3、读取excel文件
data = pd.read_excel("F:/datafrog/201708收银.xlsx")

4、数据库读取（MYSQL）
#导入模块
from sqlalchemy import create_engine
import pymysql
pymysql.install_as_MySQLdb()   # 为了兼容mysqldb
#创建连接
engine = create_engine('mysql://用户名:密码@IP地址:端口/数据库?charset=gbk')
conn = engine.connect() 
#读取数据
data1 = pd.read_sql_query('select * from data', con=conn)
print(data1.head())
```

[参考文章：Python之Pandas知识点，详细参数讲解可看此文章](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.cnblogs.com%2FWoLykos%2Fp%2F9349581.html)

###### 3、数据写出。如将数据导入数据库，或导出为excel文件



```python
1、将数据写出为csv
import pandas as pd
data.to_csv('数据储存位置',index =  是否导出索引)
#data.to_csv('data.csv',index = False)

2、将数据写出为excel
data.to_excel('数据储存位置',index=是否导出索引)
#data.to_excel('data.xlsx',index=False)

3、将数据写入数据库
#不用在数据库中建表，在导入过程中会自动在数据库中建表
from sqlalchemy import create_engine #导入模块
engine =create_engine('mysql+pymysql://root:root@127.0.0.1/data?charset=utf8', encoding='utf-8', echo=True)#创建数据库链接
conn = engine.connect()
create_merchant.to_sql('HZ_CREATE_CUSTOMER',con=datafrog,if_exists='append',index=False)
#data.to_sql('data',con = conn)
```

[参考文章：Python之Pandas知识点，详细参数讲解可看此文章。](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.cnblogs.com%2FWoLykos%2Fp%2F9349581.html)

###### 4、排序



```csharp
1、按照1个字段排序
df.sort_values(by = 'quantity',ascending=False)  # False降序
#ascending = False,降序
#ascending = True,升序

2、按照2个及以上字段排序
df.sort_values(by = ['quantity','month'],ascending=False) # False降序
```

###### 5、计算某列有多少个不同的值,类似sql中distinct



```bash
1、计算每个不同值有在该列中有多少重复值
【方法一】
chipo['choice_description'].value_counts()
【方法二】
df["User_ID"].drop_duplicates(keep='first').count()

2、计算某列有多少个不同的重复值
df['User_ID'].nunique()
```

![img](https:////upload-images.jianshu.io/upload_images/2693156-5c114c1fa96ba6a0.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

###### 6、分组函数（类似sql中group by)



```bash
1、按照1个字段分组
df.groupby('key1').order.mean() 

2、按照2个字段分组
df.groupby(['month','chty']).order.mean() 
```

###### 7、截取某字段中前5个字符（注意：前闭后开）



```rust
df[" 地址"] = df["地址"].str[0:5]
```

###### 8、删除floor字段中的'层'字，其它内容保留。



```bash
df['floor'] = df['floor'].str.extract('(\d+)层')
```

###### 9、agg函数—常与groupby函数连用。如：每个大陆对饮品消耗的最小值、平均值、最大值



```csharp
chipo.groupby('order_id').agg({'item_price_01':'sum'}).item_price_01.mean()

2、每个大陆对饮品消耗的最小值、平均值、最大值
drinks.groupby('continent')['spirit_servings'].agg(['min','mean','max'])

案例：
df.groupby('area_level').agg({'面积':'sum','面积':'mean','单价（平方米）':'mean','价格（W）':'mean'})

类似SQL中：
Select userid,max(monitortime),avg(prince)  from student group by userid
```

###### 10、在字段中对数据进行模糊匹配，类似sql中like



```rust
1、筛选某字段以G开头的数据
euro12[euro12.Team.str.startswith('G')]

2、筛选某字段以G结束的数据
euro12['Team'].str.endwith('G')
```

###### 11、数据筛选，类似sql中like



```bash
1、选取队名为'England','Italy','Russia' 的所有数据
Euro12[euro12['Team'].isin(['England','Italy','Russia'])]

2、筛选不是欧洲队的所有数据
Euro12[~euro12['Team'] == '欧洲队')]

3、筛选小区名称有"阳光"二字的所有小区数据
【方法一】
df1[df1['小区名称'].str.contains('阳光')]  
【方法二】
df[df["小区名称"].str.contains(r'.*?阳光.*')]
【方法三】
df[df["小区名称"].isin(["阳光"])]
#类似sql中   select   *  from   df where  小区名称  like '%阳光%’

3、筛选小区名称有"阳光"或者'雅居’二字的所有小区数据
df1[df1['小区名称'].str.contains('阳光|雅居')]  
#类似where 小区名称 like '%阳光%’or 小区名称 like '%雅居%’

4、选取以字母G开头的球队数据
euro12[euro12.Team.str.startswith('G')]
```

###### 12、多个数据条件筛选，类似sql中and 、or



```bash
1、筛选时间大于2019-3-12并且小于2019-12-12所有数据
df[(df.create_date>= '2019-3-12') & (df.create_date<= '2019-12-12')]


2、筛选时间不在2019-3-12至2019-12-12的数据
df[(df.create_date>= '2019-3-12') | (df.create_date<= '2019-12-12')]
```

###### 13、pivot_table类似excel中数据透视表



```bash
【案例1】
hz_customer_order.pivot_table(index = 'product_name',
                              columns='create_year_month',
                    values = 'order_num',
                    aggfunc = 'sum')

【案例2】
df.pivot_table(index = 'user_id',
                    values = ['order_products','order_amount','order_dt'],
                    aggfunc = {'order_products':'max','order_amount':'sum','order_products':'sum'})

【案例3】
df.pivot_table(index = 'user_id',
              columns = 'month',
              values = 'order_dt',
              aggfunc  = 'count')
```

###### 14、合并两个dateframe，类似sql中union all 、left join



```csharp
1、合并两张表行的维度合并，类似sql中union all
#在合并两张表的时，索引一定要相同，或者会报错
pd.concat([data1,data2],axis = 0)

2、合并两张表，按照列的维度合并，类似sql中left join
#在合并两张表的时，索引一定要相同，或者会报错
pd.concat([data1,data2],axis = 1)

3、两张表按照某字段合并：
#类似sql中left join
pd.merge(all_data, data3, on='subject_id')

4、两张表根据某2个字段合并：
#类似sql中left join
pd.merge(all_data, data3, on=['subject_id','class'])
```

###### 15、DataFrame删除某列



```php
1、删除某列,不改变数据集，返回一个新的DataFrame
df_gender_purchase.drop(labels='消费金额1',axis=1) 

2、会改变原始数据集
df_gender_purchase.drop(labels = '消费金额1',axis = 1,inplace = True)  

df_gender_purchase = df_gender_purchase.drop(labels='消费金额1',axis=1)   

//删除total列
del crime['Total']
```

###### 16、填充DataFrame中的空值



```python
1、整张表的空值用0填充
df2.floor.fillna(0)

2、使用price平均值对空值进行填充
df['price'].fillna(df['price'].mean())  

df.isnull()  #检查数据空值
df['price'].isnull()  #检查特定列空值
```

###### 17、对df中的某个字段进行分割，一个字段拆分为多个字段



```php
df['floor'].str.split('/',expand = True)]
```

###### 18、对df中的某个字段分层。类似sql中case when



```bash
【案例1】
#方法1
df.loc[(df['面积'] >= 0) & (df['面积'] < 50),'area_level'] = '极小户型'
df.loc[(df['面积'] >= 50) & (df['面积'] < 100),'area_level'] = '小户型'
df.loc[(df['面积'] >= 100) & (df['面积'] < 150),'area_level'] = '中等户型'
df.loc[(df['面积'] >= 150) & (df['面积'] < 200),'area_level'] = '大户型'
df.loc[(df['面积'] >= 200),'area_level'] = '巨大户型'
#方法2
df['area_level'] = pd.cut(df['面积'], [0,50,100,150,200], labels=["极小户型","小户型","中等户型","大户型","巨大户型"])

【案例2】
sales_customer_order_11['age_level'] = pd.cut(sales_customer_order_11['customer_age'], [30,35,40,45,50,55,60,65], labels=["30-34","35-39","40-44","45-49","50-54","55-59","60-64"])
```

###### 19、数据提取。如选取某个字段，某行



```bash
df['股票代码']    # 根据列名称来选取，读取的数据是Series类型
df[['股票代码', '收盘价']]   # 同时选取多列，需要两个括号，读取的数据是DataFrame类型

df.iloc[0]   # 以index选取某一行，读取的数据是Series类型
df.iloc[1:3]   # 选取第一行到第二行的数据，读取的数据是DataFrame类型
df.iloc[:, 1:3] # 选取所有行，第第一列到第二列的数据
```

###### 20、统计函数(平均值，最大值，最小值，标准差，中位数等）



```css
【方法一】
df.describe()

【方法二】
df['收盘价'].max()  # 最大值
df['收盘价'].min()  # 最小值
df['收盘价'].std()  # 标准差
df['收盘价'].count()  # 非空的数据的数量
df['收盘价'].median()  # 中位数
df['收盘价'].quantile(0.25)  # 25%分位数
df['收盘价'].mean()  # 求一整列的均值，返回一个数。会自动排除空值。
```

###### 21、对某列累加求和cumsum()



```csharp
df['order'].cumsum()

【案例】
用户累计消费金额的占比（百分之多少的用户占了百分之多少的消费额）
group_user.sum().sort_values(by = 'order_amount',ascending = True).cumsum()/2500315.6300000004

#方法一：
user_cumsum = (group_user.sum().sort_values('order_amount').cumsum()/2500315.63
#方法二：
user_cumsum = group_user.sum().sort_values('order_amount').apply(lambda x: x.cumsum() / x.sum())
user_cumsum
#axis = 0按列计算
#cumsum滚动累加求和
```

###### 22、对日期的处理。(如时间数据类型转换，时间加减）



```python
1、字符串转时间
#注意时间的格式
df_dw_customer_order['create_date'] = pd.to_datetime(df_dw_customer_order.create_date,format = '%Y-%m-%d')  

2、将年转化为时间格式的年
pd.to_datetime(crime.Year, format='%Y')

pd.to_datetime('2017/09/24',format='%Y-%m-%d')  
//Timestamp('2017-09-24 00:00:00')

pd.to_datetime('2017/09/24 11:38:30',format='%Y-%m-%d %H:%M:%S')
//Timestamp('2017-09-24 11:38:30')

pd.to_datetime('2017/09/24 11:38:30',format='%Y/%m/%d %H:%M:%S')
//Timestamp('2017-09-24 11:38:30')

2、时间转化为字符串
hz_customer_order['create_date'].apply(lambda x:x.strftime('%Y-%m-%d'))


3、计算两个时间相差的天数，并把结果转为整数
(rfm.order_dt.max()-rfm.order_dt)/np.timedelta64(1,'D')

4、pandas当前时间减一天
datetime.date.today() + datetime.timedelta(days=-1)
```

###### 23、对数据进行去重drop_duplicates()



```php
#df3中有重复的行数，我们如何将重复的行数去除？
df3.drop_duplicates(
    subset=['收盘价', '交易日期'],  # subset参数用来指定根据哪类类数据来判断是否重复。若不指定，则用全部列的数据来判断是否重复
    keep='first',  # 在去除重复值的时候，我们是保留上面一行还是下面一行？first保留上面一行，last保留下面一行，False就是一行都不保留
    inplace=True

【案例一】
df['city'].drop_duplicates(keep='last')  #删除先出现的重复值
df['city'].drop_duplicates()   #删除后出现的重复值
```

###### 24、字典转化为DataFrame



```rust
【案例一】
pd.DataFrame({'a':'int','b':'str'}）

【案例二】
将[{'a':'int','b':'str'},{'a':'cat','b':'dog'}]变成datafram
df = pd.DataFrame(newlist)
```

###### 25、修改字段名



```php
df1.rename(columns = {"name":"姓名","id":"序号"}，inplace = True)
```

###### 26、数据类型转换



```csharp
1、字符串转时间
#注意时间的格式
df_dw_customer_order['create_date'] = pd.to_datetime(df_dw_customer_order.create_date,format = '%Y-%m-%d')

2、时间转化为字符串
hz_customer_order['create_date'].apply(lambda x:x.strftime('%Y-%m-%d'))

df_dw_customer_order['order'].astype(int)#将order转化为整数
df_dw_customer_order['order'].astype(str)#将order转化为字符串格式
```

###### 27、计算环比pct_change()



```go
【案例一】
product_name_list = list(gather_customer_order_month_10_11.product_name.drop_duplicates())
order_top_x = pd.Series([])
for i in product_name_list:
    #print(i)
    a=gather_customer_order_month_10_11.loc[gather_customer_order_month_10_11['product_name']==i]['order_month_product'].pct_change().fillna(0)
    #b=gather_customer_order_month_10_11.loc[gather_customer_order_month_10_11['product_name']==i]['sum_amount'].pct_change().fillna(0)
    order_top_x=order_top_x.append(a) 
```

###### 28、数据转置行变成列。df.T



```python
df.T
```

###### 29、查看数据常用操作。如多少行多少列、列字段及数据类型等



```python
df.shape  # 数据维度(行列)
df.shape[0]  # 数据行数
df.columns  #查看列名称
df.index # 查看索引
df.info()  #数据表信息：数据维度、列名称、数据格式和所占空间等信息
df.dtypes  #查看数据表各列格式
df['B'].dtype  #查看单列格式
df['name'].unique  #查看name中的唯一值
df.head(3)  # 看前3行的数据
df.tail(3)  # 看最后3行的数据
df.describe()  # 描述函数，最大值最小值中位数等
```

