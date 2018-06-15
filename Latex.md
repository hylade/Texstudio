#Texstudio

##中文乱码问题

将选项->设置->编辑器->Default Font Encoding 选择UTF-8

## 解决Editor中输入中文重叠和光标定位不准的问题

把“Disable cache of character witdh" 打勾



##如何在TexSduio中使用JabRef来插入文献,自动生成文献列表的问题

先在Bib Tex中编写参考文献源文件，如：

```latex
@article{name01, 
author = {作者, 多个作者用 and 连接}, 
title = {标题}, 
journal = {期刊名}, 
volume = {卷号}, 
number = {页码}, 
year = {年份}, 
abstract = {摘要, 这个主要是引用的时候自己参考的, 这一行不是必须的} 
} 

@book{name02, 
author ="作者", 
year="年份", 
title="书名", 
publisher ="出版社名称" 
}
```

在LaTeX源文件末尾，```\end{document}```之前添加一下两行代码： 

```latex
\bibliographystyle{preference_template} 
\bibliography{BibTeX file} 
%其中，第一行代码的大括号中的内容为参考文献的模板的文件名(不加后缀)，标准的模板名为plain 
%第二行代码中的大括号中的内容为参考文件源文件的文件名(不加后缀)
```

生成参考文献列表 
1)将模板文件(.bst)和BibTeX文件(.bib)文件存放在LaTeX当前目录下。 
2)然后使用TexStudio编译源文件(.tex)【F6】，生成对应的aux文件。 
3)在对应的位置添加参考文献引用的标签（使用\cite{参考文献标签}） 
4)使用BibTeX编译器编译BibTeX文件【F8】，生成对应的bbl文件 
5)再次编译源文件【F6】，关联参考文献，生成参考文献列表。

或者：

1.先在tex里加上两个宏包

```latex
\usepackage{cite}
\usepackage{hyperref}
```

在要插入文献的位置，添加

```latex
\usepackage{cite}
\usepackage{hyperref}
```



## latex中如何设置sci期刊名

```latex
%开头添加: 
\documentclass[journal,twoside]{IEEEtran}
%tex文中采用
\markboth{xxx-期刊名}{xxx-文章题目信息等}
%最终显示的是{xxx-文章题目信息等}
```



## 如何通过单击显示窗口文字跳转到源文件相应的位置

按住```ctrl```，单击文字即可

```latex
%----------------------------------------------------------------------------------------
Date：2018.4.16
```

------



## 算法代码排版——latex2e使用

```latex
\documentclass{article}
\usepackage[ruled]{algorithm2e}                 %算法排版样式1
%\usepackage[ruled,vlined]{algorithm2e}          %算法排版样式2
%\usepackage[linesnumbered,boxed]{algorithm2e}   %算法排版样式3
    
 \begin{document}
    How to use the algorithm2e in \LaTeX ~ file.
    Examples: 
%    ------------------------------Example - 1--------------------------------
        \begin{algorithm}[H]
            \caption{How to write algorithms}
            \KwIn{this text}
            \KwOut{how to write algorithm with \LaTeX2e }
            
            initialization\;
            \While{not at end of this document}{
                read current\;
                \eIf{understand}
                {
                        go to next section\;
                        current section becomes this one\;
                }
                {
                    go back to the beginning of current section\;
                }
        }
    \end{algorithm}
    
%    ---------------------------Example - 2-----------------------------------
    \begin{algorithm} 
%    \SetAlgoNoLine  %去掉之前的竖线
     \caption{identifyRowContext} 
      \KwIn{$r_i$, $Backgrd(T_i)$=${T_1,T_2,\ldots ,T_n}$ and similarity threshold $\theta_r$} 
      \KwOut{$con(r_i)$} 
        $con(r_i)= \Phi$\; 
        \For{$j=1;j \le n;j \ne i$} 
        { 
            float $maxSim=0$\; 
            $r^{maxSim}=null$\; 
            \While{not end of $T_j$} 
            { 
                compute Jaro($r_i,r_m$)($r_m\in T_j$)\; 
                \If{$(Jaro(r_i,r_m) \ge \theta_r)\wedge (Jaro(r_i,r_m)\ge r^{maxSim})$} 
                { 
                    replace $r^{maxSim}$ with $r_m$\; 
                } 
            } 
            $con(r_i)=con(r_i)\cup {r^{maxSim}}$\; 
        } 
        return $con(r_i)$\; 
    \end{algorithm}
    %------------------------------------------------------------------------------------
\end{document}
```

```latex
%当需要更改Input为输入，更改Output为输出时，需在算法内部插入
\SetKwInout{KIN}{输入}
\SetKwInout{KOUT}{输出}
%并用"\KIN"替代之前的"\KwIn","\KOUT"替代"\KwOut"
%上述方法需要在中文模式下进行，即需要在开始处添加"\usepackage{ctex}"
```



## 如何排列公式美观

```latex
%对于较短的公式，可以使用"\align"的方式
\begin{align}
  a & = b + c \\
  & = d + e
\end{align}
%但对于较长的公式，此时再使用"\align"的方式，则由于一行排不下如此多的字符，将换行，此时将产生问题
\begin{align}
  a & = b + c \\
  & = d + e + f + g + h + i
  + j + k + l \nonumber\\
  & + m + n + o \\
  & = p + q + r + s
\end{align}

%虽然可以使用"\hspace{}"来使相应的字符对齐，但仍不精准，此时可以使用"eqnarray"
\begin{eqnarray}
  a & = & b + c \\
  & = & d + e + f + g + h + i
  + j + k + l \nonumber\\
  && +\> m + n + o \\
  & = & p + q + r + s
\end{eqnarray}

%但eqnarray仍然具有一些缺点
%1.等号两边的空间过大
\begin{eqnarray}
  a & = & a = a
\end{eqnarray}

%2.表达式有时会与公式序号接触，即使左边的空间充足
\begin{eqnarray}
  a & = & b + c\\
  & = & d + e + f + g + h^2
  + i^2 + j
\label{eq:faultyeqnarray}
\end{eqnarray}

%3.当等式左边字符较多时，eqnarray环境提供了"\lefteqn{}"方法，但当等式右侧字符较少时，公式整体将不再居中
\begin{eqnarray}
\lefteqn{a + b + c + d + e + f + g + h}\nonumber\\
  & = & i + j + k + l + m \\
  & = & n + o + p + q + r + s
\end{eqnarray}    %此时等式右侧较长，较为美观

\begin{eqnarray}
\lefteqn{a + b + c + d + e + f + g + h} \nonumber\\
  & = & i + j
\end{eqnarray}    %此时等式右侧较短，极其丑陋
%----------------------------------------------------------------------------------------
%说了这么多，总结的结论竟然是不要使用eqnarray环境
```



那应该使用什么来使等式美观呢？使用IEEEeqnarray

```latex
%首先先要include IEEEarray工具包
\usepackage{IEEEtrantools}
```

对于IEEEeqnarray，可以规定作用的列数，使第一列右对齐，使中间列居中，并且具有稍大的空间，使第三列左对齐

```latex
\begin{IEEEeqnarray}{rCl}
  a & = & b + c \\
  & = & d + e + f + g + h + i + j + k \nonumber\\
  && +\> l + m + n + o \\
  & = & p + q + r + s
\end{IEEEeqnarray}
```

但我们可以规定具体的列数，如```{c}```只会产生一列，```{rCl"l}```将会产生第四列，且第三列将不会左对齐，而第四列将左对齐，第三列与第四列之间的空间，由```"```来确定



```latex
%对于equation方式，当等式较长时，公式序号可能会被强制挤到下一行，即使上一行还有空间
\begin{equation}
a = \sum_{k=1}^n\sum_{\ell=1}^n \sin \bigl(2\pi \, b_k \, c_{\ell} \, d_k \, e_{\ell} \,
f_k \, g_{\ell} \, h \bigr)
\end{equation}
```

这种情对于```IEEEeqnarray```不会发生，我们可以控制公式序号存在位置

```latex
\begin{IEEEeqnarray}{c}
a = \sum_{k=1}^n\sum_{\ell=1}^n \sin \bigl(2\pi \, b_k \, c_{\ell} \, d_k \, e_{\ell} \,
f_k \, g_{\ell} \, h \bigr)
\IEEEeqnarraynumspace
\label{eq:labelc1}
\end{IEEEeqnarray}
%or

\begin{IEEEeqnarray}{c}
a = \sum_{k=1}^n\sum_{\ell=1}^n \sin \bigl(2\pi \, b_k \, c_{\ell} \, d_k \, e_{\ell} \,
f_k \, g_{\ell} \, h \bigr)
\nonumber\\*
\label{eq:labelc2}
\end{IEEEeqnarray}
```



```latex
%对于equation，公式序号样式并不会根据字符环境变化
\textbf{\textit{\color{red}
  This is our main result:
\begin{equation}
  a = b + c
\end{equation}

%对于IEEEeqnarray，此时公式编号将发生相应的变化，较为美观

\textbf{\textit{\color{red}
  This is our main result:
\begin{IEEEeqnarray}{c}
  a = b + c
\end{IEEEeqnarray}}}
```

同时，也可以使IEEEeqnarray写法与equation写法相同

```latex
\renewcommand{\theequationdis}{{\normalfont (\theequation)}}
\renewcommand{\theIEEEsubequationdis}{{\normalfont (\theIEEEsubequation)}}
\textbf{\textit{\color{red}
This is our main result:
\begin{IEEEeqnarray}{rCl}
a & = & b + c \\
& = & d + e \IEEEyesnumber
\IEEEyessubnumber
\end{IEEEeqnarray}}}
```



对于多行等式的情况，需要```\IEEEeqnarraymulticol```

```latex
\begin{IEEEeqnarray*}{l}
a + b + c + d + e + f
\\ \qquad
+\> g + h + i + j + k + l
\qquad \\
\IEEEeqnarraymulticol{1}{r}{
+\> m + n + o + p + q }
\IEEEyesnumber
\end{IEEEeqnarray*}
```



当在IEEEeqnarray中，若公式与公式编号重叠时，可以使用```\IEEEeqnarraynumspace```



```latex
\begin{IEEEeqnarray}{rCl}
\IEEEeqnarraymulticol{3}{l}{
a + b + c + d + e + f
+ g + h
}\nonumber\\* \qquad\qquad
& = & i + j
\label{eq:label45}
\\
& = & k + l + m
\end{IEEEeqnarray}
%第一个参数{3}表示将三列合并为1列，并且根据第二个参数{l}，公式左对齐
%其中"\label"里是该公式的标签，将会在引用该公式时用到
```



```latex
\begin{IEEEeqnarray}{rCl}
a & = & b + c
\\
& = & d + e + f + g + h
+ i + j + k \nonumber\\
&& +\> l + m + n + o
\label{eq:add_space}
\\
& = & p + q + r + s
\end{IEEEeqnarray}
%在多行情况中，一行开始位置的"+"、"-"都被认为是一个信号，需要在符号和字符之间添加"\>"
```



在IEEEeqnarray中，对一元运算符和二元运算符往往难以辨别，当系统采用binary operator时，往往符号后面的空白会较大，而对于unary operator空间较小；unary的使用是正确的

要强制执行一元运算符，将一元运算符和/或一元运算符本身后面的表达式括入大括号{...}通常会起作用

需要采用binary operator时，可以在需要的地方添加```\>```

```latex
\begin{IEEEeqnarray*}{rCl’s}
a & = & - b - b - c
& (default unary) \\
& = & {-} {b} - b - c
& (default unary, no effect) \\
& = & -\> b - b - c
& (changed to binary) \\
& = & - \log b - b - d
& (default binary) \\
& = & {-} {\log b} - b - d
& (changed to unary) \\
& = & - \log b - b {-} d
& (changed $-d$ to unary)
\end{IEEEeqnarray*}
```



```latex
%对于IEEEeqnarray，将自动给公式编号，可以使用对IEEEeqnarray*可以取消所有编号
\IEEEyesnumber and \IEEEnonumber (or \nonumber).
%当需要给公式编号给出一个更小级别的编号时
\IEEEyessubnumber and \IEEEnosubnumber
%上述两种方法只能作用于语句被使用的代码中
%-----------------------------------------------------------------------------------------
\IEEEyesnumber*, \IEEEnonumber*,
\IEEEyessubnumber*, \IEEEnosubnumber*
%上述代码可以一直作用至IEEEeqnarray环境使用完毕，或者另一个星级命令被使用
%-----------------------------------------------------------------------------------------
%当需要大小编号都更换时，不能只输入"\IEEEyesnumber"，需要同时激活"\IEEEyessubnumber*"
\IEEEyesnumber
\IEEEyessubnumber*\\
%或者：
\IEEEyesnumber\label{eq:block}
\IEEEyessubnumber*
%此时对于需要
```

```latex
%-----------------------------------------------------------------------------------------
Date：2018.4.17
```

------

## 图片处理

Tex支持eps格式的矢量图

### eps图片的制作

①用Microsoft Office 中的Word或者Visio画出你需要的图形，将其另存为pdf文件。注意要一副图生成一个只有一页的pdf文件

②用Adobe Acrobat Professional打开该pdf文件，选择【工具】→【页面】→【剪裁】，设定好想要留下的区域（左图），双击，得到不含大片空白的pdf图片文件

③将剪裁好的pdf另存为eps格式，在另存对话框的下面有一个设置选项，设置里面一些参数，将一般的PostScript设为语言级三级，字体范围设为嵌入和引用的字体，然后确定保存



### eps图片的插入

当eps文件与Tex文件不在同一文件夹中时，需要在开头定义图片存储位置

```latex
\graghicspath{{../}}
```

图片插入示例：

```latex
\begin{figure}[ht]
\begin{flushleft}    %用于图片左对齐

\includegraphics[width=6cm,height=3.4cm]{SSDArchitecture.eps}	%图片长宽值可以省略，图片即为原大小；当只设定其中之一时，图片以长宽比不变的方式出现

\end{flushleft}
\caption{SSD Architecture}\label{fig:SSDArchitecture}	%设置图片标题，并使其称为label；
\end{figure}
```

[ht]设置图片位置的参数，共有h、t、b、p四种，详见

[图片位置]: http://www.ctex.org/documents/latex/graphics/node64.html



### 竖排图形

```latex
%注意使用\usepackage{graghicx}和\usepackage{subfigure}两个宏包
%由于IEEE给的是图形横排，且subfigure不支持\\换行，所以将minipage置入subfigure(）中，使其得以换行
\begin{figure}
\centering
\subfigure[the first subfigure]{
\begin{minipage}[b]{0.2\textwidth}
\includegraphics[width=1\textwidth]{fig1.eps} \\
\includegraphics[width=1\textwidth]{fig2.eps}
\end{minipage}
}	%fig1和fig2竖向排列
\subfigure[the second subfigure]{
\begin{minipage}[b]{0.2\textwidth}
\includegraphics[width=1\textwidth]{fig3.eps} \\
\includegraphics[width=1\textwidth]{fig4.eps}
\end{minipage}
}	%fig3和fig4竖向排列
\end{figure}	%fig1和fig3，fig2和fig4横向排列
```



### 横排图形

```latex
%注意使用\usepackage{graphicx}和\usepackage{subfigure}
\begin{figure}
\begin{minipage}[t]{0.5\linewidth}
\centering
\includegraphics[width=2.2in]{fig1.eps}
\caption{fig1}
\label{fig:side:a}
\end{minipage}
\begin{minipage}[t]{0.5\linewidth}
\centering
\includegraphics[width=2.2in]{fig2.eps}
\caption{fig2}
\label{fig:side:b}
\end{minipage}
\end{figure}
```

```latex
%--------------------------------------------------------------------------
2018.4.18
```

------

##页眉页脚设置

```latex
%使用fancyhdr宏包设置页眉和页脚
\usepackage{fancyhdr}

%设置plain style的属性
\fancypagestyle{plain}
\fancyhf{}	%清空当前设置

%设置页眉
\fancyhead[RE]{\leftmark}	%在偶数页的右侧显示章名
\fancyhead[LO]{\rightmark}	%在奇数页的左侧显示小节名
\fancyhead[LE,RO]{~\thepage~}	%在偶数页的左侧，奇数页的右侧显示页码

%设置页脚：在每页的右下脚以斜体显示书名
\fancyfoot[RO,RE]{\it 书名}	%"\it"采用意大利字体
\renewcommand{\headrulewidth}{0.7pt}	%页眉与正文之间的水平线粗细
\renewcommand{\footrulewidth}{0pt}	
\pagestyle{fancy}	%选用fancy style

%---------------------------------------------------------------------------
$下面内容有待考察
%当不使用fancyhdr包时
%页眉版式命令
\pagestyle{options}	%选项有plain（空头注，页码在脚注区）；empty（空头注，空脚注）；headings（头注由文献形式确定，article节号和页作为头注）；myheadings（头注内容自定义，没有脚注）单面输出可用：\markright{右页眉内容}，\markleft{左页眉内容}

%若双面输出可用
\markboth{左页头注内容}{右页头注内容}

%当只想改变一页的页眉版式，将控制命令改为
\thispagestyle{页眉排版方式}

%对于头注命令，包括
\topmargin size	%边距命令
\headheight size	%头注区高度命令
\headsep size	%头注区底部到正文顶部的距离

%对于脚注命令，包括
\footnote[num编号]{脚注内容}	%脚注内容命令
\footheight size	%脚注高度命令
\footskip size	%脚注定位命令（脚注区底部与正文底部之间的距离）
\footnotesep size	%脚注间距命令（脚注区的脚注内容行之间的间距）

%对于边注命令，包括
\marginparwidth size	%边注区宽度命令（ 页边到注释的宽度）
\marginparsep size	%边注与正文间距命令（页边注释区与正文边缘之间的距离）
\marginparpush size	%边注间距命令（多个边注之间的垂直间距）
\marginpar{边注内容}	%边注命令
%添加竖线作边注
\marginpar{\rule[Y轴方向坐标：+向上，-向下]{竖线宽度}{竖线长度}}
\marginpar{\rule[-60mm]{1mm}{60mm}}
```



## 添加脚注

