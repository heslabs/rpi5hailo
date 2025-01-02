# Raspberry Pi Camera
* https://www.raspberrypi.com/documentation/computers/camera_software.html
* Picamera2 Python library [[PDF]](https://datasheets.raspberrypi.com/camera/picamera2-manual.pdf)
  
---
## Install a Raspberry Pi camera
https://www.raspberrypi.com/documentation/accessories/camera.html#install-a-raspberry-pi-camera

---
## Picamera2 Python library
Picamera2 Python library [[PDF]](https://datasheets.raspberrypi.com/camera/picamera2-manual.pdf)

* Picamera2 is a Python library that gives convenient access to the camera system of the Raspberry Pi.
* It is designed for cameras connected with the flat ribbon cable directly to the connector on the Raspberry Pi itself, and not for other types of camera, although there is some limited support for USB cameras.
* Picamera2 is built on top of the open source libcamera project, which provides support for complex camera systems in
Linux.
Picamera2 directly uses the Python bindings supplied by libcamera, although the Picamera2 API provides access
at a higher level.

<img src="https://github.com/user-attachments/assets/dce40d92-bb71-4135-bcda-cb75d9286b25" width=350>

---
###  Installation and updating

```
$ sudo apt install -y python3-picamera2
```

```
python3-picamera2 is already the newest version (0.3.23-1).
The following packages were automatically installed and are no longer required:
  chromium-browser chromium-browser-l10n chromium-codecs-ffmpeg-extra edid-decode libcamera0.2
  libraspberrypi0 libwpe-1.0-1 libwpebackend-fdo-1.0-1 linux-headers-6.1.0-rpi7-common-rpi
  linux-headers-6.1.0-rpi8-common-rpi
```

---
## Raspberry Pi - Camera software

* Raspberry Pi OS Bullseye and later images by default run the libcamera camera stack, which is required for Picamera2.
* You can check that libcamera is working by opening a command window and typing:
```
rpicam-hello
```
* Error message
```
Made X/EGL preview window
ERROR: *** no cameras available ***
```
* Error message
```
[0:55:55.693937356] [71164]  INFO Camera camera_manager.cpp:325 libcamera v0.3.2+99-1230f78d
libEGL warning: DRI3: failed to query the version
libEGL warning: DRI2: failed to authenticate
X Error of failed request:  BadRequest (invalid request code or no such operation)
  Major opcode of failed request:  155 ()
  Minor opcode of failed request:  1
  Serial number of failed request:  16
  Current serial number in output stream:  16
```

---
## Sony IMX500: AI Camera
https://www.raspberrypi.com/documentation/accessories/ai-camera.html#ai-camera
  
Install the IMX500 firmware
The AI camera must download runtime firmware onto the IMX500 sensor during startup. To install these firmware files onto your Raspberry Pi, run the following command:
```
$ sudo apt install imx500-all
```

<img src="https://github.com/user-attachments/assets/71f11c03-e0f2-47c7-9db3-68543fa94102" width=550>


---
### Increasing the amount of available CMA memory.
* The default CMA size on Pi devices is: 256MB if the total system memory is less than or equal to 1GB, otherwise 320MB.
* CMA memory is still available to the system when "regular" memory starts to run low, so increasing its size does not normally starve the rest of the operating system.
* As a rule of thumb, all systems should usually be able to increase the size to 320MB if they are experiencing problems; 1GB systems could probably go to 384MB and 2GB or larger systems could go as far as 512MB.
* But you may find that different limits work best on your own systems, and some experimentation may be necessary.
* To change the size of the CMA area, you will need edit the /boot/config.txt file. Find the line that says dtoverlay=vc4-kmsv3d and replace it with:
```
dtoverlay=vc4-kms-v3d,cma-320 for 320MB
dtoverlay=vc4-kms-v3d,cma-384 for 384MB 
dtoverlay=vc4-kms-v3d,cma-512 for 512MB
```
