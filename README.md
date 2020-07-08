# Image-Inpainting
EEC206 final project  
Click [Here](https://www.youtube.com/watch?v=R4t8kbnEbOA) to check the video demo!

Complete code can be found in Inpainting_Partial_Convolution-2.ipynb.

## Description:
Image inpainting,or the act of filling up holes in an image, can be used for a variety of tasks. It can be used in image editing to get rid of certain objects or to clean up an image. There are many approaches to image inpainting, but many are related to filling images with rectangular holes. For our project, we try to apply a pre-existing technique that uses partial convolutions, which can be applied to images that contain irregularly shaped holes. We add our own modifications to the current technique and test it on a data set based off the ICME 2019 Challenge data set. Our results indicate that the technique does work on irregular holes reasonably well.

## Method:
### Partial Convolution techniques
The Network Design uses a UNet-like architecture, replacing all convolutional layers with partial convolutional layers and using nearest neighbor up-sampling in the decoding stage. Instead of using typical padding for convolution operations, using partial convolution with appropriate masking at image boundaries can ensure the inpainted content at the image border will not be affected by invalid values outside of images. The image inpainting includes partial convolution and mask updating operations, both of which are implemented in the Partial Convolutional Layer. 

### Data Sets
The main differences between our work and Guilin et al. is that we use different data sets and different training. We also constrained the image size to 256x256, both due to computational cost, and because we believe it was a good size to crop the ground truth images provided. We have created several data sets from the ICME 2019 data. In the original challenge, there are 1541 ground truth images and a validation set. The validation set contains two folders - one for error concealment (EC), the other for object removal (OR). Both datasets are structured in the same way, but the masks differ. For a dataset, there are 70 distinct images, but each image had a subset of ways it was cropped. The total number of files are shown in Table 1. The validation test set contains damaged images that already have holes, as well as 70 ground truth images. For the training set, since we are provided 1541 ground truth images, we wanted to expand our dataset to make our neural network (NN) more robust. Thus, we applied augmentation to these ground truth images, where we used a dataset containing 7700 images for training. In Figure X, the images show the augmentation we implemented for the training dataset in our experiment, including image random flipping, color jittering, resizing, and random image rotation. Since we were not provided masks, we also generated masks using three techniques.
![](/images/augmentation.jpg)
