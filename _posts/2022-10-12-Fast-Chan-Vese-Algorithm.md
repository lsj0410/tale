---
layout: post
title: "[ED] Fast Chan-Vese Algorithm"
author: "SJ Lee"
tags: Edge-Detection Paper-Review
---

I am reading the paper [*A Fast Algorithm for Level Set Based Optimization*](https://ww3.math.ucla.edu/camreport/cam02-68.pdf) by Song and Chan.[1] While this paper discusses other optimization problems, this post will focus solely on the Chan-Vese model[2]. More on the Chan-Vese model can be found [here](https://lsj0410.github.io/2022-08-21/Active-Contours-without-Edges-1) and [here](https://lsj0410.github.io/2022-08-24/Active-Contours-without-Edges-2).

I also created a python realization of this paper, which can be found [here](https://github.com/lsj0410/Edge-Detection/tree/main/Fast-Algorithm).

<br/>

### The idea

The image segmentation model proposed by Chan and Vese[2] has a severe problem: it takes too much time. To solve this problem, Song and Chan proposed an improved algorithm that starkly improved computation time. The main idea of this algorithm is that the values of $\phi$ are actually not important in acquiring the contour $C$. What matters is the *sign* of $\phi$.

<br/>

### The algorithm

We have the energy functional defined in the Chan-Vese model as follows.

$$
\begin{equation}
\begin{split}
F(C, c_1, c_2 ) {} &= \mu \cdot \text{Length} (C) \\\\\\
&+ \lambda _1 \int_{inside(C)}{|u_0 - c_1 |^2 dxdy} \\\\\\
&+ \lambda_2 \int_{outside(C)} {|u_0 - c_2 |^2 dxdy}
\end{split}
\end{equation}
$$

$$
\begin{equation}
\begin{split}
F(\phi, c_1, c_2 ) {} &= \mu \int_\Omega |\nabla H(\phi)|dxdy \\\\\\
&+ \lambda _1 \int_\Omega{|u_0 - c_1 |^2 H(\phi)dxdy} \\\\\\
&+ \lambda_2 \int_\Omega {|u_0 - c_2 |^2 (1-H(\phi)) dxdy}
\end{split}
\end{equation}
$$

Let $\phi$ have only $1$ and $-1$ as values. Sweep through each pixel in the image. Calculate the increment in the energy $F$ if the value of $\phi$ for the pixel is changed from $1$ to $-1$ or vice versa: i. e. if the pixel is moved from inside the contour to outside or vice versa. If the energy decreases after such modification, switch $\phi$. If not, move on to the next pixel.

We know that $c_1$ and $c_2$ are also functions of $H(\phi)$. Let there be $m$ points with $\phi(P)=1$ and $n$ points with $\phi(P)=-1$. Take a point $P_0$ with $\phi(P_0)=1$. Supposing we switch to $\phi(P_0)=-1$, we can easily calculate the new values of $c_1$ and $c_2$ and the change in $F$ as follows.

$$
\tilde{c_1}=c_1 + \frac{c_1 -x}{m-1}
$$

$$
\tilde{c_2}=c_2 - \frac{c_2 -x}{n+1}
$$

$$
\Delta F = (x-c_2)^2 \frac{n}{n+1} -(x-c_1)^2 \frac{m}{m-1}
$$

Similarly, we can calculate the changes when switching $\phi(P_1)=-1$ to $\phi(P_1)=1$.

$$
\tilde{c_1}=c_1 - \frac{c_1 -x}{m +1}
$$

$$
\tilde{c_2}=c_2 + \frac{c_2 -x}{n-1}
$$

$$
\Delta F = (x-c_2)^2 \frac{n}{n+1} -(x-c_1)^2 \frac{m}{m-1}
$$

For each sweep, check for the value of $\Delta F$. If $\Delta F<0$, update $\phi$, $c_1$, $c_2$, $m$, and $n$. Repeat until $\Delta F$ remains still for all pixels.

<br/>

## References

[1] Song, B. and Chan, T., 2002, "A Fast Algorithm for Level Set Based Optimization", UCLA Cam Report, 2(68), pp.1-20

[2] Chan, T. and Vese, L., 2001, "Active contours without edges", IEEE Transactions on Image Processing, 10(2), pp. 266-277
