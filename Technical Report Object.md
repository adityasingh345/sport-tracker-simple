# 📄 Technical Report: Object Detection and Tracking Pipeline

## 1. Introduction

This project implements a **real-time object detection and tracking pipeline** using a deep learning-based detector and an efficient tracking algorithm. The goal is to detect people in a video and assign consistent IDs to each individual across frames.

The system is designed to be **simple, fast, and practical**, making it suitable for applications like surveillance, sports analytics, and crowd monitoring.

---

## 2. Model / Detector Used

The object detection component is based on **YOLOv8 (You Only Look Once, Version 8)**, specifically the lightweight variant **yolov8n.pt** provided by Ultralytics.

### Key Characteristics:

* Single-stage detector (fast inference)
* Real-time performance
* High accuracy for common object classes
* Pretrained on the COCO dataset

### Why YOLOv8?

* Faster than traditional two-stage detectors (e.g., Faster R-CNN)
* Easy integration with Python and OpenCV
* Built-in support for tracking pipelines
* Optimized for both CPU and GPU environments

---

## 3. Tracking Algorithm Used

The tracking is performed using **ByteTrack**, which is integrated internally within YOLOv8’s `model.track()` function.

### How ByteTrack Works:

* Associates detections across frames using bounding box similarity
* Uses both **high-confidence and low-confidence detections**
* Applies data association to maintain object identity

### Key Advantages:

* Robust tracking even with partial detections
* Handles missed detections better than traditional trackers
* Maintains higher ID consistency

---

## 4. Why This Combination Was Selected

The combination of **YOLOv8 + ByteTrack** was chosen due to:

### 1. Simplicity

* No need to manually implement tracking algorithms
* Minimal code (~30 lines)

### 2. Performance

* Real-time detection and tracking
* Efficient on low-resource systems

### 3. Reliability

* ByteTrack improves tracking stability
* YOLOv8 provides accurate detections

### 4. Practicality

* Widely used in industry applications
* Easy to deploy and scale

---

## 5. How ID Consistency is Maintained

ID consistency refers to assigning the same ID to an object across multiple frames.

### Mechanism:

1. Each detected object is assigned a bounding box
2. ByteTrack compares current detections with previous frame tracks
3. Matching is done using:

   * Intersection over Union (IoU)
   * Confidence scores
4. If a match is found → same ID is retained
5. If no match → new ID is assigned

### Key Idea:

> Objects are tracked based on spatial continuity and detection confidence.

---

## 6. Challenges Faced

### 1. Video Output Issues

* Codec compatibility problems (mp4 writing)
* FPS mismatch leading to corrupted output

### 2. Environment Limitations

* `cv2.imshow()` not supported in Google Colab
* Required alternative visualization methods

### 3. Performance Constraints

* Processing large videos is slow on CPU
* Memory usage increases with longer videos

### 4. Detection Noise

* False positives in crowded scenes
* Occasional missed detections

---

## 7. Failure Cases Observed

### 1. Occlusion

* When one person blocks another, tracking may fail
* IDs may switch or disappear

### 2. Fast Motion

* Rapid movement causes tracking instability
* Bounding boxes may lag

### 3. Low Resolution

* Small or blurry objects are harder to detect
* Leads to missed detections

### 4. Similar Appearance

* People with similar clothing may get ID switches

---

## 8. Possible Improvements

### 1. Use Stronger Models

* Replace yolov8n with yolov8s or yolov8m for better accuracy

### 2. Re-Identification (Re-ID)

* Add appearance-based tracking
* Helps maintain ID even after occlusion

### 3. GPU Acceleration

* Use CUDA-enabled GPU for faster inference

### 4. Post-processing

* Apply smoothing to bounding boxes
* Reduce jitter in tracking

### 5. Multi-class Tracking

* Extend beyond person detection
* Track vehicles, animals, etc.

---

## 9. Conclusion

This project demonstrates a **simple yet powerful pipeline** for object detection and tracking using modern deep learning techniques. By leveraging YOLOv8 and ByteTrack, the system achieves a good balance between **accuracy, speed, and simplicity**, making it suitable for real-world applications.

---

