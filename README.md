# Trashcan Full Detection
Zhouyu Jiang
* [Github Page](https://github.com/Hypersaki/Trashcan-Full-Detection)
* [Edge Impulse Page](https://studio.edgeimpulse.com/studio/394655)

## Introduction
In this project, a Transfer learning model is deployed on the device used to whether if the trash can in the kitchen is full or not. A camera installed on the device continuously takes pictures of the inside of the trash can and provides data visualization via an LED Strip. The overall appearance of the project is shown below：

In everyday life, the trash cans in the kitchen are often full and no one clears them. There may be times when this is a self-consciousness on the part of the individual not to clean it up, this detection because through the bright LED strip and high contrast colors can provide an effective reminder. When the inside of a trash can captured through the device is sensed as being full, the LED strip will show a red light.

The MCU used in this project is an Arduino Nano 33 BLE, and a breakout board to connect the OV7675 camera to the LED Strip. The training samples of the model are manually captured pictures. They are uploaded to Edge Impulse platform. After training and deployment, the deployed model is used by the sensor device that senses the interior part of trash cans.

## Research Question
The Trashcan Full Detection project aims to make a visual alarm or notification to people to clean out the kitchen trashcan to maintain the healthy living environments.

## Application Overview
The workflow of this project is similar to most embedded image transferred learning projects. There are three parts in total in the following order: 

### Acquisition of image data & data processing
firstly, the taken pictures will be uploaded and labeled, and stored into the dataset. The data will be initially processed, including converting the image type, resizing the image to a lower resolution (96 x 96) to fit the OV7675.

### Model training & Tuning Parameters
Most of the data in the dataset will be used to train the model, while the rest will be used to validate the model. In this process, the training parameters of the model will be constantly adjusted to get the best training results.

### Deployment & Testing
The model trained on Edge Impulse will be deployed to the Arduino Nano 33 BLE. This MCU will take a picture with the OV7675 to get the image and classify the image, and will make the LED Strip respond with a red light if it detects Full garbage.

## Data
In this project, almost all of my pictures were taken by myself using my cell phone, with a few pictures using my roommate's cell phone. Most of the pictures were taken vertically from a higher angle. Initially, I was going to use 3 categories - "full", "half full" and "empty", However, it was finally neutered down to "fullbin" and "emptybin".

### Application Discussion
People may selectively delay and not take out the trash when the trash can is almost but not quite full. This does not help to improve the kitchen environmentals.
### Technically Discussion
The OV7675, an embedded edge-application camera, is so limited in its ability to take pictures that it can confuse full and not-full situations. This can exacerbate the psychology of selective procrastination.

* Classifying the image data with 4 classifications or 3 classifications will reduce the detection accuracy for the detection. Moreover, it does not fit the application scenario. Therefore, the final image data for this project uses 2 classifications.

## Model
### Why Using Edge Impulse
In this project, since the existing model using TensorFlow via Colab is too large, it requires too much RAM and Flash. The Arduino Nano 33 BLE only has 256KB of RAM and 1MB of ROM, so the model framework I chose was Edge Impulse's MobileNetV1 96x96 0.1 (final layer: 16 neurons, 0.1 dropout).
### Training Settings
The neural network was set up with 20 training cycles, a learning rate of 0.0005, and a batch size of 16. The rest of the values were defaults. This is a relatively optimal solution chosen through multiple model test setups as well as different settings. This setup resulted in a model with 93.9% accuracy and 0.12 loss rate.
### Settings Explanations
Since the total sample size is relatively small with only 100 samples for each label, the training cycles of 50-100 will not be set as in other projects with large number of samples with many classifications. in addition, Data augmentation is also enabled to improve the accuracy. Since the dataset is relatively small, the batch size is set to 16 instead of the default 32, and a batch size of 16 even performs better than the model trained with a batch size of 32. The transferred learning dataset has more distinctive features and it makes more sense to use a lower learning rate than the default value of 0.001. A lower learning rate avoids overfitting and enhances generalization.

## Experiments

## Result and Observation

## Bibliography

## Declaration of Authorship
I, Zhouyu Jiang, confirm that the work presented in this assessment is my own. Where information has been derived from other sources, I confirm that this has been indicated in the work.

**

2024/5/9

Words=
