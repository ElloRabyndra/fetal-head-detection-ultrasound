# Fetal Head Detection in Ultrasound Images

A machine learning project for detecting and identifying anatomical structures in fetal head ultrasound scans, specifically focusing on the trans-ventricular plane.

## Project Overview

This project implements **deep learning techniques** to automatically detect and localize three critical anatomical structures in fetal ultrasound images:

### Target Structures

| Structure | Abbreviation            | Medical Significance                                   |
| --------- | ----------------------- | ------------------------------------------------------ |
| **Brain** | -                       | Full fetal head region boundary                        |
| **CSP**   | Cavum Septum Pellucidum | Midline brain structure used for biometric assessment  |
| **LV**    | Lateral Ventricle       | Brain fluid-filled cavity for developmental assessment |

### Detection Method

The detection is performed on **trans-ventricular ultrasound plane images** using:

- Deep neural networks for feature extraction
- Object detection models for localization
- Bounding box annotations for precise structure identification

## Dataset

The dataset is organized in the `Trans-ventricular/` directory with comprehensive annotations:

### Dataset Contents

| Component           | Description                                                               |
| ------------------- | ------------------------------------------------------------------------- |
| **Training Images** | Ultrasound images from multiple patients (DICOM or standard image format) |
| **Annotations**     | Ground truth bounding box coordinates for each anatomical structure       |
| **Image Sets**      | Training/validation splits in standard format                             |
| **Label Maps**      | Color-coded labels for reference and visualization                        |
| **Metadata**        | Patient information and image rotation metadata                           |

### Dataset Statistics

- **Total Patients**: 40+ unique patient cases
- **Image Planes**: Trans-ventricular plane (Plane 3)
- **Annotation Format**: YOLO and Pascal VOC compatible formats
- **Ground Truth Files**: Individual `.txt` files per image with bounding box coordinates

### Label Classes

| Class      | RGB Value   | Color | Description                       |
| ---------- | ----------- | ----- | --------------------------------- |
| Brain      | (255, 0, 0) | Red   | Full fetal head boundary          |
| CSP        | (0, 255, 0) | Green | Cavum Septum Pellucidum structure |
| LV         | (0, 0, 255) | Blue  | Lateral Ventricle structure       |
| Background | (0, 0, 0)   | Black | Background region                 |

## Repository Structure

```
fetal-head-detection-ultrasound/
├── fetal_head_detection_ultrasound.ipynb    # Main Jupyter notebook for training & inference
├── README.md                                 # Project documentation
├── Trans-ventricular/                       # Primary dataset directory
│   ├── annotations/                         # Ground truth annotations
│   │   ├── bbox_labels_600_hierarchy.json
│   │   ├── class-descriptions.csv
│   │   └── default-annotations-bbox.csv
│   ├── default/                             # Label data files
│   │   └── gt_Patient*.txt                  # Ground truth bounding boxes
│   ├── ImageSets/                           # Training/validation splits
│   ├── masks/                               # Segmentation masks
│   ├── SegmentationClass/                   # Class segmentation data
│   ├── SegmentationObject/                  # Object segmentation data
│   ├── obj_train_data/                      # Training data
│   ├── default.tfrecord                     # TensorFlow record format
│   ├── labelmap.txt                         # Label mapping file
│   ├── obj.names                            # Class names
│   └── train.txt                            # Training file list
├── models/                                  # Trained model checkpoints
│   └── best_model.pt                        # YOLOv5/PyTorch model
├── files/                                   # Additional project files
└── images/                                  # Output/result images
```

## Requirements

