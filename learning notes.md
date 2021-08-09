# 《matlab初学者教程》

## 一、matlab介绍

### 1. 命令行窗口中的输入小注意

一行敲完了不要加分号。

一个语句在一行内太长了，需要在第一行末尾加上**完整省略号**（......），然后开始第二行书写。

```matlab
x1=1/2+1/3+1/4......
+1/5+1/6
```

### 2.编辑调试器

编辑调试器一般用于创建M文件，或者修改已存在的M文件。

创建一个M文件：主页-新建脚本

打开一个M文件：主页-打开-文件夹中选择

在编辑器窗口输入M文件的语句，然后在命令行窗口输入M文件名就可以输出相应的结果。

**在脚本文件中，每一行的末尾需要输入分号。**

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-1.png)

### 3.图像窗口

在脚本文件中可以进行相关图像的打印。

例如下面输出从0到6以0.1为间隔的sin(x)的图像。

```matlab
% this m-file calculates and plots the function sin(x) for 0<=x<=6.
x=0:0.1:6;
y=sin(x);
plot(x,y);
```

### 4. whos和clear

在命令行输入whos，可以查看在**当前工作区**内的所有变量和数组状况表（包括执行过的M文件中的变量和数组）。

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-2.png)

可以在命令行输入之前使用过的变量（可以参考工作区），然后就可以输出对应的变量的值啦。

在命令行中使用clear可以清除本工作区的变量。

```matlab
clear var1, var2
```

然后就可以看到在工作区对应的变量var1, var2消失了。

## 二、matlab基础

### 1. 变量的初始化

数组的大小由数组的行数和列数共同决定，**注意行数在前**。

#### (1)用赋值语句初始化变量

```matlab
var=expression
```

var是变量名，expression可以是一个标量、一个数组或者常量、其他变量和数学运算符号的联合。

数组变量也可以初始化。**用括号和分号建立数组。**所有元素按照行阶排序，每一行的值从左往右，顶部的行置于最前，底部的行置于最后。

```matlab
[3.4] %表示1*1数组，一个标量，此时数组可以省略
[1 2 3] %创建了1*3数组，即一个一维行向量
[1;2;3] %创建了3*1数组，即一个一维列向量
[1,2,3;4,5,6] %创建了2*3数组

[1,2,3
4,5,6] %创建了一个2*3数组

[] %空数组，注意和全为0的数组的区别
```

数组创建时，**并非每个元素都需要定义。**没有定义的元素会被自动创建并初始化为0。

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-3.png)

**在每个赋值语句末尾的分号有“停止重复”的作用。**

> 重复可以方便快速查验代码的正确性和显示赋值语句的结果，但会降低工作速度。

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-4.png)

#### (2)用捷径表达式赋值

**克隆运算符**：可以指定一系列的数值，它规定了初值、末值和步长。

```matlab
first:step:last
```

当步长为1时，可以省略step，变成：

```matlab
first:last
```

例如：下面的语句可以生成包含100个元素的数组$$\displaystyle [\frac{\pi}{100},\frac{2\pi}{100},...,\pi]$$

```matlab
angles=(.01:.01:1)*pi;
```

**转置运算符**：用行向量的转置初始化列向量或者更加复杂的矩阵。

```matlab
>> f=[1:4]'

f =

     1
     2
     3
     4
>> t=[3:6];
>> g=[t' t']

g =

     3     3
     4     4
     5     5
     6     6

```

#### (3)用内置函数来初始化

用matlab内置函数来初始化数组。

```matlab
zeros(n)  %创建一个n*n零矩阵
zeros(n,m) %创建一个n*m零矩阵
zeros(size(arr)) %创建一个与数组arr大小相同的零矩阵
ones(n) %创建一个n*n的全一矩阵
ones(n,m) %创建一个n*m全一矩阵
eye(n) %创建一个n*n的单位矩阵
eye(n,m) %创建一个n*m的单位矩阵
length(arr) %返回一个向量的长度，或者返回二维数组中最长的哪一维的长度
size(arr) %返回指定数组的行数和列数
```

#### (4)使用关键字input初始化变量

