# Raspberry Pi 5 and Hailo 8L

---
## Prepare Hardware
<img src="https://github.com/user-attachments/assets/8c251980-c6b1-4653-8229-52147943389e" width=600>

---
## Install AI kit on RPi5

Install AI kit on RPi5
* https://www.raspberrypi.com/documentation/accessories/ai-kit.html
     
The Raspberry Pi AI Kit bundles the Raspberry Pi M.2 HAT+ with a Hailo AI acceleration module for use with Raspberry Pi 5. The kit contains the following:
* Hailo AI module containing a Neural Processing Unit (NPU)
* Raspberry Pi M.2 HAT+, to connect the AI module to your Raspberry Pi 5
* thermal pad pre-fitted between the module and the M.2 HAT+
* mounting hardware kit
* 16mm stacking GPIO header

<img src="https://github.com/user-attachments/assets/55673538-d651-4ae7-afd6-07d2f5588eef" width=450>

---
## Prepare software

### Update the system
```
sudo date -s "$(wget -qSO- --max-redirect=0 google.com 2>&1 | grep Date: | cut -d' ' -f5-8)Z"
sudo apt update
sudo apt full-upgrade
```

---
### Download hailo software on hailo office web
* Note: you need an official Hailo account and ensure you are logged in. Click this link download the necessary libs as follows:
* Get Hailo’s Software Downloads and Documentation, Sign in / Sign up is required
     * https://community.hailo.ai/

#### Download packages
* HailoRT – PCIe driver Ubuntu package (deb): 4.19.0, September 30, 2024	
* HailoRT – Python package (whl) for Python 3.11, aarch64: 4.19.0, September 30, 2024	
* HailoRT – Ubuntu package (deb) for arm64: 4.19.0, September 30, 2024	

#### Installation guide
* HailoRT v4.19.0
     * https://hailo.ai/developer-zone/documentation/hailort-v4-19-0/?sp_referrer=install/install.html#ubuntu-installer-requirements

---
<img src="https://github.com/user-attachments/assets/da5251f8-446b-4375-89e4-f880c2ee7bd1" width=400>

---
<img src="https://github.com/user-attachments/assets/db65c4bc-0dd3-41eb-8878-374aa53c0df1" width=800>

---
<img src="https://github.com/user-attachments/assets/1f5dc008-6eda-4289-ad0d-5339f2e99fb8" width=800>

