YOLOv8 Car Detection on a Short YouTube Clip

This notebook demonstrates a simple end-to-end pipeline for running YOLOv8 object detection on a short segment of a YouTube video. The workflow is:

Install dependencies
Installs ultralytics (YOLOv8), yt-dlp (YouTube video downloader), and opencv-python (video processing support).

Download a short clip from YouTube (5 seconds)
Uses yt-dlp to download only a 5-second segment (00:00–00:00:05) and saves it as live_clip.<ext> (usually mp4, but may vary depending on available formats).

Run YOLOv8 and detect only cars
Loads the pretrained yolov8n.pt model and runs inference on the downloaded clip, filtering detections to cars only using classes=[2] (COCO class index for “car”).
The model is configured with:

conf=0.30 confidence threshold

imgsz=480 inference resolution

vid_stride=2 to process every 2nd frame (speed-up)

Save annotated output video
YOLO saves an output video with bounding boxes to:
./yolo_live_cars/

Display the processed video inline
The notebook reads the saved MP4 output and embeds it using an HTML <video> tag for inline playback.

Notes / Common Pitfalls

The notebook may fail if the downloaded clip is not named exactly live_clip.mp4 (e.g., it could be live_clip.webm).
A robust approach is to reuse the dynamically detected filename from the download step (e.g., via glob("live_clip.*")) instead of hardcoding the path.

Although a comment may reference “60 seconds,” the notebook actually downloads 5 seconds.
