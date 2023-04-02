# Common Test 1.Multi-Class Classification
The task is to build a model that can identify different types of lensing images, which are images of distant galaxies that are distorted by the gravity of a massive object in front of them. 

The model should be able to distinguish between images that have no substructure, images that have subhalo substructure, which are small clumps of dark matter, and images that have vortex substructure.

## Dataset
The [Dataset](https://drive.google.com/file/d/1B_UZtU4W65ZViTJsLeFfvK-xXCYUhw2A/view) Consists of 30k train images and 3k test images, all of size 1x150x150

![Task1 input](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/Task1.png?raw=true)

**Note:** The Original Directories names are **train** for the 30k one and **val** for the 3k one, but since we used it for testing we will call it test for the rest of the document.

## Data Preprocessing
The data is resized and the channels are duplicaetd ti make it 3 channels

## Evaluation Criteria
The model should be evaluated by how well it can separate the classes using a ROC curve and an AUC score, which measure the trade-off between true positive and false positive rates.

## Approach
The task of classifying lensing images can benefit from trying different architectures that trade-off between accuracy and latency.
- **MobileNetV3** small is a lightweight model that uses depth-wise convolutions, squeeze and excitation modules, and h-swish activation to achieve high accuracy with low latency. 
- **Resnet18** is a deeper model that uses residual connections, batch normalization, and ReLU activation to learn complex features with moderate latency. 
- **EfficientNetb5** is a scalable model that uses compound scaling, depth-wise separable convolutions, and swish activation to achieve state-of-the-art accuracy with high latency. Comparing these architectures can help to find the optimal balance between performance and resource consumption for the task.

## Results
### Summary
The Following table shows the results of the models on the test set (3k images)
|Model|Validation Loss|Validation Accuracy|Validation ROC AUC|
|-|-|-|-|
|EfficientNet b5|0.1710|95.88%|0.9931|
|Resnet18|0.2997|93.63%|0.9871|
|MobileNetV3_s|0.3270|88.67%|0.9741|

### ROC Curves

1. EfficientNet b5
![EfficientNet b5 ROC Curve](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/EffNetb5_ROC.png?raw=true)

2. Resnet18
![Resnet18 ROC Curve](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/Resnet18_ROC.png?raw=true)

3. MobileNetV3_s|
![MobileNetV3_s ROC Curve](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/MobileNetV3_ROC.png?raw=true)

### Confusion Matrices
<!-- make 2 images in one row -->


1. EfficientNet b5 
![EfficientNet b5 Confusion Matrix](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/EffNetb5_confusion_matrix.png?raw=true)

2. Resnet18 
![Resnet18 Confusion Matrix](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/Resnet18_confusion_matrix.png?raw=true)

3. MobileNetV3_s
![MobileNetV3_s Confusion Matrix](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/MobileNetV3_confusion_matrix.png?raw=true)

### Checkpoints
you can find the checkpoints of the 3 models [here](https://drive.google.com/drive/folders/1yjNUPtligEerNZlvzEfXuK-SqP5kNwvm?usp=share_link)
### Conclusion
- **EfficientNet b5** b5 model is the best model for this task, it has the highest accuracy and the highest ROC AUC score, but it is also the most computationally expensive model. 
- **Resnet18** model is the second best model, it has a lower accuracy and ROC AUC score, but it is also less computationally expensive. 
- **MobileNetV3_s** model is the worst model for this task, it has the lowest accuracy and ROC AUC score, but it is also the least computationally expensive model.

# Specific Test III. Learning Mass of Dark Matter Halo 
The task is to use machine learning to estimate the mass of dark matter halos around galaxies from images of gravitational lensing. Gravitational lensing is a phenomenon where the light from distant sources is bent by the gravity of massive objects in the foreground. 

By analyzing the shape and distortion of the lensed images, one can infer the properties of the dark matter halos that cause the lensing. 
## Dataset
The [Dataset](https://drive.google.com/file/d/1hu472ALwGPBcTCXSAM0VoCWmTktg9j-j/view) consists of 20k images of size 1x150x150, and it has been splitted into 81:9:10 for train, validation, and test respectively.

![Task3 input](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/Task3.png?raw=true)
## Data Preprocessing
The data is resized for EfficientNet b5 only, and the channels are duplicaetd ti make it 3 channels, horizontal and vertical flips are applied to the data randomly

## Approach
The same Approach in Task1 is used here, but the model is trained on the log of the mass of the halo, and the loss function is the mean squared error (MSE)

## Results
### Summary
The Following table shows the results of the models on the test set (2k images)
|Model|MSE Loss
|-|-|
|EfficientNet b5|4.8e-5|
|Resnet18|0.2997|6.8e-5|
|MobileNetV3_s|6.1e-5|

### Regression Plots (True vs Predicted)
1. EfficientNet b5
![EfficientNet b5 Regression Plot](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/Effnetb5_Reg.png?raw=true)

2. Resnet18
![Resnet18 Regression Plot](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/MobileNetV3_Reg.png?raw=true)

3. MobileNetV3_s
![MobileNetV3_s Regression Plot](https://github.com/0ssamaak0/ML4SCI-GSOC23-Tests/blob/master/imgs/Resnet18_Reg.png?raw=true)

### Checkpoints
you can find the checkpoints of the 3 models [here](https://drive.google.com/drive/folders/1Tmoi57-YvGRfJjatPR4xRGxAUE_-tUzX?usp=share_link)

### Conclusion
- **EfficientNet b5** b5 model is the best model for this task, it has the lowest MSE loss, but it is also the most computationally expensive model.

- **Resnet18** and **MobileNetV3_s** have similar MSE losses, but **MobileNetV3_s** is less computationally expensive than **Resnet18**.

