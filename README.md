# Raspberry Pi 5 with M.2 Hailo AI Processor

---
## RPi5 AI kit Overview

The Raspberry Pi AI Kit bundles the Raspberry Pi M.2 HAT+ with a Hailo AI acceleration module for use with Raspberry Pi 5. The kit contains the following:
* Hailo AI module containing a Neural Processing Unit (NPU)
* Raspberry Pi M.2 HAT+, to connect the AI module to your Raspberry Pi 5
* thermal pad pre-fitted between the module and the M.2 HAT+
* mounting hardware kit
* 16mm stacking GPIO header

<img src="https://github.com/user-attachments/assets/55673538-d651-4ae7-afd6-07d2f5588eef" width=300>
<img src="https://github.com/user-attachments/assets/e4333ba6-222d-4a44-b167-2a43a7617929" width=450>



---
## Install the dependencies required to use the NPU. Run the following command from a terminal window:
```
$ sudo apt install hailo-all
$ sudo apt remove hailo-all
```
This installs the following dependencies:
* Hailo kernel device driver and firmware
* HailoRT middleware software
* Hailo Tappas core post-processing libraries
* The rpicam-apps Hailo post-processing software demo stages



---
## Validate device
```
$ hailortcli scan
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
### Check PCIe interface - Hailo-8 AI Processor
```
$ lspci
0000:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0000:01:00.0 Co-processor: Hailo Technologies Ltd. Hailo-8 AI Processor (rev 01)
0001:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0001:01:00.0 Ethernet controller: Raspberry Pi Ltd RP1 PCIe 2.0 South Bridge
```


---
## Hailo RPi5 Examples
https://github.com/hailo-ai/hailo-rpi5-examples

* Clone the repository and navigate to the repository directory:
* Run the following script for quick installation
```
$ git clone https://github.com/hailo-ai/hailo-rpi5-examples.git
$ cd hailo-rpi5-examples
$ ./install.sh
```

---
### Detection Example:
This example demonstrates object detection using the **YOLOv8s** model for Hailo-8L (13 TOPS) and the **YOLOv8m** model for Hailo-8 (26 TOPS) by default. It also supports all models compiled with HailoRT NMS post process. Hailo's Non-Maximum Suppression (NMS) layer is integrated into the HEF file, allowing any detection network compiled with NMS to function with the same codebase.

####  Run the Example:
* Opening a new terminal session and sourced the environment setup script
* Run the detection example using Python script
* To close the application, press Ctrl+C.
```
$ source setup_env.sh
$ python basic_pipelines/detection.py
```
* Using USB camera input: Detect the available camera using this script:
* Run example using USB camera - Use the device found by the previous script:
* For additional options, execute command with help option:
```
$ python basic_pipelines/get_usb_camera.py
$ python basic_pipelines/detection.py --input /dev/video<X>
$ python basic_pipelines/detection.py --help
```
* Example
```
$ python basic_pipelines/get_usb_camera.py
USB cameras found on: /dev/video0
$ python basic_pipelines/detection.py --input /dev/video0
```

---
<img src="https://github.com/user-attachments/assets/302bc752-8eaf-4949-9307-cd2eee852d6a" width=450>


---
### Pose Estimation Example
This example demonstrates human pose estimation using the yolov8s_pose model for Hailo-8 Lite (H8l) and the yolov8m_pose model for Hailo-8 (H8)

#### To Run the Example:
* Opening a new terminal session andsourced the environment setup script
* Run the example using Python script
* To close the application, press Ctrl+C
* For additional options, execute command with --help option
```
$ source setup_env.sh
$ python basic_pipelines/pose_estimation.py
```
* Run example using Pi camera
```
$ python basic_pipelines/pose_estimation.py --input rpi
$ python basic_pipelines/pose_estimation.py --help
```

---
<img src="https://github.com/user-attachments/assets/2f5edc26-8755-4cac-be16-02550d535664" width=450>

---
### Instance Segmentation Example
This example demonstrates instance segmentation using the yolov5n_seg model for Hailo-8 Lite (H8l) and the yolov5m_seg model for Hailo-8 (H8).
* Opening a new terminal session andsourced the environment setup script
* Run the example using Python script
* To close the application, press Ctrl+C
* For additional options, execute command with --help option
```
$ source setup_env.sh
$ python basic_pipelines/instance_segmentation.py
$ python basic_pipelines/instance_segmentation.py --help
```

---
<img src="https://github.com/user-attachments/assets/bf88d093-2b67-4215-8b3e-f07afd2d074a" width=450>

---
<img src="https://github.com/user-attachments/assets/949b412f-0974-4877-886e-9408dd305951" width=450>

---
## Resource

* Raspberry Pi hardware - Introduction
  * https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#introduction 
* Raspberry Pi 5 uses PCIe hat/dual hat
  * https://wiki.seeedstudio.com/raspberry_pi_5_uses_pcie_hat_dual_hat/
* Raspberry Pi - AI Kit and AI HAT+ software
  * https://www.raspberrypi.com/documentation/computers/ai.html
* Install Hailo Software & Verify Installation
  * https://wiki.seeedstudio.com/clip_application_on_rpi5_with_ai_kit/
* Hailo’s Software Downloads and Documentation
  * https://community.hailo.ai
* HailoRT v4.19.0 - Installing HailoRT on Ubuntu
  * https://hailo.ai/developer-zone/documentation/hailort-v4-19-0/?sp_referrer=install/install.html#installation-on-ubuntu
* HailoRT v4.20.0 documentation
  * https://hailo.ai/developer-zone/documentation/hailort-v4-20-0
* Hailo TAPPAS - Optimized Execution of Video-Processing Pipelines: 
  * https://github.com/hailo-ai/tappas
* Hailo Raspberry Pi5 Examples
  * https://github.com/hailo-ai/hailo-rpi5-examples
* Hailo RPi5 Basic Pipelines
  * https://github.com/hailo-ai/hailo-rpi5-examples/blob/main/doc/basic-pipelines.md
* Benchmark of Multistream Inference on Raspberrypi 5 with Hailo8
  * https://wiki.seeedstudio.com/benchmark_of_multistream_inference_on_raspberrypi5_with_hailo8
  * https://www.youtube.com/watch?v=CHxg7qWTMYw
* YOLOv8 - Ultralytics
  * https://docs.ultralytics.com/models/yolov8
* Testing Raspberry Pi's AI Kit - 13 TOPS for $70 (2024.07)
  * https://www.jeffgeerling.com/blog/2024/testing-raspberry-pis-ai-kit-13-tops-70)

