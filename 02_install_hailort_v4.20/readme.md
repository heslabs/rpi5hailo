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
