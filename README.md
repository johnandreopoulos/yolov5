Certainly! Here’s an updated version of the YOLOv5 Object Detection Setup Guide, now including a section on how to label images for your dataset.

---

# YOLOv5 Object Detection Setup Guide  
A comprehensive, step-by-step guide to setting up YOLOv5 for object detection tasks.

![YOLOv5 Banner](https://github.com/user-attachments/assets/754178a3-52ec-4682-9f0b-60b84eded75b)

## Table of Contents
- [YOLOv5 Object Detection Setup Guide](#yolov5-object-detection-setup-guide)
  - [Table of Contents](#table-of-contents)
    - [1. **Install Anaconda**](#1-install-anaconda)
    - [2. **Labelling Images**](#2-labelling-images)
    - [3. **Create and Activate a Virtual Environment**](#3-create-and-activate-a-virtual-environment)
    - [4. **Clone the YOLOv5 Repository**](#4-clone-the-yolov5-repository)
    - [5. **Configure the Dataset for Face Detection**](#5-configure-the-dataset-for-face-detection)
    - [6. **Train the YOLOv5 Model**](#6-train-the-yolov5-model)
    - [7. **Perform Object Detection with the Trained Model**](#7-perform-object-detection-with-the-trained-model)
    - [8. **Fix `--view-img` Error**](#8-fix---view-img-error)
      - [1. **Ensure OpenCV GUI Support**](#1-ensure-opencv-gui-support)
      - [2. **Platform-Specific Fix for Windows**](#2-platform-specific-fix-for-windows)
    - [Summary of Changes](#summary-of-changes)

---

### 1. **Install Anaconda**
Download and install [Anaconda](https://www.anaconda.com/) to manage environments, dependencies, and packages efficiently.

---

### 2. **Labelling Images**
<details>
<summary>Click to Expand in order to see Labelling Process</summary>

Labelling your images is a crucial step in preparing your dataset for training the YOLOv5 model. Here’s how to use **LabelImg** for this purpose:

1. **Install LabelImg**  
   Download the LabelImg software from the [LabelImg Releases](https://github.com/HumanSignal/labelImg/releases) page and install it.

2. **Extract the Zip File**  
   Unzip the downloaded file to your desired location.

3. **Open the Labelling Application**  
   Locate and run the `labelImg.exe` file to open the application.

4. **Open Image Directory**  
   In the left sidebar, click on the **"Open Dir"** button. Navigate to and select the folder containing your images (e.g., `train_data/images/train`).  
   ![Open Directory](https://github.com/user-attachments/assets/bed0d225-3284-461a-b079-091efd2ab152)

5. **Set Save Directory**  
   Before labelling, click on **"Change Save Dir"** in the left sidebar. Set the path to `train_data/labels/train`.  
   ![Change Save Directory](https://github.com/user-attachments/assets/ce4b4730-cd29-427f-bf52-08a5caa12ccd)

6. **Labelling Process**  
   For each image, follow these steps:
   - **Create Rectangle**: Draw a rectangle around the object of interest.
   - **Size the Rectangle**: Adjust the rectangle to fit the object properly.
   - **Label the Object**: Select the appropriate class (e.g., "face") for the object within the rectangle.
   - **Save**: Save your labelled data using the **Save** option (usually Ctrl+S).

   ![Labelling Process](https://github.com/user-attachments/assets/78170913-0930-4e94-b3a4-13724266420d)

- Ensure all images are located in the `/train_data/images/train` folder.
- Save all labelled text files in the `/train_data/labels/train` folder.

</details>

---

### 3. **Create and Activate a Virtual Environment**
Create and activate a virtual environment to isolate your YOLOv5 dependencies using Anaconda. Run the following commands in the terminal:

```bash
conda create -n yolov5 python=3.10
conda activate yolov5
```

---

### 4. **Clone the YOLOv5 Repository**
Clone the YOLOv5 repository and install dependencies by running the following commands:

```bash
git clone https://github.com/johnandreopoulos/yolov5
cd yolov5
git clone https://github.com/ultralytics/yolov5
cd yolov5
pip install -r requirements.txt
```

---

### 5. **Configure the Dataset for Face Detection**
To configure your dataset for custom face detection, follow these steps:

1. Navigate to the `<project_root>/yolov5/data` directory.
2. Rename `coco128.yaml` to `custom_data.yaml`.
3. Modify `custom_data.yaml` to specify the paths to your training and validation images, and define the class (in this case, "face"):

```yaml
train: ../../train_data/images/train/  # Path to training images
val: ../../train_data/images/val/      # Path to validation images

# Classes
names:
  0: face
```

---

### 6. **Train the YOLOv5 Model**
Use the following command to start training the YOLOv5 model on your custom dataset:

```bash
python train.py --img 640 --batch 16 --epochs 100 --data custom_data.yaml --weights yolov5s.pt --nosave --cache
```

<details>
<summary>Training Parameters</summary>

- `weights`: Path to model weights, default is 'yolov5s.pt'.
- `source`: Input source (file, URL, webcam).
- `data`: Path to dataset YAML file (default: 'data/coco128.yaml').
- `imgsz`: Inference image size (default: 640x640).
- `conf_thres`: Confidence threshold (default: 0.25).
- `iou_thres`: IOU threshold for non-max suppression (default: 0.45).
- `max_det`: Max number of detections per image (default: 1000).
- `device`: CUDA device or 'cpu' (default: auto-detect).
- `view_img`: Display inference results using OpenCV.
- `save_txt`, `save_csv`: Save results in text/CSV format.
- `nosave`: Do not save inference results (default: False).
- `classes`: Filter detections by class index.
- `augment`: Augmented inference.
- `project`: Directory to save results (default: 'runs/detect').
- `name`: Experiment name (default: 'exp').
- `line_thickness`: Bounding box thickness (default: 3).
- `half`: Use FP16 half-precision inference (default: False).

</details>

---

### 7. **Perform Object Detection with the Trained Model**
Once training is complete, use the trained model for object detection. Replace `<PATH_OF_TEST_FILE>` with the path to the test image or video:

```bash
python detect.py --weights runs/train/exp/weights/last.pt --source <PATH_OF_TEST_FILE> --view-img
```

The detection results will be saved in a new folder (`runs/detect/expX`), with `expX` representing the experiment number.

---

### 8. **Fix `--view-img` Error**
If you encounter the following error while using the `--view-img` flag:

```bash
cv2.error: OpenCV(4.10.0) error: (-2:Unspecified error) The function is not implemented.
```

Follow these steps to resolve it:

#### 1. **Ensure OpenCV GUI Support**
Uninstall `opencv-python-headless` and reinstall `opencv-python` with GUI support:

```bash
pip uninstall opencv-python-headless opencv-python
pip install opencv-python
```

#### 2. **Platform-Specific Fix for Windows**
1. **Find Line 288**:
   Open the `detect.py` file and scroll to **line 288**.

2. **Edit the Code**:
   Replace this section with the following updated code to ensure compatibility with both Windows and Linux:
   ```python
   # Stream results
   im0 = annotator.result()
   if view_img:
       # Handle both Windows and Linux platforms for the window display
       if platform.system() in ["Linux", "Windows"] and p not in windows:
           windows.append(p)
           cv2.namedWindow(str(p), cv2.WINDOW_NORMAL | cv2.WINDOW_KEEPRATIO)  # allow window resize
           cv2.resizeWindow(str(p), im0.shape[1], im0.shape[0])
   
       # Show the frame
       cv2.imshow(str(p), im0)
       cv2.waitKey(1)  # 1 millisecond
   ```

### Summary of Changes
- **Modify the Operating System Check**: Change the condition from checking only for "Linux" to check for both "Linux" and "Windows".

This adjustment will allow the `cv2.namedWindow()` function to work correctly on Windows, thus resolving the issue when using `--view-img`.

If you have any further questions or need additional clarification, feel free to ask!

---

By following these steps, you can set up YOLOv5 for object detection, label your images effectively, train your model, and perform detection tasks efficiently. If issues persist, further troubleshooting methods can be explored to ensure smooth operation.