# numpy数组与矢量运算  

## numpy数组对象  

### 数组的属性  
```ndim```       返回int,表示数组维度。  
```shape```     返回tuple,表示数组的尺寸，(n,m)。   
```size```       返回int,表示数组的元素总数,n*m。
```dtype```      返回data-type,描述数组中元素类型。  
```itemsize```   返回int，表示数组的每个元素大小（以字节为单位）。   

### numpy的数据类型  
![dtype](https://pic4.zhimg.com/80/v2-87bc2518cce18166c1150bce4513aa5f_1440w.jpg)  

### 自定义数据类型  
```类型名=numpy.dtype([(字符串：'name',np.数据类型,长度),(数值：'name',np.数据类型),(···)···])```  
如果想创建自定义数据类型的数组，就要先定义异构数据类型（如pro_type），再在创建时用dtype指定数据类型（pro_type）  

### 创建数组对象  
```numpy.array(object,dtype=None,copy=True,order=None,subok=False,ndmin =0)```  
```object```:接受array，表示想要创建数组，无默认。  
```dtype```:接受data-type,表示数组所需要的数据类型，默认为保存对象所需的最小类型。  
```ndmin```:接收int，指定最小维度,默认为None。  

### 创建数组的其他方法  
一般含步长的都不包后  
```numpy.arrange(start,stop,step)```通过步长来创建等差一维数组。  
```numpy.linspace(start,stop,num)```通过元素个数来创建一维等差数组。（添加endpoint=0,可设置为不包含终止值)  
```numpy.logspace(start,stop,num)```通过元素个数来创建一维等比数组，起始值和终止值代表10的幂。（可修改参数base来调整基数）  
```numpy.zeros(shape,dtype)```            创建全0数组。   
```numpy.ones(shape,dtype)```             创建全1数组。   
```numpy.eyes(shape,dtype)``` ```numpy.identity(shape,dtype)```生成主对角线为1，其余元素全为0的数组。  
```numpy.diag(v)```                 生成对角线为v中元素的数组，其余元素为0。  
```numpy.asarray(shape,dtype)```                 将python序列转换为ndarray。  
```numpy.empty(shape,dtype)```            指定形状分配空间但不初始化。  

## numpy数组操作  
### 数组的索引和切片
一维：
```
数组名[索引（下标）]        #索引
数组名[start:stop;step]    #切片
```  
二维:
```
数组名[行索引,列索引]  
数组名[rows_start:rows_end:rows_step,cols_start:cols_end:cols_step]  
```  
高维数组的索引和切片可参考二维数组的索引和切片方法以此类推。  
数组切片可用来修改元素的值。  
数组切片时，行或列索引可以使用省略号（···），表示行或列索引*长度*与数组行或列的*维度*相同。    

整数索引:
从两个序列的对应位置取出两个整数来组成行下标和列下标。  
```
#整数索引
a=np.array([[1,2,3],[4,5,6],[7,8,9]])
b=a[(0,1,2),(0,1,0)]
print(b)           #[0,0],[1,1],[2,0]
```  

布尔值索引:  
当结果对象是布尔运算结果时，将使用布尔值索引。  
索引对象为逻辑表达式时，返回符合式子的所有元素。（一维数组）  
整数索引和布尔索引属于高级索引，只返回副本不改变原本的值。  
### 修改数组形状  