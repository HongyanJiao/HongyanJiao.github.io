---
layout:     post
title:      使用CTex做slides
subtitle:   windows系统下基于CTeX编辑环境做slides
date:       2018-10-26
author:     矫红岩
header-img: img/go-bg.png
catalog: true
tags:
    - latex
    - slides
---

## CTeX环境配置
关于CTeX：
- [CTeX下官方网址](http://www.ctex.org)
- [CTeX论坛](http://bbs.ctex.org)
- [CTeX下载地址](http://www.ctex.org/ctexdownload)
![image](https://github.com/HongyanJiao/HongyanJiao.github.io/blob/master/img/ctex-download.png?raw=true)<br />
这里最好选择稳定版本，我用的是清华TUNA开源镜像<br />
![image](https://github.com/HongyanJiao/HongyanJiao.github.io/blob/master/img/ctex-download2.png?raw=true)<br />
选择CTeX_2.9.2.164_Full.exe安装<br />
## 编辑脚本
在安装目录下找到WinEdt目录，点击WinEdt.exe开始编辑
![image](https://github.com/HongyanJiao/HongyanJiao.github.io/blob/master/img/ctex-edt.png?raw=true)<br />
先看个简单的例子

```
\documentclass{beamer}
\usepackage{CJK}
\begin{document}
\begin{CJK*}{GBK}{kai}
\title{使用CTex做slides}
\subtitle{windows系统下基于CTeX编辑环境做slides}
\date{2018.10.26}
\frame {
    \titlepage
}
\frame {

	\frametitle{CTeX环境配置}
    \framesubtitle{一个简单的例子}
    \linespread{2.5}
    \begin{itemize}
    	\item CTeX下官方网址
    	\item CTeX论坛
        \item CTeX下载地址
    \end{itemize}
}
\end{CJK*}
\end{document}
```
F9运行，或点击左上圈出的图标
![image](https://github.com/HongyanJiao/HongyanJiao.github.io/blob/master/img/ctex-beamer.png?raw=true)<br />
## 解析脚本
我们来看一下刚刚做了什么：
1. beamer是制作slides需要用到的包；
2. CJK是汉字包，{CJK*}{GBK}{kai}表示国标编码，汉字用楷体书写；
3. title是标题页，可以设置主标题和副标题；
4. 每一个\frame{}表示slides的一页；
5. date日期可以自己手动设置，不设置会默认编辑当天的日期；
6. linespread用来设置行间距，括号内的数字可以自由调整；
7. itemize表示列举；
## 稍复杂的情况

```
\frame{
    \frametitle{插入图片及左右分区功能}
    \begin{columns}
    \column{.6\textwidth}
    \includegraphics[height=1.9in]{graph}
    \column{.4\textwidth}
    \begin{description}
      \item[B] Begin
      \item[I] Inside
      \item[O] Otherwise
    \end{description}
    \end{columns}
}
```

![image](https://github.com/HongyanJiao/HongyanJiao.github.io/blob/master/img/ctex-graph.png?raw=true)<br />

我们再来看看刚刚做了什么：
1. \column{.number\textwidth}把一页分为左右两部分，这里是四六分，当然可以是其他数字，加和为10即可；
2. 插入图片：\includegraphics[height=1.9in]{graph}，这里in表示英寸inch，也可以写cm，图片和脚本放在同一个文件夹中，只需要写图片名称，不需要添加后缀；
3. description与itemize类似，只是多了个解释说明的作用，可以看到被描述的部分颜色变蓝；