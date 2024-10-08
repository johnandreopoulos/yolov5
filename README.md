# YOLOv5 Object Detection Setup Guide

### Steps to Set Up YOLOv5 for Object Detection

1. **Install Anaconda**  
   Download and install [Anaconda](https://www.anaconda.com/) to manage environments and dependencies.

2. **Install Labeling Tool**  
   Install a labeling tool from the [YOLOv5 Labeling Guide](https://github.com/ultralytics/yolov5/wiki/Labeling) to annotate your dataset.

3. **Setup a Virtual Environment**  
   After installing Anaconda, open a terminal and run the following command:
   ```bash
   conda create -n yolov5 python=3.10
   conda activate yolov5
   ```
   ![cmd_1PStphtame](https://github.com/user-attachments/assets/601bc4fc-ba2f-4a4e-9891-9f112119b7e2)

4. **Clone the Repository**
   ```bash
   git clone https://github.com/johnandreopoulos/yolov5
   ```
   ![cmd_rA3CQlWpzn](https://github.com/user-attachments/assets/10412768-1b57-49a0-8597-fd90d78e3d78)

5. **Navigate to the Cloned Repository**  
   Move to the cloned repository directory:
   ```bash
   cd yolov5
   ```
   ![cmd_TA5Oz2vGs1](https://github.com/user-attachments/assets/3e583a0b-071a-4782-b130-1244cbc1ba11)

6. **Set Up the YOLOv5 Environment**  
   Clone original yolov5 repository and run the following commands. (Installing may be differ on your network connection)
   ```bash
   git clone https://github.com/ultralytics/yolov5
   cd yolov5
   pip install -r requirements.txt
   ```
   ![cmd_Gv85QBvXKe](https://github.com/user-attachments/assets/fe697756-2fac-4ad1-a423-de61f2a81982)

   
8. **Configure the Dataset**
   - Find folder path `<project_root>/yolov5/data`
   - Rename file called `coco128.yaml` to `custom_data.yaml`
   Edit the file  to match your dataset. For example, if you are detecting faces, the configuration will look like this:
   ```yaml
   train: ../../train_data/images/train/  # Path to training images
   val: ../../train_data/images/val/      # Path to validation images

   # Classes
   names:
     0: face
     # 1: other_class
     # 2: another_class

   # Download script/URL (optional)
   download: https://github.com/ultralytics/assets/releases/download/v0.0.0/coco128.zip
   ```

10. **Train the Model**  
   In the `yolov5` directory, run the following command to start training and wait for it to end the process:
   ```bash
   python train.py --img 640 --batch 16 --epochs 100 --data custom_data.yaml --weights yolov5s.pt --nosave --cache
   ```

   After training completes, a folder named `runs` and a `weights` folder will be created inside the `yolov5` directory, containing the results and model weights.

11. **Run Detection**  
   Use the trained model to perform detection on your test dataset:
   ```bash
   python detect.py --weights runs/train/exp/weights/last.pt --source ../../train_data/images
   ```

   The detection results will be saved in a new directory called `runs/detect/expX`, where you can find images with detected objects (e.g., "faces").

This setup guide will help you get started with YOLOv5 for object detection tasks efficiently.
