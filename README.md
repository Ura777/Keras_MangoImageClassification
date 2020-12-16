# Keras_MangoImageClassification
This project was inspired by [AI CUP 2020 Mango Image Recognition Challenge](https://aidea-web.tw/aicup_mango).  
The purpose of this challenge is helping mango farmers to classify the grade of mango quickly and robust.  
In this project, we try to use Keras to implement simple DenseNet121, ResNeXt50 and VGG16 in short time.

**Thanks for my teammates to finish this project together!!!**

## Grade description
* A: The mango has no blemishes and the color is even and beautiful.  
* B: The color of mango is uneven. If the defect area can be covered by a thumb, it can still be sold.
* C: Mango cannot be sold. It has dark spots, anthracnose and rotten.

## Dataset
There are 2 stages.   
In stage 1, competitors will get Train set and Development set.  
In stage 2, competitors will get Test set.

* Train set
  5600 images.   
  Each image has already labeled the grade, please check train.csv.   
  Use in training and validation.
  
* Development set
  800 images.  
  Each image has already labeled the grade, please check dev.csv.  
  Use in testing.

* Test set
  1600 images.  
  No labels.
 
Number of images per grade in the dataset:
Grade|Train set|Development set| Test set
-----|---------|---------------|---------
A|1792|243|blinded
B|2068|293|blinded
C|1740|264|blinded
Total|5600|800|blinded

## Data preprocess
According to offical document, the preprocessing are:
* Resize image as (224, 224)
* Rotate the image by angle, the degree is 15.
* Horizontally flip the image with given probability, the porbability is 0.5.
* Normalize the image with mean \[0.485, 0.465, 0.406\].

## Set up environment
* Google colab
* Python 3.6
* Tensorflow 1.X

## Model
Use Keras to implement:
* DenseNet121
* ResNeXt50
* VGG16

## Model parameters
All models are save best weights.  
Because of the limitation from Google colab, all models freeze some layers.  

**DenseNet121**
Parameter name|Value
--------------|-----
optimizer|SGD(lr=0.01, momentum=0.9)
loss|binary_crossentropy
metrics|accuracy
epochs|100
early stopping|10 epochs
batch_size|128

**ResNeXt50**
Parameter name|Value
--------------|-----
optimizer|SGD(lr=0.01, momentum=0.9)
loss|binary_crossentropy
metrics|accuracy
epochs|100
early stopping|10 epochs
batch_size|64

**VGG16**
Parameter name|Value
--------------|-----
optimizer|SGD(lr=0.01, momentum=0.9)
loss|binary_crossentropy
metrics|accuracy
epochs|100
early stopping|10 epochs
batch_size|128

## Predict accuracy
In "Model name" column, the R is ResNeXt50, V is VGG16, D is DenseNet121 and A is AlexNet.
R+V+D|65.688%|72.250%

Model name|Baseline|Keras
----------|--------|-----
DenseNet121|49.875%|61.188%
ResNeXt50|59.000%|64.188%
VGG16|65.250%|72.250%

## Ensemble learning - Voting
According to the predict accuracy, we can know VGG16 is better than DenseNet121 and ResNeXt50.  
So, the voting weights are:
Model name|Voting weights
----------|--------
DenseNet121|1
ResNeXt50|1
VGG16|3

## Ensemble learnig - Predict accuracy
In "Model name" column, the R is ResNeXt50, V is VGG16 and D is DenseNet121.
Model name|Baseline|Keras
----------|--------|-----
R+V+D|65.688%|72.250%

## Offical highest predict accuracy model vs. Keras
In "Model name" column, the A is AlexNet.
Model name|Predict Accuracy
----------|----------------
A+V+D|70.250%
R+V+D|72.250%