| Dependency       | Version | Purpose                           |
| ---------------- | ------- | --------------------------------- |
| Python           | 3.7+    | Core programming language         |
| Jupyter Notebook | Latest  | Interactive notebook environment  |
| OpenCV           | Latest  | Image processing and manipulation |
| NumPy            | Latest  | Numerical computations            |
| PyTorch          | Latest  | Deep learning framework           |
| Matplotlib       | Latest  | Data visualization                |
| scikit-learn     | Latest  | Machine learning utilities        |

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/ElloRabyndra/fetal-head-detection-ultrasound.git
cd fetal-head-detection-ultrasound
```

### 2. Install Required Packages

```bash
pip install -r requirements.txt
```

### 3. Launch the Jupyter Notebook

```bash
jupyter notebook fetal_head_detection_ultrasound.ipynb
```

## Usage

The main workflow is contained in the Jupyter notebook with the following pipeline:

| Step                      | Description                                             |
| ------------------------- | ------------------------------------------------------- |
| **1. Data Loading**       | Load and preprocess ultrasound images from the dataset  |
| **2. Model Architecture** | Define or load the object detection model               |
| **3. Training**           | Train the model on annotated images with bounding boxes |
| **4. Evaluation**         | Test model performance using validation metrics         |
| **5. Inference**          | Run detection on new ultrasound images                  |
| **6. Visualization**      | Display detection results with bounding boxes           |

### Quick Start

1. Open the notebook: `fetal_head_detection_ultrasound.ipynb`
2. Run all cells sequentially from top to bottom
3. Check the `images/` directory for visualization outputs

### Output Format

Detection coordinates are stored in `.txt` format:

```
x1 y1 x2 y2 (top-left x, top-left y, bottom-right x, bottom-right y)
```

## Model Details

The project implements state-of-the-art object detection techniques to localize anatomical structures:

### Architecture Features

- **Bounding Box Regression**: Precise localization of three anatomical structures
- **Multi-class Classification**: Detection of Brain, CSP, and LV simultaneously
- **Data Augmentation**: Enhanced model generalization through image transformations
- **Validation Metrics**:
  - Precision: Accuracy of positive predictions
  - Recall: Coverage of actual objects
  - mAP (mean Average Precision): Overall detection performance

### Model Checkpoint

Pre-trained model available at:

```
models/best_model.pt
```

Load and use the model for inference on new ultrasound images.

## Results

### Output Files

Detection results are organized as follows:

| Output Type       | Location                     | Format  | Description                           |
| ----------------- | ---------------------------- | ------- | ------------------------------------- |
| Visualized Images | `images/`                    | PNG/JPG | Ultrasound images with bounding boxes |
| Bounding Boxes    | `Trans-ventricular/default/` | `.txt`  | Coordinate annotations (x1 y1 x2 y2)  |
| Metrics           | Console/Notebook             | Numeric | Precision, Recall, mAP scores         |

### Expected Performance

- **Detection Accuracy**: Multiple anatomical structures per image
- **Annotation Format**: YOLO/Pascal VOC compatible format
- **Visualization**: Color-coded bounding boxes:
  - Red: Brain
  - Green: CSP
  - Blue: LV

## Contributing

We welcome contributions to improve this project! Here's how you can help:

### Ways to Contribute

- **Bug Reports**: Report issues via GitHub Issues
- **Feature Requests**: Suggest improvements and enhancements
- **Pull Requests**: Submit code improvements and fixes
- **Documentation**: Enhance project documentation
- **Dataset Improvements**: Contribute annotated data

### Guidelines

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Make your changes with clear commit messages
4. Push to your branch (`git push origin feature/improvement`)
5. Open a pull request with detailed description

## License

This project is provided **as-is** for research and educational purposes.

Licensing details:

- **Usage**: Research and educational use permitted
- **Restrictions**: Check individual dependencies for their licenses
- **Disclaimer**: No warranty provided; use at your own risk

## Contact & Support

For questions, inquiries, or collaboration opportunities:

- **Project Owner**: ElloRabyndra
- **GitHub**: [ElloRabyndra/fetal-head-detection-ultrasound](https://github.com/ElloRabyndra/fetal-head-detection-ultrasound)
- **Issues**: Use GitHub Issues for bug reports and feature requests

---

**Last Updated**: 2026  
**Status**: Active Development

## References

This project addresses important applications in fetal ultrasound imaging:

### Clinical Applications

- **Prenatal Screening**: Early detection of developmental anomalies
- **Biometric Measurements**: Automated measurement of fetal structures
- **Anomaly Detection**: Identification of structural abnormalities
- **Clinical Decision Support**: Assistance for healthcare professionals

### Technical Background

The **trans-ventricular plane** is a standard anatomical plane in fetal ultrasound imaging used for:

- Assessing fetal brain development
- Measuring brain structures (ventricles, CSP)
- Evaluating neurological development
- Detecting potential complications

### References for Further Reading

For more information on fetal ultrasound analysis and object detection in medical imaging, refer to:

- YOLO (You Only Look Once) documentation
- PyTorch deep learning framework
- Medical image analysis literature on fetal assessment