```latex
%利用脚注命令\footnote{}
\usepackage{footmisc}
\footnote[number]{脚注内容}	%对于number可选参数而言，只能用来改变缺省的脚注编号。这个命令只适用于一般的文本段落，而不能在图形、报表等环境中使用

%一般使用脚注只需要在首页添加作者信息等，故不需要额外的宏包，但此时添加的脚注自动编号，且首行缩进
%由于一般论文不需要首行缩进，可以引入footmisc宏包，并使用marginal取消首行缩进
\usepackage[marginal]{footmisc}

\renewcommand{\thefootnote}{}	%取消脚注自动编号
```



```latex
%若希望在article文档中，每当开始新的一节时，脚注编号重置为1，则需要在"\section"命令前面或后面加入如下命令
\setcounter{footnote}{0}

%--------------------------------------------------------------------------
%当需要在报表、数字模式等\footnote命令不能使用的地方使用时，可以使用\footnotemark命令
\footnotemark[number]	%这条命令在文本中输出脚注的编号，内容由\footnotetext{}命令给出

\footnotetext[number]{文本}	%可以在\footnotemark命令之后任何时候使用，但是\footnote语句不能使用的地方它也不能使用
```



## 表格内公式换行

```latex
%首先在表格开头处置入以下代码
\newcommand{\tabincell}[2]{\begin{tabular}{@{}#1@{}}#2\end{tabular}} 

%其次就可以使用"\tabincell{c}{}"插入相应的内容
\documentclass[a4paper,12pt]{article}
\begin{document}

\begin{table}
\newcommand{\tabincell}[2]{\begin{tabular}{@{}#1@{}}#2\end{tabular}}  %导言区
\centering
\begin{tabular}{|c|c|c|}
\hline
1 & \tabincell{c}{the first line \\ the next\\the next\\ last} & \tabincell{c}{one \\ one}\\ %换行,单元格内的每个元素用\tabincell{c}{放表格内容}
\hline
2 & \tabincell{c}{hello\\ aha\\ ok \\yes \\en} & \tabincell{c}{two \\ two \\ two} \\
\hline
\end{tabular}

\caption{longtitle}
\end{table}
\end{document}
```



## 彩色表格

```latex
\documentclass{article}
\usepackage{ctex}
\usepackage{xcolor}
\usepackage{colortbl, booktabs}
\begin{document}
\begin{table}  
	\centering  
	\caption{彩色的表格}	%输入表格名  
	\begin{tabular}  
		{>{\columncolor{blue}}rccccc}	%将表的第一列变为蓝色，同时由tabular定义了各列名的位置
		\toprule[1pt]	%第一根横线的宽度  
		\rowcolor[gray]{0.5}    &1 &2   &3  &4  &5\\	%将该行的颜色为灰色，且能根据数值大小进行调整  
		\midrule	%设置第二根横线  
		A   &\multicolumn{1}{>{\columncolor{green}[0pt][0pt]}c}{318.3}   &327.8  &152.0  &104.9  &135.8\\	%第一个参数{1}用于指定跨越的列数，\columncolor{}[][]的第一个参数用于指定填充的颜色，第二和第三个参数用于指定填充色彩伸出内容的长度
		B   &&\multicolumn{1}{>{\columncolor{red}[0pt][0pt]}r}{335.5}    &137.7  &290.9  &198.6\\ 
		\bottomrule[1pt]	%设置表格底线的宽度为1pt  
	\end{tabular}  
\end{table} 
\end{document}
```



## 设置表格总长

```latex
%此时不能使用"tabular"，此时需要使用"tabular*"
\begin{taular*}{12cm}{lll}
……
\end{tabular*}
%此时，若前几列有剩余的空间，都归最后一列所有
```



##表格内自动换行

```latex
\begin{table}  
\Large  
\caption{自动换行}  
\begin{center}	%创造一个居中环境
\begin{tabular}{|l|l|l|l| p{5cm}|}	%用于创建表格，且限制最后一列表格的宽度，从而表格会自动调整字符内容
\hline  
Item & Name & Gender & Habit & Self-introduction \\ \hline  
1 & Jimmy & Male & Badminton & Hi, everyone,my name is Jimmy. I come from Hamilton,and it's my great honour to give this example. My topic is about how to use p{width} command \\ \hline  
2 & Jimmy & Male & Badminton & Hi, everyone,my name is Jimmy. I come from Hamilton,and it's my great honour to give this example. My topic is about how to use p{width} command \\  
\hline  
\end{tabular}  
\end{center}  
\end{table}  
```



## 设置表格宽度

```latex
\begin{table}  
\caption{表格宽度X}  
\begin{tabularx}{10cm}{llX}  % 10cm 减去前列宽度后，剩下的通通给第三列，且当第三列中文字内容较多，会自动分行  
\hline                        
Start & End  & Character Block Name  \\  
\hline  
3400  & 4DB5 & CJK Unified Ideographs Extension A \\  
4E00  & 9FFF & CJK Unified Ideographs \\  
\hline  
\end{tabularx}  
\end{table} 
%--------------------------------------------------------------------------
%tabularx其他内容
\begin{tabularx}{10.5cm}{|X|X|X|} %表格总宽度为10.5cm，共3列，宽度均相同。每列宽度为10.5/3＝3.5。是自动计算出来的。如果将上面表将的设置改为
\begin{tabularx}{\linewidth}{|p{3cm}|X|X|}	%则表格的总宽度是行宽，第1列列宽为3cm，其他两列的列宽自动计算
\begin{tabular}{p{3.5cm}|p{2cm}|p{5cm}}	%设置了每一列的宽度，强制转换，通过这种方法可以改变任一列宽
```



## tabu包使用

```latex
\begin{table}  
\caption{tab包用法}  
\begin{center}  
\begin{tabu} to 0.8\textwidth{X[c]|X[3,b]|X[2,l]|X[c]|X[3,m]|X[1,c]}  
%0.8\textwidth 为设置表格宽度  
%X[c]表示这一列居中，所占比例为1，相当于X[1,c]  
%X[3,c]表示这一列居中，所占比例为3，这列的宽度是X[c]列的3倍
%X[3,b]表示这一列宽度比例为3，且文本底对齐
%X[3,m]表示这一列宽度比例为3，且文本居中对齐
%X[3,p]表示这一列宽度比例为3，且文本顶对齐
\hline  
i  &xi              &ni      &i    &xi               &ni\\  
\hline  
1    &0.5∼0.64       &1           &8    &1.48∼1.62      &53\\ 
……  \\
\end{tabu}  
\end{center}  
\end{table}  
%--------------------------------------------------------------------------
%表中公式输入需要加括号
```



## 水平居中显示

```latex
	\begin{tabular}{ll}  
		\\[-2mm]  
		\hline  
		\hline\\[-1mm]  
		{\bf \small Symbol}&\qquad {\bf\small Meaning}\\	%"\bf"用于显示为黑体字；"\small"用于调整字符大小  
		\hline  
		\vspace{2mm}\\[-3mm]	%"\vspace"用于调整水平空白空间  
		PMi      &   \tabincell{l}{The ith physical machine or host server in the data \\center, i = 1, 2, ?-}\\    
		\hline  
		\hline  
	\end{tabular}  
```



## 表头与内容分离

```latex
\newcommand{\tabincell}[2]
{
	\begin{tabular}{@{}#1@{}}#2\end{tabular}
}  
\renewcommand{\arraystretch}{1.5}	%用于改变格子的大小
\begin{table}[tp]	
	\centering  
	\fontsize{6.5}{8}\selectfont	%\fontsize{}{}用于改变字体大小，第一个参数用于确定字号，第二个参数用于确定行距
	\caption{Demographic Prediction performance comparison by }  
	\label{tab:performance_comparison}  
	\begin{tabular}{|c|c|c|c|c|c|c|}  
		\hline  
		\multirow{2}{*}{Method}&	%\multirow{}第一个参数用于将多行合并为1行
		\multicolumn{3}{c|}{C}&\multicolumn{3}{c|}{ D}\cr\cline{2-7}	%\cr等效于"\\"，用于换行；\cline{n-m}用于从某列开始划线  
		&Precision&Recall&F1-Measure&Precision&Recall&F1-Measure\cr  
		\hline  
		\hline  
		A&0.7324&0.7388&0.7301&0.6371&0.6462&0.6568\cr\hline  
		B&0.7321&0.7385&0.7323&0.6363&0.6462&0.6559\cr\hline  
		C&0.7321&0.7222&0.7311&0.6243&0.6227&0.6570\cr\hline  
		D&0.7654&0.7716&0.7699&0.6695&0.6684&0.6642\cr\hline  
		E&0.7435&0.7317&0.7343&0.6386&0.6488&0.6435\cr\hline  
		F&0.7667&0.7644&0.7646&0.6609&0.6687&0.6574\cr\hline  
		G&{\bf 0.8189}&{\bf 0.8139}&{\bf 0.8146}&{\bf 0.6971}&{\bf 0.6904}&{\bf 0.6935}\cr  
		\hline  
	\end{tabular}  
\end{table}
```



## 三线表

```latex
\usepackage{booktabs}  
\usepackage{threeparttable}  
  
\renewcommand{\arraystretch}{1.5} %控制行高  
\begin{table}[tp]  
  \centering  
  \fontsize{6.5}{8}\selectfont  %\selectfont用于选择已调整的字体，也就是说，当用\fontsize改变字体、行距后，需要加上\selectfont来使其应用，不然不会产生作用
  \begin{threeparttable}  
  \caption{Demographic Prediction performance comparison by three evaluation metrics.}  
  \label{tab:performance_comparison}  
    \begin{tabular}{ccccccc}  
    \toprule  
    \multirow{2}{*}{Method}&  
    \multicolumn{3}{c}{ G}&\multicolumn{3}{c}{ G}\cr  
    \cmidrule(lr){2-4} \cmidrule(lr){5-7}	%\cmidrule(){}第一个参数用于控制方向，从左往右；第二个参数用于控制划横线的范围，即使只划一个格子，也需要些{1-1}
    &Precision&Recall&F1-Measure&Precision&Recall&F1-Measure\cr  
    \midrule  
    kNN&0.7324&0.7388&0.7301&0.6371&0.6462&0.6568\cr  
    F&0.7321&0.7385&0.7323&0.6363&0.6462&0.6559\cr  
    E&0.7321&0.7222&0.7311&0.6243&0.6227&0.6570\cr  
    D&0.7654&0.7716&0.7699&0.6695&0.6684&0.6642\cr  
    C&0.7435&0.7317&0.7343&0.6386&0.6488&0.6435\cr  
    B&0.7667&0.7644&0.7646&0.6609&0.6687&0.6574\cr  
    A&{\bf 0.8189}&{\bf 0.8139}&{\bf 0.8146}&{\bf 0.6971}&{\bf 0.6904}&{\bf 0.6935}\cr  
    \bottomrule  
    \end{tabular}  
    \end{threeparttable}  
\end{table}  
```



##将表作为图的内容

```latex
\renewcommand{\arraystretch}{1.2}  
\begin{figure}%[]  
	\centering  
	\centerline{\bf (a). CDR samples}	%\centerline{}可以使一行文本居中，但在Texstudio中好像不行
	\vspace{1.5mm}  
	\begin{tabular}{|l|c|c|}  
		\hline  
		\cline{1-1}  
		\underline{\textbf{record-id}} & \textbf{caller-id} & \textbf{callee-id} \\\hline   
		1                                              & \#user-1           & \#user-2           \\\hline  
		2                                              & \#user-1           & \#user-4           \\\hline  
		3                                              & \#user-2           & \#user-1           \\\hline  
		4                                              & \#user3            & \#user-5\\\hline  
		5                                              & \#user1            & \#user-2\\\hline  
		\vdots                                             & \vdots           & \vdots\\\hline  
	\end{tabular}  
	
	\vspace{3mm}  
	\centering  
	\centerline{\bf (b). DTR samples}  
	\vspace{1.5mm}  
	\begin{tabular}{|l|c|c|c|}  
		\hline  
		\cline{1-1}  
		\textbf{record-id} & \textbf{user-id} & \textbf{online-time} & \textbf{offline-time} \\\hline  
		1    & \#user-1           & \#timestamp-1  & \#timestamp-2           \\\hline  
		2    & \#user-2           & \#timestamp-3  & \#timestamp-4           \\\hline  
		3    & \#user-2           & \#timestamp-5  & \#timestamp-6           \\\hline  
		4    & \#user3            & \#timestamp-7  & \#timestamp-8           \\\hline  
		\vdots & \vdots           & \vdots          &\vdots\\\hline  
	\end{tabular}  
	\vspace{1.5mm}  
	\caption{CDR (Call Detail Records) and DTR (Data Traffic Records) samples.}  
\end{figure}
```

```latex
%--------------------------------------------------------------------------
2018.4.19
```

------



## SCI英文论文写作

```latex
%设置行间距
\setlength{\baselineskip}{?pt}
\renewcommand{\baselinestretch}{?}	%需要放在导言区
```



```latex
%去掉容差报警的方法
\hbadness = 10000
\tolerance = 10000
\hfuzz = 150pt
```



```latex
%给字符下添加波浪线等
%需要先添加宏包:ulem
\usepackage{ulem}
\d G	%给G下加点
\xout	%斜删除线
\sout	%水平删除线
\uwave	%波浪线
\uline	%下划线
\uuline	%双下划线
```



```latex
%插入代码并调整字体格式等
\usepackage{color}
\usepackage{listings}
%首先需要引用两个宏包

\definecolor{gray}{rgb}{0.8,0.8,0.8}	%用于定义灰色
\lstset{numbers=left	%在左侧显示行号
\lstset{language=C++}	%设置语言
\lstset{breaklines}    %自动将长代码换行
\lstset{extendedchars=false}	%防止代码换页时，与标题、章节、页眉等产生冲突
\lstset{backgroundcolor=\color{gray}}	%设置背景颜色
\lstset{keywordstyle=\color{blue}\bfseries}    %设置关键字颜色并加粗
\lstset{frame=none}    %不显示背景边框
\lstset{tabsize=4}    %设置tab代表的空格数
\lstset{commentstyle=\color{red}}	%设置代码注释的格式
\lstset{stringstyle=\emph}	%设置字符串格式
\lstset{showstringspaces=false}    %不显示字符串中的空格
\lstset{frame = shadowbox}	%将代码用带有阴影的盒子包裹起来
\lstset{rulesepcolor=\color{red}}	%代码块边框为淡青色
\lstset{numberstyle=\tiny} %行号字体用小号
```





## itemize环境

```latex
%该环境用于条款列举，被列举的条款由一个实心圆标记
\begin{itemize}
	\item <条目1>
	\item <条目2>	%输出时为"·<条目2>"
\end{itemize}
```



## enumerate环境

```latex
%该环境用于条款列举，被列举的条款与itemize中不同，由数字引导
%可以多重嵌套
\begin{enumerate}
	\item <条目1>	%输出"1.<条目1>"
		\begin{enumerate}
			\item <条目1>	%输出"(a).<条目1>"
		\end{enumerate}
	\item <2>	%输出"2.<2>"
\end{enumerate}

%Latex可以自动处理四重enumerate嵌套，编号规则为第一级自然数，第二级(a),(b)，第三级编号为小写罗马数字i，ii，第四级为A,B
```



## tabbing环境

```latex
%用于制作无线框表格，不能逐级嵌套使用
\begin{tabbing}
	<表文内容>
\end{tabbing}
%实例：
\documentclass[12pt]{article}
\usepackage{ctex}
\begin{document}
	\begin{tabbing}	%制表位控制行：每个制表位用\=表示，第一个制表位默认，不需加\=，如下命令中\hspace*{100bp}就是第一个制表位，这个制表位表示这里是空白
			\hspace*{100bp}\=article\quad \=文章类\kill	%制表位正文行：跳格\>用来跳到下一个制表位，第一个制表位也不需要使用跳格命令
			\>book    \>书籍类\\
			\>report  \>报告类\\
			\>article \>文章类\\
			\>letter  \>书信类
	\end{tabbing}	
	\begin{tabbing}	%如下一行称为样本行，样本行末尾不能以\\结尾，必须以\kill结束，这行仅用来设置制表位，不被显示
			朝代\hspace*{20bp} \=诗人\hspace*{20bp} \=代表作\kill
			%tabbing环境不会自动分行，换行必须以\\实现
			唐朝  \>李白  \>将进酒\\
			唐朝  \>杜甫  \>石门吏\\
			宋朝  \>苏轼  \>水调歌头
	\end{tabbing}
%\' 和 \` 的作用：\'左对齐；\`右对齐
	\begin{tabbing}
			朝代\hspace*{20bp} \=诗人\hspace*{20bp} \=代表作\kill
			朝代\'  \>诗人  \>代表作\\
			唐朝  \>李白  \`\>将进酒\\
			唐朝  \>杜甫\'  \>石门吏\\
			宋朝  \>苏轼  \`水调歌头
	\end{tabbing}	
%重音符\=  \'  \`  在tabbing环境内部不起作用，如果要在tabbing环境内部使用重音，要将\换成\a，如下所示
		\begin{tabbing}
			重音符\hspace*{5bp} \= 代码\kill
			\a=o \> $\backslash$a=o\\
			\a'o \> $\backslash$a'o\\
			\a`o \> $\backslash$a`o\\
			\a=a \> $\backslash$a=a\\
			\a'a \> $\backslash$a'a\\
			\a`a \> $\backslash$a`a\\
			\ldots \> \ldots
		\end{tabbing}
\end{document}

```



## table环境

```latex
\begin{table}[位置参量]
	<表文内容>
\end{table}
%位置参量有四种：h（当前行或者下一行），b（底部），t（顶部），p（另面设置专用表格页）
```



## tabular环境

```latex
%用于制作有线框表格
\begin{tabular}[对齐方式选择]    %左对齐l，右对齐r，居中c
	<表文内容>
\end{tabular}

%表格中的竖线："|"
%表格中的横线："\hline"
%双横线："\hline\hline"
%行扩充{实际就是在一定范围内添加横线}：\cline{i-j}	
%单行列元素缩并（将当前行某个区域范围内的n列缩成一列）：\multicolumn{列数}{列参数}{条目正文}
```



