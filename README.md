# YOLOv5 Face Detection Setup Guide
> Step-by-Step Guide to Setting Up YOLOv5 for Face Detection

![Banner](https://github.com/user-attachments/assets/754178a3-52ec-4682-9f0b-60b84eded75b)

## Table of Contents
- [YOLOv5 Face Detection Setup Guide](#yolov5-face-detection-setup-guide)
  - [Table of Contents](#table-of-contents)
    - [1. **Install Anaconda**](#1-install-anaconda)
    - [2. **Labelling** `No need for this project`](#2-labelling-no-need-for-this-project)
    - [3. **Create and Activate a Virtual Environment**](#3-create-and-activate-a-virtual-environment)
    - [4. **Clone the YOLOv5 Repository**](#4-clone-the-yolov5-repository)
    - [5. **Navigate to the Cloned Repository**](#5-navigate-to-the-cloned-repository)
    - [6. **Install Dependencies**](#6-install-dependencies)
    - [7. **Configure the Dataset for Face Detection**](#7-configure-the-dataset-for-face-detection)
    - [8. **Train the YOLOv5 Model**](#8-train-the-yolov5-model)
    - [9. **Run Object Detection Using the Trained Model**](#9-run-object-detection-using-the-trained-model)


### 1. **Install Anaconda**
   Download and install [Anaconda](https://www.anaconda.com/) to manage environments, dependencies, and packages efficiently.

### 2. **Labelling** `No need for this project`
1. **Install Labelling**  
   Begin by installing the [LabelImg](https://github.com/HumanSignal/labelImg/releases) software.

2. **Extract the Zip File**  
   Unzip the downloaded file to your desired location.

3. **Open Labelling Application**  
   Locate and open the `labelImg.exe` file.

4. **Open Image Directory**  
   In the left sidebar, click on the **"Open Dir"** option. Navigate to and select the folder containing your images, e.g., `train_data/images/train`.  
   ![Open Directory](https://github.com/user-attachments/assets/bed0d225-3284-461a-b079-091efd2ab152)

5. **Set Save Directory**  
   Before you begin labelling, click on **"Change Save Dir"** in the left sidebar. Set the path to `train_data/labels/train`.  
   ![Change Save Directory](https://github.com/user-attachments/assets/ce4b4730-cd29-427f-bf52-08a5caa12ccd)

6. **Labelling Process**  
   For each image, follow these steps:
   - **Create Rectangle**: Draw a rectangle around the object of interest.
   - **Size the Rectangle**: Adjust the rectangle to fit the object properly.
   - **Save**: Save your labelled data.

   ![Labelling Process](https://github.com/user-attachments/assets/78170913-0930-4e94-b3a4-13724266420d)

- Ensure all images are located in the `/train_data/images/train` folder.
- Save all labelled text files in the `/train_data/labels/train` folder.

--- 

This structure makes the instructions clear and easy to follow while emphasizing important information.

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
   This command starts training the YOLOv5 model on your custom dataset:
   ```bash
   python train.py --img 640 --batch 16 --epochs 100 --data custom_data.yaml --weights yolov5s.pt --nosave --cache
   ```
   - **`--img 640`**: Use images resized to 640x640 pixels.
   - **`--batch 16`**: Train with 16 images at a time.
   - **`--epochs 100`**: Repeat the training process 100 times.
   - **`--data custom_data.yaml`**: Use the dataset defined in `custom_data.yaml`.
   - **`--weights yolov5s.pt`**: Start with pre-trained weights from the YOLOv5 small model.
   - **`--nosave`**: Do not save intermediate model checkpoints during training.
   - **`--cache`**: Load images into memory for faster training.

   After training, the model weights and results will be saved in the `runs/train/exp/weights` directory.

### 9. **Run Object Detection Using the Trained Model**
   Once training is complete, use the trained model to detect faces in your test images or videos. Replace `<PATH_OF_TEST_FILE>` with the path to the image or video file you wish to process:
   ```bash
   python detect.py --weights runs/train/exp/weights/last.pt --source <PATH_OF_TEST_FILE>
   ```
   Detection results will be saved in the `runs/detect/expX` directory for review.

---

By following this guide, you can set up YOLOv5 for face detection, train your model, and run face detection on images or videos efficiently.