在脚本文件中，可以用来提示使用者输入。显示提示语句，等待用户驶入一个值。

```matlab
my_val=input('Enter an input value:')
```

输入一个数：直接键入；

输入一个数组：必须加上中括号[]。

按下回车键时，窗口中输入的任何值都会被存储于变量my_val。

如果什么都不输入就按下回车键，那么它就是一个空矩阵。

如果input函数中含有字符's'作为它的第二个参数，那么输入的数据就被当作字符串。

```matlab
>> my_val=input('Enter a variable:')
Enter a variable:[1,2,3;4,5,6]

my_val =

     1     2     3
     4     5     6

>> int1=input('Enter an input int:')
Enter an input int:1.23

int1 =

    1.2300

>> int2=input('Enter an input int:','s')
Enter an input int:1.23

int2 =

    '1.23'

```

### 2.多维数组

matlab允许创建多维数组，这些数组的每一维对应一个下标，每一个单个元素都可以通过它的下标被调用。

例如下面**用两个语句创建2×3×2的数组**：

```matlab
>>  c(:,:,1)=[1,2,3;4,5,6];
>> c(:,:,2)=[6,7,8;9,10,11];
>> whos c
  Name      Size             Bytes  Class     Attributes

  c         2x3x2               96  double              

>> c

c(:,:,1) =

     1     2     3
     4     5     6


c(:,:,2) =

     6     7     8
     9    10    11

```

**注意**：上面用冒号:表示省略/指代。这个三维数组的显示方法和一般的大致相同。

**访问多维数组时，最好写清楚访问的位置，即行数和列数要写清楚。**

```matlab
>> c(2,2,2)

ans =

    10

```

### 3.特殊变量

matlab中有一些预先定义好的变量，可以随时调用。

```matlab
pi %有15个有效值的圆周率
i,j %代表虚数
inf 或者 Inf %代表无穷大，一般是除以0产生的
NaN %表示没有这个数，一般是通过数学运算得到的，比如0/0
clock %这个特殊变量包含了当前的年、月、日、时、分、秒，是一个六元素行向量
date %当前的日期，使用字符形式，如30-Dec-2007
eps %变量名为epsilon（ε）的简写。表示计算机能够识别的两个数之间的最小数
ans %用于存储表达式的结果，当一个结果没有明确的赋值给某个变量时


%测试如下：

>> clock

ans =

   1.0e+03 *

    2.0210    0.0030    0.0050    0.0150    0.0520    0.0283

>> date

ans =

    '05-Mar-2021'

>> eps

ans =

   2.2204e-16

```

### 4. 标量运算和数组运算

#### (1)标量运算符

加法，减法，乘法，除法，乘方，括号

#### (2)数组运算和矩阵运算

1. 数组运算

	针对两数组相对应的运算使用的。**两个数组的行和列必须相同（即必须时方阵）。**也可以用于一个标量和数组的运算，**此时标量将和数组的每一个元素进行运算。**

	```matlab
	>> a=[1,3;2,4];
	>> b=[-1,3;-2,1];
	>> a+b
	
	ans =
	
	     0     6
	     0     5
	
	>> a+4
	
	ans =
	
	     5     7
	     6     8
	```

2. 矩阵运算

	遵守线性代数的一般规则，比如矩阵的乘法。

**一般在进行矩阵的加减法时，数组和矩阵运算时没有区别的；但是在有些操作中，它们有一定的区别，这时我们在运算符号前加一个点.来表示这是一个数组运算。**

![](C:\Users\lenovo\Pictures\Saved Pictures\常见的数组和矩阵运算.png)

### 5.matlab的内建函数

#### (1)选择性结果

max函数可以返回两个参数，第一个参数是输入的向量中的最大值，第二参数是输入向量中的最大值在向量中的位置。（**当然，也可以选择只返回一个最大值**）

```matlab
>> maxval=max([1 -5 7 3])

maxval =

     7

>> [maxval2 index]=max([1 -5 7 3])

maxval2 =

     7


index =

     3

```

min函数也有这样的功能：

```matlab
>> minval=min([1 -5 7 3])

minval =

    -5

>> [minval2 index2]=min([1 -5 7 3])

minval2 =

    -5


index2 =

     2

```

