## 头文件

 引用跳转：\usepackage[backref]{hyperref} 

对于单独的数学公式，采用`$$<return>...<return>$$`的形式来书写可以兼容markdown语法中的代码块。其中`<return>`表示回车。但是一般而言用`\[...\]`来表示未标号数学公式，因为前者是命令而后者才是latex语法，并且有更好的性质。



空行和`\\`：空行表示另起一段，`\\`表示换行但还是同一段。直观来说前者有缩进，后者无缩进。

空行在latex中被当作另一段，数学公式当作纯文本。类似下面

> If we define f(x) as 
> $$
> f(x) = 1 + x^2 + x^3 + \cdots + x^n + \cdots,
> $$
> then we have f(x) = exp(x).

即使公式另起一行，我们依然把他当作连续的文本，标点符号直接添加。

## 数学公式

### 方程式

#### align

每行都有编号，默认后对齐，可以使用`&`对齐，`&`可以有多个，例如

```
\begin{align}
x&=y           &  w &=z              &  a&=b+c\\
2x&=-y         &  3w&=\frac{1}{2}z   &  a&=b\\
-4 + 5x&=2+y   &  w+2&=-1+w          &  ab&=cb
\end{align}
```

编译后得到
$$
\begin{align*}
x&=y           &  w &=z              &  a&=b+c\\
2x&=-y         &  3w&=\frac{1}{2}z   &  a&=b\\
-4 + 5x&=2+y   &  w+2&=-1+w          &  ab&=cb
\end{align*}
$$

#### gather

每行都有编号，居中对齐。

#### equation

把里面的方程看作一个整体，只给一个编号。可以与`aligned`和`gathered`嵌套使用。

无法使用`&`对齐符，`\\`换行。

#### split

连等

```latex
\begin{equation}
\begin{split}
	f(x) & = x + x \\
		 & = 2x
\end{split}
\end{equation}
```

$$
\begin{align*}
	f(x) &= x + x \\
		 &= 2x
\end{align*}
$$

#### 长方程式

```latex
\begin{multline*}
p(x) = 3x^6 + 14x^5y + 590x^4y^2 + 19x^3y^3\\ 
- 12x^2y^4 - 12xy^5 + 2y^6 - a^3b^3
\end{multline*}
```

$$
\begin{multline*}
p(x) = 3x^6 + 14x^5y + 590x^4y^2 + 19x^3y^3\\ 
- 12x^2y^4 - 12xy^5 + 2y^6 - a^3b^3
\end{multline*}
$$

## 特殊符号

```text
\tbinom{n}{r}
```

$$
\tbinom{n}{r}
$$

### 长等号

>x \xlongequal{conditiion} b

$$
x \xlongequal{conditiion} b
$$

### 表格换行

> \begin{tabular}{|p{3cm}|p{3cm}|p{3cm}|}
>
>   \*\** & \*\** & *\*\*& 
>
> \end{tabular}

当超过3厘米，自动换行。



自动出现$$

在目录C:\Users\用户名\.vscode\extensions\james-yu.latex-workshop-版本号\syntax\latex-language-configuration.json文件中，找到一项autoClosingPairs，在其中添加[ “$”, “$” ]即可。

再settings中调整自动补全带出现时间

#### 反向搜索

> //注意修改成自己的安装路径
> "D:\Softwares\Microsoft VS Code\Code.exe" "D:\Softwares\Microsoft VS Code\resources\app\out\cli.js"  --ms-enable-electron-run-as-node -r -g "%f:%l"

https://blog.csdn.net/GoodNightBaby/article/details/122037853

矩阵。pmatrix

行列式。vmatrix

laplace算子。Delta

nabla算子。nabla

boldsymbol。向量

perp。垂直

## elegentbook

