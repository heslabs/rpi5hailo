# Hailo RPi5 Basic Pipelines
Source: [[Hailo-AI-GitHub]](https://github.com/hailo-ai/hailo-rpi5-examples)
 
* Clone the repository and navigate to the repository directory:
* Run the following script for quick installation
```
$ git clone https://github.com/hailo-ai/hailo-rpi5-examples.git
$ cd hailo-rpi5-examples
$ ./install.sh
```

---
## Detection Example:
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
## Pose Estimation Example
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
## Instance Segmentation Example
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
## Troubleshooting

---
#### meson: command not found
```
$ cd ~/hailo-rpi5-examples$
$ ./install.sh 
```
Error message:
```
./compile_postprocess.sh: line 19: meson: command not found
ninja: error: loading 'build.ninja': No such file or directory
ninja: error: loading 'build.ninja': No such file or directory
```

Solved:
```
$ sudo apt-cache search meson
gi-docgen - source code documentation tool using GObject-Introspection
meson - high-productivity build system
elpa-meson-mode - Major mode for the Meson build system files
python3-mesonpy - Meson PEP 517 Python build backend
muon-meson - Meson implementation in C
```

```
$ sudo apt install meson
Setting up ninja-build (1.11.1-2~deb12u1) ...
Setting up meson (1.0.1-5) ...
```


---
#### Dependency "hailo_tappas" not found
Run-time dependency hailo-tappas-core found: NO (tried pkgconfig and cmake)
Run-time dependency hailo_tappas found: NO (tried pkgconfig and cmake)

../meson.build:13:4: ERROR: Dependency "hailo_tappas" not found, tried pkgconfig and cmake

