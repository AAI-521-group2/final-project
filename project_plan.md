# Team Project Status Update Form

Complete as a team and designate a team lead to submit to the group assignment link in Module 4.

## Team Information

**Team Number:** Team 2

**Team Members [Full Names]:**
- Ajmal Jalal
- Aliaksei Matsarski

**Team Leader/Representative:** Ajmal Jalal

**Team GitHub Link:** https://github.com/ajmaljalal/AAI521-ObjectTracking-Project

**Additional Cloud Services:** Google Drive (for video dataset storage and sharing)

---

## Project Description

**Project Title:** Real-Time Multi-Object Tracking and Classification in Video Streams

**Short Description/Project Objectives:** 
This project aims to develop a computer vision system capable of tracking and classifying multiple objects (pedestrians, vehicles, and animals) in video sequences. The system will utilize deep learning-based object detection models combined with tracking algorithms to maintain object identities across video frames. Key objectives include:
1. Implement real-time object detection and classification
2. Track multiple objects simultaneously with unique IDs
3. Handle occlusions and object re-identification
4. Provide visual output with bounding boxes and trajectory paths
5. Calculate tracking metrics such as object count, speed, and direction

---

## Project Dataset

**Selected Dataset:** MOT20 (Multiple Object Tracking Benchmark) / COCO Dataset for Object Detection
- Primary: MOT20 - http://motchallenge.net/data/MOT20/
- Secondary: COCO Dataset - https://cocodataset.org/

**Description of Your Selected Dataset:**

**MOT20 Dataset:**
- **Data Source:** Multiple Object Tracking Benchmark Challenge
- **Number of Images/Frames:** Approximately 8,931 frames across 4 training sequences and 4 test sequences
- **Dimension of Images:** 1920×1080 pixels (Full HD resolution)
- **Size of Dataset:** ~3.5 GB
- **Video Format:** 25 FPS, captured in crowded urban environments
- **Annotations:** Bounding box coordinates, object IDs, class labels (primarily pedestrians)
- **Features:** Dense crowds, varying lighting conditions, occlusions, camera motion

**COCO Dataset (Supplementary):**
- **Data Source:** Microsoft COCO (Common Objects in Context)
- **Purpose:** Pre-training and transfer learning for object detection
- **Number of Images:** 330K images with 80 object categories
- **Annotations:** Bounding boxes, segmentation masks, object labels

---

## Description and Requirements

### What is the task, and why does it matter?

The task is to build an intelligent video surveillance system that can automatically detect, track, and classify multiple objects in video streams. This matters because:

1. **Public Safety & Security:** Automated tracking systems are crucial for monitoring public spaces, identifying suspicious behavior, and enhancing security measures
2. **Traffic Management:** Tracking vehicles and pedestrians helps optimize traffic flow, reduce congestion, and improve road safety
3. **Autonomous Vehicles:** Object tracking is a fundamental component of self-driving technology for obstacle avoidance and path planning
4. **Retail Analytics:** Understanding customer movement patterns and counting foot traffic for business intelligence
5. **Wildlife Conservation:** Tracking and monitoring animal movements for ecological research and conservation efforts

This project demonstrates practical applications of computer vision in solving real-world problems.

---

### How were the data measured? How raw is this dataset?

**MOT20 Dataset:**
- **Capture Method:** Recorded using stationary and moving HD cameras in real-world urban settings (train stations, streets, crowded areas)
- **Camera Specifications:** Various HD cameras (1920×1080 resolution) at 25 FPS
- **Pre-processing:** 
  - Frames have been extracted from video sequences
  - Manual annotations have been added for ground truth bounding boxes and object IDs
  - Images are provided in JPG format
  - Annotations are in MOTChallenge format (frame number, object ID, bbox coordinates, confidence)
- **Rawness Level:** Semi-processed
  - Original video footage has been split into frames
  - Ground truth annotations have been manually added by experts
  - No normalization or augmentation has been applied to the images
  - Original lighting, weather conditions, and camera artifacts are preserved

**COCO Dataset:**
- Captured using Flickr images with diverse real-world scenarios
- Professional photography with varying quality levels
- Extensively annotated with high-quality bounding boxes and segmentation masks
- Images are in their original resolution (varying sizes)

---

### Has this dataset been used a lot in the past for computer vision?

**Yes, extensively:**

