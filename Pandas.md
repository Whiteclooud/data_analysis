# Pandas库  
## Pandas基础  
### 数据载入  
`pd.read_csv("路径") `和`pd.read_excel("路径")`  
路径书写方法:
- 双\  
- 改成/  
- 路径前加r  
```
pd.read_csv(filepath_or_buffer, sep=’，’, header=’infer’, names=None, index_col=None, dtype=None, engine=None, nrows=None)
```   
1. 若csv有表头且为第一行,`names`和`headers`都无需指定。  
2. 若csv文件有表头但不是第一行,可能下面几行开始才是真正的表头和数据，这个时候指定`header=行索引`即可;  
3. csv文件没有表头,全部是纯数据。用`names=[列名]`手动生成表头;  
4. csv文件有表头、但并不想使用这个表头。这个时候先用`headers`选出表头和数据,再用`names`将表头替换掉,等价于将数据读取进来后再对列名进行rename;  
### Series和DataFrame  
#### 创建  
`pd.Series`,`pd.DataFrame`  
1. 列表  
2. 数组  
3. 字典(键为列名)  
4. 其他Series  
**用数组和其他Series创建，改变原数据Series对象中的值也会改变**  
#### 常用属性  
| 函数|返回值
|:---:|:---:|
|  df.index|行索引/行名|
| df.columns|列名| 
|df.values|数据内容(数组对象)|
|df.dtypes|每一列数据类型|
|df.size|数据元素个数：行*列|
|df.ndim|维度|
|df.shape| 形状(行数，列数)|
|df.info()|查看数据的基本信息|
|df.head()|查看数据的前5行  

**快速了解数据的常用方法**  
- `data.index`:查看数据的行索引  
- `data.columns`:查看数据的列名  
- `data.info()`:查看数据各列的信息  
- `data.head()`:查看数据的前n行，默认前5行  
- `data.tail()`:查看数据的后n行，默认后5行  
- `data.sample()`:随机抽取n行  
#### 查询数据  
1. 索引:提取数据的列  
`data[列名]`或`data.列名`  
DataFrame所提取出的一列数据为Series对象  
2. 切片:提取数据的行  
`data[m:n]`  
3. 按行列要求提取  
按标签:`DataFrame.loc[行索引名称标签/条件,列索引名称标签]`-**包含终止值**  
按索引:`DataFrame.iloc[行索引位置,列索引位置]`-**行列均不包含终止值**  
<table>
	<tr>
	    <th>索引方式</th>
	    <th>参数</th>
	    <th>作用</th>  
	</tr >
	<tr >
	    <p align="center">
            <td rowspan="4">DataFrame[参数]</td>
        </p>
	    <td>单个字符串（列名）</td>
	    <td>显示对应的列<br>（Series结构）</td>
	</tr>
	<tr>
	    <td>字符串列表<br>（多个列名组成的列表）</td>
	    <td>显示列表里所有的列<br>（DataFrame结构）</td>
	</tr>
	<tr>
	    <td>索引位置整数切片</td>
	    <td>满足切片的行<br>（不包含终止值）</td>
	</tr>
	<tr>
	    <td >布尔型数组</td>
	    <td>显示数组元素为True值所对应的行</td>
</table>  

#### 增删改  
- **修改数据：找到指定数据的位置，进行赋值**
- **新增一列数据：设置一个新索引，进行赋值**
- **删除数据：drop('索引名/列名'，axis='index'/'columns')**  
`dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)`

- `axis`：轴向 默认0或'index'，表示按行删除；1或'columns'，表示按列删除。
- `how`：筛选方式;默认`any`:该行/列只要有一个以上的空值，就删除该行/列；`all`:全部都为空值，就删除该行/列。
- `thresh`：非空元素最低数量;int型，默认为None。如果该行/列中，非空元素数量小于这个值，就删除该行/列。
- `inplace`：是否原地替换。布尔值，默认为False。如果为True，则在原DataFrame上进行操作，返回值为None。  

## 统计分析方法  
### 描述性统计分析
常用的统计分析指标有计数、求和、求均值、方差、标准差等
- `pd对象.describe()`描述性统计为：个数、均值、标准差、  
最小值、25%分位值、50%分位值、75%分位值，以及最大值
- `pd对象.value_counts()`：统计每一类数据出现的次数
- `pd对象.astype('category').describe()`→`category`类型的描述性统计为：  
非空值个数，类别个数，频次最多的类别，频次最多的次数  

### 分组分析(离散型数据)  
**`df.groupby(by=['分组列1','分组列2'])['统计列1','统计列2'].agg([('聚合名称',聚合函数)])`**

分组分析是指根据分组字段，将分析对象划分成不同的部分，以对比分析各组之间差异性的分析方法。  
分组分析常用的统计指标是计数、求和、平均值  

### 分布分析(连续型数据)  
分布分析是指根据分析的目的，将定量数据(连续型数据)进行等距或者不等距的分组；  
从而研究各组分布规律的一种分析方法，如学生成绩分布、用户年龄分布、收入状况分布等。  
在分布分析时，首先用cut()函数确定分布分析中的分层，然后再用groupby()函数实现分组分析  
·pd.cut(data,bins,right=true,labels=None,include_lowest=False)·
- data: 进行划分的一维数组
- bins：取整数值，表示将x划分为多少个等距的区间。取序列值，表示将x划分在指定序列中
- right：分组时是否包含右端点，默认为True（包含）
- labels：分组时是否用自定义标签来代替返回的bins，可选项，默认为NULL。
- include_lowest：分组时是否包含左端点，默认为False（不包含）。  

