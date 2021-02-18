---
layout: post
title:  "Getting data from OpenDRIVE HD maps!"
date:   2021-02-18 19:55:00 +0100
categories: Studies
tags: coding guided-research autonomous-driving
pin: false
---

# Background

During my [Guided Research]({% post_url 2021-02-12-guided-research %}) I was given a HD map of some part of the [highway A9 near Munich, Germany](https://www.google.de/maps/place/A9,+Garching+bei+M%C3%BCnchen/@48.2395578,11.632844,4154m/data=!3m1!1e3!4m5!3m4!1s0x47a11d231dc12da1:0xd702677ee0331ed4!8m2!3d48.2385588!4d11.637908).
I use this map to get the world positions of landmarks like delineators, road signs, trees... These landmarks are then matched with some video footage of cameras mounted on gantry bridges.  

My final goal is to minimize the reprojection error from the landmarks and the corresponding video pixels to find the camera world position (the extrinsic parameters).

# OpenDRIVE parser implementation

I am currently implementing a parser for the maps, which are in the [OpenDRIVE](https://www.asam.net/index.php?eID=dumpFile&t=f&f=3495&token=56b15ffd9dfe23ad8f759523c806fc1f1a90a0e8#_foreword) format. This is a XML format which is pretty complex and thus powerful to describe road networks.  
At my [OpenDRIVE](https://github.com/Brucknem/OpenDRIVE) github repository you can have a look at the implementation.

# Example images

The images each show a part of the highway A9 near Munich. In the images taken from the map you see the roads in green and the relevant landmarks in violet. There is also one delineator highlighted in red.

## Complete camera view

![Map part of the highway A9](/posts/2021-02-16-opendrive-parsing/map_view.png){: width="100%"}
_A part of the the highway A9 near Munich in the HD map_


![Map part of the highway A9](/posts/2021-02-16-opendrive-parsing/camera_view.png){: width="100%"}
_More or less the same part of the the highway A9 near Munich viewed from a camera mounted on a gantry bridge_

## Zoomed towards the highway exit

![Map part of the highway A9](/posts/2021-02-16-opendrive-parsing/map_exit.png){: width="100%"}
_The same part of the the highway A9 near Munich, zoomed towards the highway exit, in the HD map_


![Map part of the highway A9](/posts/2021-02-16-opendrive-parsing/camera_exit.png){: width="100%"}
_The same part of the the highway A9 near Munich, zoomed towards the highway exit, from a camera mounted on a gantry bridge_

