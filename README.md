# Laboratory-Work-4-Activity-Improving-CNN-Performance-Using-Regularization

## Google Colab Link: https://colab.research.google.com/drive/1KdYW12j_E1FJUR97rfISihkuKKEIlN64?usp=sharing

the model that load:  https://drive.google.com/drive/folders/1aEcz8betJWEE1dbamns0gTveOKz8Ktmg?usp=sharing

Model Link: https://drive.google.com/drive/folders/1IoJBMaHoNBhhaIUwI2K-PLa_it66cj2u?usp=drive_link
# GUIDE QUESTIONS (Student Explanation & Reflection)

## A. Model Evaluation Analysis

### 1. What were the weakest-performing classes based on the confusion matrix?
### Answer: The classes with the most off-diagonal values in the confusion matrix were the least well-performing ones, which are classes with similar appearance in the image. The flower/plant dataset classes with similar colors, leaf shapes, and leaf textures had the lowest precision and recall scores. The confusion matrix heat map was used to identify the misclassifications, which were displayed as bright cells that were not found in the diagonal.

### 2. How did Precision, Recall, and F1-score vary across classes?
### Answer: The baseline model received the following overall weighted scores: Precision 0.9285, Recall 0.9255 and F1-score 0.9254. There was a great deal of variation in individual classes. The classes with clearly and uniquely visual characteristics had scores that were around 1.0 in all three measurements, and those with similar visual characteristics to other classes had lower scores. This variation comes from the fact that the model is able to separate classes based on whether the classes are visually distinct from each other.

### 3. What does a low recall indicate in your model?
### Answer: A low recall of a particular class means that the model is not seeing many of the images of that class - it is failing to predict those images as being a different class. The model makes many errors on that class in other words. For instance, recall is low for flowers from the flower class when many images of this flower type are classified into a different flower class, although they are correctly annotated in the training data.

### 4. How does AUC score reflect model performance compared to accuracy?
### Answer: Our baseline model obtained an AUC score of 0.9738, which is excellent. Accuracy is just the percentage of the images correctly classified, while AUC reflects the model's ability to differentiate the class from the rest at all possible classification thresholds. AUC is a more representative indicator since it still has some value when there are minor class imbalance. High AUC—with near 1.0 indicating good discriminatory ability for all classes.

## B. Model Improvement

### 5. How did data augmentation affect validation accuracy?
### Answer: The accuracy of the validation set was improved from 92.55% (baseline) to 93.68% (improved model). The model was trained with a transformation, including random flips, rotations and zoom, which allowed it to learn more about each class of images in different representations. This made it difficult for the model to remember the exact training images, and caused the model to learn more general and stronger features, which led to improved performance with the validation images that were not seen during training.

### 6. Why is Batch Normalization important in CNNs?
### Answer: The idea of Batch Normalization is to ensure that activations are scaled and distributed in a similar way across the training process for each convolutional layer. We added BatchNormalization layers after each Conv2D layer on our improved model. This helped stabilize the training process by not having exploding or vanishing gradients, also used higher learning rates because it wasn't sensitive to the initialization of the weights and it was also a mild regularizer which led to more consistent and stable training overall.

### 7. What role did Dropout play in improving your model?
### Answer: After the convolutional block and the dense layer, dropout with a rate of 0.3 was used. In the training process, the Dropout was used to turn off some of the neurons randomly during each forward propagation step, so that the remaining ones acquired more independent and robust features. This helped the model not to overfit the training data. This is demonstrated by the decrease in the generalization gap from 2.53% in the baseline to 0.07% in the improved model.

### 8. How did Early Stopping prevent overfitting?
### Answer: I used early stopping with a patience of 5 epochs and used the best weights when I stopped. Training was stopped if validation loss did not get better for 5 epochs. This means that the model wouldn't be able to be trained beyond the optimal point where the loss for training continues to drop, while the loss for validation begins to rise — a common characteristic of overfitting. These callbacks along with ReduceLROnPlateau made it possible to ensure the model converged to the best possible generalization point.

## C. Performance Comparison

### 9. What improvements were observed after modifying the model?
### Answer: The following improvements were observed:

Validation Accuracy: 92.55% → 93.68% (improved)
Precision: 0.9285 → 0.9373 (improved)
Recall: 0.9255 → 0.9368 (improved)
F1-score: 0.9254 → 0.9363 (improved)
Generalization Gap: 2.53% → 0.07% (near-perfect generalization)

Training accuracy slightly decreased from 95.08% to 93.75%, which is expected and intentional — it indicates the model stopped memorizing and started truly generalizing.

### 10. Which enhancement contributed the most to performance improvement? Why?
### Answer: The batch normalization and L2 Regularization gave the maximum contribution. The use of BatchNormalization during training helped to normalize the activations within the layers, reducing the tendency for the model to overfit. L2 regularization introduced a small penalty on large weights, further preventing overfitting. The result was a dramatic decline in the generalization gap from 2.53% to 0.07%, meaning that the model changed from mere memorization of training data to learning true, transferable features.

### 11. Did the gap between training and validation accuracy decrease? Explain.
### Answer: Yeah ok the gap decreased pretty hard — from 2.53% in the baseline model, to 0.07% in the improved model. I mean, that change happened because all the regularization stuff worked together, like Dropout stopped neuron co-adaptation, BatchNormalization made the layer outputs more stable, L2 regularization kinda penalized larger weight magnitudes, and data augmentation basically increased the diversity of the training samples. Also Early Stopping made sure training stopped at the best moment, not too late. When the generalization gap is basically near zero, it means the model behaves almost the same on training and on unseen validation data, so it generalizes really well.

## D. Explainability (Grad-CAM Integration)

### 12. How did Grad-CAM help in understanding model predictions?
### Answer: Grad-CAM produced those visual heatmaps overlaid on the input images, and honestly they kinda make it clear what regions mattered most for the model’s classification call. Instead of treating the CNN as a total black box, Grad-CAM helped us, visually, check whether the model was fixated on actual plant or flower cues, like leaf form, color tone, or surface texture, or if it was paying attention to irrelevant background areas. That way we got a more straightforward look at the model’s internal way of thinking, rather than guessing in the dark.

### 13. Did the improved model focus on more relevant regions? Provide evidence.
### Answer: Yes. When Grad-CAM was applied to the test image (ChineseCroton), the heatmap of the improved model looked a lot more concentrated and focused on the leaf and plant body areas compared to the baseline model, which showed activations that were sort of scattered around. I mean this improvement seems like it’s a direct outcome of the regularization methods we used, especially BatchNormalization and Dropout, they essentially pressured the model to pick up more meaningful and spatially consistent features, instead of leaning on background patterns.

### 14. Why is explainability important in real-world AI applications?
### Answer: Explainability is critical in real world AI applications because it builds trust, accountability, and transparency in how a model decides. In high stakes areas like medical diagnosis, agricultural disease spotting, or environmental monitoring, people really want to get a sense of why a model made that specific call  not only what it output. If the system can’t explain itself, then mistakes can be harder to catch and fix before deployment, so the whole thing can drift into trouble. Techniques such as Grad-CAM and related methods help developers see whether the model is actually looking at the right cues or if it is latching onto some irrelevant feature set. Also, explainability is becoming more and more of a requirement in ethical rules and regulatory frameworks, for using AI in a responsible way.
