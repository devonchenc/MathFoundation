# Least Square Fitting

# 1. 问题
$$ y = a e^{bx}\tag{1}$$

已知一系列的 $(x_1, y_1),(x_2, y_2),...(x_n, y_n)$ 值，使用最小二乘拟合指数函数系数 $a$ 和 $b$

# 2. 将非线性指数函数转为线性函数
对式(1)取对数，则有

$$ log(y) = \log(a e^{bx}) = \log{a} + bx$$


写成矩阵形式如下，

$$Y= \begin{bmatrix}
x_1 & 1\\
x_2 & 1\\
... & ...\\
x_n & 1
\end{bmatrix}
\begin{bmatrix}
b\\
\log{a}\\
\end{bmatrix} = X\cdot A \tag{2}$$

其中$Y=log(y)$，$X= \begin{bmatrix}
x_1 & 1\\
x_2 & 1\\
... & ...\\
x_n & 1
\end{bmatrix}$，$A = (b,\log{a})^T$

由式(2)，可得
$$ \begin{aligned}Y &= X\cdot A \\
X^T Y &= X^T X A \\
A &= (X^T X)^{-1}X^TY
\end{aligned} \tag{3}$$

# 3. 求解

$$ X^T X = \begin{bmatrix}
x_1 & x_2 & ... & x_n\\
1 & 1 & ... & 1
\end{bmatrix} \cdot \begin{bmatrix}
x_1 & 1\\
x_2 & 1\\
... & ...\\
x_n & 1
\end{bmatrix}=
\begin{bmatrix}
\Sigma x^2 & \Sigma x\\
\Sigma x & n
\end{bmatrix}$$

$$ \begin{aligned}
(X^T X)^{-1} &= \frac{1}{|X^T X|}(X^T X)^*\\
&= \frac{1}{|X^T X|}
\begin{bmatrix}
n & -\Sigma x\\
-\Sigma x & \Sigma x^2
\end{bmatrix}\\
&=\frac{1}{n\Sigma{x^2}-(\Sigma{x})^2}
\begin{bmatrix}
n & -\Sigma x\\
-\Sigma x & \Sigma x^2
\end{bmatrix}
\end{aligned}
$$
所以，
$$ A=(X^T X)^{-1}X^T Y = \frac{1}{n\Sigma{x^2}-(\Sigma{x})^2}
\begin{bmatrix}
n \Sigma (xy) - \Sigma{x}\Sigma{y}\\
\Sigma {x^2}\Sigma{y} - \Sigma x \Sigma{xy}
\end{bmatrix}$$

因此 $$
\begin{aligned}
b &= \frac{n \Sigma (xy) - \Sigma{x}\Sigma{y}}{n\Sigma{x^2}-(\Sigma{x})^2}\\
\log{a} &= \frac{\Sigma {x^2}\Sigma{y} - \Sigma x \Sigma{(xy)}}{n\Sigma{x^2}-(\Sigma{x})^2}\\
a &= exp(\frac{\Sigma {x^2}\Sigma{y} - \Sigma x \Sigma{(xy)}}{n\Sigma{x^2}-(\Sigma{x})^2})
\end{aligned}$$
