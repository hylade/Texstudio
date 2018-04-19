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
%    ------------------------------Example - 1-------------------------------------------
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
    
%    ---------------------------Example - 2----------------------------------------------
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
\fancyfoot[RO,RE]{\it 书名}	%当不存在"\it"时，斜体将消失
\renewcommand{\headrulewidth}{0.7pt}	%页眉与正文之间的水平线粗细
\renewcommand{\footrulewidth}{0pt}	
\pagestyle{fancy}	%选用fancy style
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
		{\bf \small Symbol}&\qquad {\bf\small Meaning}\\	%"\bf"用于字符加粗；"\small"用于调整字符大小  
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

