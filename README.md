# Traffic-Flow-Analysis-Task

Traffic Flow Analysis – Detailed Setup & Execution
1. Requirements
Python: Version 3.8 or later

Operating System: Windows

Internet Connection: Required for downloading the YouTube traffic video and YOLO model weights

Hardware: GPU recommended for faster processing (CPU will also work)


2. Install Dependencies
Open a terminal or command prompt and run:

pip install yt-dlp ultralytics opencv-python pandas filterpy scipy
Dependency explanation:

yt-dlp → Downloads the YouTube traffic video

ultralytics → YOLOv8 object detection model

opencv-python → Video processing, drawing overlays

pandas → CSV file handling

filterpy → Kalman filter for SORT tracking

scipy → IOU computation and Hungarian algorithm


3. Prepare the Script
Save the full Python code provided above as:

traffic_flow_analysis.py

4. Run the Script
In the terminal, execute:

python traffic_flow_analysis.py


5. What the Script Does
   1.Downloads the YouTube traffic video (traffic.mp4).

   2.Loads YOLOv8 (yolov8n.pt) to detect vehicles:

   Car (COCO ID: 2)

   Motorcycle (3)

   Bus (5)

   Truck (7)

   3.Implements SORT tracking to maintain unique IDs for vehicles across frames.

   4.Defines lane boundaries at pixel positions:


   lanes_x = [300, 600, 900]
   → 3 lanes:

   Lane 1: x < 300

   Lane 2: 300 ≤ x < 600

   Lane 3: x ≥ 600

   5.Counts vehicles per lane only once per vehicle ID to avoid duplicates.

   6.Overlays on video:

  Lane boundary lines (yellow)

  Vehicle bounding boxes (blue)

  Vehicle ID + lane number (green text)

  Real-time lane counts (yellow text at top-left)

   7.Saves outputs:

  processed_traffic.mp4 → Annotated video with overlays

  traffic_analysis.csv → Vehicle log with:

   Vehicle_ID, Lane, Frame, Timestamp
Console summary showing total counts per lane

6. Output Files
After execution, you will have:

traffic.mp4 → Original downloaded video

processed_traffic.mp4 → Video with overlays & real-time counts

traffic_analysis.csv → Vehicle log file

Example traffic_analysis.csv:


Vehicle_ID,Lane,Frame,Timestamp
1,1,15,0.5
2,2,20,0.66
3,3,22,0.73
...

7. Customization
Change Lane Boundaries:
Edit in script:

lanes_x = [300, 600, 900]
Adjust values to fit your video.

Change Vehicle Classes:
In detection loop:


if cls in [2, 3, 5, 7]:
(COCO IDs: car=2, motorcycle=3, bus=5, truck=7)

Model Accuracy vs. Speed:
Change:
model = YOLO("yolov8n.pt")  # nano: fastest
to:
model = YOLO("yolov8s.pt")  # small: more accurate, slower

8. Notes
Running without a GPU may be slower.

The script overwrites old output files if run multiple times.


Works best with a fixed camera and clear lane markings.

The lane boundaries in this script are vertical lines; for curved roads, use polygon-based lane detection.
[Watch the video](https://drive.google.com/file/d/1VtA3NjdoME1FVu4_neLYcTvyDAr7b4nK/view?usp=sharing)


