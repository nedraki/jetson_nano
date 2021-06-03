## Jetson Nano

![Jetson Nano](./assets/jetson.png "Jetson Nano")

![Legend](./assets/legend.png "Jetson Nano ports")


### Quick Start

_NVIDIA® Jetson Nano™ Developer Kit is a small, powerful computer that lets you run multiple neural networks in parallel for applications like image classification, object detection, segmentation, and speech processing._

The main source of information for getting hands on is the official website of Nvidia Developer, this document is meant to give you easy access to the official documentation.

[Getting Started with Jetson Nano 2GB Developer Kit
](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-2gb-devkit)

***What do you need:***

- Nvidia Jetson Nano
- MicroSD card 32 Gb (64 Gb or more recommended)
- HDMI Display
- USB Keyboard and mouse
- USB-C power supply (5V⎓3A) (The charger of some smartphones comply with this specs)

- To prepare your microSD card, you’ll need a computer with Internet connection and the ability to read and write SD cards, either via a built-in SD card slot or adapter.

*Note:* You can also interact with your Jetson Nano via terminal (Headless Mode) from another computer, in that case, the USB Keyboard, mouse and HDMI dispaly are not necesary.

⚠️ To avoid damage, always place your Jetson Nano on a non-conductive surface.

### Write Image to the microSD Card

Intructions available for different operative systems (OS). 

- [Write Image to the microSD Card](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-2gb-devkit#prepare)

_It might take more than 10 minutes to write the image to the microSD card, take a break and come back later._

### Setup and First Boot

[Setup and First Boot](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-2gb-devkit#setup)

### SSH Connection

Once you have log-in locally on Jetson Nano, you can establish a SSH connection from another computer.

From another computer in thesame network:

`ifconfig`
Look for he IP address with the tag `inet` related to your connection

Ouput example:
`wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet XXX.X.XX  netmask XXX.XXX.XXX.X  broadcast XXX.XXX.X.XXX
        inet6 ...<`

### Virtual Network Computing

_VNC (Virtual Network Computing) enables you to control your Jetson developer kit from another computer on the same network, by viewing and interacting with the desktop of the developer kit from the other computer._

In a few works, you can get remote access to your Jetson nano

[Remote Control](https://developer.nvidia.com/embedded/learn/tutorials/vnc-setup)

## Time to code

[Tutorials Rsources](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-2gb-devkit#next)

### Your First Jetson Container

_A container is an executable unit of software where an application and its run time dependencies can all be packaged together into one entity. Since everything needed by the application is packaged with the application itself, containers provide a degree of isolation from the host and make it easy to deploy and install the application without having to worry about the host environment and application dependencies._

- [Containers](https://developer.nvidia.com/embedded/learn/tutorials/jetson-container)
- [AI-track Docker](link to ai track)

## Jetson AI Fundamentals Course


 
