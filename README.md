# yolov5

# Steps to setup yolov5 Object Detection
1. Install [Anaconda](https://www.anaconda.com/).
2. Install [Labelling](https://github.com/ultralytics/yolov5/wiki/Labeling)

3. Clone this repository
```bash
git clone https://github.com/johnandreopoulos/yolov5
```

4. Open the cloned github repository you just cloned
5. Run the following command
```bash
git clone https://github.com/ultralytics/yolov5
cd yolov5
conda create -n <NAME_OF_ENV> python=3.10
conda activate <NAME_OF_ENV>
pip install -r requirements.txt
```

Based on your labels, in our case is "<b>face</b>" class from our labels.
- Edit file <b>/yolov5/data/custom.yaml</b>. Here is how it should look:
```bash
train: ../../train_data/images/train/ # train images (relative to 'path') 128 images
val: ../../train_data/images/val/ # val images (relative to 'path') 128 images

# Classes
names:
  0: face
  # 1: other_label_name_if_any
  # 2: other_label_name_if_any
  # 3: other_label_name_if_any
  # 4: other_label_name_if_any

# Download script/URL (optional)
download: https://github.com/ultralytics/assets/releases/download/v0.0.0/coco128.zip
```

6. Run the following command in the yolov5 folder and wait for it to finish.
```python
python train.py --img 640 --batch 16 --epochs 100 --data custom_data.yaml --weights yolov5s.pt --nosave --cache
```

After that, you should have a folder called "<b>runs</b>" in your yolov5 folder and a folder called "<b>weights</b>" in your yolov5 folder.
