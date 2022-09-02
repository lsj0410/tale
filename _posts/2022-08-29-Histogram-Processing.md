---
layout: post
title: "[DIP] 2. Histogram Processing"
author: "SJ Lee"
tags: Digital-Image-Processing Digital-Signal-Processing
---

## Histogram of an image

Again we begin with our dog picture from the last post.

<div align = "center">
  
  |<img src="https://user-images.githubusercontent.com/63445411/186171143-f76d869f-034b-4c46-b0ab-479874269486.png">|
  |:--:|
  |Figure 1. Original image|
  
</div>

<br/>

This simple python code generates a histogram of the image.

```python
import matplotlib as plt
plt.hist(img)
```

<div align = "center">
  
  |<img src="https://user-images.githubusercontent.com/63445411/187153957-adcd6031-f35d-48d1-9012-88c9bc04f10d.png">|
  |:--:|
  |Figure 2. Histogram of original image|
  
</div>

<br/>

Figure 2 shows us that most of the intensity values of the pixels are located in the 180-220 zone.
Our goal is transforming this image so that the histogram is generally flat.
This process is also known as *equalizing* the image.

## The transformation

First we consider this function.

$$ p_x(i) = \frac{n_i}{MN} $$

Here $x$ is any pixel in the image, $i$ a value between 0 and 255, 
$M$ and $N$ the height and width of the image and $n_i$ the number of pixels with intensity $i$. 
This function represents the ratio of number of pixels with a certain intensity to the total number of pixels, 
which can be thought as the probability a random pixel has that certain intensity.

With this idea we consider $p_x(i)$ as a probability distribution function.
Then we can also think of $ P_x(i) = \sum_{j=0}^i p_x(j) $, a cumulative distribution function.

<div align = "center">
  
  |<img src="https://user-images.githubusercontent.com/63445411/187167039-5cb35ed8-e824-4f4e-ae65-76431973afd8.png">|
  |:--:|
  |Figure 3. Cumulative distribution function of original image|
  
</div>

<br/>

Figure 3 shows the cumulative distribution function of Figure 1.

Let $y(n)$ denote the intensity value of the pixel in the transformed image at location $n$.
Then the transformation

$$ y(n) = P_x(x(n)) \cdot 255 $$

yields the desired results.

Following is a histogram processed version of our dog image.

<div align = "center">
  
  |<img src = "https://user-images.githubusercontent.com/63445411/187164083-d7db1a45-5a3d-411a-a8eb-dcb008ffd98e.png">|
  |:--:|
  |Figure 4. Transformed image|
  
</div>

<br/>

We can see that the background, which looked consistently bright in the original image, takes a more distributed intensity.

<div align = "center">
  
  |<img src="https://user-images.githubusercontent.com/63445411/187164124-8620f0b8-93c3-4eb0-a9a4-8b627033ca6e.png">|
  |:--:|
  |Figure 5. Histogram of transformed image|
  
</div>

<br/>

Figure 5 demonstrates the histogram corresponding to Figure 4.
We see that it is indeed much flatter than Figure 2.

## Why does it work?

Then why does this simple transformation using the cumulative distribution function produce a flat histogram?
Here we present an intuitive explanation involving two kinds of images.
Suppose there is a dark image whose pixels mostly have low intensity values.
Then the cumulative distribution function would start out steep and reach near 1 fairly soon.
Using this function for intensity transformation would spread out the dark pixels to a wider intensity range.

Next imagine a bright image whose pixels mostly have high intensity values.
Our dog example is one such image.
The cumulative distribution would start out even and rise sharply near the end.
Using this function for intensity transformation would spread out the bright pixels to a wider intensity range.

<br/>

The code used for generating the images can be found [here](https://github.com/lsj0410/Digital-Signal-Processing/tree/main/dip-02).

## References

Coursera [*Fundamentals of Digital Image and Video Processing*](https://www.coursera.org/learn/digital)
