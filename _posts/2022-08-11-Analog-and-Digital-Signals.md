---
layout: post
title: "[DSP] 1. Analog and Digital Signals"
author: "SJ Lee"
tags: Digital Signal Processing
---

A **signal** is a function containing information, often of time or space. Examples of signals include music, movies, telegraphs— pretty much any media that conveys information.

**Analog signals** have continuous domain and range. The sound of a violin is an analog signal, as its volume can have any arbitrary value. But if the music is recorded on a smartphone, it becomes a **digital signal**. Digital signals have discrete domain and range. To store an analog signal onto a digital device, the signal must be **sampled** and **quantized**. Sampling turns the domain into a discrete set and quantization turns the range into a discrete set.

Sampling is represented with the **Shah function**.

$$ III_T(t)=\sum_{k=-\infty}^{\infty}\delta(t-kT) $$
