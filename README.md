# 在VSCode中编辑LaTex文本
## 目录
[准备工作](#准备工作)  
&emsp;[1安装texlive](#1安装texlive)  
&emsp;[2.下载并安装VSCode](#2下载并安装vscode)  
&emsp;[3.安装LaTex插件](#3安装latex插件)  
&emsp;[4.配置LaTex插件](#4配置latex插件)  
[创建文件](#创建文件)  
[编辑文件](#编辑文件)  
&emsp;[基本语法](#基本语法)   
&emsp;[数学编辑语法](#数学编辑语法)  

## 准备工作
### 1.安装texlive  
安装texlive可以参考这篇[文章](https://zhuanlan.zhihu.com/p/493412905)。 
### 2.下载并安装VSCode  
[VSCode官网](https://code.visualstudio.com/)    
点击Download即可下载。  
**注意：**  
在安装时，请注意勾选以下两个选项  
![](https://i.postimg.cc/9fvtCPbx/download-Warning.png)  
这样在右键菜单中我们就可以看到“Open With Code”的选项，可以直接利用windows资源管理器管理我们的Markdown文件目录。  

如果先前已经安装过VSCode但却没有勾选这两个选项，有两种补救措施：  
- 重新安装VScode  
  *简单粗暴的解决方法* 

- 修改注册表  
  *该方法可以参考这个[博客](https://www.cnblogs.com/TopStop/p/15050793.html)*  

**安装中文包**   
安装中文包可以参考这篇[文章](https://zhuanlan.zhihu.com/p/263036716)。  
### 3.安装LaTex插件  
![](https://i.postimg.cc/bwrH0pRb/20230820224154.png)  
在VSCode的商店中搜索该插件并安装。  
### 4.配置LaTex插件  
xelatex是支持中文的编译工具，而LaTex Workshop的默认编译工具为latexmk，因此我们要对新安装LaTex插件进行配置。
    
在VSCode界面按F1，键入`setjson`，选择`首选项:打开用户设置(JSON)`，进入settings.json，在该文件中添加如下代码：  
```
"latex-workshop.latex.tools": [
        {
            // 编译工具和命令
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOCFILE%"
            ]
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOCFILE%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ],
        },
        {
            "name": "pdflatex",
            "tools": [
                "pdflatex"
            ]
        },
        {
            "name": "xe->bib->xe->xe",
            "tools": [
                "xelatex",
                "bibtex",
                "xelatex",
                "xelatex"
            ]
        },
        {
            "name": "pdf->bib->pdf->pdf",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        }
    ],
```
***注意：*** *该段代码要于json文件中的源代码放在同一大括号内，同时要给源代码的末尾加上英文的逗号，否则会导致配置失败。*  
  
## 创建文件  
在创建文件时，我们需要创建后缀为.tex的文件，创建完成即可开始编辑。  

## 编辑文件  
[测试文件](https://github.com/elsieMeng0424/LaTexInVSCode/blob/main/test.tex)  

[测试文件预览样式](https://github.com/elsieMeng0424/LaTexInVSCode/blob/main/test.pdf)  
  
### 基本语法
基本框架：  
```LaTex
\documentclass{article}
%usepackage{...}
\begin{document}
    TEXT
\end{document}
```
配置中文：  
```LaTex
\usepackage[UTF8]{ctex}
\usepackage{anyfontsize}
\usepackage{fontspec} %设置字体
```  
添加数学公式编辑包：
```LaTex
\usepackage{amsmath}
```
标题、作者、日期：  
```LaTex
\title{title}
\author{author}
\date{2023/8/21}
\begin{document}
\maketitle %显示标题等内容
\end{document}
```
添加目录：
```LaTex
\tableofcontents
```
添加标题：
```LaTex
\section{}
\subsection{}
\subsubsection{}
```
添加段落：
```LaTex
\paragraph{}
\subparagraph{}
```
添加新页并跳转：
```tex
\newpage
```
取消首行缩进：
```tex
\noindent
```
设置字体大小（由大至小）：
```tex
\Huge
\huge
\LARGE
\Large
\large
\nomalsize
\small
\footnotesize
\scriptsize
\tiny
```
### 数学编辑语法
上下标：
```tex
$a^{n}$ %上标
$a_{n}$ %下标
```
分式：
```tex
$\frac{m}{n}$ %m分之n
```
开方：
```tex
$\sqrt{x}$ %x开平方
$\sqrt[n]{x}$ %x开n次方
```
累计求和：
```tex
$\sum_{i=m}^{n}$
```
积分：
```tex
$\int_{i=m}^{n}$
```
向量：
```tex
$\vec a$ %a向量
$\overrightarrow{AB}$ %由A指向B的向量
```
省略号：
```tex
$a+b+\cdots+z$
```
大括号（下方）：
```tex
$\underbrace{a+b+\cdots+z}_{26}$
```
横杠：
```tex
$\overline{m+n}$ %上横杠
$\underline{m+n}$ %下横杠
```