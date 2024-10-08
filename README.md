# YOLOv5 Object Detection Setup Guide

### Steps to Set Up YOLOv5 for Object Detection

1. **Install Anaconda**  
   Download and install [Anaconda](https://www.anaconda.com/) to manage environments and dependencies.

2. **Install Labeling Tool**  
   Install a labeling tool from the [YOLOv5 Labeling Guide](https://github.com/ultralytics/yolov5/wiki/Labeling) to annotate your dataset.

3. **Clone the YOLOv5 Repository**  
   After installing Anaconda, open a terminal and run the following command:
   ```bash
   conda create -n yolov5 python=3.10
   ```
   ![cmd_ugwyutOp1P](https://github.com/user-attachments/assets/63f610b4-6c4c-48fc-823e-5916369d4c1e)


5. **Navigate to the Cloned Repository**  
   Move to the cloned repository directory:
   ```bash
   cd yolov5
   ```

6. **Set Up the YOLOv5 Environment**  
   Create and activate a new Python environment using Anaconda:
   ```bash
   git clone https://github.com/ultralytics/yolov5
   cd yolov5
   conda create -n <NAME_OF_ENV> python=3.10
   conda activate <NAME_OF_ENV>
   pip install -r requirements.txt
   ```

7. **Configure the Dataset**  
   Edit the file `<project_root>/yolov5/data/custom.yaml` to match your dataset. For example, if you are detecting faces, the configuration will look like this:
   ```yaml
   train: ../../train_data/images/train/  # Path to training images
   val: ../../train_data/images/val/      # Path to validation images

   # Classes
   names:
     0: face
     # Uncomment and add more classes if needed
     # 1: other_class
     # 2: another_class

   # Download script/URL (optional)
   download: https://github.com/ultralytics/assets/releases/download/v0.0.0/coco128.zip
   ```

8. **Train the Model**  
   In the `yolov5` directory, run the following command to start training:
   ```bash
   python train.py --img 640 --batch 16 --epochs 100 --data custom_data.yaml --weights yolov5s.pt --nosave --cache
   ```

   After training completes, a folder named `runs` and a `weights` folder will be created inside the `yolov5` directory, containing the results and model weights.

9. **Run Detection**  
   Use the trained model to perform detection on your test dataset:
   ```bash
   python detect.py --weights runs/train/exp/weights/last.pt --source ../../train_data/images
   ```

   The detection results will be saved in a new directory called `runs/detect/expX`, where you can find images with detected objects (e.g., "faces").

This setup guide will help you get started with YOLOv5 for object detection tasks efficiently.
