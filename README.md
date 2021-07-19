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

***Using USB cable***

1. Connect the Jetson Nano to your computer via USB
2. Connect via SSH:
2.1 `ssh nvidia@192.168.55.1`

The ip address `192.168.55.1` is by default the port for SSH connections via USB; for wireless connection, it is necesary to verify the wlan address asigned to the Jetson Nano.

`ifconfig`

Look for he IP address with the tag `inet` related to your connection

Ouput example:

`wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet XXX.X.XX  netmask XXX.XXX.XXX.X  broadcast XXX.XXX.X.XXX
        inet6 ...<`

***From another computer in the same network:***

`ifconfig`

Look for he IP address with the tag `inet` related to your connection

Ouput example:

`wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet XXX.X.XX  netmask XXX.XXX.XXX.X  broadcast XXX.XXX.X.XXX
        inet6 ...<`

Finally, you can connect remotely:

`ssh ` <your_user_name>@<your_ip_address>`

For example:

`ssh <name_of_your_jetson_nano>@192.168.1.16`

***See more details about how to stream video while using ssh***

- **From another computer on a different network:**

***TBD***


### Virtual Network Computing

_VNC (Virtual Network Computing) enables you to control your Jetson developer kit from another computer on the same network, by viewing and interacting with the desktop of the developer kit from the other computer._

In a few works, you can get remote access to your Jetson nano

[Remote Control](https://developer.nvidia.com/embedded/learn/tutorials/vnc-setup)

## Jetson AI Fundamentals Course

You can enroll on the Nvidia Deep Learning institute to follow the course:

- [Enroll in course](https://courses.nvidia.com/courses/course-v1:DLI+S-RX-02+V2/about)

The system will ask you to create an Nvidia developer account and after signing in with your credentials you will have access to the course and tutorials to run several containers on your Jetson. 

***Getting to know the JetPack version of your hardware is important to install the right container:***

`dpkg-query --show nvidia-l4t-core`

Output example:

`nvidia-l4t-core	32.5.1-20210219084526`

This information is relevant to select the <tag> corresponding to the Docker container you need to run.

For example:

`docker run --runtime nvidia -it --rm --network host     --volume ~/nvdli-data:/nvdli-nano/data     --device /dev/video0     nvcr.io/nvidia/dli/dli-nano-ai:v2.0.1-r32.5.0`

_Note the `<tag>` `v2.0.1-r32.5.0` makes reference to the core version running on the Jetson._

- [Tutorials Resources](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-2gb-devkit#next)


 ### Your First Jetson Container

_A container is an executable unit of software where an application and its run time dependencies can all be packaged together into one entity. Since everything needed by the application is packaged with the application itself, containers provide a degree of isolation from the host and make it easy to deploy and install the application without having to worry about the host environment and application dependencies._

- [Containers](https://developer.nvidia.com/embedded/learn/tutorials/jetson-container)
- [AI-track Docker](link to ai track)

Container with initial notebooks

- Hello Camera
- Classification
- Regression 

`sudo docker run --runtime nvidia -it --rm --network host \
    --volume ~/nvdli-data:/nvdli-nano/data \
    --device /dev/video0 \ 
    nvcr.io/nvidia/dli/dli-nano-ai:v2.0.1-r32.4.4`


To know the network host (remote pc IP):

`hostname -I`

Example
`<network host> = 192.168.1.9`

***Tip***: The docker volume should be run with the tag that corresponds to your hardware

### Hello AI world setup in headless mode: 

[Jetson Inference repo](https://github.com/dusty-nv/jetson-inference)

#### Check video connection while using ssh (headles mode)

RTP network streams are broadcast to a particular host or multicast group over UDP/IP. When recieving an RTP stream, the codec must be specified (--input-codec), because RTP doesn't have the ability to dynamically query this. This will use RTP as input from another device:


[Streaming video in headless mode using RTP](https://github.com/dusty-nv/jetson-inference/blob/master/docs/aux-streaming.md)

- From the Jetson Inference container:
`video-viewer /dev/video0 rtp://<remote_pc_ip>:1234`

- From the computer connected for remote control

1. [Install GStreamer](https://gstreamer.freedesktop.org/documentation/installing/index.html?gi-language=c)

2. Initiate streming on Jetson device

`video-viewer /dev/video0 rtp://<remote_pc_ip>:1234`

3. Run pipeline on remote host (The pc connected to Jetson via ssh)

`sudo gst-launch-1.0 -v udpsrc port=1234 \
 caps = "application/x-rtp, media=(string)video, clock-rate=(int)90000, encoding-name=(string)H264, payload=(int)96" ! \
 rtph264depay ! decodebin ! videoconvert ! autovideosink`

It is also possible to stream and read the video output using VLC player but the latency will be higher than using GStreamer. For more details, [refere to the official docs](https://github.com/dusty-nv/jetson-inference/blob/master/docs/aux-streaming.md).

