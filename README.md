# YOLOv5 Face Detection Setup Guide

## Comprehensive Guide for Setting Up YOLOv5 for Face Detection

### 1. **Install Anaconda**
   Download and install [Anaconda](https://www.anaconda.com/) to efficiently manage environments, dependencies, and packages.

### 2. **Install a Labeling Tool (Optional)**
   > [!NOTE] 
   > Since we are focused on face detection, you may not need a separate labeling tool if the required dataset is already available or included in the process.
   If necessary, choose and install a labeling tool [YOLOv5 Labeling Guide](https://github.com/HumanSignal/labelImg/releases) to annotate your dataset.  


### 3. **Create and Activate a Virtual Environment**
   Open a terminal and create a virtual environment for YOLOv5 using Anaconda. Activate the environment with the following commands:
   ```bash
   conda create -n yolov5 python=3.10
   conda activate yolov5
   ```
   ![cmd_1PStphtame](https://github.com/user-attachments/assets/601bc4fc-ba2f-4a4e-9891-9f112119b7e2)

### 4. **Clone the YOLOv5 Repository**
   Clone the YOLOv5 repository from GitHub to your local machine:
   ```bash
   git clone https://github.com/johnandreopoulos/yolov5
   ```
   ![cmd_rA3CQlWpzn](https://github.com/user-attachments/assets/10412768-1b57-49a0-8597-fd90d78e3d78)

### 5. **Navigate to the Cloned Repository**
   After cloning, navigate to the YOLOv5 directory:
   ```bash
   cd yolov5
   ```
   ![cmd_TA5Oz2vGs1](https://github.com/user-attachments/assets/3e583a0b-071a-4782-b130-1244cbc1ba11)

### 6. **Install Dependencies from the Official YOLOv5 Repository**
   To ensure compatibility, clone the official YOLOv5 repository and install all necessary dependencies:
   ```bash
   git clone https://github.com/ultralytics/yolov5
   cd yolov5
   pip install -r requirements.txt
   ```
   This step guarantees that all required libraries for YOLOv5 are installed properly.
   ![cmd_Gv85QBvXKe](https://github.com/user-attachments/assets/fe697756-2fac-4ad1-a423-de61f2a81982)

### 7. **Configure Your Dataset for Face Detection**
   Update the dataset configuration for your custom face detection dataset:
   - Navigate to the `<project_root>/yolov5/data` directory.
   - Rename the `coco128.yaml` file to `custom_data.yaml`.
   - Modify the `custom_data.yaml` file to specify the paths to your training and validation images, as well as the class names. Example:
   ```yaml
   train: ../../train_data/images/train/  # Path to training images
   val: ../../train_data/images/val/      # Path to validation images

   # Classes
   names:
     0: face
   ```

### 8. **Train the YOLOv5 Model**
   Start training the YOLOv5 model with your custom dataset by running the following command in the YOLOv5 directory:
   ```bash
   python train.py --img 640 --batch 16 --epochs 100 --data custom_data.yaml --weights yolov5s.pt --nosave --cache
   ```
   Once training is complete, the results (including model weights) will be saved in the `runs/train/exp/weights` directory.

### 9. **Run Object Detection Using the Trained Model**
   After training, you can run object detection on your test images with the following command:
   - `<PATH_OF_TEST_FILE>` is the path of the picture/video file that you would like to detect the faces.
   ```bash
   python detect.py --weights runs/train/exp/weights/last.pt --source <PATH_OF_TEST_FILE>
   ```
   The results will be saved in the `runs/detect/expX` directory, where you can review the detection output.

This guide offers a step-by-step walkthrough for setting up and using YOLOv5 for face detection. Following these instructions will enable you to configure the environment, train a model, and run detections efficiently.
