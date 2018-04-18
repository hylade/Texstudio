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

