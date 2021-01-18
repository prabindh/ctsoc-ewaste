# IEEE CTSoc 2020 Remote Internship Project- Object detection for E-waste in Indian context

## Introduction to the problem
E-waste, or electronic waste, encompasses electrical and electronic equipment that’s outdated, unwanted, or broken. E-waste contains a laundry list of chemicals that are harmful to people and the environment, like: mercury, lead, beryllium, brominated flame retardants, and cadmium, i.e. stuff that sounds as bad as it is. When electronics are mishandled during disposal, these chemicals end up in our soil, water, and air. Thus the detection of E-waste is an essential step to work on further steps of safely disposing and recycling this waste to minimize its impact on the environment.

## Project Goals
Object detection for consumer E-waste in Indian Context.

## Dataset

### Data Collection
The datasets mentioned below were combined to form the dataset used for this project:
- https://www.kaggle.com/wangziang/waste-pictures 

- https://www.kaggle.com/kerneler/starter-e-waste-dataset-93b07fb8-a/data 

- Images downloaded from google for Indian context

### Annotation
- All images manually labelled using the abelling tool [labelImg](https://github.com/tzutalin/labelImg)
- Classes: battery, bulb, keyboard, laptop, mobile phone, monitor, mouse 

### Data Preparation
- Train/Test split- 693 : 198 : 99 (train : valid : test)
- Preprocessing steps: Auto-Orient
- Augmentation: Flip (Horizontal, Vertical); Rotation; Shear; Brightness; Exposure; Brightness; Crop
- Size of dataset before augmentation: 990 images
- Size of dataset after augmentation: 2376 images

[ Processing done via [Roboflow](https://roboflow.com/) ]

The final dataset used can be found [here](https://drive.google.com/drive/folders/1Zk47mWlZQYjBsesMEGJjCQNrwDGpB-Tl?usp=sharing)

For further details on the dataset go [here](dataset)

## Implementation

### Phase 1: Few Shot Training

Few-shot learning (FSL), is a type of machine learning problems where the training dataset contains limited information.

Common practice for machine learning applications is to feed as much data as the model can take to enable the model to predict better. However, few-shot learning aims to build accurate machine learning models with less training data. As the dimension of input data is a factor that determines resource costs (e.g. time costs, computational costs etc.), one can reduce data analysis/machine learning (ML) costs by using few-shot learning.

- You can find the Model [here](https://github.com/tensorflow/models/blob/master/research/object_detection/colab_tutorials/eager_few_shot_od_training_tf2_colab.ipynb)


### Phase 2: TF2.0 Object Detection (Roboflow)

Creating accurate machine learning models capable of localizing and identifying multiple objects in a single image remains a core challenge in computer vision. The TensorFlow Object Detection API is an open source framework built on top of TensorFlow that makes it easy to construct, train and deploy object detection models.

Tensorflow provides a collection of detection models pre-trained on the COCO 2017 dataset. These models can be useful for out-of-the-box inference. The model used for our implementations is `EfficientDet D0 512x512`.
- You can find the Model [here](https://colab.research.google.com/drive/1sLqFKVV94wm-lglFq_0kGo2ciM0kecWD#scrollTo=fF8ysCfYKgTP&uniqifier=1)


### Phase 3: Optimizations in TF2.0 Roboflow Implementation

- `momentum_optimizer`: Momentum or Stochastic Gradient Decent with momentum is method which helps accelerate gradients vectors in the right directions, thus leading to faster converging. It is one of the most popular optimization algorithms and many state-of-the-art models are trained using it

- `adam_optimizer`: Adam is a replacement optimization algorithm for stochastic gradient descent for training deep learning models. Adam combines the best properties of the AdaGrad and RMSProp algorithms to provide an optimization algorithm that can handle sparse gradients on noisy problems.

- Replacing `momentum_optimizer` with `adam_optimizer` in the model trained.

For further details on the implementation and optimization click [here](implementation)

## Results

Instead of using only the gradient of the current step to guide the search, momentum accumulates the gradient of the past steps to determine the direction to go. While momentum accelerates our search in direction of minima, RMSProp impedes our search in direction of oscillations.

Adam or Adaptive Moment Optimization algorithms combines the heuristics of both Momentum and RMSProp.

While both the models were able to detect objects from images of electronic devices that comprise of E-waste, in terms of efficiency the models compared ![here](results)

## Resources
- https://recyclecoach.com/residents/blog/an-intro-to-e-waste-why-its-a-problem/#:~:text=E%2Dwaste%20contains%20a%20laundry,soil%2C%20water%2C%20and%20air
- https://colab.research.google.com/drive/1sLqFKVV94wm-lglFq_0kGo2ciM0kecWD#scrollTo=fF8ysCfYKgTP&uniqifier=1 
- https://www.tensorflow.org/guide/tensor
- https://hackernoon.com/what-is-one-hot-encoding-why-and-when-do-you-have-to-use-it-e3c6186d008f
- https://www.tensorflow.org/guide/basic_training_loops
- https://towardsdatascience.com/breaking-down-mean-average-precision-map-ae462f623a52
- https://research.aimultiple.com/few-shot-learning/
- https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/running_on_mobile_tf2.md
- https://towardsdatascience.com/stochastic-gradient-descent-with-momentum-a84097641a5d#:~:text=Momentum%20%5B1%5D%20or%20SGD%20with,models%20are%20trained%20using%20it.
- https://machinelearningmastery.com/adam-optimization-algorithm-for-deep-learning/#:~:text=Adam%20is%20a%20replacement%20optimization,sparse%20gradients%20on%20noisy%20problems.
- https://blog.paperspace.com/intro-to-optimization-momentum-rmsprop-adam/
