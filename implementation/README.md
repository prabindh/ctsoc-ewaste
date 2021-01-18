# Implementation

## Few Shot Trial
Few-shot learning (FSL), is a type of machine learning problems where the training dataset contains limited information.

Common practice for machine learning applications is to feed as much data as the model can take to enable the model to predict better. However, few-shot learning aims to build accurate machine learning models with less training data. As the dimension of input data is a factor that determines resource costs (e.g. time costs, computational costs etc.), one can reduce data analysis/machine learning (ML) costs by using few-shot learning.

Code can be found [here](implementation\few-shot)

### Steps: 

1. Clone the tensorflow models repository if it doesn't already exist.
2. Install the Object Detection API and import necessary libraries.
3. Load images [option of annotating and labelling] and visualize.
4. Load pipeline config and build a detection model.
5. Select variables in top layers to fine-tune.
6. Load test images and run inference with new model.

## TF2.0 Object Detection (Roboflow)

Creating accurate machine learning models capable of localizing and identifying multiple objects in a single image remains a core challenge in computer vision. The TensorFlow Object Detection API is an open source framework built on top of TensorFlow that makes it easy to construct, train and deploy object detection models.

Tensorflow provides a collection of detection models pre-trained on the COCO 2017 dataset. These models can be useful for out-of-the-box inference. The model used for our implementations is `EfficientDet D0 512x512` which is found with other EfficientDet models in the Roboflow notebook [here](implementation\full-model-roboflow).

### Steps: 

1. Install TensorFlow2 Object Detection Dependencies.
2. Download Custom TensorFlow2 Object Detection Dataset.
3. Write Custom TensorFlow2 Object Detection Training Configuation.
4. Train Custom TensorFlow2 Object Detection Model.
5. Export Custom TensorFlow2 Object Detection Weights.
6. Use Trained TensorFlow2 Object Detection For Inference on Test Images.

### Note: 
- Add your own dataset link generatd on [Roboflow](https://roboflow.com/) in the notebook while training or upload your dataset in .TFRecord format. 
  ```python
  #Downloading data from Roboflow
  %cd /content
  !curl -L "DATASET LINK HERE" > roboflow.zip; unzip roboflow.zip; rm roboflow.zip
  ```

- Update the names of the TFRecord names from "cells" and "cells_label_map" to your files
    ```python
    test_record_fname = '/content/test/filename.tfrecord'
    train_record_fname = '/content/train/filename.tfrecord'
    label_map_pbtxt_fname = '/content/train/filename_label_map.pbtxt' 
    ```

## TF2.0 Object Detection (Roboflow) - Optimizers

- `momentum_optimizer`: Momentum or Stochastic Gradient Decent with momentum is method which helps accelerate gradients vectors in the right directions, thus leading to faster converging. It is one of the most popular optimization algorithms and many state-of-the-art models are trained using it

- `adam_optimizer`: Adam is a replacement optimization algorithm for stochastic gradient descent for training deep learning models. Adam combines the best properties of the AdaGrad and RMSProp algorithms to provide an optimization algorithm that can handle sparse gradients on noisy problems.

- Replacing Momentum with Adam optimizer in `/content/models/research/deploy/pipeline_file.config` after we write the custom config file:
  - Default optimizer in config file:
    ```python
    optimizer {
        momentum_optimizer: {
            learning_rate: {
                cosine_decay_learning_rate {
                learning_rate_base: 8e-2
                total_steps: 300000
                warmup_learning_rate: .001
                warmup_steps: 2500
                }
            }
            momentum_optimizer_value: 0.9
            }
            use_moving_average: false
        }
        max_number_of_boxes: 100
        unpad_groundtruth_tensors: false
    }
    ```
  - Changing it to ADAM:
    ```python
        optimizer {
        # momentum_optimizer {
            adam_optimizer: {
            learning_rate: {
                manual_step_learning_rate {
                initial_learning_rate: .0002
                schedule {
                    step: 4500
                    learning_rate: .0001
                }
                schedule {
                    step: 7000
                    learning_rate: .00008
                }
                schedule {
                    step: 10000
                    learning_rate: .00004
                }
                }
            }
            # momentum_optimizer_value: 0.9
            }
            use_moving_average: false
        }
    }
    ```

## Results

The results for the implementation can be seen [here](results) along with output images of the detections done by the models.