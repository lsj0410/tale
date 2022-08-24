---
layout: post
title: "[ED] 1. Active Contours without Edges [1]"
author: "SJ Lee"
tags: Edge-Detection Paper-Review
---

I am reading the paper [*Active Contours without Edges*](https://ieeexplore.ieee.org/abstract/document/902291?casa_token=sLi7QkfrH70AAAAA:RuzDg6_sDE5a9pYCxARH8DcSnPv9W19D-_fUQj4_gggAsBfEwX2KXHq-5uO9ypLs8yCqxxvhBw)
by Chan and Vese.[1]

I also created a python realization of this paper, which can be found [here](https://github.com/lsj0410/Edge-Detection/tree/main/Active-Contours)

<br/>

### The problem
A contour is also known as a level set. It is a line connecting points that have the same value in a certain function.
Active contours are widely used to detect objects in an image.
This paper proposes a new method of edge detection using active contours using an energy-based segmentation.
We are given an image $u_0$. Our goal is determining its boundary $C_0$. We build an evolving curve $C$, and modify $C$ until it equals $C_0$.

The energy functional $F$ is defined as the following.

$$
\begin{equation}
\begin{split}
F(c_1,c_2,C) {} & = \mu \cdot \text{Length}(C)+\nu \cdot \text{Area}(inside(C)) \\\\\\
  & + \lambda_1 {\int_{inside(C)}|u_0 (x,y)-c_1 |^2 dxdy} \\\\\\
  & + \lambda_2 {\int_{outside(C)}|u_0 (x,y)-c_2 |^2 dxdy}
\end{split}
\end{equation}
$$

Here $\mu$ and $\nu$ are nonnegative parameters and $\lambda_1$, $\lambda_2$ are positive parameters.
Generally we use values of $\lambda_1 = \lambda_2 = 1$ and $\nu=0$. 
We want to minimize the energy functional $F(c_1, c_2, C)$ in terms of $c_1$, $c_2$, $C$.

<br/>

### The Mumford-Shah functional

We consider the relationship between our energy functional and the Mumford-Shah functional.
The Mumford-Shah functional for segmentation is defined as the following.

$$ F^{MS} (u,C) = \mu \cdot \text{Length}(C) + \lambda \int_{\Omega} |u_0 (x,y)-u(x,y)|^2 dx dy + \int_{\Omega \backslash C} |\nabla u(x,y)|^2 dx dy$$

Here $u_0$ is the given image and $\mu$, $\lambda$ are positive parameters.
The solution image $u$ is obtained by minimizing this functional and is formed by smooth regions $R_i$ and sharp boundaries $C$.

<br/>

Consider the case where $F^{MS}$ is restricted to piecewise constant functions.
That is, $u=c_i$ on each connected component $R_i$.
Then $c_i$ must be the average of $u_0$ on $R_i$. 
Identifying $R_i$s that minimize $F^{MS}$ is known as the minimal partition problem.

<br/>

The active contour model with energy functional is a particular case of the minimal partition problem.
Here there are exactly two values of $c_i$. 
$c_1$ is the average of $u_0$ inside $C$ and $c_2$ is the average of $u_0$ outside $C$.

<br/>

### The level set method

In the level set method $C$ is represented by the zero level set of a Lipschitz function $\phi$ such that

$$ C=\partial \omega = \lbrace (x,y) \in \Omega : \phi(x,y)=0 \rbrace $$

$$ inside(C) = \omega = \lbrace (x,y) \in \Omega : \phi (x,y) > 0 \rbrace $$

$$ outside(C) = \Omega \backslash \bar{\omega} = \lbrace (x,y) \in \Omega : \phi (x,y)<0 \rbrace $$

We will replace $C$ with $\phi$.

<br/>

We use the Heaviside function $H$. $H(z)=1$ if $z \geq 0$ and $H(z)=0$ if $z<0$.
We also use the one-dimensional Dirac measure $\delta_0$ defined by $\delta_0 (z) = \frac{d}{dz} H(z)$.
Now we can write the terms of the energy functional as the following.

$$ \text{Length}(C)=\text{Length} \lbrace \phi =0 \rbrace = \int_{\Omega} |\nabla H(\phi(x,y))|dx dy = \int_{\Omega} \delta_0 (\phi(x,y))|\nabla \phi (x,y)|dx dy $$

$$ \text{Area}(inside(C))= \text{Area} \lbrace \phi \geq 0 \rbrace = \int_{\Omega} H(\phi(x,y))dx dy $$

$$
\begin{equation}
\begin{split}
\int_{inside(C)} |u_0 (x,y)-c_1 |^2 dx dy {} & = \int_{\phi>0}|u_0 (x,y)-c_1 |^2 dx dy \\\\\\
  & =\int_\Omega |u_0 (x,y)-c_1 |^2 H(\phi(x,y))dx dy
\end{split}
\end{equation}
$$

$$ 
\begin{equation}
\begin{split}
\int_{outside(C)} |u_0 (x,y)-c_2 |^2 dx dy {} & = \int_{\phi<0}|u_0 (x,y)-c_2 |^2 dx dy \\\\\\
  & =\int_\Omega |u_0 (x,y)-c_2 |^2 (1-H(\phi(x,y))) dx dy
\end{split}
\end{equation}
$$

<br/>

Then we can rewrite the energy functional as the following.

$$
\begin{equation}
\begin{split}
F(c_1,c_2,\phi) {} & =\mu \int_\Omega \delta_0 (\phi(x,y))|\nabla \phi (x,y)|dx dy + \nu \int_\Omega H(\phi(x,y))dx dy \\\\\\
  & + \lambda_1 \int_\Omega |u_0 (x,y)-c_1 |^2 H(\phi(x,y))dx dy \\\\\\
  & +\lambda_2 \int_\Omega |u_0 (x,y)-c_2 |^2 (1-H(\phi(x,y)))dx dy
\end{split}  
\end{equation}
$$ 

<br/>

Our solution $u$ takes the value of $c_1$ inside $C$ and $c_2$ outside $C$. Thus we can write $u$ as the following.

$$u(x,y)=c_1 H(\phi(x,y))+c_2 (1-H(\phi(x,y))) $$

To minimize $F$ given $\phi$, $c_1$ must be the average of $u_0$ inside $C$ and $c_2$ the average of $u_0$ outside $C$.

$$ c_1 (\phi)=\frac{\int_\Omega u_0 (x,y)H(\phi(x,y))dx dy}{\int_\Omega H(\phi(x,y))dx dy} $$

$$ c_2 (\phi)=\frac{\int_\Omega u_0 (x,y)(1-H(\phi(x,y)))dx dy}{\int_\Omega (1-H(\phi(x,y)))dx dy} $$

Now we see that the energy functional is a function of $H(\phi)$, which is the characteristic function of $\omega$. 

<br/>

## References

[1] T. F. Chan and L. A. Vese, 2001, "Active contours without edges", IEEE Transactions on Image Processing, vol. 10, no. 2, pp. 266-277
