# Python数据分析方法小记：

## 一、Numpy

### 1.[numpy.clip(a, a_min, a_max, out=None)[source]](https://blog.csdn.net/qq1483661204/article/details/78150203)

其中a是一个数组，后面两个参数分别表示最小和最大值，怎么用呢，老规矩，我们看代码：

```python
import numpy as np
x = np.array([1,2,3,4,5,6,7,8,9])
np.clip(x,3,8)
```

```python
Outer[88]:array([3, 3, 3, 4, 5, 6, 7, 8, 8])
```

也就是说clip这个函数将将数组中的元素限制在a_min, a_max之间，大于a_max的就使得它等于 a_max，小于a_min,的就使得它等于a_min。

```python
x=np.array([[1,2,3,5,6,7,8,9],[1,2,3,5,6,7,8,9]])
np.clip(x,3,8)
```

```python
Out[90]:array([[3, 3, 3, 5, 6, 7, 8, 8],
       	[3, 3, 3, 5, 6, 7, 8, 8]])
```

高维数组也是一样的

### 2.np.unique()[官方文档分析以及举例](https://blog.csdn.net/weixin_43977640/article/details/109692943)