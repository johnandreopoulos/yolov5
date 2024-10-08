# YOLOv5 Face Detection Setup Guide

## Step-by-Step Guide to Setting Up YOLOv5 for Face Detection

### 1. **Install Anaconda**
   Download and install [Anaconda](https://www.anaconda.com/) to manage environments, dependencies, and packages efficiently.

### 2. **Install a Labeling Tool (Optional)**
   > [Note]
   > If you already have a labeled dataset for face detection, this step can be skipped. However, if you need to label your own dataset, you can use a tool like [LabelImg](https://github.com/HumanSignal/labelImg/releases) to annotate the images.

### 3. **Create and Activate a Virtual Environment**
   Using Anaconda, create and activate a virtual environment for YOLOv5. Open a terminal and run the following commands:
   ```bash
   conda create -n yolov5 python=3.10
   conda activate yolov5
   ```
   ![cmd_1PStphtame](https://github.com/user-attachments/assets/601bc4fc-ba2f-4a4e-9891-9f112119b7e2)

### 4. **Clone the YOLOv5 Repository**
   Clone the YOLOv5 repository to your local machine using the following command:
   ```bash
   git clone https://github.com/johnandreopoulos/yolov5
   ```
   ![cmd_rA3CQlWpzn](https://github.com/user-attachments/assets/10412768-1b57-49a0-8597-fd90d78e3d78)

### 5. **Navigate to the Cloned Repository**
   After cloning the repository, navigate to the YOLOv5 directory:
   ```bash
   cd yolov5
   ```
   ![cmd_TA5Oz2vGs1](https://github.com/user-attachments/assets/3e583a0b-071a-4782-b130-1244cbc1ba11)

### 6. **Install Dependencies**
   Clone the official YOLOv5 repository and install the required dependencies:
   ```bash
   git clone https://github.com/ultralytics/yolov5
   cd yolov5
   pip install -r requirements.txt
   ```
   This ensures all the necessary libraries for YOLOv5 are properly installed.
   ![cmd_Gv85QBvXKe](https://github.com/user-attachments/assets/fe697756-2fac-4ad1-a423-de61f2a81982)

### 7. **Configure the Dataset for Face Detection**
   Prepare the dataset configuration file for your custom face detection dataset:
   - Go to the `<project_root>/yolov5/data` directory.
   - Rename `coco128.yaml` to `custom_data.yaml`.
   - Modify `custom_data.yaml` to specify the paths to your training and validation images, and define the class (in this case, "face"):
   ```yaml
   train: ../../train_data/images/train/  # Path to training images
   val: ../../train_data/images/val/      # Path to validation images

   # Classes
   names:
     0: face
   ```

### 8. **Train the YOLOv5 Model**
   Start training YOLOv5 on your custom dataset with the following command:
   ```bash
   python train.py --img 640 --batch 16 --epochs 100 --data custom_data.yaml --weights yolov5s.pt --nosave --cache
   ```
   After training, the model weights and other results will be stored in the `runs/train/exp/weights` directory.

### 9. **Run Object Detection Using the Trained Model**
   Once training is complete, use the trained model to detect faces in your test images or videos. Replace `<PATH_OF_TEST_FILE>` with the path to the image or video file you wish to process:
   ```bash
   python detect.py --weights runs/train/exp/weights/last.pt --source <PATH_OF_TEST_FILE>
   ```
   Detection results will be saved in the `runs/detect/expX` directory for review.

---

By following this guide, you can set up YOLOv5 for face detection, train your model, and run face detection on images or videos efficiently.