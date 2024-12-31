# Raspberry Pi 5 with M.2 Hailo AI Processor
 <img src="https://github.com/user-attachments/assets/e4333ba6-222d-4a44-b167-2a43a7617929" width=600>

---
## Prepare Hardware: Raspberry Pi 5 and Hailo 8L (13TOPS)
<img src="https://github.com/user-attachments/assets/658ef470-cad6-4972-abf2-48a6fd663730" width=330>

* Get Raspberry Pi AI Kit [[Github-Page]](https://github.com/heslabs/rpi5hailo/tree/main/rpi5_aikit)

---
## Install AI kit on RPi5
* Install AI kit on RPi5 [[Github-Page]](https://github.com/heslabs/rpi5hailo/tree/main/install_hailo)
  
### Installation guide
* HailoRT v4.19.0 [[Hailo-Developer-Zone]](https://hailo.ai/developer-zone/documentation/hailort-v4-19-0/?sp_referrer=install/install.html#ubuntu-installer-requirements)

### Download hailo software on hailo website
* Get Hailo’s Software Downloads and Documentation, Sign in / Sign up is required
     * https://community.hailo.ai/

#### Download packages
* HailoRT – PCIe driver Ubuntu package (deb): 4.19.0, September 30, 2024	
* HailoRT – Python package (whl) for Python 3.11, aarch64: 4.19.0, September 30, 2024	
* HailoRT – Ubuntu package (deb) for arm64: 4.19.0, September 30, 2024	



---
### Check PCIe interface - Hailo-8 AI Processor
```
lspci
0000:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0000:01:00.0 Co-processor: Hailo Technologies Ltd. Hailo-8 AI Processor (rev 01)
0001:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 21)
0001:01:00.0 Ethernet controller: Raspberry Pi Ltd RP1 PCIe 2.0 South Bridge
```

---
### Hailo RPi5 Basic Pipelines
[[Hailo-AI-GitHub]](https://github.com/hailo-ai/hailo-rpi5-examples)
 
* Clone the repository and navigate to the repository directory:
* Run the following script for quick installation
```
git clone https://github.com/hailo-ai/hailo-rpi5-examples.git
cd hailo-rpi5-examples
./install.sh
```

---
### Detection Example:
This example demonstrates object detection using the YOLOv8s model for Hailo-8L (13 TOPS) and the YOLOv8m model for Hailo-8 (26 TOPS) by default. It also supports all models compiled with HailoRT NMS post process. Hailo's Non-Maximum Suppression (NMS) layer is integrated into the HEF file, allowing any detection network compiled with NMS to function with the same codebase.

####  Run the Example:
* Opening a new terminal session and sourced the environment setup script
* Run the detection example using Python script
* To close the application, press Ctrl+C.
```
source setup_env.sh
python basic_pipelines/detection.py
```
* Using USB camera input: Detect the available camera using this script:
* Run example using USB camera - Use the device found by the previous script:
* For additional options, execute command with help option:
```
python basic_pipelines/get_usb_camera.py
python basic_pipelines/detection.py --input /dev/video<X>
python basic_pipelines/detection.py --help
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
source setup_env.sh
python basic_pipelines/pose_estimation.py
```
* Run example using Pi camera
```
python basic_pipelines/pose_estimation.py --input rpi
python basic_pipelines/pose_estimation.py --help
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
source setup_env.sh
python basic_pipelines/instance_segmentation.py
python basic_pipelines/instance_segmentation.py --help
```

---
<img src="https://github.com/user-attachments/assets/bf88d093-2b67-4215-8b3e-f07afd2d074a" width=450>


---
## Resource

* GitHub: Hailo Raspberry Pi 5 Examples [[Hailo-AI-Github]](https://github.com/hailo-ai/hailo-rpi5-examples)
* Hailo RPi5 Basic Pipelines [[Hailo-AI-Github]](https://github.com/hailo-ai/hailo-rpi5-examples/blob/main/doc/basic-pipelines.md)
* Benchmark of Multistream Inference on Raspberrypi 5 with Hailo8 [[SeeedStudio-WIKI]](https://wiki.seeedstudio.com/benchmark_of_multistream_inference_on_raspberrypi5_with_hailo8) [[Youtube]](https://www.youtube.com/watch?v=CHxg7qWTMYw)
* Raspberry Pi:Install AI kit on RPi5 [[RaspberryPi-Website]](https://www.raspberrypi.com/documentation/accessories/ai-kit.html)


