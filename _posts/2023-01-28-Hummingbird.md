---
layout: post
title: "Hummingbird"
author: "SJ Lee"
tags:
  - Paper-Review
---

This post is a review of the paper [Hummingbird: Energy Efficient GPS Receiver for Small Satellites](https://dl.acm.org/doi/abs/10.1145/3372224.3380886).

<br/>

## Motivation

The demand for small satellites is increasing, and a localization scheme is necessary for proper performance. Since small satellites have limited power supply, they need a low-power Global Positioning System (GPS). But building a low-power GPS for small satellites is difficult because of their high speed (~7.8km/s).

Duty cycling is a possible solution to this problem, but the high Doppler shift between GPS satellites and the small satellite causes an increase in Time To First Fix (TTFF).

* Small satellite: A satellite of small mass and size. Usually built for cost efficiency compared to large satellites. Multiple small satellites may provide better performance than fewer large satellite for certain purposes.[2]

* Duty cyling: Duty cycle refers to the percentage of time a periodic signal is ON in a single period compared to the entire period. The main idea of duty cycling is activating the GPS receiver only a few times per orbit.[4] The receiver is turned ON until a position fix then turned OFF for specific duration.[1]

* Time To First Fix (TTFF): Measure of time required for GPS navigation device to calculate position solution.[3]

## Goal

The authors aim to create a complete low power GPS solution for small satellites. They named this solution $\mu$GPS.

## GPS basics

The GPS constellation consists of 31 active satellites transmitting navigation messages on the same carrier frequency. Each satellite has a pseudorandom noise code so that it can be identified. The satellites orbit so that at least four satellites are visible from any point on Earth.

There are three steps to getting a position fix.

1. Acquisition: The receiver searches for signals from visible GPS satellites and locks to at least four satellites.
2. Decoding: The receiver decodes signals from locked satellites to obtain information such as GPS time or clock bias.
3. Positioning: The receiver calculates its position based on obtained data.

## $\mu$GPS receiver

Being a GPS receiver for space where environmental conditions are harsh and repair is difficult, the $\mu$GPS receiver must satisfy the following conditions.

1. Small size, physical robustness
2. High accuracy (30m for position and 30cm/s for velocity)
3. Solutions must be transmitted to On-Board Computer (OBC) at 1Hz
4. Must provide clock synchronization to OBC

The $\mu$GPS receiver contains a customized low-power GPS chip which provides raw GPS data to a low-power microcontroller which computes the navigation solution. To correct the time drift in the OBC clock, $\mu$GPS must provide time synchronization. The receiver sends Pulse Per Second (PPS) signals to the OBC, where the PPS is the time at which the $\mu$GPS front end obtains position fix.

## $F^3$ algorithm

The Fast Fix and Forward ($F^3$) algorithm is created to improve the TTFF of the receiver.

To acquire a GPS signal the receiver must know both the code and the carrier of the GPS satellites. The code information is related to the range dimension and the carrier information is related to the Doppler dimension. Because small satellites have high velocity, the range of Doppler shift is very large, making the search space large and search time long (~25min). To reduce the time consumed for code search, the algorithm estimates the position and velocity of the GPS satellites and uses this information to predict Doppler shift. Figure 1 illustrates the $F^3$ algorithm.

<div align = 'center'>

|![f1](https://i.imgur.com/uh899FP.png)|
|:--:|
|Figure 1. The $F^3$ algorithm|

</div>

## References

[1] Narayana, S. *et al*., 2020, 'Hummingbird: Energy Efficient GPS Receiver for Small Satellites', MobiCom 2020

[2] Wikipedia contributors, 'Small satellite', *Wikipedia, The Free Encyclopedia*, Retrieved Jan 25 2023, [https://en.wikipedia.org/wiki/Small_satellite](https://en.wikipedia.org/wiki/Small_satellite)

[3] Wikipedia contributors, 'Time to first fix', *Wikipedia, The Free Encyclopedia*, Retrieved Jan 25 2023, [https://en.wikipedia.org/wiki/Time_to_first_fix](https://en.wikipedia.org/wiki/Time_to_first_fix)

[4] Ebinuma, T. *et al*., 2004, 'A miniaturised GPS receiver for space applications', IFAC Automatic Control in Aerospace 2004

## Image source (All figures)

Narayana, S. *et al*., 2020, 'Hummingbird: Energy Efficient GPS Receiver for Small Satellites', MobiCom 2020