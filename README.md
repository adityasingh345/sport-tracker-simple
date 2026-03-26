# 🎯 Object Detection & Tracking Pipeline

This project performs **real-time object detection and tracking** on a video using **YOLOv8**.  
The model detects people and assigns a unique ID to each individual across frames.

---

## 🚀 Features
- Detects people in video frames
- Tracks each person with a unique ID
- Saves annotated output video
- Simple and efficient implementation using YOLOv8

---

## 🛠️ Installation

Run the following commands in Google Colab or your local environment:

```bash
pip install ultralytics opencv-python


-> Dependencies
Python 3.x
OpenCV (cv2)
Ultralytics YOLOv8

-> How to Run
Step 1: Upload input video

Place your video file as:
input.mp4
Step 2: Run the notebook

Execute all cells in the Jupyter Notebook / Google Colab file.

Step 3: Output

After execution, the processed video will be saved as:
output.mp4

-> Pipeline Overview

Load YOLOv8 model
Read video frame-by-frame
Detect people using YOLO
Track objects using built-in tracking (model.track())
Draw bounding boxes + IDs
Save output video

-> Model / Tracker Choice
Model: YOLOv8 (yolov8n.pt)
Reason:
Fast and lightweight
Good accuracy for real-time applications
Built-in tracking support (ByteTrack)


-> Assumptions
Input video contains visible people
Only person class (class 0) is tracked
Video format is supported (mp4)

-> Limitations
May fail in:
Heavy occlusion (people overlapping)
Very low resolution videos
Fast motion blur
Tracking IDs may change occasionally
Depends on GPU/CPU performance
