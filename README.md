# Object Detection for Car/Person

## Objective
Develop a model to detect and classify ```Car``` and ```Person``` in the given dataset

## Dataset
Number of Images: 2239 <br />
Total Classes: 2 <br />
Classes: ```Person``` and ```Car``` <br />
val split: 7 percent (156 Images) <br />
Images in train set after Augmentation: 6249  <br />
Images in val set: 156 <br />

## Links
Dataset: https://evp-ml-data.s3.us-east-2.amazonaws.com/ml-interview/openimages-personcar/trainval.tar.gz <br />
Model: https://www.github.com/ultralytics/yolov5

## Model used
### **Yolov5**
* The model used for this use-case was yolov5 which is a SSD(single shot detector) algorithm that divides images into a grid system and the convolutional network is responsible for detecting objects in each cell.
* Yolo is a favourite choice in object detection because of its speed and accuracy.

## Analysis
* The dataset has over 2239 images which can be considered inadequate  with a chunk of it being used for validation.
* The annotations for the dataset was in the form of COCO json, which is incompatible with the annotation yolo uses (yolo txt).


## Pre-Processing
* The dataset was split into train and val sets with the val set having over 7% of the total images.
* The train set was augmented to increase the number of instances with consideration of annotation files.
* Each image in the train set was augmented twice to create 2 augmented copies for each image.
* The coco json annotation format was converted into yolo txt format using a script.

## Training
### **Config**/**Hyperparameters**
* Optimizer: Adam
* lr: 1e-3
* Batch: 64
* Epochs: 100 + 50
* Image Dimension: (3,640,640)

### **Process**
* The primary model was trained for 100 epochs to achieve an average loss of 0.04.
* To further improve performance, the best weights from the primary model were used to further train the model by freezing the backend.






## Results
### Metrics:
* mAP @0.5 -> 0.642
* Precision -> 0.719
* Recall    -> 0.592
* F1-Score -> 0.65


### **Inference Results**
* Threshold: 0.3
* Inference Time: 37ms <br />
  
<img src="https://user-images.githubusercontent.com/42680059/150337366-867dd373-a95f-426d-a1cc-9ccbd4df7e48.jpg" width = "450" height = "450">

### **Confusion Matrix**
<img src="https://user-images.githubusercontent.com/42680059/150335217-270f9e5b-bf32-4106-8e38-9c54cdfcc34a.png" width = "500" height = "400">

#### **Analysis**:
* 65% of all ```Person``` class examples were classified  as ```Person```. Hence the recall for ```Person``` class is 65%.
* 66% of all ```Car``` class examples were classified as ```Car```. Hence the recall for ```Car``` class is 66%.
* 25% of background detections were misclassified as ```Car```. These would be **```FALSE POSITIVES```** for ```Car```.
* 75% of background detections were misclassified as ```Person```. These would be **```FALSE POSITIVES```** for ```Person```.
* No Examples of ```Person``` were misclassifed as ```Car```.
* No Examples of ```Car``` were misclassifed as ```Person```.
* 34% of ```Person``` Class detections were misclassified in the background. These would be **```FALSE NEGATIVES```** for class ```Person```.
* 34% of ```Car``` Class detections were misclassified in the background. These would be **```FALSE NEGATIVES```** for class ```Car```.


## Losses
<img src="https://user-images.githubusercontent.com/42680059/150339627-aa22eeec-61d3-467f-a230-8ecb8e3e747c.png" width = "700" height = "150">

* From the above table, it can be observed that the train losses are better for other models. 
* However, ```yolov5medcontinued-froznet``` has the lowest val losses for box, class and object.


## Conclusion
* The model performs adequately well with the used hyperparameters. The performance can be improved by using different combinations of hyperparameters and models. 


## Recommendations
* Experimenting with different optimizers
* Spatial Augmentations
* Training with multi-shot models if slower training and inference latency can be tolerated.
* Freezing the backend of the network and training the head for longer epochs
* Using a Larger Yolov5 model
