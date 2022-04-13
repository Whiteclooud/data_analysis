# 数据可视化——Matplotlib库  
## 使用pyplot创建图形  
### 显示中文  
```
#方法1：统一设置中文属性  
plt.rcParams['font.sans-serif']=['SimHei']  
plt.rcParams['axes.unicode_minus'] = False #显示中文属性设置  
y = [np.random.randint(0,10) for i in range(10)]  
plt.plot(y)  
plt.title("折线图")  
```  
```  
#方法2：通过plt.title()中设置fontproperties参数  
#加载字体的时候，可以到C:\windows\Fonts中找到你喜欢并可以显示的中文字体  
from matplotlib import font_manager  
font = font_manager.FontProperties(fname=r"C:\\Windows\\Fonts\\msyh.ttc",size=10)  
y = [np.random.randint(0,10) for i in range(10)]  
plt.plot(y)  
plt.title("折线图", fontproperties=font)  
```  
### 绘制图形函数  
#### 点线图  
```  
#单条线  
plt.plot([x],y,[fmt],data = None,**kwargs)  
#多条线一起画(指定多个[x],y,[fmt]组集)  
plt.plot([x],y,[fmt],[x2],y2,[fmt2],...,**kwargs)  
```  
x:x轴数据,列表或数组。(可选)  
y:y轴数据,列表或数组。(xy只能是位置参数,不能作为关键字参数赋值)  
fmt:接受简写来定义图的基本属性,为一个字符串。(可以与关键字参数混用,当发生冲突时,关键字参数优先)  
data:绘制带有标记数据的对象(如字典,dataframe),若传参,此时x,y不接收数据,只接收标签。  
![颜色]('https://thumbnail0.baidupcs.com/thumbnail/7d893601fo6d75eadeca06b8cae8f881?fid=1161491988-250528-130345986620849&time=1649851200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-RxtQroXqwAlY6gJh8NpXEEZbgCY%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=79447553622120281&dp-callid=0&file_type=0&size=c710_u400&quality=100&vuk=-&ft=video')
### 通用步骤  
1. 创建画布：plt.figure()  
2. 画图：plt.***()  
3. 指定图标的标题：plt.title()  
4. 指定x,y轴名称：plt.xlabel()/plt.ylabel  
5. 修改坐标刻度与取值：plt.xticks()/plt.yticks()  
6. 改变x,y轴的取值范围：plt.xlim()/plt.ylim()  
7. 显示图例：plt.legend()  
8. 展示图片：plt.show()  

### 可变参数？  
args:位置参数。
kwargs:关键字参数