#### (2)带数组输入的matlab函数的应用

如果一个函数的输入是一个数组，那么这个函数的输出也是一个数组。

```matlab
>> x=[1,2,3,4,5,6,7,8,9,10];
>> y=sin(x)

y =

    0.8415    0.9093    0.1411   -0.7568   -0.9589   -0.2794    0.6570    0.9894    0.4121   -0.5440

```

#### (3)matlab常用的函数

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab常用函数1.png)

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab常用函数2.png)

## 三、matlab画图

### 1. 画图入门

#### (1)最简单的xy图像

画一个数据图，首先要创建两个向量，由x,y构成，然后使用plot函数。

```matlab
>> x=0:0.05:10;
>> y=x.^2-10*x+15;
>> plot(x,y);
```

**注意这里的乘方务必用数组计算方法！必须要加一个小点“.”！**

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-5.png)

#### (2)标题、坐标轴标签和网格线

```matlab
title('') %添加标题，在单引号中输入标题
xlabel('') %添加x轴轴标签
ylabel('') %添加y轴轴标签
grid on %在图像中出现网格线
grid off %在图像中去除网格线
```

```matlab
>> x=0:0.01:10;
>> y=x.^2-10*x+15;
>> plot(x,y);
>> title('plot of y=x.^2-10*x+15');
>> xlabel('x');
>> ylabel('y');
>> grid on;
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-6.png)

#### (3)打印图像

在图像窗口选择“另存为”即可，可以选择存储为.tif  .png   .svg   .jpg等多种文件。

#### (4)联合作图

在同一个坐标系中做出多个函数的图像：

使用plot函数，必须将一系列的x值和每一个函数对应的y值相对应。

注意plot中使用逗号分开，不必用分号。

```matlab
>> x=0:pi/100:2*pi;
>> y1=sin(2*x);
>> y2=2*cos(2*x);
>> plot(x,y1,x,y2);
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-7.jpg)

#### (5)线的颜色、形式，符号形式

在x,y向量参数后带有相关属性的字符串的plot函数，可以选择轨迹颜色和形式和符号类型，主要包括三类：

- 轨迹的颜色
- 符号的类型（线上加圆圈、三角等）
- 线的类型（实线虚线、点画线等）

![](C:\Users\lenovo\Pictures\Saved Pictures\图像的颜色、标记类型、线型1.png)

![](C:\Users\lenovo\Pictures\Saved Pictures\图像的颜色、标记类型、线型2.png)

下面给出一个例子，**注意plot的语法**！

```matlab
>> x = 0:1:10;
>> y = x.^2 -10.*x +15;
>> plot(x,y,'r-.',x,y,'cp');
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-8.jpg)

#### (6)图例

用legend制作图例。其基本形式为：

```matlab
legend('string1','string2',...,'Location','pos')
```

其中string1, string2等是轨迹标签名，Location是一个必须写上去的（具体意义不明），pos是一个字符串，用于指定图例的位置。

```matlab
legend off %去除多余的图例
```

下面给出一个完整的xy图像的例子，注意legend的语法。**不写参数pos相当于默认在右上角。**

```matlab
x=0:pi/100:2*pi; 
y1=sin(2*x); 
y2=2*cos(2*x); 
plot(x,y1,'k-',x,y2,'b--'); 
title(' Plot of f(x)=sin(2x) and its derivative'); 
xlabel('x'); 
ylabel('y'); 
legend('f(x)','d/dx f(x)') %这里加不加分号都可以正常运行
grid on;
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-9.jpg)

legend的位置选择，'pos'字符串的取值：

