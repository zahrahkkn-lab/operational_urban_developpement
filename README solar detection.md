## Dataset description

### Data source
The dataset used in this project was created and managed in **Roboflow**. It is a **custom image dataset** assembled for solar panel detection: images were collected from **[WRITE YOUR IMAGE SOURCE: e.g., aerial/orthophoto imagery, drone photos, rooftop photographs, Google Earth screenshots, etc.]**, then uploaded to a Roboflow public project. Each image was manually annotated in Roboflow using polygon labels to outline the exact area of solar panels.

### Type of data
- **Modality:** RGB images (2D)
- **Task type:** **Instance Segmentation** (polygon-based annotations)
- **Classes:** `solar_panel` (and any other classes if you created them: **[LIST]**)
- **Annotation format:** polygon masks (exportable in formats such as COCO instance segmentation / YOLO segmentation depending on export settings)

### Dataset size and split
- **Total images:** **[N_TOTAL]**
- **Training images:** **[N_TRAIN]**
- **Validation images:** **[N_VAL]**
- **Test images:** **[N_TEST]**
- **Number of annotations (instances):** **[N_INSTANCES]** (if available in Roboflow)

> Note: These counts are visible on the Roboflow dataset/version page after you create a dataset version and split the data.

### Main characteristics of the dataset
1. **Polygon-level labels (high precision):** Solar panels are annotated using polygons rather than simple bounding boxes, which captures panel shape and area more accurately—important for downstream measurements (e.g., total PV coverage on a roof).
2. **Rooftop context and variability:** Images include real-world variation in roof materials, panel orientations, illumination conditions, and backgrounds (e.g., skylights, roof windows, HVAC units), which improves model robustness.
3. **Scale and resolution variability:** Depending on the imagery source, the dataset may contain different zoom levels and spatial resolutions, helping the model generalize to multiple viewing conditions.
4. **Preprocessing and augmentation (Roboflow versioning):** Roboflow dataset versions can apply resizing and augmentations (e.g., flips, rotations, brightness changes), which can improve performance when the number of images is limited.

### Why this dataset is appropriate for the project goals
The primary goal of the project is to **detect solar panels in images** and (optionally) estimate their **spatial extent**. This dataset is appropriate because:
- It is labeled specifically for **solar panels**, directly matching the target object class.
- The use of **instance segmentation** aligns with goals beyond “presence/absence” detection—polygons allow estimating **panel area**, separating multiple arrays, and supporting more precise spatial analysis.
- The dataset’s variability in rooftop scenes supports building a model that can generalize to different buildings and conditions, which is essential for reliable deployment and evaluation.