### 交叉分析
交叉分析通常用于分析两个或两个以上分组变量之间的关系，以交叉表形式进行变量间关系的对比分析；  
从数据的不同维度，综合进行分组细分，进一步了解数据的构成、分布特征。交叉分析有数据透视表和交叉表两种： 
#### 1.透视表  
`pivot_table()`函数返回值是数据透视表的结果，该函数相当于Excel中的数据透视表功能。  
**透视表 `pd.pivot_table(data,values,index,columns,agg,func,fill_value,margins)`**
-  `data`：要应用透视表的数据框。
-  `values`：待聚合的列名，默认聚合所有数值列。
-  `index`：用于分组的列名或其他分组键，出现在结果透视表的行。
-  `columns`：用于分组的列名或其他分组键，出现在结果透视表的列。
-  `aggfunc`：聚合函数或函数列表，默认为'mean'，可以是任何对groupby有效的函数。
-  `fill_value`：用于替换结果表中的缺失值。
-  `margins`：添加行/列小计和总计，默认为False。

**在交叉分析前，先用cut()函数确定交叉分析中的分层，然后再利用pivot_table()函数实现交叉分析**  
#### 2.交叉表  
交叉表（Cross-Tabulation，简称crosstab）是一种用于计算分组频率（size）的特殊透视表  
**`pd.crosstab(待分组的行数据,待分组的列数据)`**  

### 结构分析
结构分析是在分组和交叉的基础上，计算各组成部分所占的比例，进而分析总体的内部特征的一种分析方法。  
重点在于了解各部分占总体的比例,例如:求公司中不同学历员工所占的比例，产品在市场的占有率、股权结构等  
在结构分析时，先利用pivot_table()函数进行数据透视表分析，  
然后，通过指定axis参数对数据透视表按行或列进行计算（**当axis=0时按列计算，axis=1时按行计算**）。  
主要包括：add,sub,multiply,div;sum,mean,var,sd  
### 相关分析  
相关分析（Correlation Analysis）用于研究现象之间是否存在某种依存关系,  
并探讨具有依存关系的现象的相关方向以及相关程度,是研究随机变量之间相关关系的一种统计方法。  
线性相关关系主要采用皮尔逊（Pearson）相关系数r来度量连续变量之间线性相关强度:  
r>0，线性正相关；  
r<0，线性负相关；  
r=0，表示两个变量之间不存在线性关系，但并不代表两个变量之间不存在任何关系  
| 相关系数\|r\|取值范围 |相关程度
|:---:|:---:|
|  0⩽\|r\|<0.3  | 低度相关 |
| 0.3⩽\|r\|<0.8  | 中度相关| 
| 0.8⩽\|r\|⩽1 | 高度相关

**相关分析函数包括DataFrame.corr()和Series.corr(other):**   
**计算相关系数的corr()函数只会对数据框中的数据列进行计算**
- 如果由数据框调用corr()函数，那么将会计算列与列之间的相似度。
- 如果由序列调用corr()方法，那么只是该序列与传入的序列之间的相关度。函数返回值如下。
- DataFrame调用：返回DataFrame。
- Series调用：返回一个数值型数据，大小为相关度。  

## Pandas函数使用  
### 通用函数  
**1. 行列通用函数`apply()`**  
`DataFrame.apply(函数,axis)`:指定的轴方向应用自定义函数(默认axis=0:对列；axis=1:对行)  
DataFrame:若使用的对象为Series,则默认一整列,整个Series是一个对象,一个整体。  
函数:若函数为内置函数,例如`mean`,则需要用''包起来。  
`lambda 参数:表达式`  
参数列表：多个参数用逗号隔开,例如a,b,c  
**2. 元素级通用函数`applymap() & map()`**  
`DataFrame.applymap(函数)`对数据框(DataFrame)对象每个元素进行操作  
`Series.map(函数)`对数据框的某一列(series)对象每个元素进行操作  
**2. 可使用NumPy的通用函数**  
### 排序和排名  
**1. 索引排序**
`DataFrame.sort_index()`：排序默认使用升序排序，ascending=False 为降序排序  
`DataFrame.reset_index(level=None, drop=False, name=NoDefault.no_default, inplace=False)`  
inplace:是否在原数据上改动,默认为False。  
**2. 按值排序**  
`DataFrame.sort_values('columns',ascending=True,na_position)`  
根据某一列名进行排序,若有其他相同列名则报错。  
ascending:是否升序排列,默认为True,降序为False。  
na_position:排序后空值的位置，‘first’或‘last’, default ‘last'。  
inplace:是否在原数据上改动,默认为False。  
**3. 排名**  
`DataFrame.rank(ascending, method = ‘max’,axis)`  
返回每个元素在原序列中的排名,初始值为1。有N个相同的元素，排名会相加并除以N。  
若对DataFrame进行排名,则根据axis指定的轴进行排名。   
ascending:是否升序排列,默认为True,降序为False。  
method:'max','min','first'。排名相同时的取值,默认取均值。  
inplace:是否在原数据上改动,默认为False。  
|参数|说明
|:---:|:---:|
|average|默认值,即在相等分组中,为各值分配平均排名|
|min|使用整个分组的最小排名|
|max|使用整个分组的最大排名|
|first|按值在原始数据中出现的顺序分配排名|
|dense|于min类似,但是排名每次只会增加1,即并列的数据只占一个名次|  
`nlargest()和nsmallest()方法`  
`DataFrame.nsmallest(n,columns)`:在数据中找到columns列为最小的n个值  
`DataFrame.nlargest(n,columns)`:在数据中找到columns列最大的n个值  