**MOT20 Dataset:**
- **Benchmark Status:** Official benchmark dataset for the Multiple Object Tracking Challenge
- **Research Papers:** Used in 500+ research publications on object tracking
- **Competitions:** Featured in annual MOTChallenge workshops at CVPR and ICCV conferences
- **Key Applications:**
  - Deep SORT (Simple Online and Realtime Tracking with a Deep Association Metric)
  - FairMOT (Fair Multi-Object Tracking)
  - ByteTrack
  - TransTrack
- **Leaderboards:** Active leaderboard with state-of-the-art tracking methods competing for best performance

**COCO Dataset:**
- One of the most widely used datasets in computer vision
- Foundation for modern object detection architectures (YOLO, Faster R-CNN, RetinaNet, etc.)
- Used in thousands of research papers and practical applications

**Benefits of using established datasets:**
- Validated ground truth annotations
- Standardized evaluation metrics
- Ability to compare our results with state-of-the-art methods
- Availability of pre-trained models for transfer learning

---

### What is the feature extraction plan?

Our feature extraction strategy will employ a multi-stage approach:

**1. Object Detection Features:**
- **Backbone Network:** Use a pre-trained CNN (ResNet50 or EfficientNet) on ImageNet
- **Detection Model:** Implement YOLOv8 or Faster R-CNN for real-time object detection
- **Extracted Features:**
  - Bounding box coordinates (x, y, width, height)
  - Object class probabilities
  - Detection confidence scores
  - Deep feature embeddings from the backbone network (512 or 1024-dimensional vectors)

**2. Appearance Features:**
- Extract Re-ID (re-identification) features using a Siamese network or ResNet
- Generate 256 or 512-dimensional appearance embeddings for each detected object
- These features help distinguish between different objects of the same class

**3. Motion Features:**
- **Kalman Filter:** Predict object position in the next frame based on velocity and acceleration
- **Optical Flow:** Calculate motion vectors between consecutive frames
- **Trajectory Features:** Track speed, direction, and acceleration patterns

**4. Temporal Features:**
- Use LSTM or Transformer layers to capture temporal dependencies
- Track historical positions and appearance changes over time

**5. Data Augmentation (for training):**
- Random crops and resizes
- Color jittering and brightness adjustments
- Horizontal flips
- Motion blur to simulate camera movement

---

### Is there any bad data, cropped images, or quality issues?

**Potential Data Quality Issues:**

**1. Occlusions:**
- Objects frequently occlude each other in crowded scenes
- Partial visibility can affect detection accuracy
- **Solution:** Use re-identification features to maintain track continuity; implement occlusion handling in tracking algorithm

**2. Low Image Quality in Some Frames:**
- Motion blur from fast-moving objects or camera movement
- Poor lighting conditions in some sequences
- **Solution:** Apply image enhancement techniques; use temporal smoothing across frames

**3. Challenging Scenarios:**
- Dense crowds with many overlapping objects
- Small object sizes at distance
- Camera angle and perspective changes
- **Solution:** Multi-scale detection; implement perspective-aware tracking

**4. Annotation Imperfections:**
- Some boundary cases with ambiguous object boundaries
- Occasional missing annotations in extremely crowded frames
- **Solution:** Use data validation; potentially supplement with additional annotations

**5. Class Imbalance:**
- More pedestrian examples than vehicles or animals
- **Solution:** Use weighted loss functions; apply class-balanced sampling

**6. Frame Rate Variations:**
- Some sequences may have slight frame rate inconsistencies
- **Solution:** Implement adaptive tracking parameters; use frame-to-frame delta times

**Handling Strategy:**
- Implement robust data preprocessing pipeline
- Use data augmentation to improve model generalization
- Apply outlier detection to identify and handle corrupted frames
- Document and report data quality metrics in our final report
- These are NOT hard stops - we will implement appropriate preprocessing and model robustness techniques

---

## Team Responsibilities

### What are the contributions and areas of responsibility of each team member for the project?

