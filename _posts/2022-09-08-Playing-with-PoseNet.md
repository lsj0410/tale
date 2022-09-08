---
layout: post
title: "[Coral] Playing with PoseNet"
author: "SJ Lee"
tags:
  - Coral
---

[PoseNet](https://github.com/google-coral/project-posenet) is an open source pose estimation model optimized for edge TPU provided by Google. It identifies people in an image and returns **keypoint values**, the x, y coordinates of their eyes, ears, nose, shoulders, knees, etc.

## Connecting the camera

To run PoseNet on Coral first connect the Coral camera to the Coral board.

<div align = "center">

|![Coral and camera](https://i.imgur.com/5DEXbVx.jpg)|
|:--:|
|Figure 1. The Coral board and the camera|

</div>

<br/>

On the top left corner of the board there is a camera connector. If the connector is closed, flip it open.

<div align = "center">

|![open](https://i.imgur.com/sx2XwZK.jpg)|![closed](https://i.imgur.com/Usoq5bb.jpg)|
|:--:|:--:|
|Figure 2. Camera connector open|Figure 3. Camera connector closed|

</div>

<br/>

Then push the strip connected to the camera into the connector and close the connector.

<div align = "center">

|![connected](https://i.imgur.com/7vGJyWb.jpg)|
|:--:|
|Figure 4. Camera connected to Coral board|

</div>

<br/>

Next connect Coral to the computer. Refer to [this post](https://lsj0410.github.io/2022-09-02/Getting-Started-with-Coral) if you don't know how.

Now check whether the camera is well connected to the Coral board. Type the command `v4l2-ctl --list-devices`. If the camera is connected, you will see the name of the camera in the command line.

<div align = "center">

|![camera connection](https://i.imgur.com/0reI8MJ.png)|
|:--:|
|Figure 5. Checking camera connection|

</div>

<br/>

## Running PoseNet

Then clone the PoseNet github repo with the command `git clone https://github.com/google-coral/project-posenet`. Now if you type `ls` in the command line, you will see a new folder *project-posenet* containing the contents of the repository.

The code we will run is `pose_camera.py`. It detects people from streamed camera video and overlays keypoints and a skeleton over it. However to successfully display video output from Coral one must have a HDMI cable and a corresponding screen. Since I do not have such equipment I modified the code to check PoseNet is functioning properly in a different way.

``` python
for pose in outputs:
  draw_pose(svg_canvas, pose, src_size, inference_box)
  if pose.score < 0.4: continue
  print('\nPose Score: ', pose.score)
  for label, keypoint in pose.keypoints.items():
    print('  %-20s x=%-4d y=%-4d score=%.1f' %
    (label.name, keypoint.point[0], keypoint.point[1], keypoint.score))
```
<br/>

I added the `print` lines from `simple_pose.py` and added it to `pose_camera.py`. Now we can see the output coordinates as text.

<div align = "center">

|![posenet output](https://i.imgur.com/ThmdnSh.png)|
|:--:|
|Figure 6. PoseNet output|

</div>

<br/>
