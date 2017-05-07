>RBF 核函数怎么就对应到高维空间了?

要彻底解决“怎么就对应到”这个问题，我想最好的（唯一的？）办法就是把这个到高维空间的特征映射求出来，要看结果的直接拉到最后。 不过在跳进数学的海洋之前，先要回顾一下SVM 的分类函数:
$$
f(\mathbf{x}) = sign(\sum_i\alpha_i \mathbf{x_i} \cdot \mathbf{x} + \mathbf{b})
$$

对于所有$\alpha_i \neq 0$ 的 $i$, $\mathbf{x_i}$ 就是支持向量 (support vector)，或者说，比较难分类的点。例如在性别分类的问题中，就是那些“不男不女”的脸。对于一个新的数据点，我们只需要关心这个数据点和所有支持向量的**点积**，然后线性组合一下，就可以算出这个分类函数的值。

有些时候，训练集不是线性可分的，但是可以通过映射到高维空间中进行线性分割。

![](lift.png)

我们就需要在高维空间中计算分类函数：
$$
f(\mathbf{x}) = sign(\sum_i\alpha_i \mathbf{\varphi(x_i)} \cdot \mathbf{\varphi(x)} + \mathbf{b})
$$

幸运的是，我们其实并不需要高维空间中的向量，而只是高维空间中两个向量的点积。定义函数K 使得: 
$$
K(\mathbf{x_1}, \mathbf{x_2}) =  \mathbf{\varphi(x_1)} \cdot \mathbf{\varphi(x_2)}
$$

高维空间中的分类函数就变成了：
$$
f(\mathbf{x}) = sign(\sum_i\alpha_i K(\mathbf{x_1}, \mathbf{x_2})+ \mathbf{b})
$$
所以选择对高维空间的映射，就相当于选择函数 $K$。计算在高维空间中的分类，就相当于用函数$K$ 代替原来的向量点积。无论是选还是算，都只和函数$K$有关。 至于高维空间的映射究竟是什么，其实不重要。哦对了，这个函数 K有一个名字，叫做核函数 (Kernel Function)。

---
不过有时候算算映射究竟是什么，也有助于更好得理（zhuāng）解（bī）。既然这里题主问到RBF核函数的特征映射是什么，激发了我的好奇心（随手推了一下，哪知道这么复杂！），那我就正好回答一下吧！在求 RBF 核函数的特征映射之前，我们先要求多项式核函数（Polynomial Kernel）的特征映射。

多项式核函数:
$$K_d(\mathbf{x_1}, \mathbf{x_2}) = (\mathbf{x_1}^T\mathbf{x_2})^d $$

寻找
$$\mathbf{\Phi}_d(\mathbf{y})^T\mathbf{\Phi}_d(\mathbf{x}) = K_d(\mathbf{x}, \mathbf{y}) = (\mathbf{y}^T\mathbf{x})^d = (\sum_{i=1}^{n}x_iy_i)^d $$

根据多项式定理 (Multinomial theorem)
$$
(x_{1}+\cdots +x_{m})^{n}=\sum _{{|\alpha |=n}}{n \choose \alpha }\mathbf{x}^{\alpha }, \alpha = (\alpha_1,\alpha_2,…,\alpha_m)
$$
这里用到了三个记号, 
$$|\alpha| = \sum_{i=1}^m\alpha_i, $$
$$\mathbf{x}^\alpha = x_1^{\alpha_1}x_2^{\alpha_2}\cdots  x_m^{\alpha_m}, $$
$$
{n \choose \mathbf{\alpha} } = {n \choose \alpha_1,\alpha_2,…,\alpha_m } = \frac{n!}{\alpha_1!\alpha_2!…,\alpha_m!}
$$
带入上面的式子，
$$
\begin{align}  
\mathbf{\Phi}_d(\mathbf{y})^T\mathbf{\Phi}_d(\mathbf{x}) 
&= (\sum_{i=1}^{n}x_iy_i)^d \\
&= \sum _{{|\alpha |=d}}{d \choose \alpha }\mathbf{x}^{\alpha }\mathbf{y}^{\alpha }\\
&= \sum _{{|\alpha |=d}}\sqrt{{d \choose \alpha }}\mathbf{x}^{\alpha }\sqrt{{d \choose \alpha }}\mathbf{y}^{\alpha }\\
&= \langle \sqrt{{d \choose \alpha}} \mathbf{y}^\alpha \rangle^T \langle \sqrt{{d \choose \alpha}} \mathbf{x}^\alpha \rangle, \forall |\alpha|= d
\end{align}
$$
于是我们找到了d次多项式核函数的特征映射：
$$
\mathbf{\Phi}_d(\mathbf{x}) = \langle \sqrt{{d \choose \alpha_1, \alpha_2, \cdots, \alpha_n }} x_1^{\alpha_1}x_2^{\alpha_2}\cdots  x_n^{\alpha_n} \rangle , \forall \sum_{i=1}^n \alpha_i= d
$$

