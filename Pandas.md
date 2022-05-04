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