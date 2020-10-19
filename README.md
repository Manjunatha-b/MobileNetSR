# MobileNetSR

Model based on depthwise convolution and deconvolution using residual blocks for real time super resolution. 

# Details:

1. <b>Generator</b>: 12k parameters with 2 residual blocks and skip connections, inspired by SRGAN
2. <b>Discriminator</b>: same as SRGAN but implemented with depthwise convolutions for speed
3. <b>Loss</b>: Perceptual and adversarial with 0.001 weightage for adversarial loss
4. <b>Batch size: </b>32, any more and google colab crashes without enough memory
5. <b>Execution time</b>: generator for 426x240 (240p image) = ~ 0.3s.
6. <b>Epoch time</b>: takes about 47 mins to train an epoch.
7. <b>Dataset</b>: DIV2K cut to 256x256 and scaled down with opencv bilinear(default) to 128x128

# Problems:

1. Requires 2000 epochs for result, and that will take me weeks on google colab, and if results arent great it will take a long time to reiterate. I am currently looking at <b>*15*</b> epochs a <b>*day*</b>  :c.
1. Saving the test image output at every epoch to check results as i go as it is an expensive computation
1. Saving model at each epoch in case colab kicks me out telling free use is over so i can load and start again.

# Future Plan:

1. Quantize with onnx to get ~6x speedup to reach approx 20fps output rate of model