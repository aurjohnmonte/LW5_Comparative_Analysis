# CNN Image Classification — Final Report

## Overview
This project implements and compares multiple pre-trained CNN models for image classification using transfer learning. Grad-CAM is applied for model explainability.

## Models Used
- VGG16
- ResNet50
- MobileNetV2
- Teachable Machine model
- Custom models (1st, 2nd, Enhancement, Best)

## Dataset
- Path: `ImageDataset/`
- Split: 80% train / 20% validation
- Image size: 224×224

## Project Structure
```
├── notebook.ipynb         # Main Colab notebook
├── README.md              # This file
├── visualizations/
│   ├── confusion_matrices/
│   ├── roc_curves/
│   ├── gradcam_comparison.png
│   └── gradcam_all_models.png
└── guide_questions.md     # Final reflection answers
```

## How to Run
1. Open `notebook.ipynb` in Google Colab
2. Mount Google Drive and set `dataset_path`
3. Run all cells in order
4. Grad-CAM outputs saved to Drive automatically

## Results Summary
See Part 12 comparison table in the notebook.

## Key Findings
- Best model: [fill in]
- Highest accuracy: [fill in]
- Best F1-score: [fill in]
- Grad-CAM insight: [fill in]

## References
- TensorFlow / Keras documentation
- Grad-CAM: Selvaraju et al. (2017)
- ImageNet pre-trained weights
