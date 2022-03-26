# The Theoretical Basis for data communication 

## 傅里叶分析

一个周期性函数$g(t)$（周期为$T$），可以写为一个傅里叶展开式：
$$
g(t) = {\frac{1}{2} c} + {\sum_{n=1}^{\infin}}{a_n \sin(2 \pi n f t)} + {\sum_{n=1}^{\infin}}{b_n \cos(2 \pi n f t)}
$$
其中：$f= \frac{1}{T}$

由于：
$$
{\int_{0}^{T}}\sin(2 \pi k f t) \sin(2 \pi n f t) dt = \begin{cases}
0 && {k \neq n} \\
T/2 && {k = n}

\end{cases}
$$
可以求解得到：

$a_n = \frac{2}{T}{\int_{0}^{T}} g(t)\sin(2 \pi n f t) dt $，

$b_n = \frac{2}{T}{\int_{0}^{T}} g(t)\cos(2 \pi n f t) dt $，

$c = \frac{2}{T}{\int_{0}^{T}} g(t) dt $

## 带宽有限的信号

> *这里书上举了一个传输字符 'b' 的例子，对理解很重要。*

可以直接看书，有时间再补充。

## 信道的最大数据传输速率

- 对于无噪音的理论传输，采用奈奎斯特定理：

  maximum data rate $R = 2 B \log_2 V$ bits/sec

- 对于一般有噪音的情况，采用香农定理估计：

  maximum number of bits/sec $R = B \log_2 (1+S/N)$

> 其中 ：
>
> $R$ 为传输速度，$B$ 为带宽，$V$ 为信号的离散等级，$S$ 为信号的能量，$N$ 为噪音的能量
