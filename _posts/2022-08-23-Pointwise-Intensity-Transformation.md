---
layout: post
title: "[DIP] 1. Pointwise Intensity Transformation"
author: "SJ Lee"
tags: Digital-Image-Processing Digital-Signal-Processing
---

## Image enhancement

Image enhancement is the process of making an image `look better',
which is certainly a subjective goal and can vary for different situations.
Pointwise intensity transformation is a type of image enhancement technique.

## Pointwise intensity transformation

Pointwise intensity transformation is modifying the intensity of each point independently with each other.
Such transformation is done when the image is too dark, too bright, or when we want to look into a specific intensity region.
Pointwise intensity transformation can be represented with a function that maps the intensity in the original image to the modified intensity.
Every pixel that has the same intensity in the original image must have the same intensity in the transformed image as well.

<div align = "center">

<img src = "https://user-images.githubusercontent.com/63445411/186169976-6a7c02ce-db59-4b98-959d-3b98b46ba2f7.png">

Figure 1. Pointwise intensity transformations

</div>

Figure 1 describes several examples of pointwise intensity transformations.
The identity maps the image to an identical image.
The negative turns the bright parts of the image dark and the dark parts bright.
The power > 1 turns the image generally dark, and power < 1 turns the image bright.
Dynamic range expansion spreads out the middle intensity range and turns the bright/dark parts brighter/darker.

<br/>

The following figures demonstrate each transformation in action.
Figure 2-1 is the original image of a dog. Figures 2-2, 2-3, 2-4, 2-5, 2-6 are the results of each transformation.

<div align = "center">

|<img src = "https://user-images.githubusercontent.com/63445411/186171143-f76d869f-034b-4c46-b0ab-479874269486.png">|<img src = "https://user-images.githubusercontent.com/63445411/186171143-f76d869f-034b-4c46-b0ab-479874269486.png">|<img src = "https://user-images.githubusercontent.com/63445411/186171506-9eae3897-862c-4c15-ab28-c9c5315aa6a5.png">     |
|:--:|:--:|:--:|
|Figure 2-1. Original image|Figure 2-2. Identity transformation|Figure 2-3. Negative transformation|
|<img src = "https://user-images.githubusercontent.com/63445411/186171889-c50be4d5-4da2-4cf2-abed-b76ec18ec749.png">|<img src = "https://user-images.githubusercontent.com/63445411/186171936-0e8bbefd-591a-4f3c-b809-f9678f4a3b72.png">|<img src = "https://user-images.githubusercontent.com/63445411/186171966-7cb8c1a7-0a11-4a89-8f77-99fb8e883cf0.png">|
|Figure 2-4. Power transformation (gamma > 1)|Figure 2-5. Power transformation (gamma < 1)|Figure 2-6. Dynamic range expansion|

</div>

<br/>

Another interesting pointwise intensity transformation technique is bit plane slicing.
Each pixel in a 8-bit image has a value ranging from 0 to 255 and can be written in 8 binary digits. 
Then this image can be separated into 8 bit planes where each pixel in the $i$ th bit plane represents the $i$ th binary digit of the pixel.
Figures 3- $i$ ( $1 \leq i \leq 8$ ) each represent the $i$ th bit plane of the dog image (Figure 2-1).

<div align = "center">

|<img src = "https://user-images.githubusercontent.com/63445411/186176084-72d0631a-17c6-43fa-83cb-b5697df31577.png">|<img src = "https://user-images.githubusercontent.com/63445411/186176131-bf707b5c-d581-4477-bb14-601feeb91062.png">|<img src = "https://user-images.githubusercontent.com/63445411/186176282-5c623bd0-41a6-42c3-bd4d-d3c496196944.png">|<img src = "https://user-images.githubusercontent.com/63445411/186176323-4623b8b5-2fc9-4860-955d-52f52f8ca4b3.png">|
|:--:|:--:|:--:|:--:|
|Figure 3-1. Bit plane 1|Figure 3-2. Bit plane 2|Figure 3-3. Bit plane 3|Figure 3-4. Bit plane 4|
|<img src = "https://user-images.githubusercontent.com/63445411/186176365-889f8e61-8bb2-4f3d-b382-6f1fb2db8f80.png">|<img src = "https://user-images.githubusercontent.com/63445411/186176402-e1bc1f9f-9d16-4c6d-a488-0577f970f372.png">|<img src = "https://user-images.githubusercontent.com/63445411/186176442-85727565-79ca-4e87-858c-99121e9b750e.png">|<img src = "https://user-images.githubusercontent.com/63445411/186176469-4e36cbb2-4cf8-466c-acbb-5b8fbcb53584.png">|
|Figure 3-5. Bit plane 5|Figure 3-6. Bit plane 6|Figure 3-7. Bit plane 7|Figure 3-8. Bit plane 8|

</div>

<br/>

We see that the higher bit planes are fairly close to the original image.
Taking some of these planes and adding them, we get the following results.

<div align = "center">

|<img src = "https://user-images.githubusercontent.com/63445411/186176512-8f43e061-0254-43b5-a728-fbf5dbf6bde4.png">|<img src = "https://user-images.githubusercontent.com/63445411/186176555-c1bdcbab-1487-4bff-a2da-2ae6eb2d2dcf.png">|
|:--:|:--:|
|Figure 4-1. Bit plane 7+8|Figure 4-2. Bit plane 6+7+8|

</div>

<br/>

Each of these images use far less pixels than the original image and are sufficient to recognize that the object in the image is a dog.
In some cases this may be a viable compression technique.

The code used for generating the images can be found [here](https://github.com/lsj0410/Digital-Signal-Processing/tree/main/dip-01).

## References

Coursera [*Fundamentals of Digital Image and Video Processing*](https://www.coursera.org/learn/digital)

