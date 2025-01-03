# HailoRT v4.20.0

Reference: HailoRT v4.20.0 documentation
* https://hailo.ai/developer-zone/documentation/hailort-v4-20-0/

---
## Installation on Ubuntu
Reference: https://hailo.ai/developer-zone/documentation/hailort-v4-20-0/?sp_referrer=install/install.html#installation-on-ubuntu

The HailoRT Ubuntu offers several files, select the files according to your requirements:

* HailoRT PCIe driver and FW
    * HailoRT PCIe driver and FW - hailort-pcie-driver_<version>_all.deb
* HailoRT for the platform architecture
    * hailort_<version>_arm64.deb – HailoRT for arm64
* PyHailoRT for the the platform architecture and installed Python version
    * hailort-<version>-cp310-cp310-linux_aarch64.whl – PyHailoRT for python3.10, aarch64

---
### Download
* Download the relevant files for your environment from our Developer Zone.
    * https://hailo.ai/developer-zone/sw-downloads/

#### Select latest release
* Software Package: AI Software Suite
* Software Sub-Package: HailoRT
* Architecture: ARM64
* OS: Linux
* Python Version: 3.11

 
#### Release date: January 1, 2025

| Package name | version | Downlaoded File |
| :- | :-: | :- |
| HailoRT – PCIe driver Ubuntu package (deb) | 4.20.0 | hailort-pcie-driver_4.20.0_all   |
| HailoRT – Python package (whl) for Python 3.11, aarch64 | 4.20.0 | hailort-4.20.0-cp311-cp311-linux_aarch64.whl |
| HailoRT – Ubuntu package (deb) for arm64 | 4.20.0 | hailort_4.20.0_arm64.deb |

---
### Find machine’s architecture
To install HailoRT hailort_<version>_<arch>.deb is required. Information about machine’s architecture can be found using:

```
# .deb architecture
$ dpkg --print-architecture
arm64
```

---
### Find your python version
You can find your python version and architecture using:
```
# Python version major and minor digits
$ python -V | cut -d. -f1,2 | tr -dc '0-9.' | xargs
3.11
# .whl architecture
$ uname -m
aarch64
```

---
### Installation of the PCIe Driver 
Run the following command to install only the PCIe driver:
```
$ sudo dpkg --install hailort-pcie-driver_4.20.0_all.deb
```

---
### Installation HailoRT
```
$ sudo dpkg --install hailort_<version>_$(dpkg --print-architecture).deb
$ sudo dpkg --install hailort_4.20.0_arm64.deb
```
PC restart is required after driver installation.
  
### Validate device
After boot, you can use the hailortcli tool and run hailortcli scan to validate that the device is identified:
```
$ hailortcli scan
```
The log message will be:
```
Hailo Devices:
[-] Device: 0000:04:00.0
```
 
### Identifying Device’s Serial Number
Run the following command to obtain the serial number from the device:
```
$ hailortcli fw-control identify
```

The log message will be:
```
Executing on device: 0000:04:00.0
Identifying board
Control Protocol Version: 2
Firmware Version: 4.20.0 (release,app,extended context switch buffer)
Logger Version: 0
Board Name: Hailo-8
Device Architecture: HAILO8L
Serial Number: HLDDLBB243900626
Part Number: HM21LB1C2LAE
Product Name: HAILO-8L AI ACC M.2 B+M KEY MODULE EXT TMP
```

---
### Installation of pyHailoRT into a New Environment
Run the following command to install PyHailoRT into a new virtual environment:
```
$ virtualenv -p python<python_version> hailo_platform_venv && . hailo_platform_venv/bin/activate && pip install ./hailort-<version>-<python_tag>-<abi_tag>-<platform_tag>.whl
```
For example, for installing PyHailoRT v4.20.0 to a Python-3.11 environment on a x86_64 platform, the command would be:
```
$ virtualenv -p python3.11 hailo_platform_venv
$ source hailo_platform_venv/bin/activate && pip install ./hailort-4.20.0-cp311-cp311-linux_aarch64.whl
```
The log message will be:
```
Successfully installed argcomplete-3.5.3 contextlib2-21.6.0 future-1.0.0 hailort-4.20.0 netaddr-1.3.0 netifaces-0.11.0 numpy-1.26.4
```

---
### Installation of pyHailoRT into an Existing Environment
Run the following command to install PyHailoRT into existing virtual environment:
```
$ source <virtualenv>/bin/activate && pip install ./hailort-<version>-<python_tag>-<abi_tag>-<platform_tag>.whl
```
For example, for installing PyHailoRT v4.20.0 to a Python-3.11 environment on a x86_64 platform, the command would be:
```
$ cd ~/halio/hailort-4.20.0
$ source hailo_platform_venv/bin/activate && pip install ./hailort-4.20.0-cp311-cp311-linux_aarch64.whl
```
---
### Uninstalling HailoRT
Remove the PCIe driver:
```
sudo dpkg --purge hailort-pcie-driver
```

Remove HailoRT (excluding pyhailort):
```
sudo dpkg --purge hailort
```
Remove pyhailort (if installed):
```
source hailo_platform_venv/bin/activate
pip uninstall hailort
```

### hailo-rpi5-examples
```
$ cd ~/hailo-rpi5-example
$ source ../hailort_4.20.0/hailo_platform_venv/bin/activate
$ ./install.sh
$ source setup_env.sh
$ python basic_pipelines/detection.py
```

---
## Troubleshooting

---
### -lgsthailometa: No such file or directory
/usr/bin/ld: cannot find -lgsthailometa: No such file or directory
/usr/bin/ld: cannot find -lhailo_tracker: No such file or directory
/usr/bin/ld: cannot find -lhailo_gst_image: No such file or directory
/usr/bin/ld: cannot find -lhailo_cv_singleton: No such file or directory
collect2: error: ld returned 1 exit status
ninja: build stopped: subcommand failed.
