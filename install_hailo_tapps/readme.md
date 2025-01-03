---
## Install Tapps
* https://wiki.seeedstudio.com/benchmark_of_multistream_inference_on_raspberrypi5_with_hailo8/
* Install necessary libs
```
$ sudo apt-get install -y rsync ffmpeg x11-utils python3-dev python3-pip python3-setuptools python3-virtualenv python-gi-dev libgirepository1.0-dev gcc-12 g++-12 cmake git libzmq3-dev
$ sudo apt-get install -y libopencv-dev python3-opencv
$ sudo apt-get install -y libcairo2-dev libgirepository1.0-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio gcc-12 g++-12 python-gi-dev
$ sudo apt install python3-gi python3-gi-cairo gir1.2-gtk-3.0
```

#### Set hailo_pci force_desc_page_size
```
$ sudo nano /etc/modprobe.d/hailo_pci.conf
```
#### And then input the following content.
```
options hailo_pci force_desc_page_size=4096
```
* Finally, press Ctrl+X, type Y, and press Enter to save the file

#### And then reboot the raspberrypi5
```
$ sudo reboot
```
#### Download Tapps
```
$ git clone --depth 1 https://github.com/hailo-ai/tappas.git
```
#### Download hailort to tapps
```
$ cd tappas
$ mkdir hailort
$ git clone https://github.com/hailo-ai/hailort.git hailort/sources
```
#### Change common.py
```
$ nano downloader/common.py
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
#### Install tappas
```
$ ./install.sh --skip-hailort --target-platform rpi5
```

Expected log message:
```
Found ninja-1.10.2.git.kitware.jobserver-1 at /home/demo/hailo/tappas/hailo_tappas_venv/bin/ninja
ninja: Entering directory `build.release'                                                           
[34/124] Compiling C++ object plugins/libgsthailopython.so.p/python_hailopython_infra.cpp.o
...
Tappas was successfully installed.
    To start using it please set required environment variables, by running:
    source /home/demo/.hailo/tappas/tappas_env
```
### Check PCIe interface
```
$ lspci
```
Expected log message:
```
0000:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0000:01:00.0 Co-processor: Hailo Technologies Ltd. Hailo-8 AI Processor (rev 01)
0001:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0001:01:00.0 Ethernet controller: Raspberry Pi Ltd RP1 PCIe 2.0 South Bridge
```
