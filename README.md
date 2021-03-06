# Image-Inpainting
EEC206 final project  
Click [Here](https://www.youtube.com/watch?v=R4t8kbnEbOA) to check the video demo!

Complete code can be found in Inpainting_Partial_Convolution-2.ipynb.

## Our main contributions:
Our contributions in this project compared to other similar works inculde  
- Training dataset augmentation( Including images and masks)
- Improved the Structural Similarity Index Measure (SSIM) to 0.92 compared to the result in [[2]](https://arxiv.org/pdf/1804.07723.pdf)




## Description:
Image inpainting, or the act of filling up holes in an image, can be used for a variety of tasks. It can be used in image editing to get rid of certain objects or to clean up an image. There are many approaches to image inpainting, but many are related to filling images with rectangular holes. For our project, we try to apply a pre-existing technique that uses partial convolutions, which can be applied to images that contain irregularly shaped holes. We add our own modifications to the current technique and test it on a data set based off the ICME 2019 Challenge data set. Our results indicate that the technique does work on irregular holes reasonably well.

## Method:
### Partial Convolution techniques
The Network Design uses a UNet-like architecture, replacing all convolutional layers with partial convolutional layers and using nearest neighbor up-sampling in the decoding stage. Instead of using typical padding for convolution operations, using partial convolution with appropriate masking at image boundaries can ensure the inpainted content at the image border will not be affected by invalid values outside of images. The image inpainting includes partial convolution and mask updating operations, both of which are implemented in the Partial Convolutional Layer. 

### Data Sets
The main dataset for the training model is used from ICME Challenge dataset.  
The main differences between our work and Guilin et al. is that we use different data sets and different training. We also constrained the image size to 256x256, both due to computational cost, and because we believe it was a good size to crop the ground truth images provided. We have created several data sets from the ICME 2019 data. In the original challenge, there are 1541 ground truth images and a validation set. The validation set contains two folders - one for error concealment (EC), the other for object removal (OR). Both datasets are structured in the same way, but the masks differ. For a dataset, there are 70 distinct images, but each image had a subset of ways it was cropped. The total number of files are shown in Table 1. The validation test set contains damaged images that already have holes, as well as 70 ground truth images. For the training set, since we are provided 1541 ground truth images, we wanted to expand our dataset to make our neural network (NN) more robust. Thus, we applied augmentation to these ground truth images, where we used a dataset containing 7700 images for training. In Figure X, the images show the augmentation we implemented for the training dataset in our experiment, including image random flipping, color jittering, resizing, and random image rotation. Since we were not provided masks, we also generated masks using three techniques.

### Image Augmentation
In order to make our model more robust, image augmentation was applied to our image and mask training dataset. The 6 images below show the augmented dataset for our implementation, including randomly flipped, rotated, and slightly discolored versions of the ground truth images. The augmented dataset is used to imporve the training model by increasing the diversity of available dataset.  
<img src="/images/augmentation.jpg" width="300">

### Result
The image on the left is covered with rectangular masks, and the image on the right shows the result after implementing image inpainting.  
<img src="/images/result.jpg" width="300">
### Citations
[1][Context Encoders: Feature Learning by Inpainting](https://arxiv.org/pdf/1604.07379.pdf)  
[2][Image Inpainting for Irregular Holes Using Partial Convolutions](https://arxiv.org/pdf/1804.07723.pdf)   
[3][High-Resolution Image Inpainting using Multi-Scale Neural Patch Synthesis](https://arxiv.org/pdf/1611.09969.pdf)   
