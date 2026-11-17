# Traffic Sign Detection Using YOLO11n

An object detection project using **YOLO11n** to detect and classify traffic signs across 17 categories. The project includes dataset inspection, annotation analysis, model training, cross-validation, and independent test evaluation.

## Project Overview

Traffic sign detection is an important computer vision task for intelligent transportation systems and driver assistance applications.

The objective of this project is to develop an object detection model capable of identifying traffic signs and locating them within road images.

The project follows a structured workflow, starting with dataset inspection and preparation, followed by model training, cross-validation, and evaluation on an independent test set.

## Dataset

The project uses the **German Traffic Sign Detection Benchmark (GTSDB)** dataset obtained through Roboflow.

| Property          | Description         |
| ----------------- | ------------------- |
| Task              | Object Detection    |
| Number of classes | 17                  |
| Training images   | 606                 |
| Validation images | 58                  |
| Test images       | 26                  |
| Image dimensions  | 300 × 300 pixels    |
| Annotation format | YOLO Bounding Boxes |
| Dataset license   | CC BY 4.0           |

### Dataset Preparation and Analysis

Before training, the dataset was inspected to assess its structure and annotation quality.

The analysis included:

- Checking image and label file consistency.
- Inspecting empty and annotated label files.
- Analyzing class distribution across dataset splits.
- Examining bounding box dimensions and object sizes.
- Reviewing sample images and their annotations.
- Excluding one class (`road narrows`) because it had no training or validation instances.

The final model was trained on 17 traffic sign classes.

## Methodology

### 1. Data Preparation

The training and validation subsets were combined to create a development dataset containing 664 images.

A **3-Fold Multilabel Stratified Cross-Validation** strategy was applied to evaluate model performance across different data partitions while maintaining a more balanced class distribution.

### 2. Model Training

The project uses **YOLO11n**, a lightweight object detection model initialized with pretrained weights.

Main training configuration:

| Parameter               | Value           |
| ----------------------- | --------------- |
| Model                   | YOLO11n         |
| Framework               | Ultralytics     |
| Input image size        | 640 × 640       |
| Batch size              | 16              |
| Maximum epochs          | 80              |
| Early stopping patience | 20              |
| Cross-validation folds  | 3               |
| Training environment    | Google Colab    |
| GPU                     | NVIDIA Tesla T4 |

Each cross-validation fold was trained independently using pretrained YOLO11n weights.

### 3. Final Model Training

After cross-validation, the final model was trained using the combined training and validation data.

The final training duration was set to **48 epochs**, based on the average best epoch observed across the three folds.

### 4. Model Evaluation

The final model was evaluated on the independent test set, which was not used during training or cross-validation.

Evaluation metrics included:

- Precision
- Recall
- mAP\@50
- mAP\@50–95
- Confusion Matrix
- Visual inspection of predicted bounding boxes

## Results

### Cross-Validation Results

The following table presents the results obtained across the three validation folds.

| Fold     |  Precision |     Recall |    mAP\@50 | mAP\@50–95 |
| -------- | ---------: | ---------: | ---------: | ---------: |
| Fold 1   |     63.50% |     60.90% |     70.70% |     44.30% |
| Fold 2   |     84.00% |     60.50% |     72.60% |     47.20% |
| Fold 3   |     88.90% |     57.70% |     76.80% |     52.70% |
| **Mean** | **78.80%** | **59.70%** | **73.37%** | **48.07%** |

### Independent Test Results

The final model was evaluated on 26 test images containing 13 annotated traffic sign instances.

| Metric     | Test Result |
| ---------- | ----------: |
| Precision  |      39.15% |
| Recall     |      34.21% |
| mAP\@50    |      30.38% |
| mAP\@50–95 |      20.57% |

The test results indicate that the model's performance on the independent test set was considerably lower than its cross-validation performance.

## Error Analysis

To better understand the model's behavior, the evaluation included confusion matrix analysis and visual inspection of predictions.

The analysis revealed several challenges:

- False positive detections.
- Missed detections of annotated traffic signs.
- Classification errors between visually similar categories.
- Difficulties detecting small traffic signs.

Dataset inspection also revealed that many images had empty annotation files. Some of these images appeared to contain traffic signs during visual inspection, suggesting possible annotation-quality issues that may affect model evaluation.

## Limitations

Several limitations should be considered when interpreting the results:

- The independent test set is very small, containing only 26 images and 13 annotated objects.
- The dataset contains a high proportion of empty annotation files, and some may include unannotated traffic signs.
- Small traffic signs are more challenging to detect.
- The difference between cross-validation and test performance suggests limited generalization on the available test set.

Therefore, the reported test metrics should be interpreted cautiously and should not be considered sufficient evidence of reliable real-world deployment performance.

## Technologies and Tools

- Python
- PyTorch
- Ultralytics YOLO11
- OpenCV
- NumPy
- Matplotlib
- Google Colab
- Roboflow

## Skills Demonstrated

- Object Detection
- Computer Vision
- YOLO-based Model Training
- Dataset Inspection and Annotation Analysis
- Bounding Box Analysis
- Multilabel Stratified Cross-Validation
- Model Evaluation
- Confusion Matrix Analysis
- Error Analysis and Visualization

## Project Structure

```text
YOLO-Traffic-Sign-Detection/
│
├── YOLO-traffic-sign-detection.ipynb
├── README.md
└── requirements.txt
```

## How to Run

1. Clone the repository:

```bash
git clone https://github.com/shahed127/YOLO-Traffic-Sign-Detection.git
cd YOLO-Traffic-Sign-Detection
```

2. Install the required dependencies:

```bash
pip install -r requirements.txt
```

3. Download the dataset and configure its path in the notebook.
4. Open the notebook in Google Colab or Jupyter Notebook.
5. Run the cells sequentially to reproduce the dataset analysis, training, and evaluation workflow.

## Future Improvements

Potential directions for further development include:

- Using a larger and more diverse dataset.
- Reviewing and correcting potentially missing annotations.
- Improving small-object detection.
- Exploring alternative YOLO model sizes and configurations.
- Evaluating the model on a larger independent test set.

---

**Project Type:** Computer Vision | Object Detection
**Model:** YOLO11n
**Dataset:** German Traffic Sign Detection Benchmark (GTSDB)
