# YOLO-object-detection

Currently there are 3 main implementations of YOLO

1. Darknet: (https://pjreddie.com/darknet/). This is the “official” implementation, created by the same people behind the algorithm. It is written in C with CUDA, hence it supports GPU computation. https://pjreddie.com/publications/

2. AlexeyAB/darknet (https://github.com/AlexeyAB/darknet)

3. Darkflow (https://github.com/thtrieu/darkflow/). This is port of Darknet to work over TensorFlow. DarkFlow is a Python implementation of the YOLO2 Object Detection system using TensorFlow as the backend.

# Installation:

mkdir darkflow

cd darkflow

pip install Cython

git clone https://github.com/thtrieu/darkflow.git

cd darkflow

pip install .

wget https://pjreddie.com/media/files/yolov2.weights cd

cd darkflow/cfg

# # Training with custom images,Steps:

+ To create dataset

(LabelImg is a graphical image annotation tool and label object bounding boxes in images)

https://github.com/tzutalin/labelImg

brew install qt 

brew install libxml2

make qt5py3

python3 labelImg.py

LabelImg is a graphical image annotation tool. It is written in Python and uses Qt for its graphical interface. Annotations are saved as XML files in PASCAL VOC format, the format used by ImageNet. Besdies, it also supports YOLO format


+ Folder structure:

  + darkflow

     + darkflow-master
  
       + train
   
         + images
    
         + annotations

cp cfg/yolo.cfg cfg/yolo-new.cfg

+ modify configuration file: cfg/yolo-new.cfg

vi cfg/yolo-new.cfg

￼We need to modify two lines:

1. In the last [convolutional] section, we need to change the number of filters , the formula is filters=(number of classes + 5)*5 , since we have only one class, we set filters=30 .

2. Under the section [region] there is a line to specify the number of classes (around line 244), we need to change it to classes=1 or the number of classes we have.

+ Firstly at the top of file, need to change the batch size to 64 and subdivisions to 64 (they will be commented out)

+ Change height and width to 288 and 288 for faster training

+ Training: In the darkflow/darkflow-master directory, execute the following line:

python flow --model cfg/yolo_1_class.cfg --load yolov2.weights --train --annotation train/annotations --dataset train/images --epoch 500
   
