# Helmet Detection System

This repository contains a Python-based helmet detection system using the YOLOv8 model to identify motorcyclists, helmets, and license plates in video footage. The system processes videos to ensure vertical orientation and labels motorcyclists based on helmet presence.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Dataset](#dataset)
- [Model Training](#model-training)
- [File Structure](#file-structure)
- [Contributing](#contributing)
- [License](#license)

## Overview
The Helmet Detection System uses the YOLOv8 model from Ultralytics to detect motorcyclists, helmets, and license plates in video streams. It processes video frames, ensures vertical orientation, and annotates detections with bounding boxes and labels indicating helmet presence ("Helmet" or "No Helmet").

## Features
- Detects motorcyclists, helmets, and license plates using YOLOv8.
- Automatically rotates videos to vertical orientation (height > width).
- Labels motorcyclists with helmet status (green for helmet, red for no helmet).
- Saves processed videos with annotations.
- Real-time visualization of detection results.

## Requirements
- Python 3.10+
- Libraries:
  - `ultralytics`
  - `opencv-python`
  - `numpy`
  - `roboflow` (for dataset download)
- A trained YOLOv8 model (e.g., `best.pt`)
- Video input for processing

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/daud-shah/traffic_safety_-helmat_detection-
   cd helmet-detection-system
   ```
2. Create a virtual environment (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install ultralytics opencv-python numpy roboflow
   ```

## Usage
1. Ensure you have a trained YOLOv8 model (`best.pt`) and an input video.
2. Update the paths in the `helmet-detection-notebook.ipynb` for your model and video files:
   ```python
   detector = HelmetDetectionSystem(
       model_path='path/to/best.pt',
       class_names=['helmet', 'license_plate', 'motorcyclist']
   )
   detector.process_video(
       video_path='path/to/input_video.mp4',
       output_path='path/to/output_vertical.mp4'
   )
   ```
3. Run the notebook or script:
   ```bash
   jupyter notebook helmet-detection-notebook.ipynb
   ```
4. The processed video will be saved to the specified `output_path` with vertical orientation and annotations.

## Dataset
The dataset used for training is sourced from Roboflow:
- **Workspace**: object-detection-sn8ac
- **Project**: helmate-gxxio-emckf
- **Version**: 1
- **Format**: YOLOv8
- **Classes**: helmet, license_plate, motorcyclist

To download the dataset, use the provided code in the notebook:
```python
from roboflow import Roboflow
rf = Roboflow(api_key="YOUR_API_KEY")
project = rf.workspace("object-detection-sn8ac").project("helmate-gxxio-emckf")
version = project.version(1)
dataset = version.download("yolov8")
```
Replace `"YOUR_API_KEY"` with your Roboflow API key.

## Model Training
The YOLOv8 model is trained using the following command in the notebook:
```bash
yolo train model=yolov8s.pt data="/path/to/helmate-1/data.yaml" epochs=50 imgsz=640 batch=16 device=0,1
```
- **Model**: Pre-trained YOLOv8s (`yolov8s.pt`)
- **Data**: Path to the `data.yaml` file from the downloaded dataset
- **Epochs**: 50
- **Image Size**: 640x640
- **Batch Size**: 16

Training results are saved in the `runs/detect/train` directory.

## File Structure
```
helmet-detection-system/
├── helmet-detection-notebook.ipynb  # Main Jupyter notebook
├── best.pt                         # Trained YOLOv8 model (not included)
├── data/                           # Dataset directory (after download)
│   ├── train/
│   ├── valid/
│   ├── data.yaml
├── output/                         # Output directory for processed videos
└── README.md                       # This file
```

## Contributing
Contributions are welcome! Please follow these steps:
1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes and commit (`git commit -m 'Add feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```
