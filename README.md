https://colab.research.google.com/drive/1NnH0QlhdY_fmTrRJjX3CJZZV7rRH-1Dz?usp=sharing



A. Model Performance
1. Which pre-trained model achieved the highest accuracy? Why?
EfficientNetB0 achieved the highest accuracy because it uses compound scaling to balance depth, width, and resolution efficiently. It also benefits from strong ImageNet pre-trained weights that transfer well to plant classification.
2. Which model had the lowest performance? What could be the reason?
ResNet50 had the lowest performance. It has more parameters and needs more training data and epochs to adapt properly. With only 10 epochs and a frozen base, it did not converge as well as the other two models.
3. How did loss values compare across models?
EfficientNetB0 had the lowest loss, MobileNetV2 was in the middle, and ResNet50 had the highest. All models showed slightly higher validation loss than training loss, which is normal and expected behavior.

B. Evaluation Metrics
4. Why is accuracy not enough to evaluate a model?
Accuracy is misleading when classes are imbalanced. A model can score high accuracy by just predicting the majority class. Precision, Recall, and F1-score reveal how well the model performs per class, giving a more complete and honest picture of performance.
5. Which model had the best F1-score? What does it indicate?
EfficientNetB0 had the best F1-score, indicating it maintained a strong balance between Precision and Recall across all plant species classes, meaning it was both accurate and thorough in its predictions.
6. How did Precision and Recall differ across models?
EfficientNetB0 had consistently high Precision and Recall. MobileNetV2 had slightly lower Recall on minority classes. ResNet50 showed the most inconsistency, with some classes having high Precision but noticeably lower Recall.

C. Confusion Matrix Analysis
7. Which classes were frequently misclassified?
Plant species that look visually similar — sharing leaf shape, color, or texture — were most frequently misclassified. Classes with fewer training images also showed higher misclassification rates.
8. What patterns did you observe in the confusion matrix?
Most correct predictions were along the main diagonal. Off-diagonal errors were clustered between visually similar species. EfficientNetB0 had the cleanest diagonal while ResNet50 showed the most scattered errors.

D. ROC and AUC
9. Which model had the highest AUC score?
EfficientNetB0 had the highest overall AUC score, with per-class values consistently close to 1.0, showing strong ability to distinguish each plant species from all others.
10. What does AUC tell us about model performance?
AUC measures how well a model separates classes across all possible thresholds. A score of 1.0 is perfect and 0.5 is random guessing. It is more reliable than accuracy because it is not affected by class imbalance or threshold selection.

E. Explainability (Grad-CAM)
11. What did Grad-CAM reveal about model decision-making?
Grad-CAM revealed which image regions most influenced the model's prediction. It showed that the models were generally focusing on the plant's physical features like leaves and stems rather than irrelevant background areas.
12. Did the model focus on relevant image regions?
Yes, especially EfficientNetB0, whose heatmaps were concentrated on the actual plant features such as leaf shape and texture. ResNet50 occasionally highlighted background regions, explaining some of its misclassifications.
13. Which model produced the most meaningful heatmaps?
EfficientNetB0 produced the most focused and accurate heatmaps. MobileNetV2 was also reasonably clear. ResNet50 produced the least consistent heatmaps, sometimes activating on non-relevant image areas.

F. Model Comparison & Improvement
14. Which model would you recommend for deployment? Why?
EfficientNetB0 is the best choice for deployment. It achieved the highest accuracy, best F1 and AUC scores, and produced the most meaningful Grad-CAM results, all while remaining computationally efficient for both web and mobile platforms.
15. How can you further improve your best-performing model?
Fine-tune the top layers of the base model, collect more images for underrepresented classes, apply stronger data augmentation, use learning rate scheduling, and consider ensembling EfficientNetB0 with another model to boost robustness.

G. Real-World Application
16. How can your model be applied in real-world scenarios?
The model can be used in agriculture for crop and weed identification, in conservation for field species surveys, in education as a plant identification learning tool, and in the herbal medicine industry to verify medicinal plant identity before processing.
17. What are the risks of deploying an inaccurate model?
Misclassification can lead to serious consequences such as using the wrong medicinal plant, failing to detect invasive species, or causing crop losses. It can also erode user trust and create bias against underrepresented plant varieties in the dataset.
18. How can this system be integrated into a mobile/web app?
The model can be converted to TensorFlow Lite for mobile apps where users capture a plant photo and receive instant predictions. For web apps, it can be served via a Flask or FastAPI backend that accepts image uploads and returns predictions as JSON responses.
