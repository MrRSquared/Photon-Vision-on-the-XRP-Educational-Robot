# Photon With the XRP

This repository combines [Photon Vision](https://photonvision.org/) with the XRP robot. This works implementing the Photon [hardware in the loop simulation instructions](https://docs.photonvision.org/en/latest/docs/programming/photonlib/hardware-in-the-loop-sim.html). 

Currently, this is working running Photon on the XRP host laptop (Win11) and a USB camera. It should probably work on a raspberry pi too, however, you may need to use the [debian install](https://docs.photonvision.org/en/latest/docs/getting-started/installation/sw_install/other-coprocessors.html) directions on a pi image already set up as I do not think Photon's sd card image includes wifi. They say that Photon is tested to run on Buster, so I recommend a 64 Bit Legacy OS.

## To Do: 
In order to use this code with your own setup, you probably need to make a few changes to this code.

### Robot.java: 
In Robot.java, you need to update both the ip and the camera name for your photon server.

### build.gradle
In build.gradle, you need to change the XRP's ip address to your XRP robot's ip address. For more info on setting that up, check out. [WPILib's Web UI instructions](https://docs.wpilib.org/en/latest/docs/xrp-robot/web-ui.html)

