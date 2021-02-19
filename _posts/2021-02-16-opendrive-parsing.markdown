---
layout: post
title:  "Getting data from OpenDRIVE HD maps!"
date:   2021-02-18 19:55:00 +0100
categories: Studies
tags: coding guided-research autonomous-driving
pin: false
image: 
    src: /posts/2021-02-16-opendrive-parsing/map_view.png
    alt: A part of the the highway A9 near Munich in the HD map
---

During my [Guided Research]({% post_url 2021-02-12-guided-research %}) I was given some HD maps of some part of the [highway A9 near Munich, Germany](https://www.google.de/maps/place/A9,+Garching+bei+M%C3%BCnchen/@48.2395578,11.632844,4154m/data=!3m1!1e3!4m5!3m4!1s0x47a11d231dc12da1:0xd702677ee0331ed4!8m2!3d48.2385588!4d11.637908).
I use these maps to get the world positions of landmarks like delineators, road signs, trees... These landmarks are then matched with some video footage of cameras mounted on gantry bridges.  

My final goal is to minimize the reprojection error from the landmarks and the corresponding video pixels to find the camera world pose (the extrinsic parameters).

# OpenDRIVE parser & query implementation

I am currently implementing a parser for these maps, which are in the [OpenDRIVE](https://www.google.com/maps/place/48%C2%B014'21.3%22N+11%C2%B038'18.7%22E/@48.2392466,11.6363278,17z/data=!3m1!4b1!4m5!3m4!1s0x0:0x0!8m2!3d48.239243!4d11.6385165) format. This is an XML format which is pretty complex and thus powerful. It's the industry standard to describe road networks.

I was struggling really hard with the implementation of the parser, and it took me around a week to find out how to implement it. The good thing is that [ASAM](https://www.asam.net/standards/detail/opendrive/) provides a free XML schema definition (XSD) which describes how OpenDRIVE files have to be structured. The hard part was to get the definition into code so that I can process the data.

The first thing I thought of was to use an XML to C++ compiler which should generate C++ data bindings from the XSD files. I quickly found the [Code Synthesis](https://www.codesynthesis.com/products/xsd/) data binding compiler, but I couldn't get it to work at all for the OpenDRIVE V1.6 standard. I thus tried to implement the standard by hand, which did turn out to be not feasibly at all, so I again searched for ready made solutions or how to use the compiler. 

Eventually, after around one week of despair, I finally found out that our maps conform to the OpenDRIVE **V1.4** standard. I then gave the data binding compiler another try and _voila_, after another day of fiddling around, it works as I expect it to do and produces code that can parse the HD maps. I can now represent the data as a nice object model. _What a relief!_

I am now working on how to transform the landmark positions into a format so that I can use it in my camera pose estimation algorithm.

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

