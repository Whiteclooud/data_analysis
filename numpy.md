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
### 数组转换  
1. 数组转换成列表  
```数组名.tolist()```  
2. 转换数组数据类型  
```数组名.astype(numpy.数据类型)```  
### 添加、删除数组元素  
1. append()函数  
在数组的末尾添加元素，该函数会返回一个新数组，原数组不变。  
```numpy.append(arr,values,axis)```  
arr表示输入的数组,values表示向arr数组添加的元素,values数组列维度与arr列维度相同。  
values可以是单元素也可以是任意数组。  
axis表示添加的方向，若未提供axis，则在添加操作前数组会被展开。  
2. insert()函数  
在给定索引前，沿给定轴在数组中插入值，该函数会返回一个新数组，原数组不变。  
```numpy.insert(arr,obj,values,axis)```  
arr表示数组，obj表示**在其之前**插入值的索引  
若未传递axis参数，在插入前数组会被展开  
若传递了axis参数，会以广播值数组来匹配数组  
3. delete()函数  
与insert类似  
从数组中删除还可用切片表示元素范围值。  
```numpy.delete(arr,obj,axis)```  
```np.s_[::]```  

## numpy数组的矢量运算和通用函数  
### 数组的运算  
1. 相同形状数组的运算  
两个数组中索引相同的元素进行运算  
```
#2个相同形状数组arr_a,arr_b
arr_c1 = arr_a + arr_b   #加  
arr_c2 = arr_a - arr_b   #减  
arr_c3 = arr_a * arr_b   #乘  
arr_c4 = arr_a / arr_b   #除  
arr_c5 = -arr_a          #取反  
arr_c6 = arr_a**2        #平方  
arr_c7 = arr_a^2         #按位异或  
```  
2. 不同形状的数组运算  
低维数组自动将维度扩充到与高维度一致，然后再逐个元素运算。（广播机制）  
3. 数组和标量间的运算  
将数组的每个元素都与标量运算  
### 通用函数（ufunc）  
针对ndarray数组对象执行元素级运算的函数，并返回新的数组。 
![聚合函数](https://s3.ananas.chaoxing.com/doc/75/8a/0d/a71f769ff759c52c6d18f745041aee22/thumb/45.png) 
### 数组计算的四条规则  
1. 多维数组之间进行运算首先检查```shape```是否匹配  
2. 数字运算符（+—*/exp,log等）是作用于每个元素  
3. sum、mean、max、std、等聚合函数（axis = 0 : 横向；axis = 1 ：纵向）  若未指定axis,则作用于整个数组（对象是所有元素）。
4. 若数组中有nan值参与运算：通常结果是nan，若非要计算可以采用nan安全版本。  
## Numpy矩阵创建、计算及操作  
矩阵的特有属性：  
.T：返回自身的转置。  
.H:返回自身的共轭矩阵。
.I：返回自身的逆矩阵。  
.A：返回自身数据的二维数组的一个视图。  
### 矩阵的创建  
1. 使用字符串创建矩阵  
在```mat()```函数中输入一个MATLAB风格的字符串，该字符串以空格分隔列，以分号分隔行。  
例如```numpy.mat('1 2 3;4 5 6;7 8 9')```  
2. 使用嵌套序列创建矩阵  
在```mat()```函数中输入嵌套序列。  
例如```numpy.mat([[2,4,6,8],[1.0,3,5,7.0]])```    
3. 使用一个数组创建矩阵(对矩阵的修改会影响数组)   
在```mat()```函数中输入数组。  
例如```numpy.mat(numpy.arange(9).reshape(3,3))```    
4. 使用matrix()函数创造矩阵  
将字符串，嵌套序列，数组和matrix转换成矩阵。  
```matrix(data,dtype=None,copy=True)```  
data是指输入的用于转换为矩阵的数据。  
如果dtype是None，则数据类型由data的内容决定。  
5. 使用bmat()函数创建矩阵  
小矩阵合成大矩阵。  
```bmat(obj,ldict=None,gdict=None)```  
obj为matrix;  
ldict和gdict为None。  
### 矩阵的计算及操作  
矩阵的计算是对每个元素进行的。  
加，减，除时只有相同行列的矩阵才能运算。  
矢量积需要一个的行等于另一个的列。  
## 随机数的生成  
```numpy.random```模块  
1. 使用random()函数  
生成一个（d0,d1,...,dn）维的数组，数组的元素取自 **[0,1)内均匀分布的随机数**,若无参数则生成一个数。  
```numpy.random.rand(d0,d1,...,dn)```  
2. randn()函数  
生成一个（d0,d1,...,dn）维的数组,数组的元素是 **标准正态分布**随机数。若无参数，则生成一个数。  
```numpy.random.randn(d0,d1,...,dn)```
3. randint()函数  
该函的作用是生成指定范围[low,high)的随机数,若没输入high则取区间为[0,low)。  
```numpy.random.randint(low,high,size,dtype)```    
4. random()函数  
产生一个[0.0,1.0)之间的浮点数,但数组的元素不包括1。size表示生成元素个数，若没有参数则生成一个数。  
```numpy.random.random(size=None)```  
5. random模块其他随机生成函数  
![random](https://s3.ananas.chaoxing.com/doc/75/8a/0d/a71f769ff759c52c6d18f745041aee22/thumb/54.png)  

# 用Numpy进行简单的统计分析  
## 文件的读写操作  
### 使用Numpy读写文本文件  
1. 将**一维或二维**数组写入TXT文件或CSV格式文件  
```numpy.savetxt(fname,array,fmt = '%.18e',delimiter = None,newline = '\n',header = '',footer = '',comments = '#',encoding = None)```   
fname:文件名(记得加后缀名)。  
array:需要存的数组(一维或二维)  
fmt:写入文件的格式，例如%d,%f。(默认为%.18e)  
delimiter:分隔符，默认是空格。  
newline:换行符。  
header:在文件开头写入的字符串。  
footer:在文件末尾写入的字符串。  
comments:为添加到页眉和页脚的字符串标记注释符，默认为#。  
encoding:设置输出文件的编码。
2. 读取TXT文件和CSV格式文件  
```numpy.loadtxt(fname,dtype = <数据类型>,comments = '#',delimiter = None,converters = None,skiprows = 0,usecols = None,unpack = False,ndmin = 0,encoding = 'bytes')```  
fname:被读取的文件名(相对路径或绝对路径)。  
dtype:数据类型。  
comments:注释符，默认为#。  
delimiter:分隔符，默认为空格。  
converters:将某一列数据经过**函数预处理**后再读取。  
skiprows:选择跳过的行数。  
usecols:指定需要读取的列。  
unpack:默认为'False'，将数据逐行输出。当设置为'True'时，数据将逐列输出。  
ndmin:维度。  
encoding:编码方式，默认为'bytes'。    
###  使用Numpy读写二进制格式文件  
存储时可省扩展名，读取时不行。  
1. 使用save()或savez()函数写二进制格式文件  
```numpy.save(file,array)```.npy  
```numpy.savez(file,array1,array2...)```(多个数组保存到一个文件).npz  
2. 使用load()函数读取二进制格式文件  
```numpy.load(file)```  
### 使用Numpy读写多维数据文件  
1. 使用tofile()函数写入多维数据文件。  
```数组名.tofile(fid,sep = '',format = '%s')```  
fid:文件、字符串。  
sep:数据分割，默认为空格。  
format:写入数据的格式。  
2. 使用fromfile()函数读取多维数据文件  
```numpy.fromfile(file,dtype = 'float',count = -1,sep = '')```  
fid:文件、字符串。  
dtype:读取的数据类型。  
count:读取元素个数，-1表示读取整个文件。  
sep:数据分割，默认为空格。  
## Numpy常用统计函数  
1. 求最大值和最小值的函数（对大型数组而言，优于max和min函数）  
amax()和amin()返回一个数组的最大和最小值，或是沿数轴返回数组的最大和最小值。  
nanmax()和nanmin()函数用于返回忽略任何NaN的数组的最大值和最小值或者沿沿轴返回忽略NaN的最大值和最小值。  
```numpy.amax(a,[axis=None[,out=None[,keepdims=False]]])```  
a:输入数据。  
axis:轴向。  
out:替代输出数组，用于放置结果，默认为None。  
keepdims:默认为False，输出行维度为1；若为True，输出列维度为1。  
2. 求沿轴方向的取值范围  
ptp()函数能返回沿某轴方向上的最大值与最小值的插值，即maximun-minimum的值形成的数组。  
```numpy.ptp(a,[axis=None[,out=None]])```  
a:输入数据。  
axis:沿指定某个轴来计算差值。  
out:替代输出数组，用于放置结果，默认为None。  
3. 求百分位数  
percentile()和nanpercentile()函数可以沿某轴方向计算数组中第q数值的百分位数。  
```percentile(a,q[,axis,out,...])```  
a:输入数据。  
q:[0,100]范围的浮点数。  
axis:沿指定轴向计算百分位数。  
4. 求中位数  
median()和nanmean()函数可以沿某轴(axis)方向计算数组中的中位数。  
```numpy.median(a[,axis,out,overwrite_input,keepdims])```  
a:输入数据。  
axis:沿某个轴来计算中位数。  
5. 求和与加权平均值  
sum()计算数组或沿轴向计算数组相关元素之和：  
```sum(a[,axis=None])```  
average()函数是沿某轴（axis）方向计算数组中相关元素的加权平均值(权值为1时就是计算平均数)。  
```average(a[,axis=None,weights=None])```  
weights:权重。  
6. 算术平均数  
mean()和nanmean()可以计算数组或沿轴方向的算术平均数。  
```mean(a[,axis=None])```  
7. 标准差  
std()和nanstd()  
```numpy.std(a[,axis=None])```  
8. 方差  
方差是元素与元素平均数差的平方的平均数mean(abs(x-x.mean())**2)。  
var()和nanvar()  
```numpy.var(a[,axis=None,dtype=None])```  
dtype:数据类型。  
## 使用Numpy函数进行统计分析  
### Numpy的排序函数  
1. sort()函数  
返回输入数组排序的副本。  
```numpy.sort(arr[,axis,kind,order])```  
kind:指定排序的算法->快排(Quicksort)、归并排序(Mergesort)或是堆排序(Heapsort),默认为Quicksort。  
axis:默认为1；  
order:指明自定义数据类型用于排序的属性。  
2. argsort()函数  
返回排序的索引数组。  
```numpy.argsort(arr[,axis,kind,order])```  
3. lexsort()函数  
用于对**多个序列**进行排序，可以看成对电子表格进行排序，每一列代表一个序列，**排序时优先照顾靠后的列**，返回索引。  
```numpy.lexsort(keys[,axis])```  
keys:键序列。  
### Numpy的去重与重复函数  
1. unique()函数  
返回输入数组去重后的值，并按照**从小到大**的顺序取排列。  
可以返回去重后的值组成的去重数组、去重数组的索引数组、去重数组的下标和去重值的重复数量等结果。  
```numpy.unique(arr,return_index,return_inverse,return_counts)```  
return_index若为True，返回**去重数组**和**去重数组组索引数组**；  
return_inverse若为True，返回**去重数组**和**去重数组元素在原数组中的下标**(可用于重构原数组)；  
return_counts若为True,返回**去重数组**和**去重数组中的元素在原数组中的出现次数**；  
补充：np.bincount(arr):返回arr中元素出现的个数（从0到最大值）  
2. tile()函数  
将一个已有的数组重复一定的次数(对整个数组)。  
```numpy.tile(arr,reps)```  
reps:重复的次数。  
3. repeat()函数  
对数组的每个元素进行重复。  
```numpy.repeat(arr,repeats,axis=None)```  
```a.repeat(repeats,axis)```  
repeats:指定重复的次数(对行/列，放在数组中)。  
4. 常用统计函数  
![aa](https://s3.ananas.chaoxing.com/doc/75/8a/0d/a71f769ff759c52c6d18f745041aee22/thumb/59.png)  
### Numpy的搜索和计数函数  
1. argmin()、nanargmin()、argmax()、nanargmax()  
argmin和argmax函数返回指定轴的最小元素或最大元素的索引。  
nanargmin和nanargmax用于返回忽略NaN后的结果。  
```numpy.argmin(a[,axis = None])```  
2. nonzero()函数  
返回输入数组中非零元素的索引。  
```numpy.nonzero(a)```  
3. where()函数  
返回满足条件x的元素索引，  
或在x为True时返回y，x为False时返回z。  
```numpy.where(x[,y,z])```  
4. extract()函数  
返回满足任何条件的元素  
```numpy.extract(x,a)```  
x为条件表达式，  
a为传入数组。  
5. count_nonzero()函数  
统计Numpy数组中非0元素的个数。  
```numpy.count_nonzero(a)```  
