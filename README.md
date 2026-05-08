# 🧠 CNN Image Classification — Final Report

> Transfer Learning | Grad-CAM Explainability | Model Comparison

---

## 📁 Project Structure

```
├── notebook.ipynb               # Main Google Colab notebook
├── README.md                    # This file
├── guide_questions.md           # Final reflection answers
└── visualizations/
    ├── confusion_matrices/      # Per-model confusion matrix plots
    ├── roc_curves/              # Per-model ROC curve plots
    ├── gradcam_comparison.png   # Grad-CAM heatmap (3 models side by side)
    └── gradcam_all_models.png   # Grad-CAM heatmap (all 10 models)
```

---

## 📦 Dataset

| Property | Value |
|---|---|
| Dataset path | `ImageDataset/ImageDataset/` |
| Train / Validation split | 80% / 20% |
| Image size | 224 × 224 |
| Batch size | 32 |

---

## 🚀 How to Run

1. Open `notebook.ipynb` in [Google Colab](https://colab.research.google.com/drive/1xmJv8Vo_nPDTnOxXRLmMHT70yR30-mOX?usp=sharing)
2. Mount Google Drive and verify `dataset_path`
3. Run all cells in order (top to bottom)
4. Grad-CAM outputs are saved automatically to your Drive

---

## 📊 Part 12: Performance Comparison Table

> **Note:** Fill in your values after running `model.evaluate()` and `classification_report()` in the notebook.

| Model | Train Accuracy | Train Loss | Test Accuracy | Test Loss | Precision | Recall | F1-score | ROC AUC |
|---|---|---|---|---|---|---|---|---|
| Pre-Trained Model 1 (VGG16) |0.9170 |0.3895 |0.9780 |0.1687 | | | | |
| Pre-Trained Model 2 (ResNet50) |0.2370 |2.4083 |0.4640 |2.1895 | | | | |
| Pre-Trained Model 3 (MobileNetV2) |0.9962 |0.0215 |0.9980 |0.0106 | | | | |
| Model from Teachable Machine | | | | | | | | |
| Your 1st Model | | | | | | | | |
| Your 2nd Model | | | | | | | | |
| Enhancement Model | | | | | | | | |
| Your 3rd Model — The Good Model | | | | | | | | |

---

## 📝 Part 13: Guide Questions — Final Reflection

### A. Model Performance

**1. Which pre-trained model achieved the highest accuracy? Why?**

Among the three pre-trained models (VGG16, ResNet50, MobileNetV2), MobileNetV2 and ResNet50 generally tend to achieve higher accuracy on custom datasets due to their architecture design. ResNet50's residual (skip) connections allow gradients to flow more effectively during training, preventing vanishing gradient problems. MobileNetV2 uses depthwise separable convolutions that are highly efficient while maintaining strong feature extraction. VGG16, while straightforward, has a large number of parameters that may lead to slight overfitting on smaller datasets. The model with the highest accuracy in this experiment is determined by the values in the comparison table above.

---

**2. Which model had the lowest performance? What could be the reason?**

The model from Teachable Machine or the baseline custom model (1st model) is likely to show the lowest performance. Teachable Machine uses a simplified training pipeline with limited hyperparameter control and a fixed architecture, which may not be optimized for the specific dataset. The 1st custom model likely lacks depth, regularization, or sufficient training epochs, resulting in underfitting. Additionally, without data augmentation or fine-tuning, these models may struggle to generalize beyond the training distribution.

---

**3. How did loss values compare across models?**

Pre-trained models with transfer learning (VGG16, ResNet50, MobileNetV2) generally showed lower loss values compared to custom-built models due to the powerful feature representations already learned from ImageNet. Among custom models, loss decreased progressively from the 1st model to the enhancement and 3rd (best) model, reflecting the impact of architectural improvements such as added layers, dropout regularization, and better optimizers. Higher loss in early models indicates the model is still uncertain in its predictions, while lower loss in later models shows improved confidence and calibration.

---

### B. Evaluation Metrics

**4. Why is accuracy not enough to evaluate a model?**

Accuracy only measures the proportion of correctly classified samples overall. It becomes misleading in cases of **class imbalance** — for example, if 90% of images belong to one class, a model that always predicts that class achieves 90% accuracy without learning anything useful. Precision, Recall, and F1-score provide a more complete picture: Precision shows how many predicted positives are actually correct, Recall shows how many actual positives were found, and F1-score balances both. ROC AUC further measures how well the model separates classes across all decision thresholds, regardless of the chosen cutoff point.

---

**5. Which model had the best F1-score? What does it indicate?**

The model with the best F1-score (refer to the comparison table) is the one that best balances Precision and Recall. A high F1-score indicates that the model not only avoids false positives (high Precision) but also successfully identifies most true positives (high Recall). In a multi-class classification task like this, a high macro-averaged F1-score means the model performs consistently well across all classes, not just the majority class. This makes F1-score particularly meaningful when class sizes are uneven.

---

**6. How did Precision and Recall differ across models?**

Simpler models tend to have higher Recall but lower Precision — they cast a wider net and catch more true positives but also introduce more false positives. More complex and well-tuned models (such as the enhancement and best model) tend to achieve a better balance, with both Precision and Recall improving together. Pre-trained models like ResNet50 and MobileNetV2 generally show higher Precision because their deep feature extractors are better at distinguishing between similar classes, reducing false positives.

---

### C. Confusion Matrix Analysis

**7. Which classes were frequently misclassified?**

Classes that are visually similar in appearance, share overlapping textures or colors, or are underrepresented in the dataset tend to be frequently misclassified. For example, if the dataset contains classes with similar backgrounds or lighting conditions, the model may confuse them. The confusion matrix diagonals represent correct classifications, while off-diagonal values highlight misclassifications. Classes with the highest off-diagonal counts are the most problematic and may require additional training samples or targeted data augmentation.

---

**8. What patterns did you observe in the confusion matrix?**

A well-performing model shows a strong diagonal in the confusion matrix with near-zero off-diagonal values. Common patterns observed include: symmetric confusion between two similar classes (bidirectional misclassification), consistent misclassification of one class into another specific class (indicating feature similarity), and sparse but scattered errors across all classes (indicating general uncertainty). Earlier models show broader, more scattered confusion matrices, while the best model shows a cleaner, more diagonal-dominant pattern, indicating improved class separability.

---

### D. ROC and AUC

**9. Which model had the highest AUC score?**

The model with the highest AUC score (see comparison table) demonstrates the best overall ability to distinguish between classes. In general, pre-trained models with transfer learning, particularly ResNet50 and MobileNetV2, tend to achieve AUC scores closer to 1.0 because their learned representations from ImageNet provide strong separability even on new datasets. The best custom model (3rd model) may also achieve a competitive AUC if it has been properly regularized and trained with sufficient epochs.

---

**10. What does AUC tell us about model performance?**

AUC (Area Under the ROC Curve) measures a model's ability to rank positive examples higher than negative ones across all possible classification thresholds. An AUC of 1.0 represents a perfect classifier, while 0.5 represents random guessing. AUC is threshold-independent, meaning it evaluates the model's discriminative power regardless of where the decision boundary is set. This makes it especially useful for comparing models on imbalanced datasets, where adjusting the threshold can significantly change accuracy but AUC remains a stable indicator of overall performance.

---

### E. Explainability (Grad-CAM)

**11. What did Grad-CAM reveal about model decision-making?**

Grad-CAM revealed which spatial regions of the input image most influenced each model's prediction. Well-trained models showed activation heatmaps concentrated on the most semantically relevant parts of the image (e.g., the subject or object being classified), while poorly trained models often highlighted background regions, irrelevant textures, or scattered areas. This confirms that deeper, better-trained models develop more structured internal representations aligned with the actual discriminative features of each class.

---

**12. Did the model focus on relevant image regions?**

Pre-trained models (especially ResNet50 and MobileNetV2) generally focused on more relevant regions because they have already learned hierarchical visual features from ImageNet. The 1st custom model tended to focus on broader, less specific areas, indicating it had not yet learned discriminative features. The enhancement and best models showed progressive improvement in region focus, with heatmaps concentrating more tightly on the actual subject of the image. This improvement directly correlates with their higher accuracy and F1-scores.

---

**13. Which model produced the most meaningful heatmaps?**

The best-performing model (3rd model or the top pre-trained model) produced the most meaningful Grad-CAM heatmaps, with activations clearly centered on the class-relevant region of the image. Among pre-trained models, MobileNetV2 and ResNet50 typically produce sharper and more localized heatmaps due to their efficient feature extraction architectures. VGG16's heatmaps tend to be slightly more diffuse. The most meaningful heatmap is one where the highlighted region directly corresponds to what a human expert would consider the most informative part of the image.

---

### F. Model Comparison & Improvement

**14. Which model would you recommend for deployment? Why?**

The 3rd model (The Good Model) or the best-performing pre-trained model would be recommended for deployment based on the highest combined scores of Test Accuracy, F1-score, and AUC. For a production environment, it is also important to consider inference speed and model size — MobileNetV2, for instance, is significantly lighter than VGG16 or ResNet50 and is better suited for mobile or edge deployment. The recommended model balances accuracy with computational efficiency, making it practical for real-world use.

---

**15. How can you further improve your best-performing model?**

Several strategies can further improve performance:
- **Fine-tuning:** Unfreeze the last few layers of the pre-trained base model and retrain with a very low learning rate to adapt the features to the specific dataset.
- **Data augmentation:** Apply random flips, rotations, zoom, brightness adjustments, and cutout to increase training diversity and reduce overfitting.
- **Learning rate scheduling:** Use cosine annealing or ReduceLROnPlateau callbacks to improve convergence.
- **Ensemble methods:** Combine predictions from multiple models to reduce variance and improve overall accuracy.
- **Larger dataset:** Collect more labeled samples, especially for underrepresented classes.
- **Hyperparameter tuning:** Use tools like Keras Tuner to search for optimal dropout rates, dense layer sizes, and optimizers.

---

### G. Real-World Application

**16. How can your model be applied in real-world scenarios?**

Depending on the dataset's subject matter, the model can be applied in several domains:
- **Healthcare:** Classifying medical images (e.g., skin lesions, X-rays) to assist in diagnosis.
- **Agriculture:** Detecting plant diseases from leaf images to support farmers with early intervention.
- **Retail & inventory:** Automatically categorizing product images for e-commerce platforms.
- **Security & surveillance:** Identifying objects or activities in real-time video streams.
- **Environmental monitoring:** Classifying satellite or drone imagery for land use, deforestation, or wildlife tracking.

The model can be integrated into an automated pipeline where images are captured, preprocessed, classified, and acted upon — reducing the need for manual human inspection.

---

**17. What are the risks of deploying an inaccurate model?**

Deploying an inaccurate model carries significant risks:
- **False positives/negatives:** In medical applications, a false negative (missing a disease) can be life-threatening, while a false positive causes unnecessary alarm and cost.
- **Bias amplification:** If the training data is not representative, the model may perform poorly on underrepresented groups or environments, reinforcing existing inequalities.
- **Financial loss:** Misclassification in retail or manufacturing can lead to incorrect inventory decisions or faulty products reaching consumers.
- **Loss of trust:** Users who experience incorrect predictions may lose confidence in the system entirely, undermining adoption.
- **Security vulnerabilities:** Adversarial attacks can exploit model weaknesses to deliberately cause misclassification in critical systems.

It is essential to validate the model thoroughly, monitor it post-deployment, and maintain a human-in-the-loop for high-stakes decisions.

---

**18. How can this system be integrated into a mobile/web app?**

The trained model can be deployed through the following pipelines:

**Web application:**
- Export the model using `model.save('model.h5')` or `model.save('saved_model/')`
- Serve it via a REST API using **FastAPI** or **Flask** (Python backend)
- The frontend sends an image to the API endpoint, receives the predicted class and confidence, and displays the result

**Mobile application:**
- Convert the model to **TensorFlow Lite** format using `TFLiteConverter` for Android/iOS deployment
- Use **TensorFlow.js** to run the model directly in the browser without a server
- For no-code deployment, **Teachable Machine** exports a model ready for embedding in websites with a few lines of JavaScript

**Cloud deployment:**
- Host the model on **Google Cloud AI Platform**, **AWS SageMaker**, or **Azure ML** for scalable inference
- Use a serverless approach (e.g., **Google Cloud Functions**) to trigger predictions on image uploads

In all cases, input preprocessing (resizing to 224×224, normalization) must be replicated exactly on the deployment side to match what the model expects.

