# Matlab 使用手册

## 画图

### 对于随着循环变化的标题

```matlab
legend_str = {}
for ii = 1:n
	plot(x,y);
	legend_str{end + 1} = printf("%s", rats(alpha)); %rats()，将数以分数的形式输出
end
legend(legend_str);
```

### 坐标轴的调整和参数

```matlab
% 指定坐标轴刻度值和标签
xticks([n/2, n]);
xticklabels(["n/2", "n"]);

%% 调整坐标轴到y=0
% 在y=0处绘制一条水平线
line([min(x), max(x)], [0, 0], 'Color', 'black');
ax = gca; %获取当前轴对象
ax.XAxisLocation = 'origin'; %'top', 'bottom', 'origin'
```

## 数字处理

### 矩阵

### 上三角&下三角

triu(A)是A的上三角，包含对角，triu(A, 1)不包含对角

tril(A)是A的下三角，包含对角，tril(A, -1)不包含对角

```
X = [name,' will be ',num2str(age),' this year.'];
```



## 定义函数

由于matlab的函数一般支持数组级运算，因此定义函数时也要提供数组级运算支持

比如

```matlab
function y = f1(x)
	y = @(x) 1;
end
function y = f2(x)
	y = @(x) 0*x + 1;
end
quadgk(f,0,1);
```

f1会出错，f2正常运行。因为f1，matlab会把他当作常值函数来处理。

## 全局变量  global 

全局变量的好处，简化函数input。

用法：global关键词作用于比所在位置低的域。比如定义在函数外的能作用于全体，函数内部的可以作用于本身和子函数。更具体来说，是global 作用于该关键词以下的部分。

如果想要在函数内使用global 关键词，需要声明 global x 表示你要使用全局变量x了。之后对x的更改将影响全局变量中x的值。

如果不声明global 而在函数中引入新的x，那么将不影响全局变量的值。

## 风格

### 变量

小写开头，大小写混合

循环变量使用i，j，k作为前缀，但当数据中存在复数，应禁用i，j

不要用关键词作为变量名

少用数字。可能会改变的数字用常数替代

0.5 而不是.5

小心浮点树的比较

### 常数

常数（包括全局变量） 应该用大写，使用下划线分割

### 函数

函数名应该说明用途

采用小写字母，或者遵循变量命名规则

避免意义不明的缩写

#### 前缀

访问：get/set

计算：compute

查找：find

创建：initialize

布尔：is



#### 子函数

只被另外一个函数调用的函数应该作为一个子函数写在同一个文件中。

#### 测试脚本

为每一个函数写一个测试脚本。

### 条件语句

避免复杂的条件表达式，采用临时逻辑变量替换

### 循环语句

循环变量应该在循环开始前立即被赋值

少用break 和continue

嵌套循环时在end行加注释有助于分析循环体的结构

## 定义函数

如果定义某个函数g用到函数f，且f除此外不被使用，那么应将f定义转移到g中。

## 平行运算

为了尽可能利用计算资源，我们考虑parallel computing。

使用Parallel Computing Toolbox，我们可以使用parallel computing tools， 使用GPU加速。

一些术语：

* Node：独立的计算机，包含一个或多个CPU或GPU。Node可以连接形成cluster或者超级计算机。
* Thread：最小的指令集，可以被计划表独立处理。在GPU，多处理器或多核系统，多threads可以被同时执行。

函数：

parfor ，设置M=0，来测试循环是否能无序，可用于debug

ticBytes(gcp)和tocBytes(gcP)放在parfor循环前后记录传递到workders的数据量。

gpuArray 创建储存在GPU的数组，可以在GPU中运算最后在返回CPU，以此利用GPU的算力。

问题来了，我们什么时候采用并行呢？

简单来说如果并行开销 parallel overhead  小于并行节省的时间，那么我们可以选择并行。具体而言当一个loop所使用的数据量越大，经过一次loop所需时间越小，那么并行收益越低。

通常我们没法改变loop，因此往往需要限制写入loop的数据大小（这些数据会整个地分配到每个线程，因此会产生N倍的io开销）

因此我们希望变量是sliced，对于特定的loop，我们指写入特定的slice，以此减少读写数据带来的并行开销。

那么变量如何sliced呢

如果parfor-loop中的一个变量满足下列**所有**性质，那么它是可以sliced

