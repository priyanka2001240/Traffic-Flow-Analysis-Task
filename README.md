# Traffic-Flow-Analysis-Task
Traffic Flow Analysis – Detailed Setup & Execution
1. Requirements
Python: Version 3.8 or later

Operating System: Windows

Internet Connection: Required for downloading the YouTube video and YOLO model weights

Hardware: GPU recommended for faster processing, but CPU will also work

2. Install Dependencies
Open a terminal or command prompt and run:


pip install yt-dlp ultralytics opencv-python pandas filterpy scipy
Dependency explanation:

yt-dlp → Download the YouTube traffic video

ultralytics → YOLOv8 object detection model

opencv-python → Video processing, drawing overlays

pandas → CSV file handling

filterpy → Kalman filter for SORT tracking

scipy → IOU computation and Hungarian algorithm

3. Prepare the Script
Save the full Python code you provided above as:


traffic_flow_analysis.py
4. Run the Script
In the terminal, run:

python traffic_flow_analysis.py
5. What the Script Does
Downloads the YouTube traffic video (traffic.mp4).

Loads YOLOv8 (yolov8n.pt) for detecting vehicles (car, motorbike, bus, truck).

Implements SORT tracking to maintain vehicle IDs across frames.

Defines lane boundaries at fixed x-coordinates (lanes_x = [300, 600, 900]).

Counts vehicles per lane and prevents duplicate counts.

Overlays:

Lane boundaries (yellow lines)

Vehicle bounding boxes

Vehicle IDs and lane numbers

Real-time lane counts

Outputs:

processed_traffic.mp4 → Annotated output video

traffic_analysis.csv → CSV with columns:


Vehicle_ID, Lane, Frame, Timestamp
Console summary of total counts per lane.

6. Output Files
After execution, you will have:

traffic.mp4 → Original downloaded video

processed_traffic.mp4 → Video with overlays & counts

traffic_analysis.csv → Vehicle data log

Example traffic_analysis.csv:

Vehicle_ID,Lane,Frame,Timestamp
1,1,15,0.5
2,2,20,0.66
3,3,22,0.73
...

7. Customization
Change Lane Boundaries: Edit


lanes_x = [300, 600, 900]
to fit your video’s lane positions.

Add/Remove Classes: In detection loop, modify:


if cls in [2, 3, 5, 7]:
Class IDs (COCO dataset):
2 = car, 3 = motorcycle, 5 = bus, 7 = truck.

8. Notes
If your PC is slow, consider using a smaller YOLO model (yolov8n.pt is already the smallest, but you can try lowering frame rate before processing).

The script overwrites old output files if run multiple times.

Works best if the video camera is fixed and lanes are clearly visible
