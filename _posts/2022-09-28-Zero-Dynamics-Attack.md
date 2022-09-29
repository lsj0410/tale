---
layout: post
title: "Zero Dynamics Attack"
author: "SJ Lee"
tags:
  - Control
---

The posts under the tag **Control** are rearranged versions of notes I took while studying control theory last year.

<br/>

## Prerequisite: The normal form

We use differential equations to describe a linear system. There are multiple forms of describing an identical system, and the **normal form** is one of them. A system in normal form is written as the following.

$$
\begin{equation}
\begin{split}
\dot{x_1} & = x_2 \\
\dot{x_2} & = x_3 \\
{} & \; \; \vdots \\
\dot{x_{r - 1}} & = x_{r} \\
\dot{x_r} & = \phi_: ^ T x_: + \phi_z^T x_z+ bu \\
\dot{x_z} & = Sx_z+px_1 \\
y & = x_1
\end{split}
\end{equation}
$$

Here $u$ is the input, $y$ the output, and $r$ the **relative degree** of the system. The state $x$ is divided into $x_: = [x_1 , x_2 , \cdots, x_r]^T$ and $n-r$ dimensional $x_z$. 

* **Relative degree**: The difference betwen the orders of the numerator and the denominator in the transfer function of the system

<br/>

## Control system attacks

There are two major types of attacks in a modern control system. One is the **actuator attack**, and the other is the **sensor attack**. The two attacks are described in Figure 1. Supposing the plant and controller themselves are both secure, the adversary would attack the communication network between them. An attack on the actuator signal $u(t)$ is called the actuator attack, and an attack on the sensor measurement $y(t)$ is called the sensor attack. These attacks are denoted by the corruption to the original signals, $a_a(t)$ and $a_s(t)$.

<div align = "center" >

|![attack](https://i.imgur.com/ajXkSeQ.png)|
|:--:|
|Figure 1. Actuator attack and sensor attack|

</div>

<br/>

A **stealthy** attack is an attack that cannot be detected at the output. Obviously, these kind of attacks are particularly dangerous. A **disruptive** atttack is an attack that makes part of a system diverge. Let us denote the detection level as $L_\text{detect}$ and the hazard level as $L_\text{hazard}$, the actual state and output as $x$ and $y$ and the attack-free state and output as $x_{\text{af}}$ and $y_{\text{af}}$. Then a disruptive attack is an attack such that $||x(t^*)-x_\text{af}(t^*)|| \geq L_\text{hazard}$ for some $t^* \geq t_0$. For this attack to be stealthy, it must satisfy $||y(t)-y_{\text{af}}(t)|| \leq L_\text{detect}$ for all $t \in [t_0, t^*]$. [1]

<br/>

## Zero dynamics attack

What is a zero dynamics attack? The **zero dynamics** of a control system is the dynamics that sends the output of the system to zero. Let the input of a system be $u(t)$ and the output $y(t)$. Then there exists some pair of initial condition and input that satisfies $y(t)=0$ for $t \geq 0$. Let us revisit equation (1). If $y = x_1 = 0$, $x_:$ is reduced to zero. Then the remaining zero dynamics is $\dot{x_z} = Sx_z$. This is the reason we use the normal form when discussing zero dynamics: it is easy to identify the zero dynamics of the system. [2]

A **zero dynamics attack** is an actuator attack that pushes the system states along the zero dynamics. Since the zero dynamics send the output to zero, the zero dynamics attack is fundamentally stealthy. [1]

<br/>

## References

[1] Shim, H. et al., 2022, "Zero-dynamics attack, variations, and countermeasures." *Security and Resilience of Control Systems*, Springer, Cham, pp.31-61.

[2] 심형보, 2019, "Zero dynamics를 이용하여 제어시스템을 몰래 공격하는 방법", 제어$\cdot$로봇$\cdot$시스템학회지, 25(3), pp.13-19