# IEEE CTSoc 2020 Remote Internship Project- Object detection for E-waste in Indian context

## Introduction to the problem
E-waste, or electronic waste, encompasses electrical and electronic equipment that’s outdated, unwanted, or broken. E-waste contains a laundry list of chemicals that are harmful to people and the environment, like: mercury, lead, beryllium, brominated flame retardants, and cadmium, i.e. stuff that sounds as bad as it is. When electronics are mishandled during disposal, these chemicals end up in our soil, water, and air. Thus the detection of E-waste is an essential step to work on further steps of safely disposing and recycling this waste to minimize its impact on the environment

## Project Goals
Object detection for consumer E-waste in Indian Context

## Dataset

### Data Collection
The datasets mentioned below were combined to form the dataset used for this project:
- https://www.kaggle.com/wangziang/waste-pictures 
  [Images of classes "bulb" and "battery" manually labelled]
  
- https://www.kaggle.com/kerneler/starter-e-waste-dataset-93b07fb8-a/data 
  [Labelled images of classes "keyboard", "laptop", "monitor", "mouse", "mobile phone"] 

Labelling tool uses: [labelImg](https://github.com/tzutalin/labelImg)

### Data Preparation
1. Train/Test split - 636 : 128 : 91 (train : valid : test)
2. Preprocessing steps- Auto-Orient, Resize to 416 x 416
3. Augmentation- Flip (Horizontal, Vertical); Rotation; Shear; Brightness; Noise
4. Size of dataset before augmentation: 909 images
5. Size of dataset after augmentation: 2181 images

[ Processing done via [Roboflow](https://roboflow.com/) ]

## Implementation

### Phase 1: Few Shot Training
[You can find the Model here](https://github.com/tensorflow/models/blob/master/research/object_detection/colab_tutorials/eager_few_shot_od_training_tf2_colab.ipynb)

Steps: 
1. Load pre-trained model.
2. Upload 4-5 images on which detection has to be performed [option of annotating and labelling images as well].
3. Modify/Re-train last layer of model for the required detection.
5. Test result on new images by uploading it on the colab notebook.

### Phase 2: TF2.0 Roboflow
[You can find the Model here](https://colab.research.google.com/drive/1sLqFKVV94wm-lglFq_0kGo2ciM0kecWD#scrollTo=fF8ysCfYKgTP&uniqifier=1)

Steps: Mentioned in colab notebook link above.

Note: Add your own dataset link [generatd on https://roboflow.com/] in the notebook while training or upload your dataset in .TFRecord format.

### Phase 3: Optimizations in TF2.0 Roboflow Implementation

- Replacing `momentum_optimizer` with `adam_optimizer`

## Resources
- https://recyclecoach.com/residents/blog/an-intro-to-e-waste-why-its-a-problem/#:~:text=E%2Dwaste%20contains%20a%20laundry,soil%2C%20water%2C%20and%20air
- https://colab.research.google.com/drive/1sLqFKVV94wm-lglFq_0kGo2ciM0kecWD#scrollTo=fF8ysCfYKgTP&uniqifier=1 
- https://www.tensorflow.org/guide/tensor
- https://hackernoon.com/what-is-one-hot-encoding-why-and-when-do-you-have-to-use-it-e3c6186d008f
- https://www.tensorflow.org/guide/basic_training_loops
- https://towardsdatascience.com/breaking-down-mean-average-precision-map-ae462f623a52
