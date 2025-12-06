# Project Summary: Real-Time Multi-Object Tracking

#### **Team:** Team 2 (Ajmal Jalal, Aliaksei Matsarski)
#### **Course:** AAI-521-05 Applied Computer Vision for AI
#### **Date:** December 5, 2025

## 1. Objective
The goal of this project was to develop an intelligent computer vision system capable of tracking diverse traffic agents in complex urban environments. Unlike standard benchmarks (e.g., MOT20) which focus solely on pedestrians, this system simultaneously tracks **Vehicles, Pedestrians, and Traffic Lights** to simulate an Autonomous Driving perception layer.

## 2. Technical Approach
We implemented a **Tracking-by-Detection** pipeline utilizing state-of-the-art deep learning models:

* **Detection (YOLOv8m):** We employed the YOLOv8 Medium model (pre-trained on MS COCO) for robust object detection. This model was selected for its balance of real-time inference speed and high accuracy on small objects like distant traffic lights.
* **Tracking (DeepSORT):** We integrated the DeepSORT algorithm to assign unique IDs to detected objects. By leveraging a Re-Identification (ReID) neural network and Kalman Filtering, the system maintains object identities even through temporary occlusions (up to 30 frames).

## 3. Key Implementations
To adapt the general-purpose models to the specific requirements of urban traffic analysis, we implemented specific logic layers:

* **Class Grouping Logic:** To handle high variance in vehicle types (e.g., Tuk-tuks, Buses, Motorbikes in Bangkok traffic), we implemented a custom aggregation layer that maps multiple COCO Class IDs (2, 3, 5, 7) into a single unified **"Vehicle"** class.
* **Streaming Inference:** We utilized generator-based streaming (`stream=True`) to process high-resolution video data without exceeding GPU memory limits.
* **Spatial-Temporal Analytics:** Beyond visual output, the system parses tracking logs to generate quantitative insights, including object density time-series and spatial trajectory maps ("spaghetti plots").

## 4. Results
The final system successfully processes raw video inputs to produce:
1.  **Annotated Video:** H.264 MP4 output with bounding boxes, class labels, and unique track IDs.
2.  **Traffic Analytics:** Visualization of traffic flow density and movement patterns.
3.  **Robust ID Switching:** Minimized identity switches during object crossings and occlusions.