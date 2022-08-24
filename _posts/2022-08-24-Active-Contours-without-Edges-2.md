---
layout: post
title: "[ED] 2. Active Contours without Edges [2]"
author: "SJ Lee"
tags: Edge-Detection Paper-Review
---

Continued from [**Active Contours without Edges [1]**](https://lsj0410.github.io/2022-08-21/Active-Contours-without-Edges-1).

Instead of $H$ and $\delta$ we will use regularizations $H_{\epsilon}$ and $\delta_\epsilon$ of $H$, $H_{2, \epsilon}$ and $\delta_{2, \epsilon}$ in particular.

$$ H_{2, \epsilon}(z)=\frac{1}{2}(1+\frac{2}{\pi}\text{atan}(\frac{z}{\epsilon})) $$

$$ \delta_{2, \epsilon}(z) = \frac{\partial}{\partial z}H_{2, \epsilon}(z) $$

Now we write $F$ as $F_{\epsilon}$, a function of $H_\epsilon$ and $\delta_\epsilon$.

$$
\begin{equation}
    \begin{split}
    F_\epsilon(c_1, c_2, \phi) {} & = \mu \int_\Omega \delta_\epsilon(\phi(x, y))|\nabla\phi(x, y)|dxdy \\\\\\
    & +\nu\int_\Omega H_\epsilon(\phi(x, y))dxdy\\\\\\
    & +\lambda_1 \int_\Omega |u_0(x, y)-c_1|^2 H_\epsilon (\phi(x, y)) dxdy\\\\\\
    & +\lambda_2 \int_\Omega |u_0(x, y)-c_2|^2 (1-H_\epsilon (\phi(x, y))) dxdy
    \end{split}
\end{equation}
$$

For $F_\epsilon$ to be minimal $\frac{\partial F}{\partial \phi}$ must be 0 for fixed $c_1$ and $c_2$. We will use an artificial time parameter $t$ to denote the descent of $\phi$. We write $\phi(t, x, y)$ with $\phi(0, x, y)=\phi_0(x, y)$ being the initial contour. Then calculating the partial derivatives we have:

$$
\frac{\partial \phi}{\partial t} = \delta_\epsilon (\phi) \left[\mu \text{div} \left(\frac{\nabla \phi}{|\nabla \phi|} \right)-\nu -\lambda_1 (u_0 -c_1)^2 \right]=0
$$

Solving this PDE is the essence of finding $\phi$. The Chan-Vese algorithm consists of the following steps.

1. Initialize $\phi^0$ by $\phi_0$ and set $n=0$.

2. Compute $c_1(\phi^n)$ and $c_2(\phi^n)$ by eqns (12) and (13) in the previous post.

3. Solve (4) and obtain $\phi^{n+1}$.

4. Check if solution is stationary. If not, increment $n$ by 1 and repeat.

<br/>

## References

[1] T. F. Chan and L. A. Vese, 2001, "Active contours without edges", IEEE Transactions on Image Processing, vol. 10, no. 2, pp. 266-277