* 第一层的索引类型为圆括号()或花括号{}。
* 固定的索引列表，也就是说不能既有A(i)又有A(i+1)
* 索引列表中只有一个索引是涉及循环变量的
* 数组形状在赋值过程中保持不变

## for

for中创造的变量再for循环全部结束后才会被free，所以会for循环会产生非常多的内存消耗。

## 匿名函数

matlab的函数句柄是一个工作区，里面存放了该匿名函数依赖的所有函数。

如如果你创造了一个h=@(x) f(x) + g(x)，那么f和g就会再h的工作区内。即使clear f g，h的工作区内仍然会保留f和g，h也能正常工作。

```
functions(f).workspace
```

将返回一个struct来查看f的workspace。如果在f中使用了某个class的成员，那么f会将整个class储存在f的workspace，不用说，这将造成极大的内存浪费。

## arrayfun

B= arrayfun(f,A)，等价于B(i) = f(A(i))，相当于f不支持向量化运算，那么利用这个函数可以在外部实现向量化。

## cellfun

和arrayfun 一样只不过A是cell

## reshape

reshape(A,m,n)：重新排列

## table

T = table(a', b', c', 'VariableNames', {'A', 'B', 'C'});

但是我们有表格数据格式要求，我们可以采用num2str函数[s = num2str(A,formatSpec)](https://www.mathworks.com/help/matlab/ref/num2str.html?searchHighlight=num2str&s_tid=srchtitle_support_results_1_num2str#d126e1103941)

%u 十进制整数

%f 浮点数 num2str(order,'%.2f')

%e 指数符号，数值 num2str(E, '%.2e')

T.(n).(m,:) = '-'，第n列第m行的元素改为-，这可以用来处理没有表格中没有数据的元素

table2latex(T, filename)：将table转换为latex中的table，这不是matlab原生的函数，但网上有分享的函数文件

## plot

```matlab
plot(x, y);
lgd = legend('Name1', 'Name2');
lgd.FontSize = 14; % 调整变量名大小
lgd.Location = 'northwest' % 
% 使用LaTeX语法命名X轴和Y轴标签
xlabel('$数学公式$','Interpreter','latex');
ylabel('$数学公式$','Interpreter','latex');

% 开启次刻度显示
ax = gca;       % gca 用于获取当前的 axes 对象
ax.XMinorTick = 'on';
ax.YMinorTick = 'on';
```

Location的可选参数

| `north`              | Inside top of axes                                           |
| -------------------- | ------------------------------------------------------------ |
| `'south'`            | Inside bottom of axes                                        |
| `'east'`             | Inside right of axes                                         |
| `'west'`             | Inside left of axes                                          |
| `'northeast'`        | Inside top-right of axes (default for 2-D axes)              |
| `'northwest'`        | Inside top-left of axes                                      |
| `'southeast'`        | Inside bottom-right of axes                                  |
| `'southwest'`        | Inside bottom-left of axes                                   |
| `'northoutside'`     | Above the axes                                               |
| `'southoutside'`     | Below the axes                                               |
| `'eastoutside'`      | To the right of the axes                                     |
| `'westoutside'`      | To the left of the axes                                      |
| `'northeastoutside'` | Outside top-right corner of the axes (default for 3-D axes)  |
| `'northwestoutside'` | Outside top-left corner of the axes                          |
| `'southeastoutside'` | Outside bottom-right corner of the axes                      |
| `'southwestoutside'` | Outside bottom-left corner of the axes                       |
| `'best'`             | Inside axes where least conflict with data in plot           |
| `'bestoutside'`      | Outside top-right corner of the axes (when the legend has a vertical orientation) or below the axes (when the legend has a horizontal orientation) |
| `'layout'`           | A tile in a tiled chart layout. To move the legend to a different tile, set the `Layout` property of the legend. |
| `'none'`             | Determined by `Position` property. Use the `Position` property to specify a custom location. |

## exportgraphics

使用这个来保存图片而不是save。优点是不会流出多余的边界空白（margins）

## figure

创建图像窗口

`gca`： 返回当前图窗中的当前坐标区。当前坐标去包括 plot, title ,xlim。 图窗的CurrentAxes属性储存其当前坐标区。

更好的做法是在创建坐标区或图时将其赋给某个变量，而不是依赖 `gca`。

`gcf`：返回当前图窗的句柄。

`cla`：清除坐标区的所有可见图形。

`close all`：清除所有图片
