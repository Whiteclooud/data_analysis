# numpy数组与矢量运算  

## numpy数组对象  

### 视图与副本  
副本是一个数据的完整的拷贝，如果我们对副本进行修改，它不会影响到原始数据，物理内存不在同一位置。  
视图是数据的一个别称或引用，通过该别称或引用亦便可访问、操作原有数据，但原有数据不会产生拷贝。如果我们对视图进行修改，它会影响到原始数据，物理内存在同一位置。  

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
1. 一维：
```
数组名[索引（下标）]        #索引
数组名[start:stop;step]    #切片
```  
2. 二维:
```
数组名[行索引,列索引]  
数组名[rows_start:rows_end:rows_step,cols_start:cols_end:cols_step]  
```  
高维数组的索引和切片可参考二维数组的索引和切片方法以此类推。  
数组切片可用来修改元素的值。  
数组切片时，行或列索引可以使用省略号（···），表示行或列索引*长度*与数组行或列的*维度*相同。    

3. 整数索引:
从两个序列的对应位置取出两个整数来组成行下标和列下标。  
```
#整数索引
a=np.array([[1,2,3],[4,5,6],[7,8,9]])
b=a[(0,1,2),(0,1,0)]
print(b)           #[0,0],[1,1],[2,0]
```  

4. 布尔值索引:  
当结果对象是布尔运算结果时，将使用布尔值索引。  
索引对象为逻辑表达式时，返回符合式子的所有元素。（一维数组）  
整数索引和布尔索引属于高级索引，只返回副本不改变原本的值。  
### 修改数组形状  
1. 用维度属性修改:  
```arr.shape(x0,x1,x2,...,xn)```  
2. reshape()函数  (原数组不变创建一个新数组)  
```arr.reshape(x0,x1,x2,...,xn)```  
arr.reshape(3,-1)可自动计算后面的维度。       
3. resize()函数  
元素个数与之前不一样所以不能用-1。    
```arr.resize(x0,x1,x2,...,xn)```(修改原数组)
若新数组大于原来则重复之前元素。  
```np.resize(a,(new_shape))```(不改变原数组)
若新大于旧则补0。  
### 数组的展平  
按行展平，添加参数(“F”)可按列展平  
将多维数组展平成一维数组  
1. ravel()函数 (返回视图)  
```数组名.ravel()```  
2. flatten()函数 (返回副本)  
```数组名.flatten()```  
### 数组转置和轴对换  
--------------转置--------------  
1. transpose()函数   
```np.transpose(arr)```  
翻转给定数组的维度，并返回视图。  
2. ndarray.T  
```数组名.T```  
属于ndarray类，用法类似1。     
--------------轴对换--------------  
操作数组轴的索引。   
3. rollaxis()函数  
向后滚动特定的轴，直到一个特定位置。  
```numpy.rollaxis(arr,axis,start)```    
arr表示数组，axis表示要向后滚动的轴，start表示滚动到特定位置，默认为0，表示完整的滚动。 
4. swapaxes()函数  
交换数组的2个轴  
```numpy.swapaxes(arr,axis1,axis2)```   
arr表示数组，axis1表示对应第一个轴的整数，axis2表示对应第二个轴的整数。  
### 数组的连接  
1. concatenate()函数  
用于沿指定轴连接相同形状的两个或多个数组。  
```numpy.concatenate((arr1,arr2,...,arrn),axis)```  
arr1,arr2,...,arrn)表示**相同维度**的数组序列，axis表示连接的方向，默认为0。  
2. hstack()函数  
水平方向拼接  
```numpy.hstack(arrays)```  
3. vstack()函数  
竖直方向拼接  
```numpy.vstack(arrays)```  
4. stack()函数   
新数组维度+1，再沿输入的维度加入一系列数组(概念不好理解，可参考实例。)   
```numpy.stack(arrays,axis)```  
arrays表示相同形状的数组序列，axis等于几就说明在哪个**维度**上进行堆叠。  
5. stack()函数与concatenate()函数的区别  
stack函数会增加数组的维度，concatenate函数不会。  
### 数组的分割  
1. split()函数  
```numpy.split(arr,indices_or_sections,axis)```  
arr表示被分割的数组,indices_or_sections表示分割成几个大小相同的子数组，若参数为一维数组则表示分割点，arr将按照分割的来分割数组。  
2. hsplit()函数:水平方向分割  
```numpy.hsplit(arr,indices_or_sections)```  
3. vsplit()函数：竖直方向分割  
```numpy.hsplit(arr,indices_or_sections)```