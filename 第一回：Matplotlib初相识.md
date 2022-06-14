# Matplotlib初相识
[[Course]]
[学习内容](https://datawhalechina.github.io/fantastic-matplotlib/%E7%AC%AC%E4%B8%80%E5%9B%9E%EF%BC%9AMatplotlib%E5%88%9D%E7%9B%B8%E8%AF%86/index.html)

## 认识matplotlib
+ 可以生成动态，交互式的图表，不止于静态
+ 可用于多种环境和IDE下
+ Python可视化的起源，pandas和seaborn绘图接口是基于matplotlib的

## 一个最简单的绘图例子
```python
import matplotlib.pyplot as plt
import matplotlib as mpl
import numpy as np

fig, ax = plt.subplots() # 创建一个包含axes的figure
ax.plot([1, 2, 3, 4], [1, 4, 2, 3])
```

![](https://cdn.jsdelivr.net/gh/YikunHan42/Image-Host/202206141639055.png)


jupyter notebook中，默认出现`<matplotlib.lines.Line2D at 0x23155916dc0>`，因为绘图代码默认打印出最后一个对象

避免的方法：
1. 在代码块最后加一个分号
2. 在代码块最后加一句`plt.show()`
3. 在绘图时将绘图对象显式赋值给一个变量，如将`plt.plot([1,2,3,4])`改成`line = plt.plot([1,2,3,4])`

或者像MATLIB命令一样，直接使用`matplotlib.pyplot`方法直接在当前axes上绘制图像，所以上述可以简化为：
```python
line = plt.plot([1, 2, 3, 4], [1, 4, 2, 3])
```

## Figure的组成
+ Figure: 顶层，像容器一样包含所有元素
+ Axes: 核心，容纳大量元素用以构造子图，figure可以包含一或多个子图
+ Axis: 处理所有和坐标轴，网格有关的元素
+ Tick: 用于处理所有与刻度有关的元素
![](https://cdn.jsdelivr.net/gh/YikunHan42/Image-Host/202206141656880.png)


## 两种绘图接口
1. 显示创建figure和axes，上面调用绘图方法，面向对象模式(OO)
2. 依赖pyplot自动创建figure和axes，并绘制

![](https://cdn.jsdelivr.net/gh/YikunHan42/Image-Host/202206141702398.png)

以上图为例，两种创建方式分别如下所示：
```python
x = np.linspace(0, 2, 100)

fig, ax = plt.subplots()  
ax.plot(x, x, label='linear')  
ax.plot(x, x**2, label='quadratic')  
ax.plot(x, x**3, label='cubic')  
ax.set_xlabel('x label') 
ax.set_ylabel('y label') 
ax.set_title("Simple Plot")  
ax.legend() # 图例
plt.show()
```

```python
x = np.linspace(0, 2, 100)

plt.plot(x, x, label='linear') 
plt.plot(x, x**2, label='quadratic')  
plt.plot(x, x**3, label='cubic')
plt.xlabel('x label')
plt.ylabel('y label')
plt.title("Simple Plot")
plt.legend()
plt.show()
```

## 通用绘图模板
边用边查，补丁式学习，此处给出OO模式的代码示例

![](https://cdn.jsdelivr.net/gh/YikunHan42/Image-Host/202206141708521.png)

```python
# step1 准备数据
x = np.linspace(0, 2, 100) # 0~2序列，观测值为100
y = x**2

# step2 设置绘图样式，这一模块的扩展参考第五章进一步学习，这一步不是必须的，样式也可以在绘制图像是进行设置
mpl.rc('lines', linewidth=4, linestyle='-.')

# step3 定义布局， 这一模块的扩展参考第三章进一步学习
fig, ax = plt.subplots()  

# step4 绘制图像， 这一模块的扩展参考第二章进一步学习
ax.plot(x, y, label='linear')  

# step5 添加标签，文字和图例，这一模块的扩展参考第四章进一步学习
ax.set_xlabel('x label') 
ax.set_ylabel('y label') 
ax.set_title("Simple Plot")  
ax.legend() ;
```

## 思考题
+  请思考两种绘图模式的优缺点和各自适合的使用场景
	pyplot多用于交互式绘图，oo方法更常用于静态绘图
+  在第五节绘图模板中我们是以OO模式作为例子展示的，请思考并写一个pyplot绘图模式的简单模板
```python
x = np.linspace(0, 2, 100)
y = x**2

mpl.rc('lines', linewidth=4, linestyle='-.')

plt.plot(x, y, label='linear')

plt.xlabel('x label')
plt.ylabel('y label')
plt.title("Simple Plot")
plt.legend()
plt.show()	
```