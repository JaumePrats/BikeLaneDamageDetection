# BikeLaneDamageDetection
Detection and classification of bike lane damage using object detection. 

This repository is part of the degree thesis "Micromobility Safety Applications Using AI", submitted to the faculty Escola Tècnica d'Enginyeria de Telecomunicació de Barcelona UPC, by Jaume Prats.

The objective of this project is to develop a system to reinforce micro-mobility safety by detecting the damage on bike lanes. To achieve this goal, a dataset has been created and subsequently used to train an object detector. Afterward, a set of experiments has been conducted to explore different techniques used to improve the detection performance. 

The project has been developed using [MMDetection](https://github.com/open-mmlab/mmdetection) and the dataset created during this thesis.

## Content
* Custom configuration files used to train the models in MMDetection.
* Annotations of the dataset in PASCAL VOC and COCO format.

## BLDD Dataset
The Bike Lane Damage Detection 2021 Dataset is a dataset created during the four months of this project. It contains 370 images of bike lanes from the Barcelona Metropolitan Area with 677 instances of damages. The dataset is unbalanced with two under-represented classes.

The dataset contains annotations in PASCAL VOC and COCO format of the five following classes:
* D00 - Longitudinal Crack
* D10 - Transverse Crack
* D20 - Alligator Crack (under-represented)
* D40 - Pothole (under-represented)
* D50 - Manhole

The dataset has been divided between train set (70%), validation set (20%), and test set (10%):
* Train - 259 images
* Validation - 74 images
* Test - 37 images

## Experiments
A total of 6 experiments have been conducted in this thesis to try to increase the detector performance. Each corresponds to a configuration file:

### BLDD
The base detector from the project, used as a reference to evaluate the techniques applied in other experiments. It is based on the *faster_rcnn_r50_caffe_fpn_mstrain_1x_coco* config from MMDetection, which uses a Faster R-CNN network with an R50-FPN backbone.

### BLDD_BAL
In the second experiment, the unbalanced problem has been addressed by adding images from the [RDD2020 dataset](https://data.mendeley.com/datasets/5ty2wb6gvg/1) to the training set. A total of 153 images containing the two under-represented classes were added to achieve the balance of the training set. The resulting training set is composed of 412 images with 909 instances.

### BLDD_BAL100
This experiment intends to evaluate the effect that incrementing the dataset size has on the performance of the detector. Taking the balanced training set from the last experiment as a basis, an additional 100 images from the RDD2020 dataset have been added. Resulting in a training set of 512 images and 1119 instances. 

Unlike the experiments described above, in the following experiments, no modifications have been made to the initial dataset. These focus on the use of augmentation techniques during training.

### BLDD_DA_PIPELINE
In this experiment data augemntation is implemented on the fly in the configuration file. The following augmentation strategies are applied:
* Horizontal FLip
* Motion Blur
* Gaussian Noise
* Rotation (between -15 and 15 degrees)
* Brightness
* Cutout (8 squares of 25x25)
* Color Modification


### BLDD_DA_FLIP
To further evaluate the flip transform, this model uses only the horizontal flip augmentation during training.

### BLDD_DA_BLUR
To evaluate the effects of using blur augmentation, this model is trained using only Motion Blur transform.






