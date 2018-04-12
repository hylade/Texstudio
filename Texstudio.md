# Texstudio

##控制序列

此处的第一行 `\documentclass{article}` 中包含了一个控制序列（或称命令/标记）。所谓控制序列，是以反斜杠`\`开头，以第一个**空格或非字母** 的字符结束的一串文字，他们并不被输出，但是他们会影响输出文档的效果。这里的控制序列是 `documentclass`，它后面紧跟着的 `{article}` 代表这个控制序列有一个必要的参数，该参数的值为 `article`。这个控制序列的作用，是调用名为 “article” 的文档类

部分控制序列还有被方括号`[]`包括的可选参数



## %号使用

在 TeX 风格的文档中，从 “%” 开始，到该行末尾的所有字符，都会被 TeX 系统无视，只作为供人类阅读的注释。除非在 “%” 前加上反斜杠来取消这一特性



## 中文输入

```tex
\documentclass[UTF8]{ctexart}
\begin{document}
你好，world!
\end{document}
```



## 作者、标题、日期输入

```tex
\documentclass[UTF8]{ctexart}
\title{你好，world!}
\author{Liam}
\date{\today}
\begin{document}
\maketitle %该控制序列能将导言区中定义的标题、作者、日期安装预定的格式展现出来
你好，world!
\end{document}
```



## 章节和段落

如：

```tex
\documentclass[UTF8]{ctexart}
\title{你好，world!}
\author{Liam}
\date{\today}
\begin{document}
\maketitle
\section{你好中国}
中国在East Asia.
\subsection{Hello Beijing}
北京是capital of China.
\subsubsection{Hello Dongcheng District}
\paragraph{Tian'anmen Square}
is in the center of Beijing
\subparagraph{Chairman Mao}
is in the center of 天安门广场。
\subsection{Hello 山东}
\paragraph{山东大学} is one of the best university in 山东。
\end{document}

```



在article/ctexart中，定义了五个控制序列来调整行文结构：

```latex
\section{}
\subsection{}
\subsubsection{}
\paragraph{}
\subparagraph{}
```



此外，在report/ctexrep中，还有```\chapter{}```；在文档类book/ctexbook中，还有```\part{}```



## 插入目录

通过控制序列```\tableofcontents```，可以插入目录

若再```\maketitle```之前插入，则将分页，第一页为目录，第二页为内容；若再之后插入，则先为标题等，再显示目录，再显示内容



## 插入数学公式

需要在导言区加载 `amsmath` 宏包：

```latex
\usepackage{amsmath}
```



### 数学模式

LaTeX 的数学模式有两种：行内模式 (inline) 和行间模式 (display)。前者在正文的行文中，插入数学公式；后者独立排列单独成行，并自动居中

在行文中，使用 `$ ... $` 可以插入行内公式，使用 `\[ ... \]` 可以插入行间公式，如果需要对行间公式进行编号，则可以使用 `equation` 环境

```latex
\begin{equation}
………
\end{equation}
```



### 公式标点规范

行内公式的标点，应该放在数学模式的限定符之外，而行间公式则应该放在数学模式限定符之内



### 上下标

需要表示上标，可以使用 `^` 来实现（下标则是 `_`）。**它默认只作用于之后的一个字符**，如果想对连续的几个字符起作用，请将这些字符用花括号 `{}` 括起来，例如：

```latex
\[z = r\cdot e^{2\pi}.\]
```



### 根式与分式

根式用 `\sqrt{·}` 来表示，分式用 `\frac{·}{·}` 来表示（第一个参数为分子，第二个为分母）

```latex
\documentclass{article}
\usepackage{amsmath}
\begin{document}
$\sqrt{x}$, $\frac{1}{2}$.

\[ \sqrt{x}, \]

\[ \frac{1}{2}. \]
\end{document}
```



### 运算符

一些小的运算符，可以在数学模式下直接输入；另一些需要用控制序列生成，如

```latex
\pm\; %省略号 
\times \; %乘号 
\div\; %除号 
\cdot\; %点号
\cap\; %∩
\cup\; %∪
\geq\; %>=
\leq\; %<=
\neq\; %≠
\approx \; %≈
\equiv \; %≡
```



连加、连乘、极限、积分等大型运算符分别用 `\sum`, `\prod`, `\lim`, `\int`生成。他们的上下标在行内公式中被压缩，以适应行高。我们可以用 `\limits` 和 `\nolimits` 来强制显式地指定是否压缩这些上下标。例如：

``` latex
$ \sum_{i=1}^n i\quad \prod_{i=1}^n $
$ \sum\limits _{i=1}^n i\quad \prod\limits _{i=1}^n $
\[ \lim_{x\to0}x^2 \quad \int_a^b x^2 dx \]
\[ \lim\nolimits _{x\to0}x^2\quad \int\nolimits_a^b x^2 dx \]
```



多重积分可以使用 `\iint`, `\iiint`, `\iiiint`, `\idotsint` 等命令输入。

```latex
\[ \iint\quad \iiint\quad \iiiint\quad \idotsint \]
```

​	

## 定界符

各种括号用 `()`, `[]`, `\{\}`, `\langle\rangle` 等命令表示；注意花括号通常用来输入命令和环境的参数，所以在数学公式中它们前面要加 `\`。因为 LaTeX 中 `|` 和 `\|` 的应用过于随意，amsmath 宏包推荐用 `\lvert\rvert`和 `\lVert\rVert` 取而代之



```latex
\[ \Biggl(\biggl(\Bigl(\bigl((x)\bigr)\Bigr)\biggr)\Biggr) \]
\[ \Biggl[\biggl[\Bigl[\bigl[[x]\bigr]\Bigr]\biggr]\Biggr] \]
\[ \Biggl \{\biggl \{\Bigl \{\bigl \{\{x\}\bigr \}\Bigr \}\biggr \}\Biggr\} \]
\[ \Biggl\langle\biggl\langle\Bigl\langle\bigl\langle\langle x
\rangle\bigr\rangle\Bigr\rangle\biggr\rangle\Biggr\rangle \]
\[ \Biggl\lvert\biggl\lvert\Bigl\lvert\bigl\lvert\lvert x
\rvert\bigr\rvert\Bigr\rvert\biggr\rvert\Biggr\rvert \]
\[ \Biggl\lVert\biggl\lVert\Bigl\lVert\bigl\lVert\lVert x
\rVert\bigr\rVert\Bigr\rVert\biggr\rVert\Biggr\rVert \]
```


## 省略号

省略号用 `\dots`, `\cdots`, `\vdots`, `\ddots` 等命令表示。`\dots` 和 `\cdots` 的纵向位置不同，前者一般用于有下标的序列。

```latex
\[ x_1,x_2,\dots ,x_n\quad 1,2,\cdots ,n\quad
\vdots\quad \ddots \]
```



## 矩阵

`amsmath` 的 `pmatrix`, `bmatrix`, `Bmatrix`, `vmatrix`, `Vmatrix` 等环境可以在矩阵两边加上各种分隔符。

```latex
\[ \begin{pmatrix} a&b\\c&d \end{pmatrix} \quad
\begin{bmatrix} a&b\\c&d \end{bmatrix} \quad
\begin{Bmatrix} a&b\\c&d \end{Bmatrix} \quad
\begin{vmatrix} a&b\\c&d \end{vmatrix} \quad
\begin{Vmatrix} a&b\\c&d \end{Vmatrix} \]
```



### 小矩阵

使用 `smallmatrix` 环境，可以生成行内公式的小矩阵。

```latex
Marry has a little matrix $ ( \begin{smallmatrix} a&b\\c&d \end{smallmatrix} ) $.
```



## 多行公式

### 长公式

#### 不对齐

无须对齐的长公式可以使用 `multline` 环境。

```latex
\begin{multline}
x = a+b+c+{} \\
d+e+f+g
\end{multline} %当不需要编号时，可以使用multline*代替
```



#### 对齐

需要对齐的公式，可以使用 `aligned` *次环境*来实现，它必须包含在数学环境之内。

```latex
\[\begin{aligned}
x ={}& a+b+c+{} \\
&d+e+f+g
\end{aligned}\]
```



#### 公式组

无需对齐的公式组可以使用 `gather` 环境，需要对齐的公式组可以使用 `align` 环境。他们都带有编号，如果不需要编号可以使用带星花的版本。

```latex
\begin{gather}
a = b+c+d \\
x = y+z
\end{gather}

\begin{align}
a &= b+c+d \\
x &= y+z
\end{align}
```



#### 分段函数

分段函数可以用`cases`次环境来实现，它必须包含在数学环境之内。

```latex
\[ y= \begin{cases}
-x,\quad x\leq 0 \\
x,\quad x>0
\end{cases} \]
```



## 插入图片和表格

### 图片

用 `graphicx` 宏包提供的 `\includegraphics` 命令。比如你在你的 TeX 源文件同目录下，有名为 `a.jpg` 的图片，你可以用这样的方式将它插入到输出文档中：

```latex
\documentclass{article}
\usepackage{graphicx}
\begin{document}
\includegraphics{a.jpg}
\end{document}
```



图片可能很大，超过了输出文件的纸张大小，或者干脆就是你自己觉得输出的效果不爽。这时候你可以用 `\includegraphics` 控制序列的可选参数来控制。比如

```latex
\includegraphics[width = .8\textwidth]{a.jpg}
```



### 表格

`tabular` 环境提供了最简单的表格功能。它用 `\hline` 命令表示横线，在列格式中用 `|` 表示竖线；用 `&` 来分列，用 `\\` 来换行；每列可以采用居左、居中、居右等横向对齐方式，分别用 `l`、`c`、`r` 来表示

```latex
\begin{tabular}{|l|c|r|}
 \hline
操作系统& 发行版& 编辑器\\
 \hline
Windows & MikTeX & TexMakerX \\
 \hline
Unix/Linux & teTeX & Kile \\
 \hline
Mac OS & MacTeX & TeXShop \\
 \hline
通用& TeX Live & TeXworks \\
 \hline
\end{tabular}
```



### 浮动体

插图和表格通常需要占据大块空间，所以在文字处理软件中我们经常需要调整他们的位置。`figure` 和 `table` 环境可以自动完成这样的任务；这种自动调整位置的环境称作浮动体(float)。我们以 `figure` 为例

```latex
\begin{figure}[htbp]
\centering
\includegraphics{a.jpg}
\caption{有图有真相}
\label{fig:myphoto}
\end{figure}
```

“htbp” 选项用来指定插图的理想位置，这几个字母分别代表here, top, bottom, float page，也就是就这里、页顶、页尾、浮动页(专门放浮动体的单独页面) 。`\centering` 用来使插图居中；`\caption` 命令设置插图标题，LaTeX 会自动给浮动体的标题加上编号。注意 `\label` 应该放在标题命令之后



## 版面设置

### 页边距

设置页边距，推荐使用 `geometry` 宏包。可以在[这里](http://texdoc.net/texmf-dist/doc/latex/geometry/geometry.pdf)查看它的说明文档。

比如我希望，将纸张的长度设置为 20cm、宽度设置为 15cm、左边距 1cm、右边距 2cm、上边距 3cm、下边距 4cm，可以在导言区加上这样几行：

```latex
\usepackage{geometry}
\geometry{papersize={20cm,15cm}}
\geometry{left=1cm,right=2cm,top=3cm,bottom=4cm}
```



### 页眉页脚

设置页眉页脚，推荐使用 `fancyhdr` 宏包

在页眉左边写上我的名字，中间写上今天的日期，右边写上我的电话；页脚的正中写上页码；页眉和正文之间有一道宽为 0.4pt 的横线分割，可以在导言区加上如下几行：

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
\lhead{\author}
\chead{\date}
\rhead{152xxxxxxxx}
\lfoot{}
\cfoot{\thepage}
\rfoot{}
\renewcommand{\headrulewidth}{0.4pt}
\renewcommand{\headwidth}{\textwidth}
\renewcommand{\footrulewidth}{0pt}
```



### 首行缩进

`CTeX` 宏集已经处理好了首行缩进的问题（自然段前空两格汉字宽度）



### 行间距

我们可以通过 `setspace`宏包提供的命令来调整行间距。比如在导言区添加如下内容，可以将行距设置为字号的 1.5 倍：

```latex
\usepackage{setspace}
\onehalfspacing
```



###段间距

可以通过修改长度 `\parskip` 的值来调整段间距。例如在导言区添加以下内容

```latex
\addtolength{\parskip}{.4em}
```

则可以在原有的基础上，增加段间距 0.4em。如果需要减小段间距，只需将该数值改为负值即可	