## math环境

```latex
需要用$……$将公式或数学符号括起来
```



## 界标排版命令

```latex
%动态开界标命令
\left<界标排版命令><数学公式>
%动态闭界标命令
<数学公式>\right<界标排版命令>
$$f(a,b,c) = (a+b)+\left\{\frac{a+b}{a-b}\right\}+\left[\frac{1}{c+d}\right]$$

%---------------------------------------------------------------------------
%有时排版只需要一个动态界标即可，此时需要用界标控制字符"."来充当另一个被省略的界标
$$f_{ij} = \left\{
	\begin{array}{ll}
	y & {\rm if} y>0\\	%"\rm"表示使用rome字体
	z+y & {\rm otherwise}
\end{array}
\right.$$
```



## 版式选择

```latex
\twoside	%双面输出
\twocolumn	%左右两列排列
\titlepage	%标题内容单独占一页
```



## 字体命令

```latex
\rm	%罗马字体命令
\bf	%黑体命令
\it	%意大利字体命令
\sc	%小号大写字体命令
\sl	%斜体命令
\tt	%打字机体命令
\em	%强调型字体命令：当前字体为罗马字体时，则强调型为意大利字体；当前字体为非罗马字体时，则强调型为罗马字体
```

```latex
%---------------------------------------------------------------------------
%2018.4.20
```

------



## 盒子

```latex
\mbox{内容}	%当希望一个文本不会换行输出时，可以使用，此时无边框

\fbox{内容}	%有边框

\makebox[宽度][位置]{文本}	%可指定盒子宽度，文本在盒子中的位置（l：左端；r：右端；s：两端，默认是居中）；无框
\framebox	%与\makebox类似，有框
%---------------------------------------------------------------------------
\framebox[2.5cm][l]{.........}
\framebox[3cm][s]{XXX \dotfill XXX}	%"\dotfill"点填充，向两边延伸，直到该横向范围内被点与字符填满
%---------------------------------------------------------------------------
%给单个字母加斜线，需要用\makebox
\makebox[0pt][l]{/}S
```



## verbatim环境

```latex
%verbatim环境能够原样输出其中的内容，空格不会特殊表示
\begin{verbatim}
……
\end{verbatim}
%verbatim*中空格会特殊表示

```



 ## 块注释

```latex
%当需要整体注释时，可以使用块注释命令
\iffalse %块注释命令开始
……
\fi %块注释命令结束
```



## 产生随机文本

```latex
\usepackage{lipsum}
\lipsum[num]
```



## 首行缩进

```latex
%Latex中默认每一节的段首不会自动缩进，此时需要在导言区引入
\setlength{\parindent}{2em}
\usepackage{indentfirst}

%但当在中文段落后紧跟一个英文段落或其他情况下，段落仍会出现不缩进的情况，此时可以在该段段首添加
\indent
```



##段距行距

```latex
%LaTeX用\baselineskip表示当前的行距，其默认值大约是当前字号的1.2倍，如果当前字号是10pt，那么\baselineskip是12pt。这对英文排版是合适的，对中文就显得太拥挤
%通常把行距设为字号的1.8倍：
\setlength{\baselineskip}{1.8em}
%LaTeX 用\parskip表示段距，我一般把它设为1ex：
\setlength{\parskip}{1ex}
%注意这些修改长度的命令最好都放在正文区（即\begin{document}之后）
```



## 设置纸张大小

```latex
%当要求使用b5纸，单面打印时
\documentclass[10pt, b5paper]{report}
\usepackage[body={12.6cm, 20cm}, centering, dvipdfm]{geometry}
% 以上将版心宽度设为 12.6cm，高度 20cm，版心居中，且自动设置PDF文件的纸张大小。
```



## titlesec宏包使用

```latex
%在 xelatex 中使用 \usepackage 指令使用 titlesec 宏包时,可以指定一些格式选项，如下：
\usepackage[center]{titlesec}
%其中 center 可使标题居中,还可设为 raggedleft (居左，默认), raggedright (居右)。标题由标签与标题内容构成，其格式通常在 xelatex 文档导言区通过 titlesec 宏包提供的指令 \titleformat 进行设定。 
%\titleformat 指令用法如下：
\titleformat{command}[shape]{format}{label}{sep}{before}[after]
%各参数含义如下：
%command 是要重新定义的各种标题命令,比如 \part，\chapter，\section，\s section，\s s section，\paragraph，\s paragraph等；
%shape 是用来设定段落形状的,可选的参数有 hang 、 block 、 display 
%format 用于定义标题外观,比如使标题居中、字体加粗等；
%label 用于定义定义标题的标签,就是标题内容前面的标号；
%sep 定义标题的标签与标题内容之间的间隔距离。
%before 用于在标题内容前再加些内容；
%after 用于在标题内容后再加些内容。
%实例
\titleformat{\chapter}{\centering\Huge\bfseries}{第\,\thechapter\,章}{1em}{}
%其 中, shape 、 before 、 after 参 数 都 被 省 略 掉 了。 format 参 数 将章标题设置为居中( \centering )显示、字号为 \Huge，字体被加粗显示 \bfseries ；在设置 s section 格式,未采用居中,而是采用默认的居左,另外将标题的字号也降了一级( \large )。 label 参数将标题的标签设置为 “第 xxx 章”格式。sep 参数设置标签与标题内容之间以一个字(1em)的宽度为间隔。
%该内容需要放置在导言区
```

```latex
%-----------------------------------------------------------------------------
%2018.4.21
```

------



## 拆分并独立编译

