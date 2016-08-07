

#Problem Statement

Detect the person in images with fashion models, find the best possible bounding box.

#Data

22 images with fashion models.
Problems:- Not only humans, but also human parts (legs, torso,etc) 
         - Various Scales


#Methods

- Cascade Training, HOGs + SVM one of the basic techniques for human
detection.
Problems: few images, occlusions. It is impossible
to train a good detector for humans or human parts. There are
pre-trained models that detect humans and/or human parts (face, upper,etc) but they are not
applicable to these data (big number of false positives).

- Convolutional Neural Networks (cNN) can overcome the problems of the cascade training with HOGs, it is
suitable for detecting humans as well as human parts. One of the best
methods for human detection in images.
Problem: few images for training, Solution: there are available pretrained
models for object detection such as ImageNet.

#R-CNN (caffe framework)

Caffe framework: Caffe is a deep learning framework made with expression, speed, and modularity in mind. It is developed by the Berkeley Vision and Learning Center (BVLC) and by community contributors.

R-CNN is a state-of-the-art visual object detection system that combines bottom-up region proposals with rich features computed by a convolutional neural network.
See here: https://github.com/rbgirshick/rcnn

Imagenet: ImageNet is an image database organized according to the WordNet hierarchy (currently only the nouns), in which each node of the hierarchy is depicted by hundreds and thousands of images. Currently it has an average of over five hundred images per node.It is a useful resource for researchers, educators, students and all of you who share our passion for pictures. 
http://www.image-net.org/

Steps:

Step 1: Load Imagenet.

Step 2: Selective Search: Finding possible bounding boxes with objects. “Selective Search for Object
Recognition”J. R. R. Uijlings, K. E. A. van de Sande, T. Gevers, A. W. M. Smeulders
2013 IJCV.

 Step 3: Detect objects in the proposed areas (with caffe/python/detect.py). Only the bounding boxes
containing a person are kept.

Step 4: Out of all detected objects, we keep the 4 most confident that the detected object is a person. If
there is a great difference on the confidence between these 4, the bounding box is created by finding the
min and max points of each of the 4 detections, otherwise the min of the bounding box is mean of the
mins and the max is the mean of the maxs. If the first proposal is very strong (>1 and there is a great
difference between the first and the rest) we only keep that one.


#Instructions

Inside the _temp folder there is a det_input.txt file,write the path of the image that you
want to test. If you want to test the whole data set at once (better results according to Selective Search method), just add all the paths here.

The ipython file name is caffe_fashion_human_detection.ipynb. It is the main method.

To download  ImageNet: ./scripts/download_model_binary.py models/bvlc_reference_rcnn_ilsvrc13

It also needs the data/ilsvrc12.

Platform: Ubuntu 14.04 with i3 2.5 and 4 GB RAM. Caffe is running only on CPU
and not on GPU. Python 2.7 + Jupyter

For the result images see the reults folder. I have uploaded the selective search code in a zip file. It has a few changes  to the original,
that is why it is preferred to download and run this version. Please copy the detect.py file into the caffe/python/ folder, there also some improvements of the
original from caffe framework

See https://github.com/BVLC/caffe for more details, installation instructions etc. about the caffe framework.

#Training an R-CNN detector on another dataset

It should be easy to train an R-CNN detector using another detection dataset as long as that dataset has complete bounding box annotations (i.e., all instances of all classes are labeled).

To support a new dataset, you define three functions: (1) one that returns a structure that describes the class labels and list of images; (2) one that returns a region of interest (roi) structure that describes the bounding box annotations; and (3) one that provides an test evaluation function.








