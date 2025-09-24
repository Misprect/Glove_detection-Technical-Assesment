# Glove_detection-Technical-Assesment
# Glove Detection - YOLOv5

## Dataset
**Dataset Name:** ["gloves-detection-huhre", workspace- "abbos-aliboev"]
**Source:** ["https://universe.roboflow.com/abbos-aliboev/gloves-detection-huhre/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true", "Roboflow Universe"]
weights & biases(logs and validations testings)-[https://wandb.ai/jain-aryaman11-university-of-petroleum-and-energy-studies/train?nw=nwuserjainaryaman11 for better log and weight and biases view]
## Model
**Model Used:** YOLOv5s
The model was trained for **30 epochs** to detect two classes: `gloves` and `no-gloves`.

## Preprocessing and Training
The dataset was preprocessed and annotated for use with YOLOv5. The images were split into training, validation, and testing sets. The model was trained using the `train.py` script provided by the YOLOv5 repository. Key training parameters included:
- **Epochs:** 30
- **Image Size:** 640
- **Batch Size:** 16 (or as per your setup)
- **Optimizer:** SGD

## What Worked and What Didn't
**What Worked:**
- The YOLOv5s model achieved a high mAP50 of over 93%, demonstrating excellent performance in detecting both `gloves` and `no-gloves`.
- The chosen confidence threshold of 0.35 effectively filtered out most low-confidence false positives.

**What Didn't:**
- Initially, there were issues with file pathing. The `detect.py` script and model loading failed due to incorrect relative paths, which required changing them to absolute paths.
- The log-saving script failed because the `logs` directory was not created programmatically, leading to a `FileNotFoundError`. This was resolved by adding a directory creation step.

## How to Run the Script
1.  **Clone the YOLOv5 repository:**
    `git clone https://github.com/ultralytics/yolov5`
2.  **Place this project:**
    Copy the `Part_1_Glove_Detection` folder into the root of the cloned repository.
3.  **Install requirements:**
    `pip install -r yolov5/requirements.txt`
4.  **Run the detection script:**
    Use the following command from the root of the `yolov5` directory.
    `python Part_1_Glove_Detection/detection_script.ipynb`