| 设置               | 位置                                      |
| ------------------ | ----------------------------------------- |
| 'North'            | inside plot box near top                  |
| 'South'            | inside bottom                             |
| 'East'             | inside right                              |
| 'West'             | inside left                               |
| 'NorthEast'        | inside top right (default for 2-D plots)  |
| 'NorthWest'        | inside top left                           |
| 'SouthEast'        | inside bottom right                       |
| 'SouthWest'        | inside bottom left                        |
| 'NorthOutside'     | outside plot box near top                 |
| 'SouthOutside'     | outside bottom                            |
| 'EastOutside'      | outside right                             |
| 'WestOutside'      | outside left                              |
| 'NorthEastOutside' | outside top right (default for 3-D plots) |
| 'NorthWestOutside' | outside top left                          |
| 'SouthEastOutside' | outside bottom right                      |
| 'SouthWestOutside' | outside bottom left                       |
| 'Best'             | least conflict with data in plot          |
| 'BestOutside'      | least unused space outside plot           |

#### (7)对数尺度

打印数据既可以对数尺度，也可以线性尺度，于是就有4种组合，每种组合都有各自的意义。

```matlab
plot %x,y都是线性尺度
semilogx %x轴是对数尺度，y轴是线性尺度
semilogy %x轴是线性尺度，y轴是对数尺度
loglog %x,y都是对数尺度
```

下面举出四种不同方式下的函数图像：

```matlab
x=0:pi/100:2*pi; 
y1=exp(x).*sin(10*x); 
y2=sin(10*x);
plot(x,y1,'m-',x,y2,'b-.'); 
title(' Plot of f1(x)=exp(x)*sin(2*x) and f2(x)=sin(2*x) '); 
xlabel('x'); 
ylabel('y'); 
legend('f(x)','f2(x)','Location','North');
grid on;
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-10.jpg)

```matlab
x=0:pi/100:2*pi; 
y1=exp(x).*sin(10*x); 
y2=sin(10*x);
semilogx(x,y1,x,y2); 
title(' Plot of f1(x)=exp(x)*sin(2*x) and f2(x)=sin(2*x) '); 
xlabel('x'); 
ylabel('y'); 
legend('f(x)','f2(x)','Location','North');
grid on;
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-11.jpg)

```matlab
x=0:pi/100:2*pi; 
y1=exp(x).*abs(sin(10*x)); 
y2=abs(sin(10*x));
semilogy(x,y1,x,y2); 
title(' Plot of f1(x)=exp(x)*sin(2*x) and f2(x)=sin(2*x) '); 
xlabel('x'); 
ylabel('y'); 
legend('f(x)','f2(x)','Location','North');
grid on;
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-12.jpg)

```matlab
x=0:pi/100:2*pi; 
y1=exp(x).*abs(sin(10*x)); 
y2=abs(sin(10*x));
loglog(x,y1,x,y2); 
title(' Plot of f1(x)=exp(x)*sin(2*x) and f2(x)=sin(2*x) '); 
xlabel('x'); 
ylabel('y'); 
legend('f(x)','f2(x)','Location','North');
grid on;
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-13.jpg)

### 2. 简单的二维图像

#### (1) 控制x,y轴的上下限

利用**axis命令/函数可以实现设定和修改坐标的上下限**。

通常预设值是范围足够显示输入值的每一个点。

![](C:\Users\lenovo\Pictures\Saved Pictures\axis函数.png)

matlab无论遇到什么命令，都会转化为一个函数进行操作。只有带有字符参数的函数才能当作命令，带有数字参数的函数只能被当作函数。所以axis有时当作命令，有时候当作函数。

```matlab
x=-2*pi:pi/20:2*pi;
y=sin(x); 
plot(x,y);
title('Plot of sin(x) vs x');
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-14.jpg)

当限定范围后：

```matlab
x=-2*pi:pi/20:2*pi;
y=sin(x); 
plot(x,y);
title('Plot of sin(x) vs x');
axis([0 pi 0 1]);
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-15.jpg)

#### (2) 在同一坐标系内画多个图像

一般情况下，创建一个新的图像就要用到一个plot命令，**前面的数据就会自动消失**。可以采用hold命令加以修改。

```matlab
hold on %所有新的图像都会叠加在原来存在的图像上
hold off %可以恢复默认情况，用新的图像来替代原来的图像
```

例如，在同一坐标系种画出sin x和cos x的图像