考虑简单的情况做个验证: $n=2, d=2$ 时
$$
\mathbf{\Phi}_2(\langle x_1, x_2\rangle) = \langle x_1^2, x_2^2, \sqrt{2}x_1x_2\rangle
$$
$n=2, d=3$ 时
$$
\mathbf{\Phi}_3(\langle x_1, x_2, x_3\rangle) = \langle x_1^3, x_2^3, x_3^3, \sqrt{3}x_1^2x_2, \sqrt{3}x_1^2x_3, \sqrt{3}x_2^2x_1, \sqrt{3}x_2^2x_3, \sqrt{3}x_3^2x_1, \sqrt{3}x_3^2x_2, \sqrt{6}x_1x_2x_3\rangle
$$

---
RBF 核函数: 
$$K(\mathbf{x_1}, \mathbf{x_2})= exp(-\frac{||\mathbf{x_1}-\mathbf{x_2}||^2}{2\sigma^2}) $$

寻找 $\mathbf{\Phi(x)}$ 使得
$$K(\mathbf{x},\mathbf{y}) = \mathbf{\Phi(y)}^T\mathbf{\Phi(x)}$$

$\mathbf{\Phi(x)}$ 就是我们要寻找的从低维到高维的映射函数。

$$
\begin{align}  
K(\mathbf{x}, \mathbf{y}) 
& = exp(-\frac{||\mathbf{x}-\mathbf{y}||^2}{2\sigma^2})\\
& = exp(-\frac{1}{2\sigma^2}(\mathbf{x}-\mathbf{y})^T(\mathbf{x}-\mathbf{y}))\\ 
& = exp(-\frac{1}{2\sigma^2}(\mathbf{x}^T\mathbf{x} + \mathbf{y}^T\mathbf{y}- 2\mathbf{y}^T\mathbf{x}))\\ 
& = exp(-\frac{1}{2\sigma^2}(||\mathbf{x}||^2+||\mathbf{y}||^2))\cdot exp(\frac{1}{\sigma^2}\mathbf{y}^T\mathbf{x})\\ 
& = C \cdot exp(\frac{1}{\sigma^2}\mathbf{y}^T\mathbf{x})\\ 
& = C \cdot \sum_{i=0}^{\infty}\frac{(\frac{1}{\sigma^2}\mathbf{y}^T\mathbf{x})^i}{i!}\\ 
& = \sum_{i=0}^{\infty}\frac{C}{\sigma^{2i}i!}(\mathbf{y}^T\mathbf{x})^i\\ 
\end{align}
$$

因此，RBF Kernel 是所有多项式核函数的线性组合。其实到这里就已经可以看出RBF所对应的特征映射函数就是由多项式核函数所对应的特征映射函数组合而成。 不过既然都写了这么多了，干脆一口气把准确的表达式也写出来吧。

定义 $a_k= \sqrt{\frac{C}{\sigma^{2k}k!}}$, 其中 $C = exp(\frac{||\mathbf{x}||^2+||\mathbf{y}||^2}{-2\sigma^2})$ 

结合
$$\mathbf{\Phi}_k(\mathbf{y})^T\mathbf{\Phi}_k(\mathbf{x}) = (\mathbf{y}^T\mathbf{x})^k $$
我们得到，
$$a_k\mathbf{\Phi}_k(\mathbf{y})^Ta_k\mathbf{\Phi}_k(\mathbf{x}) = \frac{C}{\sigma^{2k}k!}(\mathbf{y}^T\mathbf{x})^k $$
带入 $K(\mathbf{x}, \mathbf{y})$ 得到，
$$
\begin{align}  
K(\mathbf{x}, \mathbf{y}) 
& = \sum_{i=0}^{\infty}\frac{C}{\sigma^{2i}i!}(\mathbf{y}^T\mathbf{x})^i\\ 
& = \sum_{i=0}^{\infty}a_i\mathbf{\Phi}_i(\mathbf{y})^Ta_i\mathbf{\Phi}_i(\mathbf{x})\\ 
& = \mathbf{\Phi(y)}^T\mathbf{\Phi(x)}
\end{align}
$$

其中，
$$\mathbf{\Phi(x)} = \langle a_0\mathbf{\Phi}_0(\mathbf{x}), a_1\mathbf{\Phi}_1(\mathbf{x}), a_2\mathbf{\Phi}_2(\mathbf{x}), \cdots \rangle$$


Oh yeah！搞定了！我们最终找到了这个无限维向量的明确定义（擦汗-_-\\）。但这里还是不得不回到前面的话，我们其实完全不需要在意这个核函数对应的高维映射是什么，也不用去计算高维映射。直接拿核函数来用就行了！我们只需要计算核函数，就相当于计算了在高维空间中的点积，从而相当于在高维空间中做了划分。简单粗暴，这就是它的美妙之处。
