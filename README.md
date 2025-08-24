# rpi5hailo


```
Loign: soclabs@heswiki.com	
Password: heswiki12345@
```


---
### HailoRT’s documentation

* Welcome to HailoRT’s documentation!
    * https://hailo.ai/developer-zone/documentation/hailort-v4-22-0/

```

```


---
### Tutorials
* https://hailo.ai/developer-zone/documentation/hailort-v4-22-0/?sp_referrer=tutorials/tutorials.html

The tutorials below go through the inference steps in C, C++ and Python and are aimed to demonstrate HailoRT API usage. \
To download the tutorials, clone the tutorials from GitHub:
```
git clone https://github.com/hailo-ai/hailort.git
```

Run the download script to download the HEFs used by the tutorials:
```
## Ubuntu
cd hailort/hailort/scripts/ && ./download_hefs.sh && cd -
```

The C and C++ tutorials require HailoRT to be installed.

Note
* If running only C and C++ tutorials, PyHailoRT installation can be skipped.
* Python tutorials require HailoRT and PyHailoRT to be installed, and the additional following packages:
```
jupyter
matplotlib
```

* To install these packages, from the virtual environment PyHailoRT is installed into run:
```
pip install jupyter matplotlib
```

---
### Python Inference Tutorial - Single Model
* HailoRT v4.22.0
* https://hailo.ai/developer-zone/documentation/hailort-v4-22-0/?sp_referrer=tutorials_notebooks/notebooks/HRT_2_Infer_Pipeline_Inference_Tutorial.html


```
source hailo_virtualenv/bin/activate
```


---
### Compiling HailoRT from Sources

* https://hailo.ai/developer-zone/documentation/hailort-v4-22-0/?sp_referrer=install/install.html#installation-on-ubuntu

```
git clone https://github.com/hailo-ai/hailort.git
cd hailort
cmake -S. -Bbuild -DCMAKE_BUILD_TYPE=Release && cmake --build build --config release
```


#### You can now run it with:

```
build/hailort/hailortcli/hailortcli
```


---
### Installation of HailoRT Inside a Docker Container

* https://hailo.ai/developer-zone/documentation/hailort-v4-22-0/?sp_referrer=install/docker.html#docker-installation

Running the Container

```
./run_hailort_docker.sh <hailort_image_name> <hailort_container_name>
./run_hailort_docker.sh hailo_docker_hailort_4.0.tar hailort_01
```

