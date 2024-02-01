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