> **\****documentclass**[lang=cn,newtx,10pt,scheme=chinese]{elegantbook}
>
> \setcounter{tocdepth}{2}
>
> \newcommand\bs[1]{\boldsymbol{#1}}
>
> \title{}
>
> \begin{document}
>
> \maketitle
>
> \frontmatter
>
> \tableofcontents
>
> \mainmatter
>
> \today
>
> \end{document}

lim下多行 $\lim\limits_{x \to x_0 \atop y \to y_0 } f(x,y) = A$

上方加波浪号 \widetilde

上方加横线 \overline



ref 显示没有定义，在equation 环境中使用了align 环境

空心圆  \circ

\quad 一个m的宽度  quadrat 的缩写

\oint 环绕积分

\iint 双重积分

\backslash  反斜号 （数学环境下

- epsilon: ε or ϵ
- theta: θ or ϑ
- kappa: κ or ϰ
- pi: π or ϖ
- rho: ρ or ϱ
- sigma: σ or ς
- phi: φ or ϕ

```
\newcommand\bs[1]{\boldsymbol{#1}}
\renewcommand{\epsilon}{\varepsilon}
\renewcommand{\theta}{\vartheta}
\renewcommand{\kappa}{\varkappa}
\renewcommand{\rho}{\varrho} % remember my teacher and friend Adalberto!
\renewcommand{\phi}{\varphi}

```

#### 表格

环境`array`是`math mode`，`tabular`是`text mode`。`tabular`是作为文本看待，要想另起一行需要加上`center`环境。

lcr：left center right 左对齐 居中 右对齐

\hline：横线

\usepackage{amsthm}: 内含proof环境，在证明结尾会加上方括号

∅：`$\emptyset$`或`$\empty$`

∅：`$\varnothing$`



并集：\cup

交集： \cap

真包含： \subset

包含：\\subseteq  

不真包含： \not\subset



```
enumitem package
enumberate 环境 
[label=(\roman*)] 罗马
[label=(\Alph*)] 大写字母
[label=(\alph*)] 小写字母
```

\noindent 取消缩进，可以保证相似的行对齐

\pm  加减号对应 \plus \minus

置于正下方



`(\d+)\/(\d+) -> \\frac{$1}{$2}` 将你所有a/b型的分数改写为\frac{a}{b}型



attrib *.synctex.gz +h +s 隐藏synctex.gz 类型的文件

attrib *.synctex.gz +h -s 恢复显示synctex.gz类型的文件

section 的七个等级，给分单元的狂热爱好者。`\part` and `\chapter` are only available in `report` and `book`.

- -1 `\part{part}`
- 0 `\chapter{chapter}`
- 1 `\section{section}`
- 2 `\subsection{subsection}`
- 3 `\subsubsection{subsubsection}`
- 4 `\paragraph{paragraph}`
- 5 `\subparagraph{subparagraph}`

figure环境中，latex放在caption后面



## 矢量图

latex 支持矢量图格式 `svg`, `eps`, `pdf`

matlab 支持导出的矢量图格式 `PDF`、`EPS`  `EMF`

由于eps没有颜色，我建议选择PDF格式，此外PDF格式还具有更小的体积

## minipage

https://www.sascha-frank.com/latex-minipage.html

When adjusting the choices is: c (for centers) t (for top) and b (for bottom). By default, c is used for centering. It is aligned by t and/or b at the highest (top line) and/or at the lowest line (bottom line).

Besides there are still further options, which however in practical application the minipage does not play a role like the height and the adjustment (again c, t and b) within the minipage.

Example of further options

```
\begin{minipage}[t][5cm][b]{0,5\textwidth}
```

This minipage now has a defined height of 5cm, and the content will now be aligned to the bottom of the minipage.

A mistake that is often made is, there is a blank line between the \end{minipage} and \begin{minipage} left. Then the pages are no longer together.

minipage指定宽度，而高度会随着内容自动调整。为了让两个并列的minipage中的图片具有相同的size，我们需要固定二者的高度即可，

## linewidth textwidth

- `\hsize` is a TeX primitive that should not be usually used in LaTeX
- `\textwidth` is the (constant) width of the total text block
- `\columnwidth` is the (constant) width of a single column of text
  (which is the same as `\textwidth` for a single column document)
- `\linewidth` is a variable that represents the *current* size of the line of text, whether inside a column or a minipage or a list

In general, then, it's best to always use `\linewidth` if you are specifying the relative size of an image or a box, since it will adapt to the current situation.

**Note**: `\linewidth` also appears to work in *table* columns, not just text columns. See [this answer](https://tex.stackexchange.com/a/78296/13270) for an example where a fixed-width parbox is used within a table cell (actually a multirow cell)

