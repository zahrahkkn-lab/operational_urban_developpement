# Solar Panel Detection and Segmentation using YOLO

This repository presents an academic project focused on **solar panel detection and segmentation** using deep learning–based computer vision techniques.
The objective of the project is to explore the applicability of **YOLO-based models** for identifying photovoltaic (PV) panels in RGB imagery.

---

## Project Overview

The project investigates the use of a YOLO segmentation model to automatically detect and delineate solar panels in images.
The workflow includes dataset preparation, model training, and qualitative evaluation of segmentation results.

The project is intended for **educational and research purposes** and demonstrates a complete pipeline from data acquisition to model inference.

---

## Dataset Description

### Data Source

The dataset used in this project was created and managed using **Roboflow**.
It is a custom image dataset specifically assembled for **solar panel detection and instance segmentation**.

Images were collected from publicly available online sources and uploaded to Roboflow.
Each image was manually annotated using **polygon-based labels** to accurately outline the visible area of solar panels.

---

### Type of Data

- **Modality:** RGB images (2D)
- **Task type:** Instance Segmentation
- **Target class:** `solar_panel`
- **Annotation format:** Polygon masks  
  (exportable in YOLO Segmentation or COCO Instance Segmentation formats)

---

### Dataset Size and Split

- **Total images:** 20  
- **Training images:** 18  
- **Validation images:** 1  
- **Test images:** 1  

Dataset splitting and versioning were handled directly within Roboflow.

---

### Main Characteristics of the Dataset

1. **High-precision polygon annotations**  
   Solar panels are annotated using polygon masks rather than simple bounding boxes, enabling accurate representation of panel geometry and surface area.

2. **Real-world rooftop variability**  
   Images include different roof types, panel orientations, lighting conditions, and surrounding objects, improving model robustness.

3. **Scale and resolution diversity**  
   The dataset contains images with varying zoom levels and resolutions, reflecting realistic data heterogeneity.

---

## Model and Methodology

- **Model architecture:** YOLO-based segmentation model
- **Base weights:** `yolo11s-seg.pt`
- **Framework:** Ultralytics YOLO
- **Task:** Single-class instance segmentation (`solar_panel`)

The model was trained using the Roboflow-exported dataset in YOLO-compatible format.
Training outputs, including loss curves and predictions, are generated automatically by the YOLO framework.

---

## Outputs and Results

- **Training and inference outputs:** Stored in the `runs/` directory
- **Prediction results:** Segmentation masks overlaid on input images
- **Evaluation:** Qualitative visual inspection of detected solar panels

Due to the limited dataset size, the focus of this project is on **methodological demonstration** rather than quantitative performance benchmarking.

---

## Repository Structure

