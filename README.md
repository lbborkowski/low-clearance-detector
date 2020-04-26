# low-clearance-detector
Custom object detection model for low clearance signs

Launch the notebook in Google Colab by clicking on this badge: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lbborkowski/low-clearance-detector/blob/master/object_detection_tutorial_LBB_200426.ipynb)

## Overview
This repository contains a custom object detection model for low clearance signs. Low clearance signs are used to indicate bridges, overpasses, and tunnels with clearances below the standard height to avoid strikes from trucks or other large vehicles. Despite the presence of these signs throughout the U.S., bridge strikes occur hundreds of times per year. These strikes are partially caused by the use of commercial GPS which direct inexperienced drivers along routes that aren't suitable for their particular vehicle. The lack of a comprehensive database for low clearance bridges across the country prevent commercial GPS systems from issuing a warning when a truck is approaching one of these bridges. Therefore, a custom object detection model was developed to detect low clearance signs from images. This type of model could either be used to populate a database for low clearance signs or it could be run in realtime to analyze dashboard camera footage to provide the driver with an early warning. 

## Training

The model was trained on 125 images take from [OpenStreetCam](https://openstreetcam.org/) along the Merritt Parkway between Connecticut and New York City. Trucks and buses are prohibited on this limited-access parkway because of its low bridges however some bridges along this route have been struck over a hundred times over the last [decade](https://www.governing.com/community/Truck-Hits-Overpass-and-Inspiration-Hits-Blumenthal.html). Testing/evaluation was performed on a set of 24 unique images. Low clearance signs in the training and test sets were labeled using labelImg. A selection of training images is shown in Figure 1.

![](/READMEimages/train_01.png) ![](/READMEimages/train_02.png) ![](/READMEimages/train_11.png) ![](/READMEimages/train_04.png) ![](/READMEimages/train_06.png) ![](/READMEimages/train_07.png) ![](/READMEimages/train_08.png) ![](/READMEimages/train_10.png)
> *Figure 1: Labeled selection of training images*

Transfer learning was employed for the custom object detection model by starting with a pre-trained model. The model was trained using the TensorFlow Object Detection API and the model architecture used was faster_rcnn_inception_v2 trained on the COCO dataset. A faster rcnn based model was chosen in order to maintain the aspect ratio of the images (ssd-based models resize all images to 300 x 300 pixels). A total of 6500 steps/epochs were required to train the model. When run using Google Colab, training took between 20 and 30 minutes. 

## Inference
Once training was complete, inference was performed on a set of 6 images. These images were excluded from the training and test sets and were taken from a unique bridge along the Merritt Parkway (i.e., no training or test images were taken from this bridge). The output from inference is shown in Figure 2. It can be seen that the low clearance signs in all 6 images are correctly detected and classified.

![](/READMEimages/valid_1.png) ![](/READMEimages/valid_2.png) ![](/READMEimages/valid_3.png) ![](/READMEimages/valid_4.png) ![](/READMEimages/valid_5.png) ![](/READMEimages/valid_6.png)
> *Figure 2: Custom object detection model inference output*
