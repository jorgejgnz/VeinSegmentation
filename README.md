# UNet for vein segmentation

<p align="center">
  <span>English</span> |
  <a href="README.es-ES.md">Español</a>
</p>

Implementation of a UNet in Keras for veins segmentation in retinal images.

Project developed for the Computer Vision course as part of the Master's Degree MUIARFID (UPV).

The code provided by [RParedesPalacios](https://github.com/RParedesPalacios/ComputerVisionLab/blob/master/src/segmen.py) has been used as a basis for this purpose.

The dataset is composed of only 20 images so 19 images will be used for training and 1 image for test.

The following is a segmentation predicted by the model at the end of training on the single test sample.

![Predicted mask from test image.[\[long\]]{#long
label="long"}](imgs/predicted.png)

# Preprocessing

A generator was used to implement data augmentation for images and masks using the [Albumentations](https://github.com/albumentations-team/albumentations) library.

Since all the images in the dataset are positioned in the same way, with the same scale and the same rotation, we have avoided using this type of transformations. Instead, we have used a random contrast change since the contrast changes between the images in the dataset. This transformation affects the color but not the mask, so it is applied only on the image.

The following image exemplifies the chosen transformations.

![Data augmentation.[\[long\]]{#long
label="long"}](imgs/augmentation.png)

# Model

The implemented UNet consists of 5 encoder blocks with 2 convolutional layers each and 4 decoder blocks, 3 of them with 2 convolutional layers each.

The last convolutional layer converts the output to a 1-filter image with sigmoid activation function where each pixel will indicate whether that pixel is a vein or not.

The loss function used is the mean square error (MSE) between the obtained segmentation map and the expected one.

The model used (simplified for clarity) is shown below.

![UNet model.[\[long\]]{#long
label="long"}](imgs/model_simple.png)

# Training

The model converges slowly and after 200 epochs it manages to correctly segment the test image. The error decreases consistently during most of the training, as shown in the image.

![Evolution of error during training (MSE).[\[long\]]{#long
label="long"}](imgs/loss.png)

# License

[MIT](LICENSE)