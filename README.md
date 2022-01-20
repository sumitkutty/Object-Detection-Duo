# Object Detection for Car/Person

## Objective
Develop a model to detect and classify 'Car' and 'Person' in the given dataset

## Dataset
Number of Images: 2239
Total Classes: 2
Classes: ```Person``` and ```Car```
val split: 7 percent (156 Images)
Images in train set after Augmentation: 6249
Images in val set: 156 


## Model used
### **Yolov5**
* The model used for this use-case was yolov5 which is a SSD(single shot detector) algorithm that divides images into a grid system and the convolutional network in each cell is responsible for detecting objects within itself.
* Yolo is a favourite choice in object detection because of its speed and accuracy.

## Analysis
* The dataset has over 2239 images which can be considered inadequate  with a chunk of it being used for validation.
* The annotations for the dataset was in the form of COCO json, which is incompatible with the annotation yolo uses (yolo txt).


## Pre-Processing
* The dataset was split into train and val sets with the val set having over 7% of the total images.
* The train set was augmented to increase the number of instances with consideration to their annotation files.
* Each image in the train set was augmented twice to create 2 augmented copies for each image.
* The coco json annotation format was converted into yolo txt format using a script.

## Training
### **Config**
* Optimizer: Adam
* lr: 
* Batch: 64
* Epochs: 100 + 50
* Image: (3,640,640)

### Process
* The primary model was trained for 100 epochs to achieve an average loss of 0.04.
* To further improve performance, the best weights from the primary model were used to further train the model by freezing the backend.







## Recommendations
* Experimenting with different optimizers
* Spatial Augmentations
* Training with multi-shot models if slower training and inference latency can be tolerated.
* Freezing the backend of the network and training the head for longer epochs
* Using a Larger Yolov5 model


## Results
### Metrics:
* mAP@0.5 -> 0.642
* Precision -> 0.719
* Recall    -> 0.592
* F1-Score -> 0.65


### Inference Results
* Threshold: 0.3
* Inference Time: 37ms 
  COLLAGE PICTURE

### Confusion Matrix Analysis
PICTURE

ANalysis:
1
2
3

## Losses
LOSSES TABLE
* Train losses are lower in other models, but in our model, the vall loss is the lowest and hence got better generalization 

