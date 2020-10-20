# MobileNetSR

Model based on depthwise convolution and deconvolution using residual blocks for real time super resolution. 

# Details:

1. <b>Generator</b>: 12k parameters with residual blocks, inspired by SRGAN.
2. <b>Discriminator</b>: same as SRGAN but implemented with depthwise convolutions for speed
3. <b>Loss</b>: Perceptual and adversarial with 0.001 weightage for adversarial loss
4. <b>Batch size: </b>32, any more and google colab crashes without enough memory
5. <b>Execution time</b>: generator for 426x240 (240p image) = ~ 0.3s.
6. <b>Epoch time</b>: takes about 47 mins to train an epoch.
7. <b>Dataset</b>: DIV2K cut to 256x256 and scaled down with opencv bilinear(default) to 128x128

# Optimizations:

The pytorch model currently takes 5.97 seconds to process 24 images of size 256x144p.

1. Cut down to 2 residual blocks with 32 channels
1. Implemented depthwise convolutions on both generator and discriminator.
1. Gained 2 seconds boost by:
    * Removing BatchNorm2d
    * Removing ReflectionPad2d and adding padding directly in the Conv2d layers.

# Problems:

1. Saving model at each epoch in case google colab kicks me out cause of free use quota 

# Current Results:

Epoch 13 out of ~150

<img src="https://github.com/Manjunatha-b/MobileNetSR/blob/main/Results/bilinear.jpg" width="400">
<img src="https://github.com/Manjunatha-b/MobileNetSR/blob/main/Results/13.jpg" width="400">


# Future Plan:

1. Quantize with onnx to get ~6x speedup to reach approx 24fps output rate 
