## Dataset description

### Data source
The data used in this project is derived from a **publicly available YouTube video**.
A short video segment was downloaded using **yt-dlp** from a live/recorded traffic stream and used exclusively for **object detection inference**.

The video contains real-world urban traffic scenes and does not include any private or sensitive data.  
No manual annotation was performed, as detections are generated automatically using a pretrained model.

---

### Type of data
- **Modality:** RGB video frames (2D)
- **Task type:** Object Detection
- **Target class:** `car`
- **Annotation format:**  
  Bounding boxes generated automatically by a pretrained YOLOv8 model (COCO dataset)

---

### Dataset size and processing
- **Input data:** One short video clip (5 seconds)
- **Frame sampling:** Every 2nd frame (`vid_stride = 2`)
- **Total processed frames:** Dependent on the original video frame rate
- **Train / validation split:** Not applicable (inference-only workflow)

> Note: This project focuses on **model inference and visualization**, not on dataset creation or model training.

---

### Main characteristics of the dataset

1. **Real-world traffic scenes:**  
   The video captures natural traffic conditions, including multiple vehicles, varying motion patterns, and complex backgrounds, reflecting realistic deployment scenarios.

2. **Automatic model-based annotations:**  
   Bounding boxes are produced by a pretrained YOLOv8 model trained on the COCO dataset, eliminating the need for manual labeling.

3. **Temporal continuity:**  
   Unlike static images, video data preserves temporal information, allowing observation of detection consistency across consecutive frames.

4. **Lightweight and reproducible setup:**  
   The use of a short video clip and a lightweight model enables fast inference and easy reproduction of results.

---

### Why this dataset is appropriate for the project goals
The primary goal of this project is to **demonstrate video-based car detection using YOLOv8**.
This dataset is appropriate because it:
- Represents realistic urban traffic conditions
- Enables rapid testing of pretrained object detection models
- Provides clear visual feedback through annotated video output
- Requires no manual annotation or dataset preprocessing
