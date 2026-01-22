Car Detection on a Short YouTube Clip (YOLOv8)

This notebook demonstrates an end-to-end pipeline for detecting cars in a short segment of a YouTube video using Ultralytics YOLOv8.

Pipeline Overview

Install dependencies
Installs:

ultralytics for YOLOv8 inference

yt-dlp to download a short video segment from YouTube

opencv-python for video processing support

Download a 5-second clip from YouTube
Uses yt-dlp to fetch only a 5-second section (00:00–00:00:05) and saves it locally as live_clip.<ext> (typically .mp4, but the extension may vary depending on available formats).

Run YOLOv8 inference (cars only)
Loads the pretrained model yolov8n.pt and runs object detection on the downloaded clip, filtering detections to cars only using:

classes=[2] (COCO class index for “car”)

Inference configuration includes:

conf=0.30 (confidence threshold)

imgsz=480 (inference resolution)

vid_stride=2 (process every 2nd frame for faster runtime)

Save an annotated output video
YOLO writes a processed video with bounding boxes to:

/content/yolo_live_cars/ (in Colab)

or the configured project directory in other environments

Display the processed video inline
The notebook embeds the saved output video in the notebook interface for quick visual verification.

Notes / Common Pitfalls

The download step saves live_clip.<ext>, which may not always be live_clip.mp4. If the notebook hardcodes live_clip.mp4, it may fail when the downloaded format is different (e.g., .webm). A robust approach is to locate the downloaded file dynamically (e.g., using glob("live_clip.*")) and pass that path into YOLO.

Although some comments may mention “60 seconds,” the code as written downloads 5 seconds.