```latex
%当tex文件较大时，可以将其拆分为几个部分，分别编译，再在主文件main.tex中包含起来
\documentclass{book}
\begin{document}
\title{A LaTeX Book}
\author{cohomo@blogbus}
\date{}
\maketitle
\input{chap1}
\input{chap2}
\input{chap3}
\end{document}
%\input命令也可以改为\include命令，区别在于input可以放在导言区和正文区，包含的内容不另起一页；而include只能放在正文区，包含的内容另起一页

%-----------------------------------------------------------------------------
%拆分命令共有三条
\input{xxx}	% 单纯地将xxx.tex内容导入进主文件中，不分页；可放在导言区或正文区；各分文件加入宏命令后可以分别编译，但编码自动从1开始，可能造成交叉引用混乱
\include{xxx}	%分页显示内容，适于book类分chapter编写；只能放置在正文区，往往与\includeonly合用；总是显示正确的编码顺序
\includeonly{xxx}	%放在导言区；与\ include合用，指定部分或全部\include内容参与编译

%\input实例：

%main.tex
\documentclass[12pt,a4paper]{article}
\def\allfiles{}

\begin{document}
% paper title
\title{How to \textbf{compile} in files}
\maketitle

\input{abstract}
\input{introduction}
\input{implement}
\input{reference}
\end{document}

%abstract.tex
\ifx\allfiles\undefined
\documentclass[12pt,a4paper]{article}
\begin{document}
\fi
\section*{Abstract}
This is abstract.

\ifx\allfiles\undefined     %如果位置放错，可能出现意外中断
\end{document}
\fi

%introduction.tex
\ifx\allfiles\undefined
\documentclass[12pt,a4paper]{article}
\begin{document}
\fi
\section{Introduction}
This is introduction. It's the first part.

\ifx\allfiles\undefined
\end{document}
\fi

%implement.tex
\ifx\allfiles\undefined
\documentclass[12pt,a4paper]{article}
\begin{document}
\fi
\section{Inplement}
This is inplement.
If you compile it seperately, it's number is 1, else 2.
\ifx\allfiles\undefined
\end{document}
\fi

%reference.tex
\ifx\allfiles\undefined
\documentclass[12pt,a4paper]{article}
\begin{document}
\fi
\section{Reference}
This is reference.
If you compile it seperately, it's number is 1, else 3.

\ifx\allfiles\undefined
\end{document}
\fi

%注意在主文件中添加的\def\allfiles{}；在各个子文件第一行添\ifx\allfiles\undefined；\begin{document}后一行添加\fi；在\end{document}前一行添加\ifx\allfiles\undefined，后一行添加\fi
%上述方式能够使文件在无论是在主文件中还是各个子文件单独都能运行

%-----------------------------------------------------------------------------
%联合使用\include和\includeonly
%和1中类似，只需要将\input命令修改为\include命令，在导言区加入\includeonly。

%main.tex
\documentclass[12pt,a4paper]{article}
\includeonly{abstrct,introduction,implement,reference}	%根据需要删减

\begin{document}
% paper title
\title{How to \textbf{compile} in files}
\maketitle

\include{abstract}
\include{introduction}
\include{implement}
\include{reference}
\end{document}

%-----------------------------------------------------------------------------
%当使用宏包\subfiles
%main.sty
\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage[english]{babel}
%\usepackage{graphicx}
%\graphicspath{{images/}{../images/}}
\usepackage{subfiles} 
\usepackage{blindtext}

\title{Subfile Example}
\author{Team Learn ShareLaTeX}
\date{ }
\begin{document}
\maketitle
\section{Introduction}
\subfile{sections/introduction}
%\section{Second section}
%\subfile{sections/section2}
\end{document}

%introduction.sty
\documentclass[../main.tex]{subfiles}
 
\begin{document}
\textbf{Hello world!}
 
%\begin{figure}[bh]
%\centering
%\includegraphics[width=4cm]{lion-logo}
%\label{fig:img1}
%\caption{ShareLaTeX learn logo}
%\end{figure}
 
Hello, here is some text without a meaning.  This... 
\end{document}

%-----------------------------------------------------------------------------
$下述问题以后可能会碰到，先mark
%但文档中section较多，且编写时间不同时
%1.想分别编辑各个section
%2.由于preamble太多，想专门弄一个文件放置preamble
%3.想用bibtex来生成参考文件

%main.sty
\documentclass[fleqn]{article}

\usepackage{subfiles}  
\usepackage{D:/My_Preamble} %必须是绝对路径，才能让各个section*.tex在单独编译时使用到；路径可以更改；不用在每个.tex文件中再去导入各个包，较方便

\title{This is title}
\author{Jay Chou}
\date{\today}

\begin{document}
\maketitle
Hello World!

\subfile{sections/section1}	%使用子文件.tex;注意是sections文件夹中的section1文件
\subfile{sections/section2}

\bibliographystyle{unsrt}	
%参考文献标准样式：
%1.plain：按字母的顺序排列，比较次序为作者、年度和标题
%2.unsrt：样式同plain，按照引用的先后排序
%3.alpha：用作者名首字母+年度后两位作标号，以字母顺序排序
%4.abbrv：类似plain，将月份全拼改为缩写
%5.ieeetr：国际电气电子工程师协会期刊样式
%6.acm：美国计算机学会期刊样式
%7.siam：美国工业和应用数学学会期刊样式
%8.apalike：美国心理学学会期刊样式
\bibliography{D:/My_Reference} %必须是绝对路径。但各个section*.tex单独编译时使用不到(缺点)；使用bib
\end{document}

%section1.tex
\documentclass[../main.tex]{subfiles} %两个点代表返回上一级菜单

\newcommand{\AAA}{\textbf{abcdefg}} % 这个'\AAA'命令只在这个tex文件里起作用

\begin{document}
%From there on, type whatever you want.
\section{This is section 1}
Hello, this is section 1.
\end{document} 

$其他文件也是同理编辑

%接下来编辑"My_preamble.sty"文件，需要保存在"main.tex"中指定的路径

\ProvidesPackage{msqmypreamble}
\usepackage{amsmath, amssymb, amsthm}
\usepackage{cite}
%\usepackage{graphicx, graphics} 
% etc

%\setlength{\voffset}{-2.0cm}
%\setlength{\parskip}{0.2cm}
\newtheorem{thm}{Theorem} \setcounter{thm}{0}
\newcommand{\defn}{\overset{\Delta}{=}}
\newcommand{\st}{\textrm{~s.t.~}}
\newcommand{\supp}{\mathop{\rm supp}}
% etc

$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$
%当subfiles.sty文件不存在时，也可以将下述代码复制到main.tex文件所在文件夹，并保存为.sty格式

%% This is file `subfiles.sty',
%% generated with the docstrip utility.
%%
%% The original source files were:
%%
%% subfiles.dtx  (with options: `package')
%% 
%% Copyright 2002 Federico Garcia
%% 
\NeedsTeXFormat{LaTeX2e}
\ProvidesPackage{subfiles}[2002/06/08 Federico Garcia]
\DeclareOption*{\PackageWarning{\CurrentOption ignored}}
\ProcessOptions
\RequirePackage{verbatim}
\newcommand{\skip@preamble}{
    \let\document\relax\let\enddocument\relax
    \newenvironment{document}{}{}
    \renewcommand{\documentclass}[2][subfiles]{}}
\newcommand\subfile[1]{\begingroup\skip@preamble\input{#1}\endgroup}
\endinput
%%
%% End of file `subfiles.sty'.
```

```latex
%-----------------------------------------------------------------------------
%2018.4.22
```

------



## 中文字体使用

```latex
%调用方式
%{\字体名称 正文内容}
%实例：
\documentclass{article}  
\usepackage{ctex}  
  
\begin{document}  
  
中文宏包测试               \par 	%"\par"表示回车换号  
{\songti   这是宋体的样式} \par  
{\heiti    这是黑体的样式} \par  
{\fangsong 这是仿宋的样式} \par  
{\kaishu   这是楷书的样式} \par  
{\lishu   这是隶书的样式} \par %CTeX的手册中是支持隶书和幼圆的，  
{\youyuan 这是幼圆的样式} \par %但是不知是何原因编译有问题  
  
\end{document} 
```



## 全局字体设置

```latex
\setmainfont{字体名称}
\setCJKmainfont{字体名称}
%大括号中填入的即字体名称（中英文皆可，英文严格区分大小写）；前者设置的是英文字体，后者设定的是CJK字体
%也可以按照自定义的指令来命名

%设定英文字体指令
\newfontinstance{自定义指令名}{系统字体名称}
%实例：
\newfontinstance{\courier}{Courier}

%设定中文字体指令
\setCJKfamilyfont{自定义的CJKfamily名称}{系统字体名称}
\newcomman{自定义指令名}{自定义的CJKfamily名称}
%实例：
\setCJKfamilyfont{hwxk}{STXingkai}
\newcommand{\stxk}{\CJKfamily{hwxk}}
%系统名称必须与查到的名称一致，自定义名称可以随意设置，最好指令名以\开头
```



## 附录

```latex
\appendix
\appendixpage
\addappheadtotoc
%在\appendix之后的内容都是附录；\appendixpage将在一个附录名前添加"Appendices";\addappheadtotoc将把title添加至目录
%对于后两者需要引入宏包\usepackage{appendix}

%另一种方式是采用附录环境
\begin{appendices}
……
\end{appendices}
%后一种的方式不能与\appendixpage同用

%两种方法实例：
%1
\documentclass[a4paper,12pt]{article}
\begin{document}
    main body %正文内容
  \appendix
  \renewcommand{\appendixname}{Appendix~\Alph{section}}	%用于将\section{}大括号中的内容作为附录标题输出

  \section{Some Examples 1}
  some text...
  \section{Some Examples 2}
  some text...
\end{document}
%2
\documentclass[10pt,conference,twocolumn]{IEEEtran}
\begin{document}
   main body %正文内容
    \begin{appendices}
      \section{  }
      some text in Appendix A
      \section{  }
      some text in Appendix B
  \end{appendices}
\end{document}
```

```latex
%-----------------------------------------------------------------------------
%2018.4.23
```

------

## 伪代码排版（与前述latex2e排版略有区别）

```latex
\documentclass[11pt]{ctexart}  
\usepackage[top=2cm, bottom=2cm, left=2cm, right=2cm]{geometry}  
\usepackage{algorithm}  %Algorithm 环境主要作用是将代码段变成浮动体，浮动体一方面能防止代码超出页面范围，另外一方面也方面最后生成和图表目录相似的算法列表目录。也能通过标记，方便在文章其它地方引用。
\usepackage{algorithmicx}  %为描述算法提供了程序设计中的所有常用结构的表示，如：判断 (If) ，循环  (While, For, Loop), 输入(Require) ,输出(Ensure)等。在这里需要注意的是，所有 algorithmic宏包提供的命令都是全大写;algorithmicx宏包提供的命令只需首字母大写
\usepackage{algpseudocode}  %algpseudocode 宏包则是 algorithmicx 宏包的一部分，它提供了实际用来排版伪代码的环境
\usepackage{amsmath}  %提供了许多呈现公式和其他数学结构的特征
  
\floatname{algorithm}{算法}  
\renewcommand{\algorithmicrequire}{\textbf{输入:}}  
\renewcommand{\algorithmicensure}{\textbf{输出:}}  
  
\begin{document}  
    \begin{algorithm}  
        \caption{用归并排序求逆序数}  %caption{内容}和caption*{内容}前者内容前面会加上Algorithm+编号，而后者不会
        \begin{algorithmic}[1] %\begin{algorithmic}[1]中的[n]表编号间隔，为1的话表示每行都要有编号
            \Require Array数组，n数组大小  
            \Ensure 逆序数  
            \Function {MergerSort}{Array,left,right}  
                \State result←0  
                \If {left<right}  
                    \State middle←(left+right)/2  
                    \State result←result+ \Call{MergerSort}{Array,left,middle} 
                    \State result←result+ \Call{MergerSort}{Array,middle,right}  
                    \State result←result+ \Call{Merger}{Array,left,middle,right}  
                \EndIf  
                \State \Return{result}  
            \EndFunction  
            \State  
            \Function{Merger}{Array,left,middle,right}  
                \State i←left  
                \State j←middle  
                \State k←0  
                \State result←0  
                \While{i<middle \textbf{and} j<right}  
                    \If{Array[i]<Array[j]}  
                        \State B[k++]←Array[i++]  
                    \Else  
                        \State B[k++]←Array[j++]  
                        \State result←result+(middle−i)  
                    \EndIf  
                \EndWhile  
                \While{i<middle}  
                    \State B[k++]←Array[i++]  
                \EndWhile  
                \While{j<right}  
                    \State B[k++]←Array[j++]  
                \EndWhile  
                \For{i=0→k−1}  
                    \State Array[left+i]←B[i]  
                \EndFor  
                \State \Return{result}  
            \EndFunction  
        \end{algorithmic}  
    \end{algorithm}  
\end{document}  
```

```latex
%-------------------------------------------------------------------------------
%2018.4.24
```

------

## latex引理、定义、定理 自定义

```latex
%先要引入包，amsmath
\usepackage{amsmath}

%需要首先定义用法
\newtheorem{环境名}{标题}{排序单位} %排序单位一般是chapter，此时，表示定理按章节编号

%实例：
\usepackage{amsmath}  
\newtheorem{theorem}{Theorem}  
\newtheorem{lemma}{Lemma}  
\newtheorem{proof}{Proof}[section]  

\section{theorem}  
\begin{theorem}  
This is a theorem.  
\end{theorem}  
  
\begin{lemma}  
This is a lemma.  
\end{lemma}  
  
\section{Proof}  
\begin{proof}  
This is proof.  
\end{proof}  

%-------------------------------------------------------------------------------
%当需要更加精细编写定理时，需要使用ntheorem宏包
\newtheorem{lemma}{Lemma} %此时，将在"Lemma"后生成编号"1",若改为\newtheorem*{lemma}{Lemma} ，此时编号将消失  
\begin{lemma}  
This is a lemma.  
\end{lemma}  

%也可以使用该宏包中的命令来改变排版格式
\theoremheaderfont { 字体命令}    %改变标题字体
\theorembodyfont{ 字体命令}   	  %改变定理内正文字体
\theoremnumbering {计数形式} %设置序号的计数形式，它的默认值是arabic ，可改为采用alph 、Alph 、rom、Roman 、greek 、Greek 、chinese 或fnsymbol 计数形式。
\theoremstyle {格式〉 %有break等命令。break 让 定理与内容分行

%当希望结束符产生变化时，可以使用\qed command
%首先导入 amssymb宏包
\usepackage{amssymb}

%再定义使用\qed 对应的图形,如：
\newcommand{\qed}{\hfill $\blacksquare$}	%也可以用square，此时为空心方块

%再在相应的地方使用\qed即可
\qed

%实例：
\theorembodyfont{\bfseries\upshape}  %改变定理的字体
\theoremseparator{:}  %使定理标题后跟":"
\theoremstyle{break}  %使标题和内容分行
\newtheorem{theorem}{Theorem}  
\newtheorem{lemma}{Lemma}  
\newtheorem{proof}{Proof}[section]  
  
\section{theorem}  
  
\begin{theorem}[introduction]  
This is a theorem.  
\end{theorem}  
  
\begin{lemma}  
This is a lemma.  
\end{lemma}  
  
\theorembodyfont{\upshape}  
\theorembodyfont{\bf}  
\section{Proof}  %当开始proof后，其后跟着的数字会变化为n.1;n.2……
\begin{proof}  
This is proof.  
\end{proof}  

%也可以自定义环境
\newenvironment{新环境}{开始定义}{结束定义}
\newenvironment{proof}{{\noindent\it Proof}\quad}{\hfill $\square$\par}  %\noindent 表示 proof 没有缩进，\it 表示 proof 斜体， \quad 表示 proof 后面空四个空格， \hfill 表示右对齐， \square 表示方框，\par表示结尾空一段

%当需要输出中文且需要缩进时，可以使用以下代码
\newtheorem{Definition}{\hspace{2em}定义}[chapter]
\newtheorem{theorem}{\hspace{2em}定理}[chapter]
\newtheorem{lemma}{\hspace{2em}引理}[chapter]
\newtheorem{proof}{证明}[chapter]
%[计数器名称都可以更改]
```



## 使花括号变长

```latex
$	\Big\{...	\Big\}	$
```



## 使竖线变长

```latex
$	\Big|\Big|$
$	\big|\big|$
$	\bigg|\bigg|$
$	\Bigg|\Bigg|$
```



## 设置字体颜色

```latex
%1.直接使用已经定义好的颜色
\usepackage{color}
\textcolor{red/blue/green/black/white/cyan/magenta/yellow}{text}

%2.组合red、green、blue的值合成需要的颜色
\usepackage{color}
\textcolor[rgb]{r,g,b}{text}	%其中{r,g,b}代表red、green和blue三种颜色的组合，取值范围为[0-1]
\textcolor[RGB]{R,G,B}{text}	%其中{R,G,B}代表red、green和blue三种颜色的组合，取值范围为[0-255]

%3.定义新颜色，直接调用
\usepackage{color}
\definecolor{ColorName}{rgb}{r,g,b}     %这时r/g/b的定义域就在[0-1]
\definecolor{ColorName}{RGB}{R,G,B}		%这时R/G/B的定义域就在[0-255]
\textcolor{ColorName}{text}
```

```latex
%-------------------------------------------------------------------------------
%2018.4.26
```

------



## 字体格式设定

```latex
%可以通过字体命令设置也可以通过字体申明作用于后续文本
%字体类型设置
\textrm{字体}	
\textrm{Roman Family}	||	\rmfamily Roman Family	%罗马字体
\textsf{字体}
\textsf{Sans Serif Family}	||	\sffamily Sans Serif Family	%无衬线字体
\texttt{字体}
\texttt{Typewriter Family}	||	\ttfamily Typewriter Family	%打字机字体

%对于字体申明时，遇到后一个申明时，前者作用将消失，或者也可以使用{}进行范围控制

%字体系列设置(粗细、宽度)
\textmd{Medium Series}	\textbf{Boldface Series}
{\mdseries Medium Series}	{\bfseries Boldface Series}

%字体形状设置（直立、斜体、伪斜体、小型大写）
\textup{Upright Shape}	\textit{Italic Shape}
\textsl{Slanted Shape}	\textsc{Small Caps Shape}
{\upshape Upright Shape}	{\itshape Italic Shape}
{\slshape Slanted Shape}	{\scshape Small Caps Shape}

%中文字体设置
%需要使用ctex宏包
{\songti 宋体}
{\heiti 黑体}
{\fangsong 仿宋}
{\kaishu 楷书}

%字体大小设置
%字体大小设置跟\document[normal size]{article}中的normal size有关，一般只有10pt、11pt、12pt
{\tiny}
{\scriptsize}
{\footnotesize}
{\small}
{\normalsize}
{\large}
{\Large}
{\LARGE}
{\huge}
{\Huge}

%中文字号设置命令
\zihao{字号} 内容


```

```latex
%---------------------------------------------------------------------------------
%2018.4.28
```

------



## 换行和段落

"\\"只是用来换行，并不会产生新段落，故而不会产生首行缩进效果

"\par"能代替空行的作用，产生新段落



## 目录产生

通过"\tablecontents"命令，在文章开头输出目录



## 反斜杠

由于latex中两个反斜杠起着换行的作用，所以需要使用"\textbackslash"来生成反斜杠



## 引号

`：左单引号

'：右单引号

``：左双引号

''：右双引号



## 连字符

通过"-"、"--"、"---"生成短中长三种连字符



## 重音符（以o为例）

```latex
\`o;\'o;\^o;\''o;\~o;\=o;\.o;\u{o};\v{o};\H{o};\r{o};\t{o};\b{o};\c{o};\d{o}
```



## 浮动体

```latex
%当在latex中输入插图和表格等时，版式将需要改变，此时可以借助浮动体
%对于插图，可以使用figure浮动体
\begin{figure}
	\centering
	\includegraphics[scale = 0.3]{lion}
\end{figure}

%对于表格，可以使用table浮动体
\begin{table}
	内容
\end{table}
```



## 标签设置和引用

```latex
%通过lable命令设置标签
\label{}
%通过ref命令引用标签
\ref{}
```



## 数学公式

```latex
%可以通过美元符号、小括号、math环境实现行内公式
$a+b = b+a$
\(a+b = b+a\)
\begin{math}a+b = b+a\end{math}

%可以通过$$、中括号、displaymath环境、equation环境来实现行间公式排版
$$a+b = b+a$$
\[a+b = b+a\]
\begin{displaymath}a+b = b+a\end{displaymath}
\begin{equation}a+b = b+a\end{equation}	%实现公式编号
```



## 矩阵

```latex
%需要引入amsmath宏包
\begin{matrix}
	0 & 1 \\
	1 & 0
\end{matrix}

%pmatrix环境，在两端形成小括号
\begin{pmatrix}
	0 & 1 \\
	1 & 0
\end{pmatrix}

%bmatrix环境，在两端加中括号
\begin{bmatrix}
	0 & 1 \\
	1 & 0
\end{bmatrix}

%Bmatrix环境，在两端加大括号
\begin{Bmatrix}
	0 & 1 \\
	1 & 0
\end{Bmatrix}

%vmatrix环境，在两端加单竖线
\begin{vmatrix}
	0 & 1 \\
	1 & 0
\end{vmatrix}

%Vmatrix环境，在两端加双竖线
\begin{Vmatrix}
	0 & 1 \\
	1 & 0
\end{Vmatrix}

%smallmatrix环境，可以实现行内小矩阵
\begin{math}
\left(	%需要手动添加左括号
\begin{smallmatrix}
	x & -y \\ y & x
\end{smallmatrix}
\right)	%手动添加右括号
\end{math}
```



## biblatex参考文献

```latex
%需要将编译器中的bibtex改为biber
%首先引入biblatex宏包
\usepackage[stype = numeric, backend = biber]{biblatex}
%添加bib参考文献管理库
\addbibresourse{文件名.bib}
%在正文中即可通过命令进行引用
\cite{文件名}	%无格式化引用
\cite{文件名}	%带方括号的引用
\cite{文件名}	%上标引用

\printbibliography	%将文献库中所有的文献进行输出，此时标题名为REFERENCES
%可以通过命令进行修改
\printbibliography[title = {参考文献}]

%通过nocite命令可以输出未引用文献
\nocite{*}	%"*"表示输出全部，也可通过文献名来进行筛选输出
```



## 自定义命令

```latex
%通过\newcommand+<命令>+[参数个数]+[默认参数]+{定义}实现自定义命令
\newcommand\loves[2]{#1 喜欢 #2}	%参数个数最多为9个，可以使用#1、#2……#9进行表示

%可以设置默认参数，可以通过[内容]来改变该默认值，默认参数位置为首个参数
\newcommand\love[3][喜欢]{#2#1#3}
\love{1}{2}
\love[最爱]{1}{2}
```

```latex
%---------------------------------------------------------------------------------
%2018.4.29
```



## 公式箭头

```latex
% 通过witharrows宏包实现公式右侧添加箭头，使公式更加具有严谨性等
% 编译需要WithArrows环境，如果异常需要编译两次
\documentclass{ctexart}
\usepackage{witharrows}
\begin{document}
$\begin{WithArrows}
A & = (a + 1)^2 \Arrow{我们展开} \\	% 此处Arrow后跟着的便是箭头上的内容
& = a^2 + 2a + 1
\end{WithArrows}$
\end{document}

% 当具有多行公式，但需要跳过某几行公式时，可以对\Arrow进行参数设置
\documentclass{ctexart}
\usepackage{witharrows}
\begin{document}
$\begin{WithArrows}
A & = \bigl((a+b)+1\bigr)^2 \Arrow{}\Arrow{}[jump=2] \\	%此处前一个arrow将连接1、2行，后一个arrow将跳过第二行；注意此时参数设在在\Arrow{}后
& = (a+b)^2 + 2(a+b) +1 \\
& = a^2 + 2ab + b^2 + 2a + 2b +1
\end{WithArrows}$
\end{document}

% 当需要箭头离开公式一定距离时，可以通过在\Arrow{}前设置参数
\documentclass{ctexart}
\usepackage{witharrows}
\begin{document}
$\begin{WithArrows}
A & = \bigl((a+b)+1\bigr)^2
\Arrow[xoffset=1cm]{with \texttt{xoffset=1cm}} \\	% 此时，箭头离开公式1cm，若同时具有多行公式，还需要跳行连接时
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% A & = \bigl((a+b)+1\bigr)^2 \Arrow[xoffset = 2cm]{11}[jump=2]\\
% & = (a+b)^2 + 2(a+b) +1 \\
% & = a^2 + 2ab + b^2 + 2a + 2b +1
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
& = (a+b)^2 + 2(a+b) +1
\end{WithArrows}$
\end{document}

% 若需要使箭头向上，或加粗
% 当在\Arrow前需要设置多个参数时，可以将多个参数设置放在一个[]中
\documentclass{ctexart}
\usepackage{witharrows}
\begin{document}
$\begin{WithArrows}
A & = \bigl((a+b)+1\bigr)^2 \Arrow[tikz = thick, xoffset = 2cm, tikz = <-]{11}[jump=2]\\	% 此时，箭头将加粗并且反向（向上）
& = (a+b)^2 + 2(a+b) +1 \\
& = a^2 + 2ab + b^2 + 2a + 2b +1
\end{WithArrows}$
\end{document}
```

```latex
%----------------------------------------------------------------------------------
%2018.5.1
```

------



## 输入url并合理换行

```latex
% 通常而言，对于一个单词（整个\url可以视作一个长单词）不知如何进行分词，那么Tex就不会对于该单词进行断行；当单词过长且又处于某行末尾时，将出现overful box
% 本质上，需要让\url知道我们需要在何处断行
% 对于该情况，hyperref 宏包提供了两个宏 \UrlBreaks 和 \UrlBigBreaks，略有区别，但一般情况使用 \UrlBreaks 即可
\documentclass{article}
\usepackage{hyperref}
\makeatletter
\def\UrlOrds{\do\_\do\-}	% 记录了一些特殊字符
\def\UrlAlphabet{
      \do\a\do\b\do\c\do\d\do\e\do\f\do\g\do\h\do\i\do\j
      \do\k\do\l\do\m\do\n\do\o\do\p\do\q\do\r\do\s\do\t
      \do\u\do\v\do\w\do\x\do\y\do\z\do\A\do\B\do\C\do\D
      \do\E\do\F\do\G\do\H\do\I\do\J\do\K\do\L\do\M\do\N
      \do\O\do\P\do\Q\do\R\do\S\do\T\do\U\do\V\do\W\do\X
      \do\Y\do\Z}	% 记录了26个英文字母的大小写
\def\UrlDigits{\do\1\do\2\do\3\do\4\do\5\do\6\do\7\do\8\do\9\do\0}	% 记录了10个阿拉伯数字
\g@addto@macro{\UrlBreaks}{\UrlOrds}
\g@addto@macro{\UrlBreaks}{\UrlAlphabet}
\g@addto@macro{\UrlBreaks}{\UrlDigits}	% 使用LaTeX内核提供的 \g@addto@marco，将上述三个宏的内容接在其后说明，允许在上述所有字符处断行
\makeatother
\begin{document}
\url{http://foo.bar.com/documentclassarticleusepackagehyperrefbegindocumenturlenddocument}
\end{document}

%此时， url 将自动换行
```

```latex
%----------------------------------------------------------------------------------
%2018.5.2
```

------



## autoref命令直接产生引用

```latex
%当文章内容引用量较大，易产生混乱， 经常混淆，此时可以通过autoref自动生成引用，智能地告诉我们引用的内容是图、表还是公式
%首先引入hyperref包
\usepackage{hyperref}
%定义自动命令
\def\equationautorefname{式}
\def\footnoteautorefname{脚注}
\def\itemautorefname{项}
\def\figureautorefname{图}
\def\tableautorefname{表}
\def\partautorefname{篇}
\def\appendixautorefname{附录}
\def\chapterautorefname{章}
\def\sectionautorefname{节}
\def\subsectionautorefname{小小节}
\def\subsubsectionautorefname{subsubsection}
\def\paragraphautorefname{段落}
\def\subparagraphautorefname{子段落}
\def\FancyVerbLineautorefname{行}
\def\theoremautorefname{定理}

%接下来，只需要在正文相应部分使用\autoref{label名称}即可
\autoref{label}
```



##浮动体链接不准问题（一）

```latex
% 利用caption宏包修复浮动体超链接不准的问题
% 将 \caption 放在 \includegraphics 后面，然后在稳重对图片进行引用的话，点击超链接后，将调到图片位置而不是浮动体位置
% 利用 caption 宏包可以实现修复这一问题

% 实现做法十分简单，只需要在插入宏包 graphicx 和宏包 hyperref 之外，再插入 caption 宏包即可
\documentclass{article}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage{caption}

\usepackage{mwe} % 能够随机产生文本的宏包
\begin{document}
\begin{figure}[!htb]
\centering
\includegraphics[width = 0.6\linewidth]{example-image.jpg}
\caption{dummy figure}\label{fig:test}
\end{figure}
\blindtext % 添加随机文本，可以在其后通过"[]"控制添加的数量
\clearpage % 添加新一页
\blindtext

This is the hyper-reference of Figure \ref{fig:test}.
\end{document}
```

```latex
%----------------------------------------------------------------------------------
%2018.5.3
```

------

##浮动体链接不准问题（二）

```latex
% 对于上述问题，也可以通过引入 hypcap 的宏包，来解决该类问题
\documentclass{article}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage[all]{hypcap} % 在 hypcap 宏包前添加 all 选项，说明 hypcap 宏包会处理全部类型的浮动体，
\usepackage{mwe} % 是"Minimal Working Example"的简写，是为了产生无意义的测试文字而加载的宏包，实际使用时可以去掉
\begin{document}
\begin{figure}[!htb]
\centering
\includegraphics[width = 0.6\linewidth]{example-image.jpg}
\caption{dummy figure}\label{fig:test}
\end{figure}
\blindtext
\clearpage
\blindtext

This is the hyper-reference of Figure \ref{fig:test}.
\end{document}

% 此时效果与前述类似
```



## 章节编号问题

在 LaTeX 标准文档类中，提供了$\section$，和$\section*$两种命令，用于排版章节标题。其中不带星号的版本有章节编号，会列入目录，同时修改章节标记。带星号的版本只有章节标题格式而不编号，不列入目录，也不会修改章节标记

但有时会希望不编号的章节标题也列入目录中，此时可以考虑三种方法

1. 使用$\section*$手工做目录的处理
2. 使用$\section$但是抑制编号生成

```latex
% 1
% 对于手工做目录的方法，由于在 LaTeX 中处理目录是需要编译两次的，第一次编译过程中， \section 命令将目录信息写入 .aux 文件中，随后在第二次编译过程中， LaTeX 就读取了 .aux文件中的对应信息，形成目录，因此可以考虑模仿 \section 写入 .aux 文件的过程即可
% 对于这种方法，在 LaTeX 中提供了 \addcontentsline{<辅助文件后缀>}{<章节等级>}{名字} 来完成工作
\documentclass{ctexart}
\begin{document}
\tableofcontents
\section*{不编号的章节标题}
\addcontentsline{toc}{section}{不编号的章节标题}
\end{document}

% 2
% 在 LaTeX 标准文档类中， secnumdepth 这个计数器用来控制章节编号深度的。在 article 中，这个计数器默认值是 3，对应的章节命令是 \subsubsection。也就是说，在默认情况下， article 会对 \subsubsection 及其以上所有的章节标题进行编号，也就是 \part, \section, \subsection,\subsubsection
% 在标准文档类中，最大的标题是 \part，它在 book 和 report 中的层次是 [-1] ，在 article 类中的层级是 [0] 。因此，我们只需要将计数器设置为 -2 ，之后章节命令都将不编号
\documentclass{ctexart}
\makeatletter % 对于在文件中需要使用包含 "\@" 字样的命令时，需要借助 \makeatletter 和 \makeatother 命令，即通过前者使 "@" 变为普通字母，通过后者回到原始类
% 符号 @ 是一个保留符号。它在用户编写 .tex 文档的时候和开发者编写宏包/文档类的时候具有不同含义。我们用 \makeatletter 将 @ 的含义切换到开发者模式；在进行修改之后，用 \makeatother 将 @ 的含义切换到用户模式
\newcommand\specialsectioning{\setcounter{secnumdepth}{-2}}
\makeatother
\begin{document}
\tableofcontents
\section{正常编号的章节标题}
\specialsectioning
\section{不编号的章节标题}
\end{document}
% 对于上述方法，可能需要多次编译
```

```latex
%----------------------------------------------------------------------------------
%2018.5.4
```

------



## section中 XeTeX logo显示问题

```latex
% 对于下述代码运行过程中将报错
\documentclass{article}
\usepackage{graphicx}
\def\XeTeX{\leavevmode
\setbox0=\hbox{X\lower.5ex
\hbox{\kern-.15em\reflectbox{E}}\kern-.1667em \TeX}
\dp0=0pt \ht0=0pt \box0 }
\begin{document}
\TeX, \XeTeX
\section{\TeX, \XeTeX}
\TeX, \XeTeX
\end{document}
% 错误信息
! Undefined control sequence. \Gscale@box #1[#2]#3->\leavevmode \def \Gscale@x {#1}\def \Gscale@y {#2}\set...

% 解决方法只需引入另一个宏包即可
\documentclass{article}
\usepackage{xltxtra}
\begin{document}
\TeX, \XeTeX
\section{\TeX, \XeTeX{}, \XeLaTeX{}}
\TeX, \XeTeX
\end{document}
```



## 生成术语

```latex
% 在撰写论文的时候，有时需要生成论文的术语表，用以说明论文中所使用的符号或者是专业术语，给出其解释，可以使用 nomencl 包完成该任务
\documentclass{article}
\usepackage{nomencl} % 引入包
\makenomenclature

\begin{document}
\section*{Main equations}
\begin{equation}
	$$a=frac{N}{A}$$ % 此处需要注意，当在 \begin{equation} 和 \end{equation} 之间存在空行时或者当公式两边不存在 "$$" 将报错
\end{equation}

\nomenclature{$a$}{The number of angels per unit area}
\nomenclature{$N$}{The number of angels per needle point}
\nomenclature{$A$}{The area of the needle point}

The equation $sigma = m a$

\nomenclature{$sigma$}{The total mass of angels per unit area}
\nomenclature{$m$}{The mass of one angel} % 添加专业术语及其解释

follows easily.
\printnomenclature % 生成

\end{document}

% 当完成上述步骤后，由于文件中不存在 .nls 文件，仍无法使用
% 需要执行下述步骤
% 1
% 在文件文件夹中打开 cmd ，输入
latex <filename>.tex
% 2
% 继续输入
makeindex <filename>.nlo -s nomencl -o <filename>.nlc
% 3
% 重新编译源文件即可

% 当你需要使用中文的 术语表 的名字，可以使用下述命令进行修正
\renewcommand{\nomname}{术语表}
```

```latex
%-----------------------------------------------------------------------------------
%2018.5.5
```

------



## 通过enumerate宏包设置列表编号对齐方式

```latex
% 当采用 enumerate 环境默认的编号对齐方式时，编号右对齐，内容左对齐
% 当采用 enumitem 宏包，设置 align = left ，此时编号和内容都为左对齐；但此时编号与内容的间距过大
% 此时可以通过修改控制列表内容与页面的左右间距的命令 \parshape 来实现
% 解决方法为：量取每一个编号的宽度，动态调整 \parshape 的缩进；同时借助 enumitem 包中的 \SetLabelAlign 定义一个特殊的对齐方式

\documentclass{article}
\usepackage{enumitem}
\makeatletter

% 定义对齐方式 hang
\SetLabelAlign{hang}{
  #1
\aftergroup\adjustparshapeindent}
% 编号 #1 会通过 \sbox 存到 \@tempboxa 中，为避免全局设置，
% 需要用 \aftergroup 跳到盒子外部来设置
\newcommand*\adjustparshapeindent{
  \@ifnextchar\egroup
    {\aftergroup\adjustparshapeindent}
    {\adjustparshapeindent@auxi}}
\newcommand*\adjustparshapeindent@auxi{
  \unless\ifdim\wd\@tempboxa=\labelwidth
    \adjustparshapeindent@auxii
  \fi}
% 调整 \parshape 的缩进
\newcommand*\adjustparshapeindent@auxii{
  \dimen@ = \dimexpr\wd\@tempboxa-\labelwidth\relax
  \labelwidth = \wd\@tempboxa
  \advance\linewidth -\dimen@
  \advance\leftmargin \dimen@
  \advance\@totalleftmargin \dimen@
  \parshape \@ne \@totalleftmargin \linewidth}

\makeatother

\begin{document}
\begin{enumerate}[align=hang, start=9]
\item test\\test
\item test\\test
\end{enumerate}
\end{document}
```



## 选择题列表环境

```latex
% 当想设置的选择题题目之间需要通过灰色线条隔开时，此时可以通过以下方法
% TiKz 介入定制
\documentclass{article}
\usepackage{tikz}
\usepackage{enumitem}

\newlist{fancyenum}{enumerate}{2}
\setlist[fancyenum,1]{ % 表示对一级列表进行设置；标签为阿拉伯数字加点
  leftmargin=12pt,
  labelsep=10pt,
  label={\protect\begin{tikzpicture}[]
    \protect\node[overlay,text width=\textwidth,fill=gray!20,anchor=west,inner sep=0pt,minimum height=2em] (bg) {};
    \protect\node[overlay,anchor=west,minimum height=2em,inner sep=0pt,fill=black,align=center,text width=2em,text=white,font=\bfseries] at (bg.west) {\arabic*};
    \protect\node {\rule[5em]{0pt}{0pt}};
    \protect\end{tikzpicture}} % \protect 命令用于保护脆弱的命令，由于某些宏在使用时会被展开，但在生成表或者写成辅助文件时，直接展开就会报错，此时需要将展开的时机进行延迟，该命令的大致作用既是如此，延迟展开
  }
\setlist[fancyenum,2]{label=\Alph*),topsep=0pt,leftmargin=22pt} % 表示对二级列表进行设置；标签为括号加小写英文加点

\begin{document}
\sffamily %以下内容采用无衬线字体

\begin{fancyenum}
\item Some test text
  \begin{fancyenum}
  \item First
  \item Second
  \item Third
  \end{fancyenum}
\item Some test text
  \begin{fancyenum}
  \item First
  \item Second
  \item Third
  \end{fancyenum}
\item Some test text
  \begin{fancyenum}
  \item First
  \item Second
  \item Third
  \end{fancyenum}
\end{fancyenum}

\end{document}
```



```latex
%------------------------------------------------------------------------------------
%2018.5.6
```

------



## 带圈数字和带圈数字列表

```latex
% 对于带有圆圈的数字， LaTeX中提供了 \textcircled 命令，但效果并不好，这里使用的 TiKZ 绘制的方法
% 基本思路：定义一个新命令，接受一个数字参数，用 TikZ 在其周围画上圆圈，同时需要考虑基线与对齐的问题
\usepackage{tikz}
\newcommand*{\circled}[1]{\lower.7ex\hbox{\tikz\draw (0pt, 0pt)
    circle (.5em) node {\makebox[1em][c]{\small #1}};}}
% 完成带圆圈数字的定义

% 如果上述命令需要在列表中使用时，由于具有前一次提到的'脆弱命令'的问题，需要处理一下，此处与上次不同，选择使用 etoolbox 宏包提供的 \robustify 来进行处理
% 同时结合 enumitem 宏包完成
\documentclass{article}
\usepackage{tikz}
\usepackage{etoolbox}
\usepackage{enumitem}

\newcommand*{\circled}[1]{\lower.7ex\hbox{\tikz\draw (0pt, 0pt)
    circle (.5em) node {\makebox[1em][c]{\small #1}};}}
\robustify{\circled} % 使用 \rubustify 进行强化

\begin{document}
\mbox{}\rlap{\rule{.7\linewidth}{.4pt}} % \mbox{} 用于绘制盒子，不具有线条；\rule[提示]{宽度}{高度} 用于制作标尺盒子； \rlap 用于叠加图形，有 "\llap" 和 "\rlap" 两种
This is the circled number \circled{20}.

\begin{enumerate}[label=\circled{\arabic*}] % 使用 enuitem 中的 \item 命令，将其中的 \label 替换为定义的样式，同时将数字类型定义为 "\arabic*"(阿拉伯数字)
\item I
\item am
\item happy
\item to
\item today
\end{enumerate}
\end{document}
```



```latex
%------------------------------------------------------------------------------------
%2018.5.7
```

------



## 多级列表

```latex
% 通常输入多级列表的方式
\begin{itemize}
\item 1
\begin{itemize}
\item 2
\end{itemize}
\end{itemize}

% 也可以使用 iitem 包，此时输入较为方便
\begin{itemize}
\item 1
\iitem 2
\end{itemize}
```



## 在文本的同一行开始一个列表环境

```latex
% 有时希望在文本的同一行开始一个列表环境，而非在默认的下一行开始
% 同时我们希望标签仍然在垂直方向上对齐
% 此时可以使用 description 对其距离等进行修改
\documentclass{article}
\usepackage{enumitem}
\usepackage{lipsum} % just for the example

\newlength{\jeroenlen} % 设置长度
\newenvironment{example} % 设置环境
{\settowidth{\jeroenlen}{\textbf{Example:}}
\begin{description}[leftmargin=\jeroenlen,labelwidth=0pt,labelsep=0pt]
\item[\textbf{Example:}]
\begin{itemize}[leftmargin=1.5em,labelsep=.5em]}
{\end{itemize}\end{description}}

\begin{document}
\lipsum[2]
\begin{example}
\item Such and such
\item So and so
\item Enough
\end{example}
\lipsum[3]
\end{document}
```

```latex
% ------------------------------------------------------------------------------------
% 2018.5.8
```

------



## 列表继续前文计数

```latex
% 对于一般的列表环境，即 enumerate 环境，当使用新的环境后，计数将重新从 1 开始
% 使用 enumitem 宏包，并使用其 [resume] 参数能承接前文的数字
\documentclass[a4paper]{article}
\usepackage{enumitem} % load the package
\begin{document}
  \section{My items}
    \begin{enumerate}
      \item First item
      \item Second item
    \end{enumerate}
  \section {Additional items}
    \begin{enumerate}[resume] % tell the enumerate to resume numbering
      \item Third item
      \item Fourth item
    \end{enumerate}
\end{document}
```



## multienum排版

```latex
% multienum 使用简介
\mitemx{} % 该行具有一个编号
\mitemxx{}{} % 具有两个编号
\mitemxxx{}{}{} % 具有三个编号
\mitemxox{}{} % 具有三个编号，中间编号的左部为空白，所以第一个编号可以延伸到该空白中
\mitemxxo{}{} % 具有三个编号，第三个编号的左部为空白，所以第二个编号可以延伸到该空白中
```

```latex
% 实例
%This is a 2-page sample illustrating how to use the
%multienum package
\documentclass{article}
\setlength{\textwidth}{6in}
\setlength{\textheight}{8.5in}
\setlength{\topmargin}{-0.5in}
\setlength{\oddsidemargin}{0.25in}
\usepackage{multicol,multienum} % 引入包; multicol 多列使用
\begin{document}
\begin{center}
{\Large\bf Sample formating using {\tt multienumerate}} % \tt 打印字体
\end{center}

\bigskip % 段落之间间距，同类型的还有 \medskip, \smallskip
Sometimes we want to typeset the solutions to exercises. This
is easy to do using the {\tt multienumerate} environment.
\subsection*{Answers to All Exercises}
\begin{multienumerate}
\mitemxxxx{Not}{Linear}{Not}{Quadratic}
\mitemxxxo{Not}{Linear}{No; if $x=3$, then $y=-2$.}
\mitemxx{$(x_1,x_2)=(2 \frac{1}{3}t,t)$ or
$(s,3s-6)$}{$(x_1,x_2,x_3)=(2 \frac{5}{2}s-3t,s,t)$}
\mitemx{$(x_1,x_2,x_3,x_4)= (\frac{1}{4} \frac{5}{4}s
\frac{3}{4}t-u,s,t,u)$
or $(s,t,u,\frac{1}{4}-s \frac{5}{4}t \frac{3}{4}u)$}
\mitemxxxx{$(2,-1,3)$}{None}{$(2,1,0,1)$}{$(0,0,0,0)$}
\end{multienumerate}

\bigskip
\hrule

\bigskip

We can also enumerate the items using an even-only or odd
only
counter.
\subsection*{Answers to Even-Numbered Exercises}
\begin{multienumerate}[evenlist]
\mitemxxxx{Not}{Linear}{Not}{Quadratic}
\mitemxxxo{Not}{Linear}{No; if $x=3$, then $y=-2$.}
\mitemxx{$(x_1,x_2)=(2 \frac{1}{3}t,t)$ or
$(s,3s-6)$}{$(x_1,x_2,x_3)=(2 \frac{5}{2}s-3t,s,t)$}
\mitemx{$(x_1,x_2,x_3,x_4)= (\frac{1}{4} \frac{5}{4}s
\frac{3}{4}t-u,s,t,u)$
or $(s,t,u,\frac{1}{4}-s \frac{5}{4}t \frac{3}{4}u)$}
\mitemxxxx{$(2,-1,3)$}{None}{$(2,1,0,1)$}{$(0,0,0,0)$}
\end{multienumerate}

\hrule

\subsection*{Answers to Odd-Numbered Exercises}
\begin{multienumerate}[oddlist]
\mitemxxxx{Not}{Linear}{Not}{Quadratic}
\mitemxxxo{Not}{Linear}{No; if $x=3$, then $y=-2$.}
\mitemxx{$(x_1,x_2)=(2 \frac{1}{3}t,t)$ or
$(s,3s-6)$}{$(x_1,x_2,x_3)=(2 \frac{5}{2}s-3t,s,t)$}
\mitemx{$(x_1,x_2,x_3,x_4)= (\frac{1}{4} \frac{5}{4}s
\frac{3}{4}t-u,s,t,u)$
or $(s,t,u,\frac{1}{4}-s \frac{5}{4}t \frac{3}{4}u)$}
\mitemxxxx{$(2,-1,3)$}{None}{$(2,1,0,1)$}{$(0,0,0,0)$}
\end{multienumerate}

\bigskip
\hrule

\bigskip

Sometimes we want to create sublists which are
enumerated using an alpha counter.

\begin{multienumerate}
\mitemx{Which of the following numbers is the solution of the
equation
$x 3=7$:}
\begin{multienumerate} % 此时选项名为(a),(b)……；当在一个 multienumerate 环境中嵌套一个 multienumerate 环境时，内容环境的编号将变为字母
\mitemxxxx{1}{2}{3}{4}
\end{multienumerate}
\mitemx{The value of $\log_28$ is:}
\begin{multienumerate}
\mitemxxxx{1}{$-1$}{3}{$-3$}
\end{multienumerate}
\end{multienumerate}
\pagebreak

\begin{multicols}{2} % 两列
\subsection*{Answers to All Exercises}
\begin{multienumerate}
\mitemxx{Not}{Linear}
\mitemxx{Not}{Quadratic}
\mitemxx{Not}{Linear}
\mitemx{$(x_1,x_2)=(2 \frac{1}{3}t,t)$ or
$(s,3s-6)$}
\mitemx{$(x_1,x_2,x_3)=(2 \frac{5}{2}s-3t,s,t)$}
\mitemx{$(x_1,x_2,x_3,x_4)= (\frac{1}{4} \frac{5}{4}s
\frac{3}{4}t-u,s,t,u)$
or $(s,t,u,\frac{1}{4}-s \frac{5}{4}t \frac{3}{4}u)$}
\mitemxx{$(2,-1,3)$}{None}
\mitemxx{$(2,1,0,1)$}{$(0,0,0,0)$}
\mitemxx{Not}{Linear}
\mitemxx{Not}{Quadratic}
\mitemxx{Not}{Linear}
\mitemx{$(x_1,x_2)=(2 \frac{1}{3}t,t)$ or
$(s,3s-6)$}
\mitemx{$(x_1,x_2,x_3)=(2 \frac{5}{2}s-3t,s,t)$}
\mitemx{$(x_1,x_2,x_3,x_4)= (\frac{1}{4} \frac{5}{4}s
\frac{3}{4}t-u,s,t,u)$
or $(s,t,u,\frac{1}{4}-s \frac{5}{4}t \frac{3}{4}u)$}
\mitemxx{$(2,-1,3)$}{None}
\mitemxx{$(2,1,0,1)$}{$(0,0,0,0)$}
\mitemxx{Not}{Linear}
\mitemxx{Not}{Quadratic}
\mitemxx{Not}{Linear}
\mitemx{$(x_1,x_2)=(2 \frac{1}{3}t,t)$ or
$(s,3s-6)$}
\mitemx{$(x_1,x_2,x_3)=(2 \frac{5}{2}s-3t,s,t)$}
\mitemx{$(x_1,x_2,x_3,x_4)= (\frac{1}{4} \frac{5}{4}s
\frac{3}{4}t-u,s,t,u)$
or $(s,t,u,\frac{1}{4}-s \frac{5}{4}t \frac{3}{4}u)$}
\mitemxx{$(2,-1,3)$}{None}
\mitemxx{$(2,1,0,1)$}{$(0,0,0,0)$}

\end{multienumerate}

\subsection*{Multiple Choice}
\begin{multienumerate}
\mitemx{Which of the following numbers is the solution of the
equation
$x 3=7$:}
\begin{multienumerate}
\mitemxxxx{1}{2}{3}{4}
\end{multienumerate}
\mitemx{The value of $\log_28$ is:}
\begin{multienumerate}
\mitemxxxx{1}{$-1$}{3}{$-3$}
\end{multienumerate}
\mitemx{Which of the following numbers is the solution of the
equation
$x 3=7$:}
\begin{multienumerate}
\mitemxxxx{1}{2}{3}{4}
\end{multienumerate}
\mitemx{The value of $\log_28$ is:}
\begin{multienumerate}
\mitemxxxx{1}{$-1$}{3}{$-3$}
\end{multienumerate}
\mitemx{Which of the following numbers is the solution of the
equation
$x 3=7$:}
\begin{multienumerate}
\mitemxxxx{1}{2}{3}{4}
\end{multienumerate}
\mitemx{The value of $\log_28$ is:}
\begin{multienumerate}
\mitemxxxx{1}{$-1$}{3}{$-3$}
\end{multienumerate}
\end{multienumerate}
\end{multicols}

\end{document}
```

```latex
% -------------------------------------------------------------------------------------
% 2018.5.9
```

------



## 参考文献标题编号

```latex
% 一般而言，论文中参考文献、索引等章节的标题是不编号的，但是在一些特殊情况下，我们可能为其编号
% 对于参考文献而言，大体都是使用 thebibliography 环境进行排版，生产参考文献列表。该环境一方面打印参考文献标题，另一方面打印参考文献列表。打印参考文献标题的方式就是调用 \section* (在 article 文档类中) 或 \chapter* (在 book 类中)
% 我们需要做的，就是重定义 thebibliography 环境，使其调用无星号的版本（此时标题将产生编号），即调用 \section 或 \chapter
% thebibliography 环境对应的两个命令是 \thebibliography 和 \endthebibliography；而 \section* 或 \chapter* 调用位于 \thebibliography 中，故我们只需要使用 xpatch 或 etoolbox 宏包提供的 \xpatchcmd 或 \patchcmd 对 \thebibliography 打上补丁即可

% \xpatchcmd 命令介绍
% \xpatchcmd 命令接受五个参数：\xpatchcmd{命令}{搜索}{替换}{成功}{失败}
% 命令：待处理的命令
% 搜索：需要被替换的部分
% 替换：将被替换的内容
% 成功：替换成功执行的内容
% 失败：替换失败执行的内容

% 实现代码
\documentclass{article}
\usepackage{xpatch}
\xpatchcmd{\thebibliography}{\section*}{\section}{}{}
\begin{document}
\begin{thebibliography}{0}
    \bibitem{citekey} test % 对于 \bibitem ，一般使用 \bibitem[label]{cite_key} 当 [label] 缺少时，则自动使用 enumiv 计数器，对于 {citekey} 则是用来引用 
\end{thebibliography}
\end{document}
```



## 解决flushend平衡双栏文本缩进问题

```latex
% 在双栏模式下，不少用户希望最后一页双栏能够平衡起来。通常这是通过 flushend 实现最后一页的平衡，但是发现此时段落会出现一个小小的缩进
% 这是由于 flushend 新版本的包导致的，只需要添加一个参数 keeplastbox 即可
\usepackage[keeplastbox]{flushend}
```

```latex
%---------------------------------------------------------------------------------------
%2018.5.11
```

------



## 实现参考文献与正文的双向链接

```latex
% 在正文中引用参考文献时，一般需要使用 hyperref 宏包，然后，点击医用链接即可跳转到相应的参考文献，但若文章内容较多，此时通过参考文献查找到正文相应的引用的位置就较为麻烦
% 可以通过 hyperref 的参数 backref = page 或 pagebackref 即可
% 具体使用方法如下：
\usepackage[linkcolor=blue,citecolor=blue,backref=page]{hyperref}
```



## thebibliography 环境

```latex
% 可以不通过 .bib 文件来生成参考文献环境，即使用默认的 thebibliography 环境
% 参考文献格式
\begin{thebibliography}{编号样本}
\bibitem[记号]{引用标记}条目
\end{thebibliography}

% 实例
\documentclass{ctexart}
\begin{document}
引用一篇文章 \cite{article1}\\
引用一本书 \cite{boobk1}\\

\renewcommand\refname{参考文献}
\begin{thebibliography}{99} % 数字 99指的是参考文献的项目按照数字进行编号，并且最多为99个，可以按照需求进行更改
\bibitem{article1}文章标题 作者 期刊 年代 页码……
\bibitem{book1}书标题 作者 出版社 年代
\end{thebibliography}

\end{document}	

% 如何将文档类中的 Reference 改为中文的 '参考文献'
% 若是 article 类，使用 \renewcommand\refname{参考文献}
% 若是 book 类，使用 \renewcommand\bibname{参考文献}
```

```latex
% ---------------------------------------------------------------------------------------
% 2018.5.12
```

------



## 如何使连续的参考文献缩写

```latex
% 对于 latex 中参考文献，希望出现 [2]-[5] 的形式
% 可以使用 cite 包命令来实现
\usepackage{cite}
\def\citepunct{],[}
\def\citedash{]-[}
% 此时，若连续引用的文献较少时，文献之间通过 ',' 连接，若连续文献较多时，则通过 '-' 连接

% -------------------------------2018.6.1-----------------------------------------------------
% 当不采用 cite 包时，对于连续参考文献， latex 应该是默认连续，采用 '-' 连接，如 "[1-3]"，但不会对英文引用名缩写
% 当需要对英文引用名缩写时，可以使用 natbib 包
\usepackage[numbers,sort&compress]{natbib}
% 对于上述代码示例，numbers 表示数字类型的引用名，并置于前； sort&compress 表示对于英文引用名，按照字母顺序排序，并且采用缩写，并置于后；
% 将两者顺序调换，则在输出中英文缩写在前，数字内容在后
```



## 将参考文献编号左右中括号去除

```latex
% 实现代码
\usepackage[numbers]{natbib}
\setcitestyle{open = {}, close = {}}
```

```latex
% -----------------------------------------------------------------------------------------
% 2018.5.13
```

------





## 参考文献添加页码

```latex
% 在参考文献中，需要添加页码时，需要使用 'pages'
% 示例
@article{Shannon,
author = {C E SHANNON},
title = {A mathematical theory of communication},
journal = {The bell system technical journal},
year = {1948},
volume = {27},
pages = {379--423, 623--656},
}
% 对于 .bib 类型的参考文献，需要注意不同的信息之间需要用逗号隔开，且同时，最好使用 '{}' 将一组信息给括起来，不然对于有些信息将无法识别而报错
```



## 实现参考文献引用上标

```latex
% 将参考文献作为上标引用，可使用 overcite 宏包，或者使用 nabib 宏包中的 super 参数，然后在需要引用处使用 cite 命令即可
%　但上述方法中的上标引用均不出现方括号
% 若需出现方括号的情况，可以对 cite 命令的格式进行修改
\makeatletter
\def\@cite#1#2{\textsuperscript{[{#1\if@tempswa , #2\fi}]}}
\makeatother
% 此时在文中进行 cite 命令引用时，将出现上标的方括号
```

```latex
% -----------------------------------------------------------------------------------------
%2018.5.14
```

------



## 将参考文献序号改为作者缩写

```latex
% 由 latex 自动生成的参考文献列表中，序号自动为数字
% 若想将数字换为相应作者或者其他的信息，在 thebibliography 环境中，只需修改相应的 \bibitem 信息即可
% 示例
\begin{thebibliography}{99}
\bibitem[display]{cite_key} % display 即控制在文中引用时的显示样式，而 cite_key 则为该条目的标识，用于引用
```

```latex
% ------------------------------------------------------------------------------------------
% 2018.5.17
```

------



## 将公式编号样式变为参考文献中样式

```latex
% 可以通过改变相应的命令样式来实现
% 示例
\documentclass{article}
\usepackage{amsmath}
\setlength\textwidth{181.0pt}
\makeatletter
\def\tagform@#1{\maketag@@@{\ignorespaces[#1]\unskip\@@italiccorr}}
\makeatother

\begin{document}
\section{Test}
\begin{equation}\label{eq:1}
a+b=c
\end{equation}
This is a equation’s example.please see \eqref{eq:1}.
\end{document}
```

```latex
%---------------------------------------------------------------------------------------------
% 2018.6.1
```

------



## Latex辅助文件

```latex
% 对于 Latex 在使用交叉引用、参考文献、目录等功能时，首先需要生成辅助文件，然后再次编译时读入相应的辅助文件才能得到正确的结果
% Latex 中辅助文件一般有以下几种
.log % 排版引擎生成的日志文件，供排查错误使用
.aux % 生成的主辅助文件，记录交叉引用、目录、参考文献的引用等
.toc % 生成的目录记录文件
.lof % 生成的图片目录记录文件
.bbl % BibTex 生成的参考文献记录文件
.blg % BibTex 生成的日志文件
.idx % LaTex 生成的供 makeindex 处理的索引记录文件
.ind % makeindex 处理 .idx 文件，生成的格式索引记录文件
.ilg % makeindex 生成的日志文件
.out % hyperref 宏包生成的 PDF 书签记录文件

% 当某些辅助文件中出现某些错误时，若没有删除原辅助文件，继续编译，那么错误的部分仍然在，读取的时候，读取到的仍然是错误的部分，所以需要将原辅助文件删除，重新编译生成相应的辅助文件，再二次编译，从而获得正确的结果 
```



## Latex 宽度

```latex
% latex 中宽度涉及到页面宽度的有以下几种：
\linewidth % 当前行的宽度
\columnwidth % 当前分栏的宽度
\textwidth % 整个页面版芯的宽度
\paperwidth % 页面纸张的宽度

$ 宽度关系
% 对于单栏文本， \columnwidth 和 \textwidth 应该保持一致；
% 对于多栏文本， \textwidth = n * \columnwidth + (n - 1) * \columnsep
% 对于 minipage环境，除了 \paperwidth 之外，其余三个宽度值都将随 minipage 的宽度发生变化，并且当 minipage环境结束时，恢复原样
% 对于  parbox ， \textwidth 与 \columnwidth 不会改变，但 \linewidth 会发生变化

% 对于各个宽度， \linewidth 是相对最灵活的值，它在 list 环境中 或在 \parbox 中都将发生变化

$ 总结
% 当需要在列表中使用表格、图片的宽度时，应该使用 \linewidth
% 需要充满整个页面宽度时，应该使用 \textwidth ；例如 figure / table
% 需要充满整个分栏时，需要使用 \columnwidth ；例如 figure / table / tabularx / tabu

% ---------------------------------------------------------------------------------------------
% 对于 minipage 和 \parbox
% 对于整个段落需要放入一个盒子中时，可以使用 \parbox 或者 minipage ，两者语法类似，并且都提供了对齐方式、宽度等的选项。
% 需要注意：这里的对齐方式是指盒子与周围内容的纵向关系，分别用 t 、 c 、 b 表示居顶、居中和居底对齐
% \parbox 使用
\parbox[pos][height][contentpos]{width}{text}
% minipage 使用
\begin{minipage}[pos][height][contentpos]{width}
text
\end{minipage}

% 两者区别在于，在 \parbox 中无法使用全部命令和环境，但在 minipage 中，几乎可以使用所有命令和环境
```

```latex
% ---------------------------------------------------------------------------------------------
% 2018.6.2
```

------

```latex
% 将脚注缩进固定宽度
% 需要 scrextend 包，命令如：
\deffootnote[<mark width>]{<indent>}{<parindent>}{<definition>}
% ---------------------------------------------------------------------------------------------
\documentclass{book}
\usepackage{scrextend} % 引用缩进包
\deffootnote[1.5em]{1.5em}{1em}{\thefootnotemark.\space} % 缩进数量定义
\usepackage{lipsum} % 用于生成随机文字
\usepackage{hyperref} %用于生成超链接

\begin{document}
\mainmatter % \mainmatter 将打开阿拉伯页码计数器，并对页码从新计数
\setcounter{footnote}{8} % 从 '8' 开始计数，则生成的脚注开始数字为 '9'
a\footnote{\lipsum*[2]}b\footnote{\lipsum[2]\lipsum*[3]}
\end{document}

% ---------------------------------------------------------------------------------------------
% 也可以通过 footmisc 包来实现
\documentclass{book}
\usepackage[hang]{footmisc}
% do this \AtBeginDocument so that all font settings will be already made
\AtBeginDocument{
 % set the \footnotemargin to 1.5em at \footnotesize
 \footnotesize\setlength{\footnotemargin}{1.5em}\normalsize
 % set the footnote parindent equal to the normal parindent
 \edef\hangfootparindent{\the\parindent}
 % no parskip in foonotes
 \renewcommand{\hangfootparskip}{0pt}
}
\usepackage{lipsum}
\begin{document}
\mainmatter
\setcounter{footnote}{8}
a\footnote{\lipsum*[2]}b\footnote{\lipsum[2]\lipsum*[3]}
\end{document}
```

```latex
% center 环境与 \centering 命令的区别
% 很多情况再插入图片时，会使用 \begin{center}...\end{center}来使图片居中，但这个环境会产生额外的垂直空白，应该是使用 \centering 命令
\usepackage{graphicx}
\begin{figure}[ht]
\centering
\includegraphics{filename}
\caption{text}
\end{figure}

% 对于两者，看起来效果是一样的，但是略有差异
% 对于 center 环境，定义如下：
\def\center{\trivlist \centering\item\relax}
\def\endcenter{\endtrivlist}
% 所以对于 center 环境，实际是一个 trivlist 列表，也是产生空白的原因

% 对于 \centering，定义如下
\def\centering{%
  \let\\\@centercr
  \rightskip\@flushglue\leftskip\@flushglue
  \parindent\z@\parfillskip\z@skip}
% 可以看出， \centering 环境实际上是通过 \leftskip ， \rightskip 命令来实现居中效果
% 所以不会产生垂直空白，但由此需要限制命令作用的范围
{\centering Text    
}
```

```latex
%----------------------------------------------------------------------------------------------
% 2018.6.9
```



```latex
% mathptmx 宏包是一个为 LaTex 设计的字体哄好，默认 rmfamily 为 Nimbus Roman No9 L 类型字体；同时将数学字体设置为 Italic 字形
% 使用该宏包可能需要借助 fontenc 宏包来辅助设置字体编码
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{mathptmx}
\begin{document}
This is the typeface Nimbus Roman No9 L, and fontface for mathematics has been modified to the Italic counterpart.
Enjoy!
\end{document}
% 对于 fontenc 宏包，用于英文，主要是用于欧洲重音字符等
% fontenc 用来嵌入字体（一般用 T1 ，不用 OT1 ; inputenc 用来识别输入编码（这个只在写非英文的、带声调的拉丁语系如法、德、中欧和UTF8有点意义，CJK完全用的自己的体系）
%　对于 T1 ：
%　在 LaTeX 中，默认字体是按 OT1 编码的计算机现代字体，它不包含欧洲重音字符，因此也无法对欧洲文字进行断词处理；该宏包可以调用各种编码字体，并可有多重选项，其中最后的选项将成为系统默认编码；欧洲 EC 字体就是采用 T1 科克编码字体，它把有关重音符号的一些字母作为独立的字母，而不是像 OT1 编码，将普通字母和重音符号进行组合。华盛顿大学斯拉夫编码的 OT2 字体可用于俄语、保加利亚语等斯拉夫语的排版
% 例如，在 OT1 编码下（或是其它不包含字符形状 ö 的编码），\"{o} 会被翻译成 \accent"7F o；在 T1 编码下，则是 \char"F6

% ----------------------------------------------------------------------------------------------
% 作为 mathptmx 类似的宏包， newtx 宏包也使用 Nimbus Roman No9 L 及 Itallic 字形
% 同时，newtx 还会做额外的工作：
% 将正文 Sans Serif 字体设置为 Helvetica （某个开源近似版）
% 将正文 Monospace 字体设置为 Times 的等宽版本
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{newtxtext, newtxmath}
\begin{document}
This is the typeface Nimbus Roman No9 L, and fontface for mathematics has been modified to the Italic counterpart.
\textsf{The sans serif family is Helvetica} and \texttt{the monospace family is also Times}.
Enjoy! % \textsf 为无衬线字体； \texttt 为打字机字体
\end{document}
```

```latex
% LaTex 字体机制
$ .def 文件
% t1enc.def 之类的 <encoding>enc.def 文件定义了字符形状与编码的对应关系，LaTeX 读入这些文件之后，才能在相应的编码下正确调用字符形状来排版。在任意时刻，都有一个当前的字体编码。诸如 \"{o} 的命令，在不同编码下的效果是不一样的。例如，在 OT1 编码下（或是其它不包含字符形状 ö 的编码），\"{o} 会被翻译成 \accent"7F o；在 T1 编码下，则是 \char"F6
% 当加载 fontenc 宏包的时候，LaTeX 就会读入 <encoding>enc.def 文件。具体读入的文件，由 fontenc 宏包的参数确定。每次读入 <encoding>enc.def 文件就改变一次当前字体编码。和大多数宏包不同，fontenc 宏包可以加载多次，以便根据不同的字体指定不同的编码。有一些字体相关的宏包，会在内部隐式地调用 fontenc 宏包（比如 textcomp 宏包）。在 \begin{document} 处的字体编码，则是最后一次传给 fontenc 宏包的参数

$ .fd 文件
% 当 LaTeX 遇到 \fontfamily{<family>}\selectfont 的时候（可能隐式地调用，比如在 \ttfamily 之类的字体声明处，以及在 \textsf 之类的字体命令处），LaTeX 会在内部标中查询是否有已知的，由 \DeclareFontFamily{<encoding>}{<family>}{<tokens>} 定义的组合

% <encoding>+<family>
% <encoding> 就是当前的字体编码。
% 假设当前的字体编码是 T1，然后希望使用 Palatino 字族（ppl），但 T1+ppl 的组合没有定义（也就是 \T1+ppl 命令未定义，对的，命令中间有个加号），那么 LaTeX 就会去寻找 t1ppl.fd 或者大写版本的 T1ppl.fd 文件。如果二者都找不到，那么 LaTeX 就会输出警告，告诉用户「当前的字体我找不到，不过我会用另外的字体来替代。不过，这种替代，不会改变当前的字体编码

% .fd 文件总是以 \DeclareFontFamily 声明开头，然后跟着若干个 \DeclareFontShape 命令。这些命令组合在一起，对应了 <encoding>+<family> 的组合
%当然，你也可以在导言区里写 \DeclareFontFamily 或者 \DeclareFontShape 这样的命令。\DeclareFontShape 必须与紧跟的 \DeclareFontFamily 对应。这些声明会对应字体四个维度的属性声明，并对应一个字体尺寸文件（font metric file）

\usefont{T1}{ppl}{b}{it} %会指向 pplb8t 这个字体尺寸。具体来说，字体尺寸文件又两种：.vf 文件或者 .tfm 文件。如果存在 pplb8t.vf 文件，那么 TeX 会优先加载它，否则就会加载 pplb8t.tfm 文件。二者必需有一个，否则就会报错

%在 \DeclareFontShape 命令中，你可以设定字体替换等规则；如果 LaTeX 没有找到合适的字体替换规则，那么就会使用默认字体去替换。如果 .fd 文件里，或者导言区中的，\DeclareFontShape 写错了，也会导致错误（Corrupt NFSS tables）

$ .vf 文件
% 字体尺寸文件可以是虚拟的，pplb8t 正是这种情况。.vf 尺寸文件中有字符边界框、意大利体修正、铅空、连字等信息，还有一些关于从其它文件中（虚拟的或者实际存在的）选择时字符形状的信息。此处，pplb8t.vf 选择了一个实际存在的字符形状 pplb8r

(MAPFONT D 0
   (FONTNAME pplb8r)
   (FONTCHECKSUM O 25012244013)
   (FONTAT R 1.0)
   (FONTDSIZE R 10.0)
   )

% 并按照 T1 字体编码重新对字符形状做了排序。例如，在 pplb8t.vf 的 "F7" 位上 （八进制 `367），有如下声明

(CHARACTER O 367
   (CHARWD R 0.832996)
   (CHARHT R 0.485498)
   (CHARDP R 0.011493)
   (MAP
      (SETCHAR O 234)
      )
   )

% 即字符形状 œ（你在 LaTeX 里可以用 \oe 输出它）实际会在 pplb8r 的以八进制计算的第 `234 个位置（十六进制："9C）中取得，不过实际的用户是不会像关心它的。这里也包含了关于字符形状的尺寸信息：宽度 8.32996pt、高度 4.85498pt、深度 0.11493pt，并且意大利体修正为 0（这是在字体大小为 10pt 时候的值，否则需要按比例做额外的换算）

$ .tfm 文件
% .tfm 文件（在本例中 pplb8r.tfm 文件必须存在）中的内容格式和 .vf 文件的格式完全相同，不过，它可以指向其他字体尺寸文件

$ .vf 和 .tfm 文件区别
% .tfm 为字体描述文件，用于设定字体的宽、高和间距等，LaTex用以规划页面
% .vf 为Tex 虚拟字体

$ 虚拟字体
% 从不同物理字体文件中分别选取部分字符，组成的字体即为"虚拟字体"；在 LaTex 中，虚拟字体就像是真实字体一样
```

```latex
% ----------------------------------------------------------------------------------------------
% 2018.6.10
```



```latex
%　在 Tex Live 中如何安装已经下载好的 .sty 宏包

% 1.
% 获取相应的 .sty 文件；若找的到相应的 .sty 文件，就直接下载；若是文本文件，就先将其拷贝合适的位置，用 txt 打开，粘贴，再更改后缀名为 .sty 即可；注意，需要将完成的 .sty 文件放入到一个同名的文件夹中。如，mcode.sty 文件的文件夹名应为 mcode

% 2.
% 将该文件夹放在 Tex Live 相应的宏包文件夹中；本机相应位置为: D:\texlive\texmf-dist\tex\latex 。此时该宏包与其他宏包文件处于同一级mull

% 3.
% win+r 输入 cmd 进入 dos ，然后输入 texhash ，以用于更新目录以便 Latex 能找到安装的新宏包
```



```latex
% 如何使用 times new roman 字体
% 使用 times 宏包后，可以将文本的缺省字体换成 times new roman 字体；若安装有 mathtime 宏包，也可将数学环境中的字体都变成 times new roman 字体
\usepackage{times}
\usepackage[mtbold, mtpluscal, mtplusscr]{mathtime}

% 当没有 mathtime 宏包时，使用 mathptmx 也可
\documentclass{article}

\usepackage{amsmath}
\usepackage{times}
\usepackage{mathptmx}
\setlength\textwidth{207.0pt}
\begin{document}

Text
Text Text Text Text 
Text Text Text Text

 \begin{equation} (a+b)^2 = a^2 + 2ab
+b^2 \end{equation}
 \begin{equation} (a-b)^2 = a^2 - 2ab + b^2
\end{equation}

 $$
 \bar{x}
 $$
\begin{equation}
\sum_{i=0}^n = \int_a^b f(x)dx \end{equation}

\end{document}
```

```latex
% ------------------------------------------------------------------------------------------------
% 2018.6.11
```



```latex
% 浮动体即为会移动的文本框

% 为什么要使用浮动体
% 由于图片表格等占据篇幅较大的内容，若强行插入再"当前位置"是不合适的，通常会造成大片的空白，因此需要浮动

% 浮动体示例：
\documentclass{article}
\usepackage{mwe}  % 产生随机文字
\begin{document}
Foo
\begin{figure}[htb]  % a float environment without \caption containing text
\blindtext
\end{figure}
bar
\end{document}

% 通过编译可知，浮动体中，字体、分词、拆行等行为与正文相同；只不过，由于 figure 环境整体移动，使 Foo 与 bar 排到了同一行，而 \blindtext 的输出结果则移动到了 Foo bar 下方

% 在 Tex 的排版过程实际是一个盒子套盒子的搭积木过程（Tex 在排版时不关心具体内容，只关心每个尺寸的大小）
\documentclass{article}
\usepackage{mwe}  % 产生随机文字
\usepackage[showframe]{geometry}  % 显示内容的轮廓
\begin{document}
Foo
\begin{figure}[htb]
\rule{4cm}{3cm}\quad\rule{4cm}{3cm}\quad\rule{4cm}{3cm}\quad\rule{4cm}{3cm}
\end{figure}
bar
\end{document}

% 通过 geometry 宏包的辅助，可见，浮动体中产生了4个黑色的标尺（即通过 \rule{<width>}{<height>} 显示）
% 此处，浮动体内，同一行有4个"字符"（可以将该类内容想像为超大的字符）；由于版面宽度不足，所以 Tex 在第三个字符后折行

% ------------------------------------------------------------------------------------------------
% 浮动体题注
\documentclass{article}
\usepackage{mwe}  % for dummy text
\usepackage[showframe]{geometry}  % for showing frames of pages
\begin{document}
Foo
\begin{figure}[htb]
\rule{4cm}{3cm}\quad\rule{4cm}{3cm}\quad\rule{4cm}{3cm}\quad\rule{4cm}{3cm}

\caption{Foo bar.}
\end{figure}
bar
\end{document}

% 产生的结果中， Figure 1 是题注的标签，包含题注的类型与编号； Foo bar. 是题注的文本；两者之间通过分隔符"label sep"分割，此处使用 :
% 题注默认格式为：
% 居中： \centering
% 罗马字族： \rmfamily
% 直立字形： \upshape
% 标准字体： \normalsize
% 标准字重： \mdseries

% 由此我们可以手动创建一个相同的题注，但该题注不能自动编号
\centering
{\rmfamily\upshape\normalsize\mdseries Figure 1: Foo bar.}

% ------------------------------------------------------------------------------------------------
% 并排摆放，各自题注
% 由于题注分别针对当前环境居中，由此，我们希望为并排摆放的两个图片分别添加题注，此时需要将内容分别放置在两个独立的盒子中
\documentclass{article}
\usepackage{graphicx}
\usepackage[showframe]{geometry}  % for showing frames of pages
\begin{document}
Foo
\begin{figure}[htb]
\centering
\begin{minipage}{0.48\linewidth}
\centering
\includegraphics[width = \linewidth]{example-image-a} % 由于图片位于小页环境中，所以 \includegraphics 环境宽度参数应设置为 \linewidth ，表示当前小页的行宽
\caption{Dummy Caption A.}
\end{minipage}\hfill % 在内容两边填充空白，使其充满一行

\begin{minipage}{0.48\linewidth}
\centering
\includegraphics[width = \linewidth]{example-image-b}
\caption{Dummy Caption B.}
\end{minipage}
\end{figure}
bar
\end{document}

% ------------------------------------------------------------------------------------------------
% 纵向摆放，无题注
\documentclass{article}
\usepackage{graphicx}
\usepackage[showframe]{geometry}  % for showing frames of pages
\begin{document}
Foo
\begin{figure}[htb]
\centering
\includegraphics[width = .6\linewidth]{example-image-a}\\[2ex] % [2ex] 表示图片之间的间距，可以更改
\includegraphics[width = .6\linewidth]{example-image-b}
\end{figure}
bar
\end{document}
% 由此可见，可以使多张图片的总宽度大于页面宽度，便会换行；或者手动换行；

% ------------------------------------------------------------------------------------------------
%　多个元素与子题注
%　当希望给每个元素加上题注，但同时有共享一个题注，此时每个元素的题注便应是子题注
% 此时可以选择使用 subfig 宏包，该宏包中的 \subfloat 命令；或者使用 subcaption 中的 \subcaption 命令
% \subfloat 命令是为了其中的内容创建一个盒子，并支持设置子题注
\documentclass{article}
\usepackage{graphicx}
\usepackage{subfig}
\usepackage[showframe]{geometry}  % for showing frames of pages
\begin{document}
Foo
\begin{figure}[htb]
\centering
\subfloat[Subcaption A]{\includegraphics[width = .48\linewidth]{example-image-a}}\hfill
\subfloat[Subcaption B]{\includegraphics[width = .48\linewidth]{example-image-b}}
\caption{Two figures.}
\end{figure}
bar
\end{document}

% 当使用 caption 宏包设置题注时，应该首先使用 \subcaption 命令
% 它的使用方法与 caption 宏包命令较为相近，按照前述"并排摆放，各自题注"命令，只需将 \caption 命令改为 \subcaption 即可
% 但使用 subcaption 宏包中 \subcaption 命令需要设置小页环境，此时代码较多，较为复杂
% 此时可以使用 subcaption 中另一个命令 \subcaptionbox ；它的用法类似与 \subfloat
\subcaptionbox{Dummy Subcaption A.}{\includegraphics[width = .48\linewidth]{example-image-a}}\hfill
\subcaptionbox{Dummy Subcaption B.}{\includegraphics[width = .48\linewidth]{example-image-b}}
```

```latex
% 改变标题标签的数字格式或字母格式
\renewcommand{\thetable}{\alph{table}}
\renewcommand{\thefigure}{\Alph{table}}
\renewcommand{\thesubtable}{\Roman{subtable}}
\renewcommand{\thesubfigure}{\arabic{subfigure}}

% 每一个标签都指定了一个你要更改的标签以及希望显示的标签类型，如(alph{table})
```

### 显示序号方式

|  计数器类型  |     实现代码     | 示例 |
| :----------: | :--------------: | :--: |
|  阿拉伯数字  | \arabic{counter} | 1,2  |
|   小写字母   |  \alph{counter}  | a,b  |
|   大写字母   |  \Alph{counter}  | A,B  |
| 小写罗马数字 | \roman{counter}  | i,ii |
| 大写罗马数字 | \Roman{counter}  | I,II |



```latex
% 当有章节时，需要在图片内添加章节编号，如：
\renewcommand{\thefigure}{\thechapter.\Alph{figure}} % 将图片编号改为 1.A
```



```latex
% Caption 宏包选项与设置
% 可以设置包括编号分离、编号格式、编号与标题的字体及样式等
% 要使用这些选项，可以在引入宏包时进行设置：
\usepackage[OPTIONS]{caption}
\usepackage[OPTIONS]{subcaption}

% 也可以在使用命令时进行设置，使所有后面的标题都具有设置的样式
\captionsetup[FLOAT_TYPE]{OPTIONS}

% 对于 FLOAT_TYPE 可以是图、表、子图、子表等
% 当使用 \captionsetup 时，后续标题都将使用设置的格式；也可以选择将 \captionsetup 放入表、图等环境中，此时，只对改图、表有效

% ------------------------------------------------------------------------------------------------
% for figures: caption label is italic, the caption text is bold / italic
\captionsetup[figure]{labelfont=it,textfont={bf,it}}
% for subfigures: caption label is bold, the caption text normal.
% justification is raggedright (i.e. left aligned)
% singlelinecheck=off means that the justification setting is used even when the caption is only a single line long.
% if singlelinecheck=on, then caption is always centered when the caption is only one line.
\captionsetup[subfigure]{labelfont=bf,textfont=normalfont,singlelinecheck=off,justification=raggedright

% 此时，对于子标题是左对齐，这是由于关闭了 singlelinecheck，使得单行标题使用校正设置，否则，它将居中

% 对于上述使用方法，也可以在引入相应宏包时进行设置，具有相同效果，但此时全文标题与子标题都将具有设置的效果
\usepackage[labelfont=it,textfont={bf,it}]{caption}
\usepackage[labelfont=bf,textfont=normalfont,singlelinecheck=off,
justification=raggedright]{subcaption}
```



### 编号分离

```latex
% 可以通过 \captionsetup 中 labelformat 和labelsep 选项进行设置
```

labelformat 选项可以设置为：

|      标签格式      |            结果            |
| :----------------: | :------------------------: |
| labelformat=empty  | 没有标签，即没有数字或字母 |
| labelformat=simple |    标题中显示数字或字母    |
| labelformat=parens |     数字或字母在括号中     |

```latex
% 对于 labelsep 选项，可以设置为：
labelsep = none
labelsep = colon
labelsep = period
labelsep = space
labelsep = quad
labelsep = newline
```

```latex
% 编号分离设置示例：
\captionsetup[figure]{labelformat=parens, labelsep=newline}
\captionsetup[subfigure]{labelformat=simple, labelsep=colon}
```



```latex
% 对于无序号的标题和表格
% 可以使用不显示标题序号的命令 \caption*
\begin{figure}[tbp]
	\centering	
	\includegraphics[width=1in]{1.jpg}
	\caption*{Unnumbered figure caption.}
\end{figure}

% 设置子图与子表标题的位置
% 对于图、表，标题的位置可以设置在该浮动体的上方或下方，只需要将命令 \caption 置于图表的上方或下方即可
```



```latex
% 重置标题计数器
% 若需要重新计数标题序号，可以使用下述方法
\setcounter{figure}{0}

% 也可以使用其他的名称，不仅仅是 figure ，同时开始计数的值也可以不是 0
```



```latex
% 更改标题名称
% 当不希望图表名称是默认的如 "Fig." 或 "Figure" 或 "Table" 或 "Tab." 时，可以通过 \renewcommand 更改相应的名称
\renewcommand{\tablename}{Tbl}
\renewcommand{\figurename}{Image}
```

```latex
% -------------------------------------------------------------------------------------------------
% 2018.6.12
```



```latex
% 当希望两张水平排列且大小不同的图片在垂直方向居中，同时让各自子标题在垂直方向对齐时
% 有两种思路
% 1.
% 让两个子图的内容物高度一致，然后让这个内容物中的图形垂直居中
% 2.
% 让两个子图和各自的标题放入到2*2的表格中，再分别控制垂直对齐

% 方式1示例：
\documentclass{article}
\usepackage{floatrow}
\usepackage{caption}
\DeclareCaptionSubType[alph]{figure} % 定义标题格式
\floatsetup[subfigure]{style=plain,heightadjust=object} % 对浮动体样式进行定义；[]中参数决定浮动体类型；{}中的参数决定浮动体格式；对于 'heightadjuct = object' ，定义了浮动体的高度与内容物高度相同，并取决于最大高度
\begin{document}
\begin{figure}[!htb]
\ffigbox[\FBwidth]{ % \ffigbox 用于创建图像，标题置于图像下方；标题默认宽度为页面宽度；当添加 [\FBwidth] 后，标题宽度等于图像宽度
\begin{subfloatrow} % subfloatrow 环境，是简化的 floatrow 环境，将浮动内容的垂直对齐拓展到 subfloats 并创建定义的水平分隔符 \subfloatrowsep （由 subfloatrowsep = key 定义）
\ffigbox[\FBwidth]{\caption{dummy 1}}{\rule{3cm}{4cm}}
\ffigbox[\FBwidth]{\caption{dummy 2}}{\rule{4cm}{3cm}}
\end{subfloatrow}}
{\caption{dummy}}
\end{figure}
\end{document}

% 方式2示例：
\documentclass{article}

\usepackage{tikz}
\usepackage{subcaption}

\begin{document}
\begin{figure}[!ht]
  \centering
  \begin{subfigure}{.4\linewidth}
    \parbox[][4cm][c]{\linewidth}{ % 创建一个盒子，手工指定高度、内容对齐
      \centering
      \tikz\draw circle(1);}
    \subcaption{small}
  \end{subfigure}
  \begin{subfigure}{.4\linewidth}
    \parbox[][4cm][c]{\linewidth}{
      \centering
      \tikz\draw circle(2);}
    \subcaption{large}
  \end{subfigure}
  \caption{circle}
\end{figure}
\end{document}
```

```latex
% 浮动算法
% 浮动体类型：每个浮动体都具有一种浮动体类型， Latex 中定义了两种类型： figure 和 table 。还可以额外定义浮动体类型，如： listings 宏包定义了用于排版代码清单的浮动体；  algirithm 宏包定义了用于排版算法的浮动体。用于也可以自行定义浮动体类型，需要借助 float 宏包。浮动体从属的类型会直接影响浮动体的最终位置。
% 注意：同一类型中的不同浮动体，相对顺序是固定的。但是不同类型的浮动体之间，相对位置可能改变。

% 浮动区域：在同一栏中，浮动区域为栏的顶部和栏的底部。双栏时，还有额外的区域：跨过双栏的顶部
% 还有所谓的浮动栏或浮动页（只有浮动体的栏或页）

% 浮动体位置选项：当没有显式提供位置选项时， Latex 会根据浮动体类型指定浮动体位置选项
% Latex 中默认的浮动体位置选项有5种：
1：！表示忽略一些严格的限制条件
2：h 表示有可能，放置在当前位置
3：t 表示浮动体允许放置在栏的顶部
4：b 表示浮动体允许放置在栏的底部
5：p 表示浮动体允许放置在浮动栏或浮动页
% 当某个字符不存在浮动体位置选项中，则 Latex 在尝试输出时，就不会尝试将它放在栏的底部
% 浮动体位置选项是一个组合问题，并不是排列问题：[bt] 和 [tb] 是等效的

% 浮动算法参数影响：
1. 某个浮动区域允许摆放多少个浮动体
2. 浮动区域的大小
3. 非浮动栏或浮动页中，文字区域最小时的大小
4. 一个浮动区域内连续浮动体之间的垂直距离
5. 浮动区域与前后文字区域的垂直距离

% 浮动算法基本流程
% 当 Latex 遇到一个浮动体，会根据浮动算法规则尽可能快地输出该浮动体
%	若成功：该浮动体被输出，并且 Latex 再也不会改变它的位置
%	若失败：该浮动体被 Latex 放在一个等待队列中暂存，在下一页时尝试输出
% 当一栏或者一页组装完毕后， Latex 会检查队列中的浮动体，并尝试构建一个浮动栏或者浮动页，输出尽可能多的浮动体。若等待队列中的各个类型浮动体都不允许输出在浮动栏或者浮动页中，则 Latex 会尝试将浮动体放在栏的顶部或者底部，若无法容纳，则剩余的浮动体将加入等待队列
% Latex 开始处理当前页的文本信息，过程中，也可能遇到新的浮动体
% 当 Latex 遇到了 \claerpage 或者 FloatBarrier 或者文档末尾时， Latex 会构建新的页面，将等待队列中的所有浮动体都输出在浮动栏或者浮动页中（此时不再考虑浮动体的位置选项是否制定了 p ）
% 由此可见， Latex 排版时是尽快输出排版结果。对于浮动体来说，浮动体位置的浮动算法必须是一个贪心算法。在 Latex 遇到浮动体时，就会尝试输出，这是对运行效率的妥协。但是，如此贪心地决定浮动体位置，可能在后续读入数据后，对结果并不完美：当一个图片允许放置在栏的顶部或者底部， Latex 可能将其放置在某一栏的顶部区域；同时，有一个表格，只允许放置在栏的底部，此时，表格只能换页。而最好的情况应该是，图片放置在页面底部，表格放置在顶部

% 浮动算法的规则
% 当 Latex 读入一个浮动体时，都会先检查队列中是否存在有余浮动体属于同一类型的浮动体尚输出；若存在，该浮动体便会直接加入等待队列，不尝试输出
% 若不存在同一类型时， Latex 便会检查该浮动体的位置选项
% 若位置选项中包含 ！ ， Latex 便会在处理时严格执行限制（浮动区域允许浮动体最多数量、浮动区域最大面积）；否则，便会严格执行，以期望获得最美观的结果
% 下一步， latex 便会检查是否存在 h 选项
%	若存在， Latex 便会尝试将浮动体放在当前位置；若当前位置尚有足够的空间，则输出成功；否则，加入等待队列；
%	若不存在，检查 t 选项。若存在，并且上述条件没能限制浮动体，则浮动体在顶部输出，并终止浮动体处理；
%	最后，检查 b 选项。同样，若没有限制条件约束该浮动体，便会在栏底输出
% 运行至此，若没有合适的输出位置，浮动体便会加入等待队列
% 注意： p 选项在此不起作用，只有在分页时才起作用

% 浮动算法在分页时的规则
% 在分页时，首先会检查等待队列，并尽可能清空；否则， Latex 会尝试构建浮动栏或浮动页
% 但只有具有 p 的浮动体才会被放在浮动栏或者浮动页中，否则将被留在等待队列中。需要注意的是，对于同一类型的浮动体，若第一个浮动体不允放置在浮动栏或者浮动页中，则所有该类型浮动体都将被留在等待列表中，等待下一步处理
% 若有浮动体可以进行输出，那么 Latex 会尝试构建浮动栏或者浮动页，并尽可能多的输出浮动体直到栏或者页满或者触发了某些限制条件
% 生成浮动栏或者浮动页的操作将一直持续到等待列表中再无可用的浮动体，此时 Latex 将尝试将剩余的浮动体放在下一页的栏的底部或者顶部，此时： h 选项再无作用；并且输出浮动体时将不按照源代码中读取的顺序，而是从等待队列中一次读取

% 浮动体算法的参数与限制条件
% 四个计数器
totalnumber （默认为3） 在非浮动页上浮动体的最大数量
topnumber （默认为2） 在一个栏的顶部浮动体的最大数量
bottomnumber （默认为1） 在一个栏的底部浮动体的最大数量
dbltopnumber （默认为2） 在双栏排版中，横跨双栏顶部浮动体的最大数量

% 五个区域比例
\topfraction (默认为0.7) 栏的顶部区域占据当前栏的最大比例
\bottomfraction (默认为0.3) 栏的底部区域占据当前栏的最大比例
\dbltopfraction (默认为0.7) 在双栏排版中，横跨双栏的顶部区域占据当前页的最大比例
\textfraction (默认为0.2) 在非浮动栏或者浮动页中，文字区域占据的最小比例
\floatpagefraction (默认为0.5) 在浮动栏或者浮动页中，浮动体至少应当占据的最小比例

% 五个垂直距离（默认值取决于文档类默认字号）
\floatsep 栏的顶部或底部区域中，连续浮动体之间的垂直距离
\dbltopfloatsep 双栏排版中，横跨双栏的浮动区域中，浮动体之间的垂直距离
\textfloatsep 栏的顶部或者底部的浮动区域与文字区域之间的垂直距离
\dbltextfloatsep 双栏排版中，横跨双栏的浮动区域与文字区域之间的垂直距离
\intextsep 对 h 生效的浮动体，与前后文字之间的垂直 距离

% 浮动算法导致的问题及解释
% 1.双栏排版中，跨栏浮动体总是放入等待列表
% 对于双栏排版，双栏浮动体总是被 Latex 放入到等待列表中，因此，跨栏浮动体至少要在下一页顶部输出
% 原因在于：若想跨栏浮动体在当前页的顶部输出，则若架设 Latex 在遇到该浮动体时，第一栏的排版已经完成，那么 Latex 必须回溯，破坏已经排版完成的第一栏，对效率不利

% 2. h 表示"若有可能，放在这里"
% h 选项仅在一种情况下发生，等待列表中没有该类型浮动体，并且当前页有足够的空间摆放；若用户希望"我一定要放在这里时"，需要使用 Float 宏包提供的 H 选项
```

```latex
% -------------------------------------------------------------------------------------------------
% 2018.6.13
```


```latex
% 浮动体处理超宽问题

% 浮动体主要用于处理高度比较大，且不不方便分割的内容：比如图片和表格；实际上，此类内容除了高度较大外，宽度一般也较大。 Latex 在水平方向，会从版芯左边界开始排版，若图片或者表格的宽度超过版芯的宽度，此时需要进行处理

% 缩小
% 对于尺寸过大的内容，最直接的方法便是缩小；对于图片，若使用 graphicx 宏包，便可以通过 width = \linewidth 的参数将图片缩放到填满页面宽度大小；对于表格，也可以通过 graphicx 宏包中的 \resizebox 命令进行处理
% 示例
\documentclass{article}
\usepackage{showframe}
\usepackage{graphicx}
\begin{document}
\begin{table}[!htb]
\centering
\caption{Oh, this table is overfull!}\label{tab:overfull}
\rule{1.1\linewidth}{3cm}
\end{table}

\begin{table}[!htb]
\centering
\caption{Imagine that this is a table.}\label{tab:resized}
\resizebox{\linewidth}{!}{\rule{1.1\linewidth}{3cm}}
\end{table}

\begin{figure}[!htb]
\centering
\includegraphics[width = \linewidth]{example-image} % 内嵌图形
\caption{A fit figure.}\label{fig:example-image}
\end{figure}

% -------------------------------------------------------------------------------------------------
% 居中

% 由于图表在缩小后可能看不清；对于 \verb 之类的内容，不能放入大多数 box 之内
% 此时，我们可以对图表进行居中处理；由于超宽图表不居中的原因在于 Latex 从版芯左边界开始排版，所以只需要让 Latex 不从版芯的左侧开始排列就能解决该问题
% 在 Latex 中决定开始排版位置的参数是 \leftskip 这个宏，在 Latex 中它被默认为 z@ 
% 我们可以修改这个宏，比如改为 \setlength{\leftskip}{-20pt} ，表示 Latex 将从版芯左侧边界左边的 20pt 开始排版

% 同理，在 Latex 中还有 \rightskip 用于确定水平方向排版的终止位置与版芯右边界的距离
% 左右侧的 skip 类似于两个弹簧，向中间挤压内容，所以，我们不难对 \leftskip 和 \rightskip 进行以下处理
1.默认情况下，应贴着两侧边界
2.最差情况，允许内容向左右侧向两侧延伸，超过版芯但不超过纸张宽度
3.同时具有让内容居中的能力
% 所以大致命令应为：
\setlength{\leftskip}{0pt plus 1fil minus \marginparwidth}
\setlength{\rightskip}{\leftskip}

% 为了使用方便，我们可以将其定义为一个新命令：
\makeatletter
\newcommand*{\centerfloat}{%
  \parindent \z@
  \leftskip \z@ \@plus 1fil \@minus \marginparwidth
  \rightskip \leftskip
  \parfillskip \z@skip}
\makeatother

% 示例：
\documentclass{article}
\usepackage{showframe}
\usepackage{graphicx}
\makeatletter
\newcommand*{\centerfloat}{
  \parindent \z@
  \leftskip \z@ \@plus 1fil \@minus \marginparwidth
  \rightskip \leftskip
  \parfillskip \z@skip}
\makeatother
\begin{document}
\begin{table}[!htb]
\centerfloat
\caption{Oh, this table is adjusted!}\label{tab:adjusted}
\rule{1.1\linewidth}{3cm}
\end{table}
\end{document}

% 对于上述命令， adjustbox 宏包具有类似的效果；同时，它里面的命令参数与 graphicx 宏包中的 \includegraphics 的 key-value 参数类似，用于实现各类 box 效果。它的优秀之处在于，内嵌的环境或者宏都适用于 \verb 之类的内容
% 示例
\documentclass{article}
\usepackage{showframe}
\usepackage{adjustbox}
\begin{document}
\begin{table}[!htb]
\centering
\caption{Oh, this table is adjusted by the package adjustbox!}\label{tab:adjusted}
\adjustbox{center}{\rule{1.1\linewidth}{3cm}}
\end{table}
\end{document}

% -------------------------------------------------------------------------------------------------
% 旋转

% 若超宽不是特别大，可以考虑将其旋转90°
% 此时，需要使用 rotating 宏包中提供的 sidewaystable 和 sidewaysfigure 环境（还包括带 * 版本，用于在双栏模式下通栏排版），分别对应于 table 和 figure 

% 示例
\documentclass{article}
\usepackage{showframe}
\usepackage{rotating}
\begin{document}
\begin{sidewaystable}[!htb]
\centering
\caption{Let's rock!}\label{tab:rotated}
\rule{0.8\linewidth}{3cm}
\end{sidewaystable}
\end{document}

% 此时需要注意的是，旋转之后的长、宽就交换了，所以示例中的 0.8\linewidth 表示0.8倍的版芯高度；对于 rotating 宏包，默认的是将内容逆时针旋转90°，也可以传入 clockwise 参数，改变旋转方向
```

```latex
% -------------------------------------------------------------------------------------------------
% 2018.6.14
```



```latex
% 如何将4个图拼接成为一个图
\documentclass{article}

\usepackage{tikz} % 使用 tikz 宏包
\usetikzlibrary{positioning} % 使用 positioning 库

\begin{document}
\begin{tikzpicture} % 需要使用 tikzpicture 环境作图
\scope[nodes={inner sep=0,outer sep=0}]
\node[anchor=south east] (a) % 设置锚点，应该设置在4幅图中点，(a)表示对节点命名为 a ；但是实际上，锚点位置好像与 anchor 设置的位置相反
  {\includegraphics[width=4cm]{example-grid-100x100bp.png}};
\node[anchor=south west] (b)
  {\includegraphics[width=4cm]{example-image-1x1}};
\node[anchor=north east] (c)
  {\includegraphics[width=4cm]{example-image-1x1}};
\node[anchor=north west] (d)
  {\includegraphics[width=4cm]{example-grid-100x100bp.png}};
\node[right=1mm of b] (e) % 在节点 b 右侧 1mm 处添加节点 e
  {\includegraphics[height=4cm]{example-image-4x3}};
\node[below=2mm of c.south west,anchor=north west] (f)
  {\includegraphics[width=8cm]{example-image-16x9}};
\endscope
\foreach \n in {a,b,c,d} { % 类似于循环命令
  \node[anchor=north west,fill=yellow] at (\n.north west) {(\n)};
}
\node[anchor=north east,fill=green] at (e.south east) {(e)};
\node[anchor=south west,fill=green] at (f.south east) {(f)};
\end{tikzpicture}

\end{document}
```

```latex
% 如何让段落上下文间距相等
% 由于设置 \fontsize 或 \baselineskip 或比例系数后，并且行距定义为基线之间的距离，添加浮动体或其他内容后，往往导致其上下空白间距不同
% 示例
\documentclass{article}
\usepackage{graphicx}
\setlength\intextsep{0pt} % 设置间距为 0pt

\begin{document}
\noindent\rule{\linewidth}{1pt}
\begin{figure}[htbp]
\centering
\includegraphics[width=.5\linewidth]{example-image.pdf}
\caption{example-image}
\end{figure}
\noindent\rule{\linewidth}{1pt}
\end{document}

% 通过编译后可以看到，浮动体底部与正文将存在一定的距离，不是设置的 0pt ，这个间距是 Tex 中插入行间 glue 产生的，按通常做法，需要在浮动体下方文字之间设置 \nointerlineskip 加以抑制
% glue 的做法是用"厚度"为 \baselineskip-\prevdepth 的 glue 将后文内容添加到垂直列的底部，但由于后文是段落的首行，往往会添加厚度为 \parskip 的 glue

% 添加 \nointerlineskip 做法
\documentclass{article}
\usepackage{graphicx}
\setlength\intextsep{0pt}

\begin{document}
\noindent\rule{\linewidth}{1pt}
\begin{figure}[htbp]
\centering
\includegraphics[width=.5\linewidth]{example-image.pdf}
\caption{example-image}
\end{figure}
\nointerlineskip % 抑制行间距
\noindent\rule{\linewidth}{1pt}
\end{document}

% -------------------------------------------------------------------------------------------------
% 但由于添加的浮动体很有可能浮动到别的地方，此时的主要困难变为找到具体添加 \nointerlineskip 的位置，下文给出了向西解释和方法
\documentclass{article}
\usepackage{graphicx}
\setlength\intextsep{0pt}
\usepackage{etoolbox}
\makeatletter
%% http://tex.stackexchange.com/a/40363
\patchcmd{\@addtocurcol}
  {\vskip \intextsep}
  {\edef\save@first@penalty{\the\lastpenalty}\unpenalty
   \ifnum \lastpenalty = \@M  % hopefully the OR penalty
     \unpenalty
   \else
     \penalty \save@first@penalty \relax % put it back
   \fi
   \ifnum\outputpenalty <-\@Mii
     \addvspace\intextsep
     \vskip\parskip
   \else
     \addvspace\intextsep
   \fi}
  {\typeout{*** SUCCESS ***}}{\typeout{*** FAIL ***}}
\patchcmd{\@addtocurcol}
  {\vskip\intextsep \ifnum\outputpenalty <-\@Mii \vskip -\parskip\fi}
  {\ifnum\outputpenalty <-\@Mii
     \aftergroup\vskip\aftergroup\intextsep
     \aftergroup\nointerlineskip
   \else
     \vskip\intextsep
   \fi}
  {\typeout{*** SUCCESS ***}}{\typeout{*** FAIL ***}}
\patchcmd{\@getpen}{\@M}{\@Mi}
  {\typeout{*** SUCCESS ***}}{\typeout{*** FAIL ***}}
\makeatother

\begin{document}
\noindent\rule{\linewidth}{1pt}
\begin{figure}[htbp]
\centering
\includegraphics[width=.5\linewidth]{example-image.pdf}
\caption{example-image}
\end{figure}
\noindent\rule{\linewidth}{1pt}
\end{document}
```

```latex
% -------------------------------------------------------------------------------------------------
% 2018.6.15
```

