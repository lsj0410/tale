---
layout: post
title: "[Coral] Getting Started with Coral"
author: "SJ Lee"
tags: Coral
---

Through the [*Ambient AI Bootcamp*](https://gsds.snu.ac.kr/category/board-50-GN-KFUcID30-20210318235757/#none) from [Seoul National University Graduate School of Data Science](https://gsds.snu.ac.kr/), I was given a chance to experience AI on edge TPU with Google Coral. This post is based on the practice sessions during the Bootcamp.


## The Coral Dev Board

[Coral](https://coral.ai/) is an edge device toolkit provided by Google. The [Coral Dev Board](https://coral.ai/products/dev-board/) is a single-board computer that performs high-speed ML inferencing. It supports Tensorflow Lite models that satisfy certain characteristics.[1]

<div align = "center">

  |<img src="https://user-images.githubusercontent.com/63445411/187583092-6352ba66-1d75-4e7e-b571-274e0316a395.png">|
  |:--:|
  |Figure 1. The Coral Dev Board|

</div>

<br/>

The Coral Dev Board has two USB-C ports. The left is the data port and the right is the power port. Use cables to connect the data port to your computer and the power port to the power socket.

## Setup(Windows)

Before you begin, you must make sure that [Python 3](https://www.python.org/) is installed in your computer. Check the location of your `python.exe` file. If it is located in folders whose names contain empty space(' ') or other special characters, it might be safer to place a copy of your Python 3 executable file in a location with a simpler address, e.g. `/C/Executables`.

Open the [Git Bash](https://gitforwindows.org/) terminal and enter the following commands. Replace `/C/Executables/Python37_64` with the location of your python executable file. This code makes it available to run python files with the command `python3`.

{% highlight markdown %}
$ echo "alias python='winpty /C/Executables/Python37_64/python.exe'" >> ~/.bash_profile
$ source ~/.bash_profile
```
{% endhighlight %}

<br/>

Then install the [Mendel Development Tool(mdt)](https://coral.ai/docs/dev-board/mdt/) with the following code. Replace `Executables/Python37_64` with the location of your python executable file.

{% highlight markdown %}
```
$ python -m pip install mendel-development-tool
$ echo 'export PATH="$PATH:$HOME/.local/bin"' >> ~/.bash_profile
$ echo 'export PATH="$PATH:$HOME/Executables/Python37_64/Scripts"' >> ~/.bash_profile
$ echo "alias mdt='winpty mdt'" >> ~/.bash_profile
$ source ~/.bash_profile
```
{% endhighlight %}

<br/>

Now we can connect to our Coral board with mdt. Here are some of the `mdt` commands that are used often.
<br/>

`mdt devices`: looks for Coral boards nearby

`mdt shell`: connects to Coral board

`mdt push <FILE>`: pushes file from local computer to Coral board

<br/>

Keep in mind that the `mdt` commands are used when *not* connected to the Coral board. You cannot push a local file to Coral with `mdt push` when you are already connected to Coral. You must run `exit` to break the connection before pushing files.

When connecting to Coral for the first time, first run `mdt devices`. Git bash will show you the **name** of the board(for example, mine is `yellow-valet`) connected to the computer via the cable. Then run `mdt shell` to connect to that device.
Now we can connect the board to Wi-Fi to access the board more easily. Use the following command. Replace `<NETWORK_NAME>` and `<PASSWORD>` with corresponding values.

{% highlight markdown %}
```
nmcli dev wifi connect <NETWORK_NAME> password <PASSWORD> ifname wlan0
```
{% endhighlight %}

<br/>

After connecting your Coral board to Wi-Fi, `mdt shell` alone may not locate your device if there are multiple boards connected to the same Wi-Fi. There are two ways to mitigate this problem. First, you may run `mdt shell <BOARD_NAME>` to connect directly to the desired board. Or you could tell your computer to memorize the name of your Coral board. For this run `mdt set preferred-device <BOARD_NAME>`. Then `mdt shell` would always be able to locate your board when connecting.

## References

[1] Google, 2020, "Dev Board", Coral, Retrieved 12:05, August 31, 2022 from https://coral.ai/products/dev-board/
