# Ultralytics YOLOv8
* YOLOv8 - Ultralytics [[Ultralytics]](https://docs.ultralytics.com/models/yolov8/)

---
YOLOv8 is the latest iteration in the YOLO series of real-time object detectors, offering cutting-edge performance in terms of accuracy and speed. Building upon the advancements of previous YOLO versions, YOLOv8 introduces new features and optimizations that make it an ideal choice for various object detection tasks in a wide range of applications.

---
<img src="https://github.com/user-attachments/assets/ba224e0a-5d37-4852-ab28-9378f0fca840" width=1000>

---
## Performance

---
| Model | Size | mAP | x86 CPU@ONNX | A100@TensorRT | RPI5+H8L(13T) | CA76@TFLite | RTX4060 (12GB) |
|:-:|:-|-:|-:|-:|-:|-:|-:|
| Price | | | USD 800 | USD ~ | USD 180 | USD 80 | USD 1,500 |
| Power | | | 45W | > 100W |  8W |  5W | > 100W |
| YOLOv8n | 640x640 | 37.3 | 12.4fps | 1,010.1fps | | 2.5fps| 1.35ms, 740fps | 
| YOLOv8s | 640x640 | 44.9| 7.8fps (2.9X) | 833.3fps (416X) | 30fps (15X) | 2.0fps (1X) | ~ 610fps (305X) |
| YOLOv8m | 640x640 | 50.2 | 4.2fps | 546.4fps | | | |

---
### RPI5 with Halio 8 AI processor (26TOPS)
* Run multistream detection inference - Benchmark Result [[SeeedStudio]](https://wiki.seeedstudio.com/benchmark_of_multistream_inference_on_raspberrypi5_with_hailo8/)
* All the results are based on inference with a model **YOLOv5** input size of 640x640, batch size is 8, and a video resolution of 1280x760, which is 720p.

<img src="https://github.com/user-attachments/assets/a974369c-58c3-4c0a-bcf4-28ef358a8b22" width=600>




---
#### YoloV8s object detection demo [[Raspberry forum]](https://forums.raspberrypi.com/viewtopic.php?t=373669)
* We've tested YoloV8s object detection demo. 120fps video input. 680*680
```
Pi5 8GB without Hailo 2fps;
Pi5 8GB with hailo PCIe gen2 41fps;
Pi5 8GB with hailo PCIe gen3 82fps;
CM4 4GB with hailo PCIe gen2 38fps.
```
---
### Yolov8n @ Consumer GPUs
https://docs.ultralytics.com/integrations/tensorrt/#__tabbed_5_2
<img src="https://github.com/user-attachments/assets/ffda0408-e6ab-461d-9f7a-b1c21dc66b71" width=800>

---
### Performance: Detection (COCO)
<img src="https://github.com/user-attachments/assets/571c34e5-8c3c-4951-8737-bbf462202a5a" width=850>

---
### Performance: Segmentation (COCO)
<img src="https://github.com/user-attachments/assets/07e4a50d-5162-4f2f-9c4a-2ef448fb449e" width=1000>

---
### Performance: Pose (COCO)
<img src="https://github.com/user-attachments/assets/f45ef69a-b0d3-4de9-8cde-052be243f8ed" width=1000>

---
### Performance: Classification (ImageNet)
<img src="https://github.com/user-attachments/assets/a923b3d9-97f1-41fc-bd0d-cb208d1afc32" width=1000>
