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
### 通用步骤  
1. 创建画布：plt.figure()  
2. 画图：plt.plot()  
3. 指定图标的标题：plt.title()  
4. 指定x,y轴名称：plt.xlabel()/plt.ylabel
5. 修改坐标刻度与取值：plt.xticks()/plt.yticks()  
6. 改变x,y轴的取值范围：plt.xlim()/plt.ylim()  
7. 显示图例：plt.legend()  
8. 展示图片：plt.show()  

### 可变参数？  
args:位置参数。
kwargs:关键字参数