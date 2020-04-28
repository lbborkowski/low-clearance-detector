# Low Clearance Sign Detector
*Custom object detection model for low clearance signs*

Launch the Jupyter notebook in Google Colab by clicking on this badge: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lbborkowski/low-clearance-detector/blob/master/low_clearance_detector_200426.ipynb)

## Overview
This repository contains the files for a custom object detection model for low clearance signs. Low clearance signs are used to indicate bridges, overpasses, and tunnels with clearances below the standard height to avoid strikes from trucks or other large vehicles. Despite the presence of these signs throughout the U.S., bridge strikes occur hundreds of times per year. These strikes are in part caused by the use of consumer GPS apps by inexperienced drivers which direct them along routes that aren't suitable for their particular vehicle. The lack of a comprehensive database for low clearance bridges across the country prevent GPS systems from issuing a warning when a truck is approaching one of these bridges. Therefore, a custom object detection model was developed to detect low clearance signs from street view images. This type of model could either be used to help populate a database for low clearance signs or it could be run in real time on dashboard camera footage to provide the driver with an early warning. 

The custom object detection model for low clearance signs was developed using the [TensorFlow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection) and run in [Google Colaboratory](https://colab.research.google.com/notebooks/welcome.ipynb). The input is dashcam images which include at least one labeled low clearance sign. Once trained, the model localizes and classifies these signs in unlabeled images.

## Training

The model was trained on 125 images taken from [OpenStreetCam](https://openstreetcam.org/) along the Merritt Parkway which runs between central Connecticut and New York City. Trucks and buses are prohibited on this limited-access parkway because of its low bridges however certain bridges along this route have been struck more than a hundred times over the last decade as discussed in this [article](https://www.governing.com/community/Truck-Hits-Overpass-and-Inspiration-Hits-Blumenthal.html). Throughout training, testing/evaluation was performed on a set of 24 unique images. Low clearance signs in the training and test sets were labeled using [labelImg](https://github.com/tzutalin/labelImg). The procedure provided [here](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/training.html#) was followed to convert the *.xml files output from labelImg to *.csv and then to *.record files which are required for TensorFlow. A selection of labeled training images is shown in Figure 1.

![](/READMEimages/train_01.png) ![](/READMEimages/train_02.png) ![](/READMEimages/train_11.png) ![](/READMEimages/train_04.png) ![](/READMEimages/train_06.png) ![](/READMEimages/train_07.png) ![](/READMEimages/train_08.png) ![](/READMEimages/train_10.png)
> *Figure 1: Selection of labeled training images*

Transfer learning was employed for the custom object detection model by starting with a pre-trained model. The model architecture used was faster_rcnn_inception_v2 trained on the COCO dataset, obtained from the [TensorFlow Detection Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md). A faster rcnn based model was chosen in order to maintain the aspect ratio of the images (ssd-based models resize all images to 300 x 300 pixels). A total of 6500 steps/epochs is required to train the model. When run using Google Colab, training takes about 20 minutes. 

## Inference
Following training, inference was performed on a set of 6 images. These images were excluded from the training and test sets and were taken from a unique bridge along the Merritt Parkway (i.e., no training or test images were taken from this bridge). The output from inference is shown in Figure 2. It can be seen that the low clearance signs in all 6 images are correctly detected and classified.

![](/READMEimages/valid_1.png) ![](/READMEimages/valid_2.png) ![](/READMEimages/valid_3.png) ![](/READMEimages/valid_4.png) ![](/READMEimages/valid_5.png) ![](/READMEimages/valid_6.png)
> *Figure 2: Custom object detection model inference output*