```matlab
x = -pi:pi/20:pi; 
y1 = sin(x); 
y2 = cos(x); 
plot(x,y1,'b-'); 
hold on; 
plot(x,y2,'k--'); 
hold off;
legend ('sin x','cos x','Location','Northeast');
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-16.jpg)

没有hold on语句则只有sin x的图像，没有cos x的图像；没有hold off对图像没有影响，但是可能会对之后的操作造成干扰。

#### (3) 创建多个图像窗口

matlab可以创建多个图象窗口，每个窗口都有不同的数据。用图象数（整数）加以区分。这些窗口中的一个成为当前图像窗口，所有新的图画命令都将会展示在那个窗口中。

我们用**figure**函数来选择当前窗口。函数形式为**figure(n)**，其中n代表图象数。当这个函数被执行时，图n为成为当前图象，执行所有的画图命令。窗口不存在时，matlab将自动创建。

**gef**函数用于返回当前图象数。

```matlab
figure(1); 
x = x:0.05:2;
y1 = exp(x); 
plot(x,y1); 
figure(2); 
y2 = exp(-x);
plot(x,y2);
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-17.png)

#### (4) 子图象

在一个图像窗口中有一系列的坐标系，创建出多个子图象。

```matlab
subplot(m,n,p) %m行，n列，第p个图象
```

这个命令在当前图象窗口创建了m×n个子图象，按照m行、n列排列，并选择子图象p来接受当前所有画图命令。这些子图象按照从左到右、从上到下编号。如果subplot命令创建的新坐标系和原来的坐标系相冲突，那么原来的坐标系会被自动删除。

```matlab
figure(1); 
subplot(2,1,1); 
x = -pi:pi/20:pi; 
y = sin(x); 
plot(x,y,'r-'); 
title('Subplot 1 title y = sin(x)'); 
subplot(2,1,2); 
x = -pi:pi/20:pi; 
y = cos(x); 
plot(x,y,'b--');
title('Subplot 2 title y = cos(x)');
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-18.jpg)

#### (5)对画线的增强控制

设置线宽、标识颜色、标识填充色、标识的大小。

![](C:\Users\lenovo\Pictures\Saved Pictures\linewide & marker.png)

都可以在`plot`命令中调节：

```matlab
plot(x,y,'PropertyName',value,...)
```

画出一个图象，轨迹的宽度为3，颜色为黑色，圆圈标识的宽度为6，每个标识为红色边缘和绿色内核。

```matlab
x=0:pi/6:10*pi;
y=sin(x/2);
plot(x,y,'k-',x,y,'wo','LineWidth',3,'MarkerSize',6,'MarkerEdgeColor','r','MarkerFaceColor','w');
title('y=sin(x)');
xlabel('x');
ylabel('x');
grid on;
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-19.jpg)

#### (6) 文本字符串的高级控制

> 使用的时候貌似容易出现一些问题。

画图中可能会用到文本字符串（标签、坐标轴标签），可以用黑体、斜体来格式化，也包括特殊的希腊字母或数字符号。

文本的字体可以通过**stream modifiers**修改。一个stream modifiers时一个特殊的字符序列，用于告诉编译器改变它的行为。

常用的是：

| stream modifiers |        含义         |
| :--------------: | :-----------------: |
|       \bf        |        黑体         |
|       \it        |        斜体         |
|       \rm        |    恢复正常字体     |
|    \fontname     |     字体的名字      |
|    \fontsize     |     字体的大小      |
|      _{xxx}      | xxx作为某字符的上标 |
|      ^{xxx}      | xxx作为某字符的下标 |

一旦一个stream modifier插入到一个文本字符串中，它将持续发挥作用，知道这个字符串结束或者消失。如果一个modifier后再跟着一个{}，那么只对{}中的文本起作用。

**如果需要插入特殊的希腊字母或者数字符号，可以参考latex转义序列。即matlab中的这些语法和latex是一样的。**

#### (7)极坐标图象

**！！注意！！matlab官网推荐的是使用`polarplot`函数在极坐标中绘制线条。**

```matlab
polarplot(theta,rho) %theta是辐角，rho是长度
polarplot(theta1,rho1,theta2,rho2,...) %绘制多个对组
```

函数**`polar`**用于在极坐标系中画图。

```matlab
polar(theta,r)
```

theta代表一个弧度角数组，r代表一个距离数组。

