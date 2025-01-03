# Hailo TAPPAS 

Rdference: Hailo TAPPAS - Optimized Execution of Video-Processing Pipelines [[Github]](https://github.com/hailo-ai/tappas)

<img src="https://github.com/user-attachments/assets/f3a46cdd-cf2e-44be-9475-f936050f4002" width=450>

---
## Overview
* TAPPAS is Hailo's set of **full application examples**, implementing pipeline elements and pre-trained AI tasks.
* Demonstrating Hailo's system integration scenario of specific use cases on predefined systems (software and Hardware platforms).
* It can be used for evaluations, reference code and demos:
    * Accelerating time to market by reducing development time and deployment effort
    * Simplifying integration with Hailo’s runtime SW stack
    * Providing a starting point for customers to fine-tune their applications

---
<img src="https://github.com/user-attachments/assets/6652d300-4d99-4d98-a189-24e3ee471bfd" width=800>

---
## How to Set Up Raspberry Pi 5 and Hailo
* https://github.com/hailo-ai/hailo-rpi5-examples/blob/main/doc/install-raspberry-pi5.md
     
---
## Install Tapps
Reference: https://wiki.seeedstudio.com/benchmark_of_multistream_inference_on_raspberrypi5_with_hailo8/

---
### Install necessary libs

```
$ sudo apt-get install -y rsync ffmpeg x11-utils python3-dev python3-pip python3-setuptools python3-virtualenv python-gi-dev libgirepository1.0-dev gcc-12 g++-12 cmake git libzmq3-dev
$ sudo apt-get install -y libopencv-dev python3-opencv
$ sudo apt-get install -y libcairo2-dev libgirepository1.0-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio gcc-12 g++-12 python-gi-dev
$ sudo apt install python3-gi python3-gi-cairo gir1.2-gtk-3.0
```

If got the error message, try 'apt --fix-broken install' with no packages (or specify a solution).
```
$ sudo apt --fix-broken install
```

---
#### Set hailo_pci
1. Set hailo_pci force_desc_page_size
```
$ sudo vim /etc/modprobe.d/hailo_pci.conf
```
2. Adding the following content into "hailo_pci.conf"
```
options hailo_pci force_desc_page_size=4096
```
3. And then reboot the raspberrypi5
```
$ sudo reboot
```

---
### Download and install Tappas
```
$ git clone --depth 1 https://github.com/hailo-ai/tappas.git
```

#### 1. Download hailort to tapps
```
$ cd tappas
$ mkdir hailort
$ git clone https://github.com/hailo-ai/hailort.git hailort/sources
```
 
#### 2. Modify common.py and add rpi5 platform class
```
$ cd <tappas>
$ vim downloader/common.py
```
And change the content like below, add RaspberryPI5 = 'rpi5'in common.py:
```
class Platform(Enum):
    X86 = 'x86'
    ARM = 'arm'
    IMX8 = 'imx8'
    Rockchip = 'rockchip'
    RaspberryPI = 'rpi'
    RaspberryPI5 = 'rpi5'
    
    ANY = 'any'

    def __str__(self):
        return self.value
```
#### 3. Install tappas
```
$ cd ./tappas
$ ./install.sh --skip-hailort --target-platform rpi5
```

The log message will be:
```
Found ninja-1.10.2.git.kitware.jobserver-1 at /home/demo/hailo/tappas/hailo_tappas_venv/bin/ninja
ninja: Entering directory `build.release'                                                           
[34/124] Compiling C++ object plugins/libgsthailopython.so.p/python_hailopython_infra.cpp.o
...
Tappas was successfully installed.
    To start using it please set required environment variables, by running:
    source /home/demo/.hailo/tappas/tappas_env
```


