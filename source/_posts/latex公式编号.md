---
title: latex公式编号
top: true
cover: false
toc: true
mathjax: true
date: 2020-07-31 08:50:26
password:
summary: amsmath包对于行间公式的输出提供了非常强大的功能,我们今天则是介绍基于amsmath包如何去实现特定的多行公式编号技巧.
tags:
categories:
---

> 转载自[多行公式的编号技巧](https://yuxtech.github.io/tex/latex%E5%85%AC%E5%BC%8F%E7%BC%96%E5%8F%B7%E6%8A%80%E5%B7%A7.pdf)
> [amsmath使用手册](https://yuxtech.github.io/tex/amsmath.pdf)
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
## 1 多行公式一个编号

在换行的公式中,如果直接用 **align** 环境会给每行都编号, **align*** 环境则每一行都没
有编号.但是我们可以用\notag命令指定某些行不编号,如
```latex
\begin{align}
a&=b+c\notag\\
a^2&=b^2+c^2\\
a^3&=b^3+c^3\notag
\end{align}
```

除了用 align 环境之外,我们还可以用次环境 aligned 来更好地实现这种效果
```latex
\begin{align}
\begin{aligned}
a&=b+c\\
a^2&=b^2+c^
\end{aligned}
\end{align}
```


aligned 环境可以看成一个盒子,我们还可以给这个盒子添加定界符
```latex
\begin{align}
\left\{\begin{aligned}
&a=b+c\\
&a^2=b^2+c^
\end{aligned}\right\end{align}
```

指定不同块按等号对齐,同时每个区块一个编号,这时用 split 次环境
```latex
\begin{align}
a+b&=b+c\\
\begin{split}
a&=b+c\\
a^2&=b^2+c^
\end{split}\\
\begin{split}
a&=b+c\\
a^2&=b^2+c^
\end{split}
\end{align}
```

一行两个公式两个编号,这种情况自然需要 minipage 环境支持了.
```latex
\begin{minipage}{0.5\textwidth}
\begin{equation}
a^2+b^2=c^
\end{equation}
\end{minipage}
\begin{minipage}{0.5\textwidth}
\begin{equation}
a^3=b^3+c^
\end{equation}
\end{minipage}
```

给带定界符的方程组的每一行都编号,这种情况 **amsmath** 包无法实现,我们可以用
**cases** 包的 **numcases** 环境
```latex
%\usepackage{cases}
\begin{numcases}{f(x)=}%f(x)=可以置空
1,&$x\in\mathbb Q$\\
0,&$x\notin\mathbb Q$
\end{numcases}.
```


不过上述 **numcases** 环境的效果是不尽如人意的,更好的效果是用 **empheq** 包,它可
以给 **amsmath** 包提供的数学环境添加各种定界符.

```latex
\begin{empheq}[left=\empheqlbrace,right=\empheqrbrack]{align}
&a=b+c&&a=b\\
&a^2=b^2+c^2&&a=b
\end{empheq}
```