---
### Install hailort_4.19.0_arm64.deb on respberrypi5
```
sudo dpkg -i hailort_4.19.0_arm64.deb 
sudo reboot
```
---
### Install dkms
* DKMS is a framework that facilitates the building and installation of kernel modules
* Add kernel modules with DKMS [[Github]](https://github.com/clearlinux/clear-linux-documentation/blob/master/source/guides/kernel/kernel-modules-dkms.rst)
```
sudo apt-get install dkms
```

Expected log message:
```
/etc/kernel/header_postinst.d/dkms:
dkms: running auto installation service for kernel 6.1.0-28-arm64.
dkms: autoinstall for kernel: 6.1.0-28-arm64.
Setting up linux-headers-arm64 (6.1.119-1) ...
```

---
### Install hailort-pcie-driver_4.19.0_all.deb
```
sudo dpkg -i hailort-pcie-driver_4.19.0_all.deb 
sudo reboot
```

Expected log message:
```
demo@rpi5:~/hailo$ sudo dpkg -i hailort-pcie-driver_4.19.0_all.deb 
Selecting previously unselected package hailort-pcie-driver.
Preparing to unpack hailort-pcie-driver_4.19.0_all.deb ...
Unpacking hailort-pcie-driver (4.19.0) ...
Setting up hailort-pcie-driver (4.19.0) ...
build-essential/stable,now 12.9 arm64 [installed]
Do you wish to use DKMS? [Y/n]: 
Please reboot your computer for the installation to take effect.
```

---
### Create and activate a Python virtual environment
```
python -m venv hailo_env
source hailo_env/bin/activate
```
### Install hailort-4.19.0-cp311-cp311-linux_aarch64.whl
```
pip install hailort-4.19.0-cp311-cp311-linux_aarch64.whl 
```
### Check if the software is installed.
```
hailortcli fw-control identify
```

Expected log message:
```
Executing on device: 0000:01:00.0
Identifying board
Control Protocol Version: 2
Firmware Version: 4.19.0 (release,app,extended context switch buffer)
Logger Version: 0
Board Name: Hailo-8
Device Architecture: HAILO8L
Serial Number: HLDDLBB243900626
Part Number: HM21LB1C2LAE
Product Name: HAILO-8L AI ACC M.2 B+M KEY MODULE EXT TMP
```

### Set pcie to gen2/gen3(gen3 is faster than gen2):
* Add following text to /boot/firmware/config.txt
* note: If you want to use gen2,please comment dtparam=pciex1_gen=3
```
# Enable the PCIe external connector
dtparam=pciex1
# Force Gen 3.0 speeds
dtparam=pciex1_gen=3
```
### Install Tapps
* Install necessary libs
```
sudo apt-get install -y rsync ffmpeg x11-utils python3-dev python3-pip python3-setuptools python3-virtualenv python-gi-dev libgirepository1.0-dev gcc-12 g++-12 cmake git libzmq3-dev
sudo apt-get install -y libopencv-dev python3-opencv
sudo apt-get install -y libcairo2-dev libgirepository1.0-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio gcc-12 g++-12 python-gi-dev
sudo apt install python3-gi python3-gi-cairo gir1.2-gtk-3.0
```

#### Set hailo_pci force_desc_page_size
```
sudo nano /etc/modprobe.d/hailo_pci.conf
```
#### And then input the following content.
```
options hailo_pci force_desc_page_size=4096
```
* Finally, press Ctrl+X, type Y, and press Enter to save the file

#### And then reboot the raspberrypi5
```
sudo reboot
```
#### Download Tapps
```
git clone --depth 1 https://github.com/hailo-ai/tappas.git
```
#### Download hailort to tapps
```
cd tappas
mkdir hailort
git clone https://github.com/hailo-ai/hailort.git hailort/sources
```
#### Change common.py
```
nano downloader/common.py
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
./install.sh --skip-hailort --target-platform rpi5
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

#### change batch size to 8
```
cd ./apps/h8/gstreamer/general/multistream_detection/
nano multi_stream_detection.sh
```

#### Add readonly DEFAULT_BATCH_SIZE=8 to the 14 line as follows:
```
readonly DEFAULT_NETWORK_NAME="yolov5"
readonly DEFAULT_BATCH_SIZE=8
readonly MAX_NUM_OF_DEVICES=4
```
#### Add batch_size=$DEFAULT_BATCH_SIZE to the 19 line as follows:
```
network_name=$DEFAULT_NETWORK_NAME
batch_size=$DEFAULT_BATCH_SIZE
num_of_src=12
```
#### Add batch-size=$batch_size to the 154 line as follows:
```
queue name=hailo_pre_infer_q_0 leaky=no max-size-buffers=30 max-size-bytes=0 max-size-time=0 ! \
hailonet hef-path=$hef_path batch-size=$batch_size device-count=$device_count scheduling-algorithm=0 nms-score-threshold=0.3 nms-iou-threshold=0.45 output-format-type=HAILO_FORMAT_TYPE_FLOAT32 ! \
queue name=hailo_postprocess0 leaky=no max-size-buffers=30 max-size-bytes=0 max-size-time=0 ! \
```
* Finally Ctrl+X and input Y to save the file.


---
## Run multistream inference
```
cd tappas/apps/h8/gstreamer/general/multistream_detection
sudo chmod +x multi_stream_detection.sh
./multi_stream_detection.sh --network yolov8 --num-of-sources 8 --show-fps
```

### Check PCIe interface
```
lspci
0000:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0000:01:00.0 Co-processor: Hailo Technologies Ltd. Hailo-8 AI Processor (rev 01)
0001:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0001:01:00.0 Ethernet controller: Raspberry Pi Ltd RP1 PCIe 2.0 South Bridge

```


---
## Resource

<img src="https://github.com/user-attachments/assets/e4333ba6-222d-4a44-b167-2a43a7617929" width=600>

---

* GitHub: Hailo Raspberry Pi 5 Examples
    * https://github.com/hailo-ai/hailo-rpi5-examples
* Hailo RPi5 Basic Pipelines
  * https://github.com/hailo-ai/hailo-rpi5-examples/blob/main/doc/basic-pipelines.md#pose-estimation-example
* Benchmark of Multistream Inference on Raspberrypi 5 with Hailo8
    * WIKI: https://wiki.seeedstudio.com/benchmark_of_multistream_inference_on_raspberrypi5_with_hailo8
    * Youtube: https://www.youtube.com/watch?v=CHxg7qWTMYw
* Raspberry Pi:Install AI kit on RPi5  
    * https://www.raspberrypi.com/documentation/accessories/ai-kit.html
 
