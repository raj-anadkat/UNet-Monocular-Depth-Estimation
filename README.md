# Monocular Depth Estimation Using U-Net with pretrained VGG-16 Backbone

## I. Methodology
- Our approach encompasses a monocular depth estimation model tailored for self-driving applications. We initially trained our encoder, but to improve the results, we leveraged pre-trained DenseNet, ResNet, and VGG16 backbones as encoders, We formulated a decoder trained the net work on the DIODE dataset. We used a diverse set of loss functions (smoothness, SSIM, L1) and activation functions (ReLU, Leaky ReLU, Sigmoid, Tanh).
- We explored various activation functions were, with comprehensive trials on both ReLU and Leaky ReLU. This methodology yielded a robust depth estimation model with applications in 3D point cloud mapping and self-driven car movement direction detection.

## II. Model Architecture

 <p float="left">
<img src= "https://github.com/raj-anadkat/UNet-Monocular-Depth-Estimation/assets/109377585/8f4f4e8b-dadb-4c32-8cc9-a605fc3d6c5f"alt="ROI" width="400"/>
 </p>
 
For the architecture of the network, we took a U-Net model, which has mainly three kinds of blocks.

- Upscale: UpScale block is part of the decoder network, which takes the information from the parallel down-scale block, and previous upscale block, and concate-nates to give a new output. The features from previous upscale block and upsampled, and increases the resolution of the feature map. It decodes the feature map to the depth image field.
- Downscale: The Downscale box, gives a feature vector in the same resolution, which is then downsampled using max pool, to feed to the next downscale block. It acts as the encoder to create feature maps.
- Bottleneck: The bottleneck layer acts as a buffer between the encoder and the decoder system.
  
We implemented a total of 4 blocks for downscale and upscale blocks in the model, with the channels of sizes (16,64,128,256,512) with the VGG16 backbone, and (64,128,256,512,1024) for DenseNet, and ResNet50 model.


## III. Training Losses
To train our depth estimation model, we experimented with various loss functions to optimize the model parameters. The following loss functions were employed:

- Smoothness Loss: Smoothness loss checks for a smooth transition between the depth maps. It is the summed gradient of the prediction image and minimizes it.
- SSIM (Structural Similarity Index): It is the measure of structural similarity between the prediction and the target image.
- L1 loss: We are using L1 loss as the regression loss between the prediction and the target.
  
We tried various loss weight distributions and finally set the weights as 0.25 for L1 loss, 0.9 for SSIM Loss, and 0.6 for the Smoothness Loss.

<p float="left">
  <img src="https://github.com/raj-anadkat/UNet-Monocular-Depth-Estimation/assets/109377585/3abdf060-78f7-489d-b08d-1b5e005ab629" alt="img" height="500"/>
  <img src="https://github.com/raj-anadkat/UNet-Monocular-Depth-Estimation/assets/109377585/4956ea6c-0dc0-4f87-bc8f-63712c39edba"alt="img" height="500"/>
  <img src="https://github.com/raj-anadkat/UNet-Monocular-Depth-Estimation/assets/109377585/57a6fa77-68b0-4e68-8707-09e19b4a5f31" alt="img" height="500"/>
</p>


## IV. Depth Map Results from Model with Pretrained Backbone
Shown Below are the results from the model trained on VGG-16 Backbone on the train section of DIODE Dataset (81GB).

 <p float="left">
<img src= "https://github.com/raj-anadkat/UNet-Monocular-Depth-Estimation/assets/109377585/29b77ca9-9bdc-450f-b739-36d875c37f31"alt="ROI" width="400"/>
 </p>


## V. Future Improvements
We can implement ViT(Vision Transformers) ViT applies the transformer architecture, primarily used in NLP, to image processing tasks. It divides images into patches and processes these sequentially through attention mechanisms.
- Advantages: Capable of capturing long-range dependencies in the image data. Often outperforms traditional CNNs in large-scale image recognition tasks.
- Application in Depth Estimation: Potential for improved contextual understanding and depth perception over large areas. Still in the exploratory stages for depth estimation but shows promising results.
