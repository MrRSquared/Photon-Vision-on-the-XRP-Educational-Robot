# PhotonTest
This repository shows how to use [Photon Vision](https://docs.photonvision.org/en/latest/) with an [XRP Robot](https://docs.wpilib.org/en/latest/docs/xrp-robot/index.html) running the WPILIb Software.

It is experimental, but it is working for me thus far. YMMV :)

I this works with WPILib 2024.1.1 Beta 2   Release.

Basically, it uses Photon running as an [NT server host](https://docs.wpilib.org/en/latest/docs/xrp-robot/index.html) (either on the pc itself or on a coprocessor), and it can still connect to the XRP through websockets.

## Code

First, get photon running either on your host pc or on a coprocessor, and set it up as a server like they do on the [Photon Hardware in the Loop Simulation directions](https://docs.wpilib.org/en/latest/docs/xrp-robot/index.html).

Then, add this code in your robot code.

```java
if(RobotBase.isSimulation()) {
   NetworkTableInstance inst = NetworkTableInstance.getDefault();
   inst.stopServer();
   // Change the IP address in the below function to the IP address you use to connect to the PhotonVision UI.
   inst.setServer("localhost");
   inst.startClient4("Robot Simulation");
}
```
This connects the simulator to the server.
The code above will connect to a server running on the host laptop running the wpilib software.

You can take this a step further by running Photon on a coprocessor. I do not have access to a supported pi currently, but I did get Photon working on a Pi Zero2W (not the zero 1 or 1w. there is not a Java 11 build compatible with that one). Note, this is not officially supported, but it does work with a 32 or 64 bit image. 

## Pi Install

Because Photon expects a non-wifi coprocessor, I ended up installing Photon Manually. 

- I started by flashing a legacy light image (32 or 64 bit). I set up ssh and the wifi and password to connect to my home network (but you could set it to connect to the XRP Accesspoint as well) in the raspberry pi imager. 

- Then, I connected the pi camera to the pi and booted it. 

- I found the ip address of the Pi using my router software, but you could use sniffing software to find it as well. 

- Using an SSH client, I connected to the Pi and ran the [Debian install commands from Photon's Docs](https://docs.photonvision.org/en/latest/docs/getting-started/installation/sw_install/other-coprocessors.html).
```Java
$ wget https://git.io/JJrEP -O install.sh
$ sudo chmod +x install.sh
$ sudo ./install.sh
$ sudo reboot now
```
- I updated the Photon install to the 2024 Beta 3 using winscp. The gui of winscp skipped the first step in Photon's update directions.

```Java
$ scp [jar name].jar [user]@photonvision.local:~/
$ ssh [user]@photonvision.local
$ sudo mv [jar name].jar /opt/photonvision/photonvision.jar
$ sudo systemctl restart photonvision.service
```