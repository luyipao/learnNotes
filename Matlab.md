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
