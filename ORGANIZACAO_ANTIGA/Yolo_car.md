What this notebook does (high-level)

It:

Installs required libraries.

Downloads a short 5-second clip from a YouTube live/video using yt-dlp.

Runs YOLOv8 object detection on that clip, detecting only cars.

Saves an output video with bounding boxes.

Displays the processed video inline in the notebook.

This is essentially a “download video → detect cars → show results” pipeline.

Cell-by-cell explanation
Cell 0
!pip -q install ultralytics yt-dlp opencv-python


Installs:

ultralytics: provides YOLOv8 (YOLO(...) and .predict()).

yt-dlp: downloads video/audio from YouTube and many other sites.

opencv-python: video/image handling backend often used by Ultralytics.

-q means “quiet” (less output).

Cell 1 — Download a short clip from YouTube
import subprocess, glob, os

LIVE_URL = "https://www.youtube.com/watch?v=bNaSlizKHEM"

subprocess.run([
    "yt-dlp",
    "--download-sections", "*00:00-00:00:05",
    "-f", "bv*[ext=mp4]/b",
    "-o", "/content/live_clip.%(ext)s",
    LIVE_URL
], check=True)

files = glob.glob("/content/live_clip.*")
print("Downloaded clip:", files)
VIDEO_PATH = files[0]


Key points:

subprocess.run([...]) runs the command-line tool yt-dlp from Python.

--download-sections "*00:00-00:00:05" downloads only the segment from 00:00 to 00:00:05 (5 seconds).

Note: the comment says # 60s but the code is 5 seconds, not 60.

-f "bv*[ext=mp4]/b" chooses a “best video” format, preferring mp4 when possible, otherwise falling back.

-o "/content/live_clip.%(ext)s" outputs to something like:

/content/live_clip.mp4 (most likely)

glob.glob("/content/live_clip.*") finds the downloaded file regardless of extension.

VIDEO_PATH = files[0] stores the downloaded filename for later use.

Cell 2 — Run YOLOv8 to detect cars and save a processed video
from ultralytics import YOLO
import os, torch

VIDEO_PATH = "/content/live_clip.mp4"
if not os.path.exists(VIDEO_PATH):
    raise FileNotFoundError(VIDEO_PATH)

model = YOLO("yolov8n.pt")

use_half = torch.cuda.is_available()

for _ in model.predict(
    source=VIDEO_PATH,
    classes=[2],
    conf=0.30,
    imgsz=480,
    vid_stride=2,
    half=use_half,
    stream=True,
    verbose=False,
    save=True,
    project="/content",
    name="yolo_live_cars",
):
    pass

print("Output folder: /content/yolo_live_cars/")


What each part means:

VIDEO_PATH = "/content/live_clip.mp4"
This overwrites the VIDEO_PATH from Cell 1. It assumes the downloaded file is specifically live_clip.mp4.

Existence check:

If the file is not present, it raises an error immediately.

model = YOLO("yolov8n.pt")

Loads the YOLOv8 nano pretrained model weights.

“n” = smallest/fastest variant, lower accuracy than larger models.

use_half = torch.cuda.is_available()

If a GPU is available, half=True uses FP16 (“half precision”) for speed/memory improvements.

On CPU, half precision generally does not help and can cause issues; so it stays False.

model.predict(...) does inference on the video:

source=VIDEO_PATH: input is the video file.

classes=[2]: detect only class 2 from the COCO dataset.

In COCO, class 2 = car.

conf=0.30: confidence threshold; detections below 0.30 are discarded.

imgsz=480: image size used during inference (trade-off speed vs accuracy).

vid_stride=2: process every 2nd frame (skips frames) for speed.

stream=True: yields results frame-by-frame as a generator.

save=True: saves outputs (annotated video/images) to disk.

project="/content", name="yolo_live_cars": output directory becomes:

/content/yolo_live_cars/

The loop:

for _ in model.predict(...):
    pass


This is a common pattern to force the generator to run through all frames, even though you’re not using the per-frame results in Python. The real goal here is the saved output file.

Cell 3 — Display the processed video inside the notebook
import glob
from base64 import b64encode
from IPython.display import HTML

video_files = glob.glob("/content/yolo_live_cars/live_clip.mp4")

if video_files:
    out_vid = video_files[0]
    mp4 = open(out_vid, "rb").read()
    data_url = "data:video/mp4;base64," + b64encode(mp4).decode()

    display(HTML(f"""
    <video width="900" controls>
      <source src="{data_url}" type="video/mp4">
    </video>
    """))
else:
    print("Erro: O vídeo processado 'live_clip.mp4' não foi encontrado ...")


What’s happening:

It looks specifically for:

/content/yolo_live_cars/live_clip.mp4

If found:

Reads the mp4 as bytes

Base64-encodes it

Embeds it into an HTML <video> tag using a data: URL

Displays inline in Jupyter/Colab

If not found:

Prints a Portuguese error message explaining the likely failure is either:

download didn’t work, or

YOLO processing didn’t finish / didn’t save.

Practical notes (important for robustness)

Possible mismatch of video filename

Cell 1 sets VIDEO_PATH = files[0] dynamically.

Cell 2 ignores that and hardcodes "/content/live_clip.mp4".

If yt-dlp outputs live_clip.webm (or anything else), Cell 2 will fail.

Better: reuse VIDEO_PATH from Cell 1, or rename/convert to mp4.

The comment “# 60s” is incorrect

The code downloads 5 seconds.

classes=[2] is COCO-specific

This works because yolov8n.pt is trained on COCO classes.
