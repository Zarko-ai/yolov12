# YOLOv12

This repository contains the implementation of a modified version of **YOLOv12**, along with the original YOLOv12 and previous versions including **YOLOv11**, **YOLOv10**, and **YOLOv8**.

The project is structured into multiple folders for clarity and organization.

---

## Folder Structure

### `model-weights/`
Contains the pretrained weights for all versions of YOLO implemented in this project:
- YOLOv8
- YOLOv10
- YOLOv11
- Original YOLOv12
- YOLOv12-Modified (small, medium, large, sm, ml)

### `yaml files/`
Includes the YAML configuration files for each model version.

### `object size classifier/`
This repository also includes a simple program designed to classify objects based on their **size distribution** within the dataset. 


##  Running a YOLOv12 Version (Modified or Original)

To run any YOLO version from this repository (e.g., YOLOv12-Modified), follow these steps:

---

###  Step 1: Install Required Dependencies

Ensure you're using the correct versions of **Ultralytics** and **Weights & Biases**:

```bash
pip install ultralytics==8.3.78 wandb==0.19.7
```

---

###  Step 2: Initialize Weights & Biases (Optional but Recommended)

Use [Weights & Biases (wandb)](https://wandb.ai/) to track your experiments, compare runs, and visualize performance:

```python
import wandb

wandb.init(
    project="name-of-the-project",  # Replace with your project name
    name="name-of-this-run"         # Replace with the specific run name
)
```

---

###  Step 3: Load the YOLOv12 Model

You can load the model architecture from a custom `.yaml` file.

```python
from ultralytics import YOLO

model = YOLO('/kaggle/working/yolov12.yaml', task="detect")
model = YOLO('/kaggle/working/yolov12.yaml').load('yolo12n.pt')
```

---

###  Step 4: Train the Model

Train your selected YOLO version using your custom dataset:

```python
model.train(
    project="YOLOv12",                    # Logs and results will be saved under this project folder
    data="path/to/data.yaml",            # Path to your dataset YAML file
    epochs=150,                          # Number of training epochs
    imgsz=640,                           # Input image size
    name="yolov12-medium",     # Name of this specific training run
    batch=16                             # Batch size
)
```

---

###  Notes

- Your `data.yaml` file should include:
  ```yaml
  train: path/to/train/images
  val: path/to/val/images
  nc: 3  # Number of classes
  names: ['class1', 'class2', 'class3']
  ```

- Training results, model checkpoints, and logs will be saved inside a directory named after the `project` and `name`.

- Using `wandb` is optional, but it provides powerful tools for logging metrics, viewing model performance, and comparing runs.
