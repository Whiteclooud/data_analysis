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
2. 画图：plt.***()  
3. 指定图标的标题：plt.title()  
4. 指定x,y轴名称：plt.xlabel()/plt.ylabel  
5. 修改坐标刻度与取值：plt.xticks()/plt.yticks()  
6. 改变x,y轴的取值范围：plt.xlim()/plt.ylim()  
7. 对某点进行标记或注释：plt.annotate()  
8. 显示图例：plt.legend()  
9. 展示图片：plt.show()   
### 创建画布  
```
plt.figure(num=None, figsize=None, dpi=None, facecolor=None, edgecolor=None, frameon=True, FigureClass=<class 'matplotlib.figure.Figure'>, clear=False, **kwargs)  
```  
figsize:接收元组,用于指定画布的宽度和高度。  
dpi:接受int,分辨率,默认为80。  

### 绘制图形函数  
属性名:  
![属性名](https://thumbnail0.baidupcs.com/thumbnail/a994e2ebdkb00aa125d8cc721bd75ccb?fid=1161491988-250528-998900937765904&time=1650006000&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-WkGDDdm1lKKytTurOHIzfOz2TY4%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=121333698134657279&dp-callid=0&file_type=0&size=c710_u400&quality=100&vuk=-&ft=video)  
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
颜色:  
![颜色](https://thumbnail0.baidupcs.com/thumbnail/7d893601fo6d75eadeca06b8cae8f881?fid=1161491988-250528-130345986620849&time=1649851200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-RxtQroXqwAlY6gJh8NpXEEZbgCY%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=79447553622120281&dp-callid=0&file_type=0&size=c710_u400&quality=100&vuk=-&ft=video)  
线形:  
![线形](https://thumbnail0.baidupcs.com/thumbnail/7d893601fo6d75eadeca06b8cae8f881?fid=1161491988-250528-130345986620849&time=1649851200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-RxtQroXqwAlY6gJh8NpXEEZbgCY%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=79580709517297378&dp-callid=0&file_type=0&size=c710_u400&quality=100&vuk=-&ft=video)  
#### 条形图  
条形图应用场景:  
1. 数量统计  
2. 频率统计  
```  
plt.bar(x, height, width=0.8, bottom=None, *, align='center', data=None, **kwargs)  
#横向条形图  
plt.barh(y, width, height=0.8, left=None, *, align='center', **kwargs)  
```  
x:一个数组或者列表,代表需要绘制的条形图的x轴坐标点。  
height:一个数组或者列表,代表需要绘制的条形图y轴的坐标点。  
width:每一个条形图的宽度,默认是0.8。  
bottom:y轴的基线,默认是0,也就是距离底部为0。  
align:对齐方式,默认是center,也就是跟指定的x坐标居中对齐,还有为edge,靠边对齐,具体靠左还是靠右,看width的正负。  
color:条形图的颜色。  
**可以通过调整bottom来绘制堆叠条形图**  
**可以通过调整width和x来绘制分组条形图**  
#### 直方图  
条形图应用场景:  
1. 显示各组数据数量的分布情况。    
2. 用于观察异常或孤立数据。  
3. 抽取样本过小,将产生较大误差,可信度低,也就失去了统计的意义。因此,样本数不应少于50个。    
```
plt.hist(x, bins=None, range=None, density=False, weights=None, cumulative=False, bottom=None, histtype='bar', align='mid', orientation='vertical', rwidth=None, log=False, color=None, label=None, stacked=False, *, data=None, **kwargs)
```  
x:数组或可以循环的序列,直方图将会从这组数据中进行分组。  
bins:数字或者序列(数组/列表等)。数字代表的是要分成多少组,若是序列,就会按序列指定的值分组。  
range:元组或None,若为元组,那么指定x划分区间的最大最小值。若为序列,那么range有没有设置没有任何影响。  
density:默认为False,为True则使用频率分布直方图。  
cumulative:若该参数与density参数都为True,那么返回值的第一个参数会不断累加,最终为1。  
**返回值:**  
n:数组。每个区间内值出现的个数。(若为频率分布直方图，那么数组内返回的是频率/组距)  
bins:数组。区间的值。  
patches:数组。每根条的对象。  
#### 散点图  
```
plt.scatter(x, y, s=None, c=None, marker=None, cmap=None, norm=None, vmin=None, vmax=None, alpha=None, linewidths=None, *, edgecolors=None, plotnonfinite=False, data=None, **kwargs)
```  
x,y:分别是x轴y轴的数据集。**两者数据长度必须一致**  
s:点的尺寸。若为一个具体数字,那么散点图的所有点都是一样大小。若为序列,那么这个序列的长度应该和x轴数据量一致,序列中每个元素代表每个点的尺寸。  
c:点的颜色。可以是一个具体的颜色,也可以是序列或cmap对象。  
marker:标记点,默认为圆,也可以换成其他。  
#### 饼图  
饼图是一个划分为几个扇形的圆形统计表,用于描述量、频率或百分比之间的相对关系的。  
```
matplotlib.pyplot.pie(x, explode=None, labels=None, colors=None, autopct=None, pctdistance=0.6, shadow=False, labeldistance=1.1, startangle=0, radius=1, counterclock=True, wedgeprops=None, textprops=None, center=(0, 0), frame=False, rotatelabels=False, *, normalize=True, data=None)  
```  
x:接受array,表示用于绘制饼图的数据(比例/数值序列)。  
labels:接受array,指定饼图每个分块的名称。  
explode:接受array,设置某几个分块距离圆心的半径。  
autopct:接受string,设置比例文字的展示方式(如保留几位小数等)。  
shadow:是否显示阴影。  
textprops:文本的属性(颜色,大小等)。  
**返回值:**  
patches:饼图上每个分块的对象。  
texts:分块的名字的文本对象。  
autotexts:分块的比例文字对象。  
可通过循环对2D对象通过setp(),set_fontsize(),set_color()等方法对文本进行设置。  
#### 箱线图  
箱线图是一种用作显示一组数据分散情况资料的统计图。它主要用作于反应原始数据的分布特征,还可以进行多组数据分布特征的比较。  
箱线图的应用场景:
1. 直观明了地识别数据中的异常值。  
2. 利用箱线图判断数据的偏态。  
3. 利用箱线图比较几批数据的形状。  
4. 箱线图适合比较多组数据,如果只是要看一组数据的分布情况,建议使用直方图。  
箱线图的绘制方法:找出一组数据的上限值、下限值、中位数、下四分位数以及上四分位数;连接两个四分位数画出箱子;再将最大值和最小值于箱子相连接,中位数在箱子。  
![箱线图](https://thumbnail0.baidupcs.com/thumbnail/690ba1e15ja059dc5e7bb1a7a83b443c?fid=1161491988-250528-922782372873065&time=1650009600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-RrxeAOKKAXNPZv4NlJRKJbJjT7E%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=121926158439866337&dp-callid=0&file_type=0&size=c710_u400&quality=100&vuk=-&ft=video)  
```
plt.boxplot(x, notch=None, sym=None, vert=None, whis=None, positions=None, widths=None, patch_artist=None, bootstrap=None, usermedians=None, conf_intervals=None, meanline=None, showmeans=None, showcaps=None, showbox=None, showfliers=None, boxprops=None, labels=None, flierprops=None, medianprops=None, meanprops=None, capprops=None, whiskerprops=None, manage_ticks=True, autorange=False, zorder=None, *, data=None)
```  
x:需要绘制的箱线图的数据。  
notch:是否展示置信区间,默认是False。如果设置为True,那么就会在盒子上展示一个缺口。  
sym:代表异常的的符号表示,默认为小圆点。  
vert:是否为垂直的,默认为True,如果设置为False那么将水平方向展示。  
whis:上下限的系数,默认是1.5,也就是上线是Q3+1.5(Q3-Q1)。如果传入的是序列,那么序列中的两个值代表的就是下限和上限的值,不需要计算。  
positions:设置每个盒子的宽度。  
labels:每个盒子的label。  
meanline和showmeans:如果这两个都为True,那么将会绘制平均值的线条。  
### 设置标题  
```
plt.title(label, fontdict=None, loc=None, pad=None, *, y=None, **kwargs)
```  
label:字符串,标题的名称。  
### 设置x,y轴的名称  
```
plt.xlabel（ylabel， fontdict=None， labelpad=None， *， loc=None， **kwargs)  
plt.ylabel（ylabel， fontdict=None， labelpad=None， *， loc=None， **kwargs)  
```
xlabel,ylabel:字符串,坐标轴的名称。  
### 修改坐标刻度与取值  
```
plt.xticks（ticks=None， labels=None， **kwargs)  
plt.yticks（ticks=None， labels=None， **kwargs)
```  
tick:列表,轴的刻度取值。  
labels:轴刻度的显示(可以为字符串)。  
rotation:刻度显示文本的旋转角度。  
### 指定坐标的取值范围  
```
plt.xlim()  
plt.ylim()  
```  
输入一个数值区间,不能使用字符串。  
### 设置文本和注释  
```
plt.annotate(text, xy, xytext, arrowprops{})  
```  
text:标注的内容。  
xy:被标注的点的坐标。  
xytext:标注内容相对与坐标的位置。  
arrowprops:箭头。  
![arrowprops](https://thumbnail0.baidupcs.com/thumbnail/5a0341d88h2a120665c816d26375217e?fid=1161491988-250528-720736193262549&time=1650013200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-rGJVjKpsQPcagBD9ZAj5sZaWaDY%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=122850698710716286&dp-callid=0&file_type=0&size=c710_u400&quality=100&vuk=-&ft=video)  
**同时设置多个注释的方法**
```
#1.zip()函数  
for i,j in zip(a,b):  #i,j分别遍历a,b  
#2.enumeric()函数  
for i,j in enumeric(data):  #遍历data,i为下标,j为值  
```
### 显示图例  
```
plt.legend(loc)  
```  
loc:表示图例放置位置。  
### 显示图像  
```
plt.show()  
```  
### 子图   
```
plt.subplot(行数,列数,第几个图)  
```  
在一个画布中绘制多个坐标系不同子图。  

### 可变参数？  
args:位置参数。  
kwargs:关键字参数  