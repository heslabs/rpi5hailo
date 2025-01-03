# Install AI kit on RPi5

* AI Kit and AI HAT+ software
    * https://www.raspberrypi.com/documentation/computers/ai.html
* Benchmark of Multistream Inference on Raspberrypi 5 with Hailo8  
  * https://wiki.seeedstudio.com/benchmark_of_multistream_inference_on_raspberrypi5_with_hailo8
    
---
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
---
<img src="https://github.com/user-attachments/assets/da5251f8-446b-4375-89e4-f880c2ee7bd1" width=400>

---
<img src="https://github.com/user-attachments/assets/db65c4bc-0dd3-41eb-8878-374aa53c0df1" width=800>

---
<img src="https://github.com/user-attachments/assets/1f5dc008-6eda-4289-ad0d-5339f2e99fb8" width=800>

---
#### Installation guide
* HailoRT v4.19.0
     * https://hailo.ai/developer-zone/documentation/hailort-v4-19-0/?sp_referrer=install/install.html#ubuntu-installer-requirements

---
#### Download packages
 
| HailoRT Package | Version | Date | File |
|:-|:-:|:-:|:-|
| PCIe driver Ubuntu package (deb) | 4.19.0 | September 30, 2024 | hailort-pcie-driver_4.19.0_all.deb |
| Ubuntu package (deb) for arm64 | 4.19.0 | September 30, 2024 | hailort_4.19.0_arm64.deb |
| Python package (whl) for Python 3.11, aarch64 | 4.19.0 | September 30, 2024 | hailort-4.19.0-cp311-cp311-linux_aarch64.whl |

---
### 1. Install Ubuntu package (deb) for arm64
File: hailort_4.19.0_arm64.deb
```
$ sudo dpkg -i hailort_4.19.0_arm64.deb 
$ sudo reboot
```
The log message will be:
```
Setting up hailort (4.19.0) ...
Do you wish to activate hailort service? (required for most pyHailoRT use cases) [y/N]: y
Starting hailort.service
Created symlink /etc/systemd/system/multi-user.target.wants/hailort.service → /lib/systemd/system/hailort.service.
```

---
### 2. Install dkms
* DKMS is a framework that facilitates the building and installation of kernel modules
* Add kernel modules with DKMS [[Github]](https://github.com/clearlinux/clear-linux-documentation/blob/master/source/guides/kernel/kernel-modules-dkms.rst)
```
$ sudo apt-get install dkms
```

The log message will be:
```
/etc/kernel/header_postinst.d/dkms:
dkms: running auto installation service for kernel 6.1.0-28-arm64.
dkms: autoinstall for kernel: 6.1.0-28-arm64.
Setting up linux-headers-arm64 (6.1.119-1) ...
```

---
### 3. Install hailort-pcie-driver_4.19.0_all.deb
```
$ sudo dpkg -i hailort-pcie-driver_4.19.0_all.deb 
$ sudo reboot
```

The log message will be:
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
### 4. Install Python package (whl) for Python 3.11

#### Create and activate a Python virtual environment
```
$ cd ~/hailo
$ python -m venv hailo_env
$ source hailo_env/bin/activate
```

#### Install Python package (whl) for Python 3.11 and aarch64 
Downloaded File: hailort-4.19.0-cp311-cp311-linux_aarch64.whl
```
$ pip install hailort-4.19.0-cp311-cp311-linux_aarch64.whl
```
The log message will be:
```
Successfully installed argcomplete-3.5.3 contextlib2-21.6.0 future-1.0.0 hailort-4.19.0 netaddr-1.3.0 netifaces-0.11.0 numpy-1.26.4 verboselogs-1.7
```


#### Check if the software is installed.
```
$ hailortcli fw-control identify
```

The log message will be:
Device Architectur: **HAILO-8L**
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

---
### Set pcie to gen2/gen3(gen3 is faster than gen2):
* Add following text to /boot/firmware/config.txt
* If you want to use gen2, please comment **"dtparam=pciex1_gen=3"**
```
# Enable the PCIe external connector
dtparam=pciex1
# Force Gen 3.0 speeds
dtparam=pciex1_gen=3
```

---
### Check PCIe interface
```
$ lspci
```
The log message will be: RPI5 with **SDCard** and Haili8L
```
0000:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0000:01:00.0 Co-processor: Hailo Technologies Ltd. Hailo-8 AI Processor (rev 01)
0001:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0001:01:00.0 Ethernet controller: Raspberry Pi Ltd RP1 PCIe 2.0 South Bridge
```

The log message will be:: RPI5 with **SSD** and Haili8L
```
0000:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0000:01:00.0 PCI bridge: ASMedia Technology Inc. ASM1182e 2-Port PCIe x1 Gen2 Packet Switch
0000:02:03.0 PCI bridge: ASMedia Technology Inc. ASM1182e 2-Port PCIe x1 Gen2 Packet Switch
0000:02:07.0 PCI bridge: ASMedia Technology Inc. ASM1182e 2-Port PCIe x1 Gen2 Packet Switch
0000:03:00.0 Non-Volatile memory controller: Shenzhen Longsys Electronics Co., Ltd. FORESEE XP1000 / Lexar Professional CFexpress Type B Gold series, NM620 PCIe NVME SSD... (rev 01)
0000:04:00.0 Co-processor: Hailo Technologies Ltd. Hailo-8 AI Processor (rev 01)
0001:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0001:01:00.0 Ethernet controller: Raspberry Pi Ltd RP1 PCIe 2.0 South Bridge
```

---
## Troubleshooting

---
### dpkg: error processing archive hailort-pcie-driver_4.19.0_all.deb


```
sudo dpkg -i hailort-pcie-driver_4.19.0_all.deb 
(Reading database ... 262329 files and directories currently installed.)
Preparing to unpack hailort-pcie-driver_4.19.0_all.deb ...
Could not test for SecureBoot, assuming SecureBoot is disabled on this machine.
Unpacking hailort-pcie-driver (4.19.0) ...
dpkg: error processing archive hailort-pcie-driver_4.19.0_all.deb (--install):
 trying to overwrite '/lib/firmware/hailo/hailo8_fw.4.19.0.bin', which is also in package hailofw 4.19.0-2
Errors were encountered while processing:
 hailort-pcie-driver_4.19.0_all.deb
```

Solution: 
```
$ cat /var/log/hailort-pcie-driver.deb.log
...
Could not test for SecureBoot, assuming SecureBoot is disabled on this machine.
######### Fri Jan  3 06:50:37 PM CST 2025 #########
```

```
sudo dpkg ­­--purge --force-all hailort-­pcie-­driver
```

