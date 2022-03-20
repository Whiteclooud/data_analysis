# numpy数组与矢量运算  
## numpy数组对象  
### 数组的属性  
```ndim```       返回int,表示数组维度。  
```shape```     返回tuple,表示数组的尺寸，(n,m)。   
```size```       返回int,表示数组的元素总数,n*m。
```dtype```      返回data-type,描述数组中元素类型。  
```itemsize```   返回int，表示数组的每个元素大小（以字节为单位）。  
### numpy的数据类型  
![dtype](/dtype.png.png)
### 创建数组对象  
```numpy.array(object,dtype=None,copy=True,order=None,subok=False,ndmin =0)```
object:接受array，表示想要创建数组，无默认。  
dtype:接受data-type,表示数组所需要的数据类型，默认为保存对象所需的最小类型。  
ndmin:接收int，指定最小维度,默认为None。  
object为唯一必要参数。  