它用来画以角度为自变量的函数的极坐标图是很有用的。

例如用polar函数在matlab中画出心型曲线。

```matlab
t = 0:pi/100:2*pi;
r = 1-sin(t);
subplot(1,2,1);
polar(t, r);
subplot(1,2,2);
t1 = t-pi/2;
r1 = 1-sin(t1);
polar(t, r1);
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-20.jpg)

### 3. 二维作图的补充说明

#### (1) 二维作图的附加类型

除了前面提到的简单的xy图象，还有针头图(stem plots)、阶梯图(stair plots)、条形图、饼图(pie plots)、罗盘图(compass plots)。

![](C:\Users\lenovo\Pictures\Saved Pictures\附加的二维作图类型.png)

针头图、条形图、罗盘图、阶梯图都可以参考下面的代码（用子图的形式，分别做出几个图象）：

```matlab
subplot(2,3,1);
x = 0:pi/4:2*pi; 
y = sin(x); 
stem(x,y); 
title('\bf Stem plot'); 
xlabel('\bf\itx');
ylabel('\bf\ity');
axis([0 2*pi -1.5 1.5]);
grid on;

subplot(2,3,2);
y = [2 2 3; 2 5 6; 2 8 9; 2 11 12];
bar(y);
title('\bf Bar plot-1'); 
ylabel('\bf\ity');

subplot(2,3,3);
x = [1980 1990 2000];
y = [15 20 -5; 10 -17 21; -10 5 15];
bar(x,y,'stacked'); %可以实现堆叠
title('\bf Bar plot'); 
xlabel('\bf\itx');
ylabel('\bf\ity');

subplot(2,3,4);
x = [1980 1990 2000];
y = [40 50 63 52; 42 55 50 48; 30 20 44 40];
barh(x,y)
xlabel('Snowfall')
ylabel('Year')
legend({'Springfield','Fairview','Bristol','Jamesville'},'Location','SouthOutside')

subplot(2,3,5);
x = -1:0.1:1;
y = ( x / 2 ) .* sqrt(1-x.^2);
compass(x,y);
title('\bf Compass plot'); 
xlabel('\bf\itx');
ylabel('\bf\ity');

subplot(2,3,6);
x = 0:pi/4:2*pi; 
y = sin(x); 
stairs(x,y);
title('\bf Stair plot'); 
xlabel('\bf\itx');
ylabel('\bf\ity');
axis([0 2*pi -1.5 1.5]);
grid on;
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-21.jpg)

饼状图和前面的图有一点点不同。把数组x传递给函数pie，函数计算出每个元素占全部元素和的百分比。

`pie`也支持选择性参数`eplode`，它是一个逻辑数组，包含元素1和0。当`explode`=1时，**它对应的扇区从整体中分离出来**。

```matlab
data = [10 37 5 6 6]; 
explode = [0 1 0 0 0];
pie(data, explode); 
title('\bfExample of a Pie Plot');
legend('One','Two','Three','Four','Five','Location','SouthOutside');
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-22.jpg)

#### (2) 作图函数

前面提到的作图，都必须要先创建数组。

**直接做出图象，而不需要创建中间数据数组的函数：`ezplot`、`fplot`**

**！！！注意：matlab官网中更为推荐`fplot`函数！！！**

```matlab
fplot(f)  % 在默认区间[-5,5]（对于x）绘制由函数y=f(x)定义的曲线
fplot(f,xinterval) % 在指定区间绘图；xinterval是区间，应当指定为[xmin,xmax]形式的二元素向量
fplot(funx,funy) % 在默认区间[-5,5]（对于t）绘制由x=funx(t)和y=funy(t)这样的参数方程定义的曲线。
fplot(funx,funy,tinterval) % 将在指定区间绘图。将区间指定为 [tmin tmax] 形式的二元素向量。
```

```matlab
subplot(1,2,1); % 参数方程的图象
xt = @(t) cos(3*t);
yt = @(t) sin(2*t);
fplot(xt,yt);
xlabel('x');
ylabel('y');
grid on;