| **Ajmal Jalal** | **Aliaksei Matsarski** |
|-----------------|------------------------|
| **Data Pipeline & Preprocessing:** <br>- Download and organize MOT20 and COCO datasets<br>- Perform exploratory data analysis (EDA)<br>- Create data preprocessing and augmentation pipeline<br>- Handle data quality checks and validation | **Object Detection Implementation:**<br>- Implement YOLOv8/Faster R-CNN architecture<br>- Fine-tune pre-trained detection models<br>- Optimize detection accuracy and inference speed<br>- Extract bounding boxes and feature embeddings |
| **Object Tracking System:**<br>- Implement SORT/DeepSORT tracking algorithm<br>- Develop re-identification module<br>- Handle occlusions and ID continuity<br>- Optimize tracking performance (MOTA, IDF1) | **Model Training & Evaluation:**<br>- Set up training pipeline in Google Colab<br>- Monitor training metrics and loss curves<br>- Perform hyperparameter tuning<br>- Calculate and analyze performance metrics |
| **Visualization & Output:**<br>- Create bounding box overlays on video frames<br>- Implement trajectory path visualization<br>- Generate annotated tracking videos<br>- Develop performance metric dashboards | **System Integration & Testing:**<br>- Integrate detection and tracking modules<br>- Build end-to-end processing pipeline<br>- Test on validation sequences<br>- Perform error analysis and debugging |
| **Version Control & Deployment:**<br>- Set up GitHub repository structure<br>- Manage branches and pull requests<br>- Code reviews and quality assurance<br>- Maintain comprehensive README documentation | **Code Optimization & Documentation:**<br>- Optimize code for performance and efficiency<br>- Write inline code comments and docstrings<br>- Document API and usage instructions<br>- Prepare code for final deployment |

**Equal Shared Responsibilities (50/50 contribution):**
- **Technical Report Writing:** Both members write equal sections (Introduction, Methods, Results, Analysis, Conclusion)
- **Presentation Development:** Co-create slides, visuals, and demonstration materials
- **Video Presentation Recording:** Equal presentation time and narration (5-6 minutes each)
- **Weekly Team Meetings:** Joint planning, progress syncs, and decision-making
- **Problem-Solving:** Collaborative debugging and technical discussions
- **Peer Review:** Review each other's code and documentation
- **Final Deliverables:** Joint responsibility for quality and timely submission

---

## Comments/Roadblocks

**Current Progress:**
- Dataset identified and download initiated
- GitHub repository created with initial structure
- Team roles and responsibilities assigned
- Literature review on YOLO, SORT, and DeepSORT algorithms in progress

**Potential Roadblocks & Mitigation Strategies:**

1. **Computational Resources:**
   - **Challenge:** Training deep learning models requires significant GPU resources
   - **Solution:** Use Google Colab Pro for GPU access; leverage pre-trained models; optimize batch sizes

2. **Model Complexity:**
   - **Challenge:** Balancing detection accuracy with real-time processing speed
   - **Solution:** Experiment with lightweight architectures (YOLO-Nano, MobileNet); implement model quantization

3. **Tracking in Dense Crowds:**
   - **Challenge:** Maintaining accurate object IDs in heavily occluded scenarios
   - **Solution:** Implement robust re-identification features; use appearance and motion cues; study state-of-the-art tracking methods

4. **Team Coordination:**
   - **Challenge:** Coordinating work across multiple team members with different schedules
   - **Solution:** Weekly synchronous meetings on Zoom; asynchronous communication via Slack; clear GitHub workflow with branches and pull requests

5. **Dataset Size:**
   - **Challenge:** Large video files may slow down data loading and processing
   - **Solution:** Implement efficient data loaders with caching; use cloud storage; preprocess frames in batches

**Next Steps:**
- Complete dataset download and initial EDA by end of Week 4
- Implement baseline object detection model by Week 5
- Integrate tracking algorithm by Week 6
- Begin comprehensive testing and evaluation in Week 6-7
- Finalize all deliverables (report, code, presentation) by end of Week 7

**Timeline on Track:** Yes, the team is progressing according to the Module 7 deadline.

---

## Additional Notes

**Tools & Technologies:**
- **Programming:** Python 3.10+
- **Frameworks:** PyTorch, OpenCV, Ultralytics (YOLOv8)
- **Tracking:** SORT/DeepSORT implementation
- **Platform:** Google Colab, Jupyter Notebooks
- **Version Control:** GitHub
- **Data Storage:** Google Drive (for large video files)
- **Visualization:** Matplotlib, Seaborn, OpenCV

**Expected Outcomes:**
- Working multi-object tracking system with >85% MOTA score
- Clear technical report documenting methodology and results
- Professional presentation demonstrating project capabilities
- Well-documented GitHub repository with reproducible code
