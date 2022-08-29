---
layout: post
title: "[DSP] 2. The Unit Step Function and the Dirac Delta Function"
author: "SJ Lee"
tags: Digital-Signal-Processing
---

The unit step function $u(t)$ takes the value of $1$ when $t$ is positive and $0$ when $t$ is negative.
In programming jargon $u(t)$ is also known as the Heaviside function. $u(0)$ is often defined as $0.5$,
but in theoretical signal processing problems people tend not to care very much about the value of $u(0)$.

<div align="center">
 
|<img src="https://github.com/lsj0410/lsj0410.github.io/blob/master/assets/images/dsp-02/unit_step.png?raw=true" />|
|:--:| 
|Figure 1. The unit step function (Image source: Wikipedia)|
  
</div>
<br/>

The Dirac delta function $\delta(t)$ represents an impulse. It has a positive value at $0$ and a value of $0$ at all other points.
There are several notable characteristics about the Dirac delta function. The first is that it is the derivative of the unit step function.
(See the graph of the unit step function above.) Another is that when integrated over the entire domain the result is $1$.
Thus in the continuous domain the value of the Dirac delta at $0$ diverges to $\infty$, and in the discrete domain the value of the Dirac delta at $0$ is $1$.

<div align="center">

|<img src="https://github.com/lsj0410/lsj0410.github.io/blob/master/assets/images/dsp-02/dirac-delta.png?raw=true" />|
|:--:| 
|Figure 2. The Dirac delta function (Image source: Wikipedia)|

</div>
<br/>

While this series of posts will mainly cover signal processing in the discrete domain,
it is worth understanding these basic functions in the continuous domain.
Hence the remaining part of this post will focus on the continuous domain.

It is easy to misunderstand that $\delta(at)$ is equal to $\delta(t)$ because they are both $\infty$ at $0$ and $0$ at all other points.
However, we must again take careful consideration of the second characteristic of the Dirac delta function.

$$\int_{-\infty}^\infty \delta(at) dt = \frac{1}{|a|}\int_{-\infty}^\infty \delta(s) ds = \frac{1}{|a|}$$

Both $\delta(at)$ and $\delta(t)$ have nonzero values only at $t=0$.
Thus we know that $\delta(at)$ must be some constant multiple of $\delta(t)$.
Therefore $\delta(at)$ is actually $\delta(t)$ divided by $|a|$.

$$\delta(at)=\frac{1}{|a|}\delta(t)$$

One may think that the Dirac delta has little practical meaning because it does not have a convergent nonzero value at any point.
However the Dirac delta is meaningful when inside an integral.
Supposing $a < 0 < b$, the following is an important characteristic of the Dirac delta function.

$$\int_a^b \delta(t)f(t) dt = f(0)$$

An intuitive explanation for this formula is given below.

$$
\begin{equation}
\begin{split}
\int_a^b \delta(t)f(t) dt {} & ={\int_a^{0-} \delta(t)f(t) dt} + {\int_{0-}^{0+} \delta(t)f(t) dt} + {\int_{0+}^b \delta(t)f(t) dt} \\\\\\
      &= \int_{0-}^{0+} \delta(t)f(t) dt = \int_{0-}^{0+} \delta(t)f(0) dt = \int_{-\infty}^{\infty} \delta(t)f(0) dt = f(0)
\end{split}
\end{equation}
$$

Now we move our focus to the Fourier transform of these functions.
The derivation of the Fourier transform of the unit step function can be rather confusing,
and a detailed explanation about the process may be included in future posts.
For now we will simply take for given that the Fourier transform of $u(t)$ is as follows.

$$U(f) = \frac{1}{j2\pi f}+\frac{1}{2}\delta(f)$$

The Fourier transform of the Dirac delta function can be easily derived using the integration characteristic of the Dirac delta function.

$$\int_{-\infty}^{\infty} \delta(t)e^{-j2\pi ft} dt = e^{-j2\pi ft} \bigg\rvert_{t=0} = 1$$

## Image sources

Wikipedia contributors. (2022, August 18). Heaviside step function. In Wikipedia, The Free Encyclopedia. Retrieved 10:12, August 19, 2022, from https://en.wikipedia.org/w/index.php?title=Heaviside_step_function&oldid=1105180870

Wikipedia contributors. (2022, August 14). Dirac delta function. In Wikipedia, The Free Encyclopedia. Retrieved 10:12, August 19, 2022, from https://en.wikipedia.org/w/index.php?title=Dirac_delta_function&oldid=1104289609