subplot(1,2,2); % 分段函数
fplot(@(x) exp(x),[-3 0],'b');
hold on;
fplot(@(x) cos(x),[0 3],'b');
hold off;
xlabel('x');
ylabel('y');
grid on;
```

<img src="C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-23.jpg" style="zoom: 67%;" />

#### (3) 柱状图

标准的matlab柱状图函数为hist。

**不推荐使用 `hist`。请改用 [`histogram`](https://ww2.mathworks.cn/help/matlab/ref/matlab.graphics.chart.primitive.histogram.html)。**

> 直方图属于数值数据的条形图类型，将数据分组为 bin。创建 `Histogram` 对象后，可以通过更改直方图的属性值修改它的各个方面。这对快速修改 bin 属性或更改显示特别有用。

函数`histogram`的用法：

```matlab
histogram(X) % 基于 X 创建直方图。histogram 函数使用自动 bin 划分算法，然后返回均匀宽度的 bin，这些 bin 可涵盖 X 中的元素范围并显示分布的基本形状。
% 参数X为要分布到各 bin 的数据，指定为向量、矩阵或多维数组。如果 X 不是向量，则 histogram 将它视作单列向量 X(:) 并绘制一个直方图。
histogram(X,nbins) % 创建以nbis为宽度的柱状图
% 使用标量 nbins 指定的 bin 数量。
% bin 数量，指定为正整数。如果不指定 nbins，则 histogram 基于 X 中的值自动计算将使用多少个 bin。示例： histogram(X,15) 创建一个带 15 个 bin 的直方图。

```

示例：

```matlab
x = randn(10000,1);
h = histogram(x)
```

绘图：

<img src="D:\matlab学习\test\untitled-1.bmp" style="zoom:67%;" />

```matlab
h = 

  Histogram - 属性:

             Data: [10000×1 double]
           Values: [1×39 double]
          NumBins: 39
         BinEdges: [1×40 double]
         BinWidth: 0.2000
        BinLimits: [-3.4000 4.4000]
    Normalization: 'count'
        FaceColor: 'auto'
        EdgeColor: [0 0 0]
```

### 4. 三维作图

一般情况下，三维图象常用于显示以下两类数据。 

1. 两个变量是同一自变量的函数，当你希望显示自变量重要性时，你可以用三维作图表示。

2.  一个变量是另外两个变量的函数。

#### （1）三维曲线作图

三维曲线作图最简单的函数是：

```matlab
plot(x,y,z);
```

示例：

```
t = 0:0.1:10; 
x = exp(-0.2*t) .* cos(2*t); 
y = exp(-0.2*t) .* sin(2*t); 
plot3(x,y,t); 
title('\bfThree-Dimensional Line Plot'); 
xlabel('\bfx'); 
ylabel('\bfy'); 
zlabel('\bfTime'); 
axis square;
grid on;
```

图像：

<img src="D:\matlab学习\test\untitled-2.bmp" style="zoom:67%;" />

#### （2）三维表面，网格，等高线图像

表面，网格，等高线图象是非常简单的方法来表示两变量的函数。

数组x, y, z分别表示每个点的坐标值，函数分别如下：

![image-20210808134651190](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210808134651190.png)

`counter`函数显示的是x,y二维平面的等高线显示。

matlab中`meshgrid`函数使得函数图像数组x,y的创建十分容易。

```matlab
[X,Y] = meshgrid(x,y) % 基于向量 x 和 y 中包含的坐标返回二维网格坐标。
% X 是一个矩阵，每一行是 x 的一个副本；Y 也是一个矩阵，每一列是 y 的一个副本。坐标 X 和 Y 表示的网格有 length(y) 个行和 length(x) 个列。
```

示例：

```matlab
[x,y] = meshgrid(-4:0.2:4,-4:0.2:4);
z = exp(-0.5*(x.^2+y.^2)); 
subplot(2,2,1);
mesh(x,y,z);
subplot(2,2,2);
surf(x,y,z);
subplot(2,2,3);
contour(x,y,z);
xlabel('\bfx'); 
ylabel('\bfy');
zlabel('\bfz');
```

函数图像：

![](D:\matlab学习\test\untitled-3.bmp)

TBC























# 知乎总结















































# 作业总结

## 1. 点电荷的电位分布

### (1) 函数总结

#### meshgrid——二维或三维网格，取坐标

[meshgrid 的语法](https://ww2.mathworks.cn/help/matlab/ref/meshgrid.html)

```matlab
[X,Y] = meshgrid(x,y) %基于向量 x 和 y 中包含的坐标返回二维网格坐标。X 是一个矩阵，每一行是 x 的一个副本；Y 也是一个矩阵，每一列是 y 的一个副本。坐标 X 和 Y 表示的网格有 length(y) 个行和 length(x) 个列。
[X,Y,Z] = meshgrid(x,y,z) %返回由向量 x、y 和 z 定义的三维网格坐标。X、Y 和 Z 表示的网格的大小为 length(y)×length(x)×length(z)。
```

可以利用向量x定义的x坐标和向量y定义的y坐标创建二维网格坐标[X,Y]。

然后在二维网格上计算关于x,y的表达式时，就可以直接用X,Y。

```matlab
>> x = 1:3;
y = 1:5;
[X,Y] = meshgrid(x,y)

