---
title: code implementations research for body tracking
category: Technical
date: 2021-04-29T20:44:07.489Z
description: how to track bodies really well in real-time?
tags: body tracking, kinect, research, code
thumbnail: /img/screen-shot-2021-04-29-at-22.49.48.png
---
best body tracking available now is with azure kinect

https://www.youtube.com/watch?v=M1lDMOjQF5Y



really good depth sensor + ML, so it's very robust

implementations:

* openframeworks - https://github.com/prisonerjohn/ofxAzureKinect

good, had to fix bugs on the open source library

* unity - https://github.com/satoshi-maemoto/Azure-Kinect-Unity-Body-Tracker

good, but has latency

* pure c++ - https://github.com/microsoft/Azure-Kinect-Samples

good but hard to work with

* touch designer

tested, works super well, no latency and lots of configurations, limitation of TD license and python coding is shitty.



guess we will go with **openframeworks**



\--

notes:

eye tracking example done for another project using javascript and only RGB images.

(slow and innacurate). open cv is better.

https://eyemaske.web.app/#/