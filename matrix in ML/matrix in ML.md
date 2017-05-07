我们就挑最简单的机器学习问题来说说矩阵是怎么用的吧。最简单的机器学习问题是什么呢？**线性回归--- 用很多很多点来拟合一条直线。**

数据：$(x_1, y_1),(x_2, y_2) ... (x_n, y_n) $

参数：选取$(m, b)$， 即直线 $y = mx + b$

目标：最小化误差 $$E = \sum_{i=1}^n(y_i - mx_i-b)^2$$

这和矩阵有什么关系呢？ 没什么关系，但是如果我用矩阵来求最小值，会很帅

$$\begin{align}
      E&=\sum_{i=1}^n(y_i - mx_i-b)^2\\
       &=\sum_{i=1}^n(y_i - 
       		\begin{bmatrix}
    					x_{1}       & 1
				\end{bmatrix}
				\begin{bmatrix}
				    m    \\    b
				\end{bmatrix})^2\\
       &=\begin{Vmatrix}
       		\begin{bmatrix}
    					y_{1} \\ \vdots \\ y_{n} 
				\end{bmatrix}
			 - 
       		\begin{bmatrix}
    					x_{1}       & 1 \\
    					\vdots       & \vdots \\
    					x_{n}       & 1 \\
				\end{bmatrix}
				\begin{bmatrix}
				    m    \\    b
				\end{bmatrix}\end{Vmatrix}^2, let \,\mathbf{h} = \begin{bmatrix}
				    m    \\    b
				\end{bmatrix}  \\
		&=\begin{Vmatrix} \mathbf{y-Xh}\end{Vmatrix}^2\\
		&= \mathbf{(y-Xh)^T(y-Xh)}\\
		&= \mathbf{y^Ty-2(Xh)^Ty + (Xh)^TXh}\\
       \\
       \\
       \frac{dE}{d\mathbf{h}}
        &=2\mathbf{X^TXh-2X^Ty}=0\\
 		\\
       \mathbf{h}
        &=\mathbf{(X^TX)^{-1}X^Ty}\\
\end{align}$$

搞定！忍不住大叫美观。 顺便提一下，$\mathbf{(X^TX)^{-1}X^T}$ 叫做 $\mathbf{X}$ 的伪逆矩阵 (Pseudoinverse)。

啊，等等，还没完。我们在这里尝试减小的误差是y方向的误差。这在拟合的直线是水平的时候效果还不错。 但是如果直线是竖直的时候，就完全GG了。偏离直线很少很少，就会带来极大的误差。这是不科学的。于是我们想要最小化的是所有点到候选直线的距离的平方和。

数据：$(x_1, y_1),(x_2, y_2) ... (x_n, y_n) $

参数：选取$(a, b, d)$, 即直线 $l: ax+by = d$ , 其中 $||(a,b)||=1 $

目标：最小化误差 $$E = \sum_{i=1}^n(ax_i+by_i-d)^2$$

其中 $|ax_i+by_i-d|$ 即点 $(x_i, y_i)$ 到直线 $l:ax+by = d $ 的距离。

$$\begin{align}
       \frac{\partial E}{\partial d}
        &=\sum_{i=1}^n-2(ax_i+by_i-d)=0\\	 
       d &=\frac{a}{n}\Sigma_{i=1}^{n}x_i + \frac{b}{n}\Sigma_{i=1}^{n}y_i\\
        &=a\bar{x} + b\bar{y}\\
\end{align}$$
Replace $d=a\bar{x} + b\bar{y}$ back into E, we have
$$\begin{align}
       E
        &=\sum_{i=1}^n(ax_i+by_i-d)^2\\
        &=\sum_{i=1}^n(ax_i+by_i-a\bar{x} - b\bar{y})^2\\
        &=\sum_{i=1}^n(a(x_i-\bar{x})+b(y_i-\bar{y}))^2\\
               &=\begin{Vmatrix}
       		\begin{bmatrix}
    					x_{1}-\bar{x}       & y_1-\bar{y} \\
    					\vdots       & \vdots \\
    					x_{n}-\bar{x}       & y_n-\bar{y} \\
				\end{bmatrix}
				\begin{bmatrix}
				    a    \\    b
				\end{bmatrix}\end{Vmatrix}^2, let \, \mathbf{h} = \begin{bmatrix}
				    a    \\    b
				\end{bmatrix} \\
		&= \mathbf{(Uh)^T(Uh)}\\
		\\
       \\
       \frac{dE}{d\mathbf{h}}
        &=2\mathbf{(U^TU)h}=0,  ||\mathbf{h}||=1\\
\end{align}$$

这就是个标准问题，求齐次线性系统的非平凡解 （Homogeneous Linear Systems non-trivial solution）。
$\mathbf{h}$ 为 $\mathbf{U^TU}$ 的最小特征值对应的特征向量。搞定！

总结一下，这个最简单的机器学习问题里面，我们都用到了哪些矩阵的知识？

- 矩阵的模
- 伪逆矩阵
- 对矩阵求微分
- 求齐次线性系统的非平凡解，这其中又涉及
	- 矩阵 SVD 分解
	- 正交矩阵
	- 特征值，特征向量

如此一个简单的的线性回归问题原来也和这么多矩阵的知识相关。所以，线性代数很重要啊！至于要看什么书，其实用不着看书。等你看完了书，你同学的machine learning论文都发了两篇了，或者kaggle都刷到前5%了，或者都做了个能识别数字的android app 准备开始创业了。要学机器学习，从现在就可以开始，从这篇文章就可以开始。 查漏补缺，有什么不懂的就去查去问，找google，找大神，慢慢的，你也就很厉害了。 