X =

     1     2     3
     1     2     3
     1     2     3
     1     2     3
     1     2     3


Y =

     1     1     1
     2     2     2
     3     3     3
     4     4     4
     5     5     5

>> X.^2 + Y.^2

ans =

     2     5    10
     5     8    13
    10    13    18
    17    20    25
    26    29    34
```

#### contour——矩阵的等高线

[contour的语法](https://ww2.mathworks.cn/help/matlab/ref/contour.html)

```matlab
contour(Z) %创建一个包含矩阵 Z 的等值线的等高线图，其中 Z 包含 x-y 平面上的高度值。MATLAB® 会自动选择要显示的等高线。Z 的列和行索引分别是平面中的 x 和 y 坐标。
contour(X,Y,Z) %指定 Z 中各值的 x 和 y 坐标。
contour(___,levels) %将要显示的等高线指定为上述任一语法中的最后一个参数。将 levels 指定为标量值 n，以在 n 个自动选择的层级（高度）上显示等高线。要在某些特定高度绘制等高线，请将 levels 指定为单调递增值的向量。要在一个高度 (k) 绘制等高线，请将 levels 指定为二元素行向量 [k k]。
contour(___,Name,Value) %使用一个或多个名称-值对组参数指定等高线图的其他选项。请在所有其他输入参数之后指定这些选项。有关属性列表，请参阅 Contour 属性。
```

```matlab
x = linspace(-2*pi,2*pi);
y = linspace(0,4*pi);
[X,Y] = meshgrid(x,y);
Z = sin(X)+cos(Y);
contour(X,Y,Z)
```

![](C:\Users\lenovo\Pictures\Saved Pictures\matlab test 1-24.jpg)

#### linspace——生成线性间距向量

`linspace` 类似于冒号运算符“`:`”，但可以直接控制点数并始终包括端点。“`linspace`”名称中的“`lin`”指示生成线性间距值而不是同级函数 `logspace`，后者会生成对数间距值。

```matlab
y = linspace(x1,x2) %返回包含 x1 和 x2 之间的 100 个等间距点的行向量。
y = linspace(x1,x2,n) %生成 n 个点。这些点的间距为 (x2-x1)/(n-1)。
```

### (2) matlab代码

```matlab
clear;
x=-100:100;
y=-100:100;
[X,Y]=meshgrid(x,y);
r1=sqrt((X+10.5).^2+Y.^2);
r2=sqrt((X-10.5).^2+Y.^2);
U=2./r1-1./r2;
u=-0.5:0.002:0.5;
figure (1);
contour(X,Y,U,u);
hold on;
plot(-10.5,0,'.','MarkerEdgeColor','r','MarkerSize',15);
plot(10.5,0,'.','MarkerEdgeColor','b','MarkerSize',15);
axis equal;
grid on;
title('正负点电荷电量比为2的等势线','FontSize',15,'FontName','msyh')
xlabel('x','FontSize',16)
ylabel('y','FontSize',16)
```

![](D:\电磁场与波\作业\电量比为2的等电位图.jpg)

























