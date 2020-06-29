# LaTeX学习与笔记收集	
适用于初学者和使用Latex排版查阅资料的排版人员。

本文将从以下4个方面进行介绍：

1. 如何选择软件？如何很快上手Latex排版
2. 在哪里找寻Latex排版模板？如何上手使用？
3. 常见使用导航
4. 待查询及遇到问题解决方式

[TOC]

## 1. 关于软件选择

软件选择，如果你是初学者，若没有任何其他基础，建议先从[在线overleaf排版教程](https://www.overleaf.com/learn) 入手。如果需求仅是偶尔排版PPT或论文，则建议没有必要安装本地版本。

- 针对高校或有论文排版任务的同学或老师，建议安装本地版本的，排版起来更为顺手

更多入门选择请参见[知乎高赞回答](https://www.zhihu.com/question/268569440)，或者参阅[知乎排版编译器选择和安装笔记](https://zhuanlan.zhihu.com/p/32280635)。

以下表格列出了三种常见的排版方式，目前比较推荐是TexLive2019+TexStudio组合或是overleaf在线工具。

| 软件                        | 说明                                                         |
| --------------------------- | ------------------------------------------------------------ |
| TexLive2019+Vscode+SmartPDF | 目前已弃用。直接原因是在我目前使用观感中，Vscode在整体使用感觉上排版效率和流畅度确实不如TexStudio。 |
| **TexLive2019+TexStudio**   | 推荐理由：术业有专攻，用专业工具。 [安装教程参考](http://static.latexstudio.net/article/2019/0527/install_TeXLive2019.pdf) |
| 如果不想安装工具            | [在线overleaf排版教程](https://www.overleaf.com/learn)  [overleaf在线模板](https://www.overleaf.com/latex/templates) |

## 2. 在哪里查询模板如何入手

首先建议初学者阅读华东科大制作的latex教程网页，内容非常全，点击 [华东师大LaTeX科技排版教程](http://math.ecnu.edu.cn/~jypan/Latex/index.html)。该教程也可作为后期排版定期浏览的一个查阅资料网站。此外，华东师大还有很多的参考资料，总之这个网站强烈推荐。

---

2020.6.29 补充：Latex有个 [Latex中文版本在线学习教程](https://www.latexstudio.net/hulatex/tutorial/ChineseBase.htm)。

---

Latex在线模板下载，请参阅[Overleaf在线模板](https://www.overleaf.com/latex/templates)。

## 3. 常见使用姿势

查阅网址和使用度娘和谷歌类似，需要啥找啥。

### 3.1 表格

如果排版过程中需要有表格，怎么办？一般考虑3种解决方案：普通表格、三线表、在线表格排版。提到表格排版，推荐在线表格排版：[在线表格排版](https://www.tablesgenerator.com/#)。

在大多数情况下，可能会对表格排版进行手动设置和调整，则需要了解基础的排版内容，表格排版一定不要忘了引入包：

```
\usepackage{float} % 浮动排版，有时候需要加
\usepackage{multirow} %合并多行单元格的宏包
\usepackage{threeparttable} %三线表
\usepackage{booktabs} % 三线表中的上中下直线线型设置\toprule、midrule、buttomrule
\usepackage{longtable} % 不宽但很长的表格可以用longtable宏包来进行分页显示，暂未用到
```

此外我们还介绍一些常见的命令：

```
\renewcommand\theadset{\renewcommand\arraystretch{0.85}%表头文字格式的详细设置
\renewcommand\theadfont{\small}%字体
\renewcommand\theadalign{rt}%行列对齐
\renewcommand\theadgape{\Gape[0.5cm][2mm]}%上下垂直距离
\setlength\extrarowheight{0pt}}%行距
```

表格排版完成可能会考虑对表格浮动和对其方式进行调整，latex表格的生成中，table是让表格浮动的环境,tabular是构造表格的环境。浮动方式`[]`一般设置为`H 当前插入，htbp 浮动插入`。对齐方式`{}`一般包括`l 左对齐， c 居中， r 右对齐`。

```
\begin{table}[表格在页面上的位置，即浮动方式]
\centering
\caption{.....}\label{...}
\begin{tabular}{对齐方式}
.........
\end{tabular}
\end{table}
```

更多需要查阅的请参考表格排版，https://www.latexstudio.net/hulatex/package/table.htm。

表格并排排版： http://blog.sina.com.cn/s/blog_630306a50101av80.html

Latex表格过大过小调整：https://blog.csdn.net/wbl90/article/details/52597429

### 3.2 图片

如果排版过程中需要插入图片，怎么办？一般考虑3种情况：一栏单图排版、一栏多图排版，排版教程请参阅：https://www.latexstudio.net/hulatex/package/figure.htm。

首先，排版需要引入头文件，一般为：

```
\usepackage{graphicx}  % 图片插入引入头文件
```

**首先，单栏单图排版**

```
% figure/Fig5-2.pdf是图片相对位置，即当前tex所在目录
% --排版
% ----test.tex
% ----figure
% ------Fig5-2.pdf
\begin{figure}  % 如果是双栏排版想一张图片占一行，用figure*，单栏排版则不用考虑
	\centering
	\includegraphics[height=2in, width=3in]{figure/Fig5-2.pdf}
	\caption{Figure name.}
	\label{Fig5-2}  % 引用用 \ref{Fig5-2}
\end{figure}
```

其次，单栏多图并排排版，以下示例为独自命名，如果想要模式请参考 [知乎Latex排版](https://zhuanlan.zhihu.com/p/32925549)

```
\begin{figure}
	\centering %图片全局居中
	%并排几个图，就要写几个minipage
	%所有minipage宽度之和要小于1，否则会自动变成竖排
	\begin{minipage}[b]{0.45\textwidth} 
		\centering % 图片局部居中
		\includegraphics[width=0.8\textwidth]{Figure/fig5-4.pdf} %局部比例
		\caption{name1.}
		\label{fig5-4}
	\end{minipage}
	\begin{minipage}[b]{0.45\textwidth} %所有minipage宽度之和＜1，否则会自动变成竖排
		\centering %图片局部居中
		\includegraphics[width=0.8\textwidth]{Figure/fig5-5.pdf}%局部比例
		\caption{name2.}
		\label{fig5-5}
	\end{minipage}
\end{figure}
```

### 3.3 算法

如果需要排版算法：

1. algorithm2e使用手册官方版，http://mlg.ulb.ac.be/files/algorithm2e.pdf
2. [参考算法排版](https://www.cnblogs.com/tsingke/p/5833221.html)，https://www.cnblogs.com/tsingke/p/5833221.html

```
\usepackage[ruled,linesnumbered]{algorithm2e} % 算法排版有很多种，其中一种方式
```

### 3.4 参考文献及引用

参考文献bib格式使用方式参阅：[Latex引用bib文件步骤](https://blog.csdn.net/lilianforever/article/details/53079169)

需要特别推荐的是，利用[JabRef](https://www.jabref.org/)是一个很不错的文献引用管理工具。

```
\usepackage{hyperref}   % 引用链接，会提示跳转
```

### 3.5 其他

1. 如果想引入带圈标号数据，请引入`\usepackage{pifont}`，按照`\ding{192}`这样进行标号。
2. 如果你是利用visio绘图，想直接导出Pdf但发现有黑边怎么办？参阅[解决LaTex中插入Visio画图有多余边框的问题](http://www.mamicode.com/info-detail-2181323.html)。
3. 如果是利用origin绘图，配色很丑怎么办？参阅[Origin 科研绘图软件 自定义配色](https://www.jianshu.com/p/892711bd4a0a)。

## 4. 有用网址集锦

关于Latex公式排版，尤其推荐在线工具和一个本地工具：

1. Latex在线公式编辑器，英文版：http://latex.codecogs.com/eqneditor/editor.php
2. Latex在线公式编辑器，中文版：https://latex.vimsky.com/
3. 从截图中提取公式，https://mathpix.com/，需要安装软件

在线表格生成的工具，刚刚在表格部分介绍过：

1. [在线表格生成工具](http://www.tablesgenerator.com/#)，http://www.tablesgenerator.com/#

以下介绍以下查阅工具资料：

1. [数学符号一览查询表](http://math.ecnu.edu.cn/~jypan/Latex/docs/MathSymb.pdf)，http://math.ecnu.edu.cn/~jypan/Latex/docs/MathSymb.pdf
2. [常见数学符号Latex表示方法](http://mohu.org/info/symbols/symbols.htm)，http://mohu.org/info/symbols/symbols.htm
3. [Latex数学公式排版知乎参阅资料](https://zhuanlan.zhihu.com/p/24502400)，https://zhuanlan.zhihu.com/p/24502400
4. [Latex细节排版纠正](https://ridiqulous.com/latex-notes-details/)，https://ridiqulous.com/latex-notes-details/
5. [Latex如何自定义定理环境](https://www.notion.so/66d6f45e15ac499b92b53b37882f8e1c)，https://www.notion.so/66d6f45e15ac499b92b53b37882f8e1c

补充

1. [switch case](https://tex.stackexchange.com/questions/79264/algorithm2e-different-ending-words-for-switch-and-case-blocks)