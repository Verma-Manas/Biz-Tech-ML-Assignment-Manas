# Gloved vs Ungloved Hand Detection

## Dataset Name and Source
- **Dataset:** Gloves Annotated Dataset  
- **Source:** [Roboflow Universe - Gloves Annotated Dataset](https://universe.roboflow.com/sana-ali/gloves-annotated-dataset)  
- This dataset consists of labeled images distinguishing gloved and bare hands.

## Model Used
- YOLOv8 (Ultralytics) pretrained model (YOLOv8n) fine-tuned on the Gloves Annotated Dataset for 10 epochs.

## Preprocessing and Training
- Dataset exported in YOLOv8 format with bounding box annotations in `.txt` files.
- Images resized to 640x640 pixels for training.
- Default YOLOv8 augmentations applied.
- Trained with batch size 16 for 30 epochs.
- Best model weights saved in `runs/detect/glove_detection/weights/best.pt`.

## What Worked and What Didn’t
- **What Worked:**  
  - YOLOv8 provided fast and accurate detection.
  - Transfer learning using pretrained YOLOv8n weights was effective.
  - Clear labeling and quality of dataset contributed to model performance.

- **What Didn’t Work / Challenges:**  
  - Some false positives in complex lighting and angles.
  - Limited dataset size restricted finer distinctions.
  - A few annotation inconsistencies required manual cleanup.


## How to Run Your Script

### 1. Install Dependencies
pip install ultralytics opencv-python matplotlib

### 2. Training (Optional)
yolo task=detect mode=train model=yolov8n.pt data=data.yaml epochs=10 imgsz=640 batch=16 name=glove_detection

### 3. Inference and Logging
Run the inference script that:
- Takes images from a folder,
- Runs detection using the trained model,
- Saves annotated images to `output/`,
- Saves detection logs as JSON files to `logs/`.

python detection_script.py --input test/images/ --output output/ --logs logs/ --model runs/detect/glove_detection/weights/best.pt --confidence 0.3

### 4. Output
- Annotated images will be in the `output/` folder.
- JSON detection logs will be saved in the `logs/` folder, containing bounding box coordinates, labels, and confidence scores.

**Author:** Manas Verma
**Date:** August 2025
