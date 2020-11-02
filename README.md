# Impact-of-Loss-function-for-Super-Resolution
Motivation:
MSE is the most commonly used regression loss function, MSE is the sum of squared distance between target values and predicted values. Using MSE as the loss function favors a high PSNR for image processing tasks. However, MSE and PSNR sometimes mismatch to human visual system.
Preprocessing：
Convert RGB image into YCbCr[5], in SRCNN the image only consider the luminance channel. So, extract the Y channel. In order to compare how loss functions impact in the super resolution task, I keep it same. It can be extended to all channels in YCbCr color space or in RGB color space.
Amplification low resolution images as the same size as the corresponding high resolution images. Randomly crop both low resolution image and high resolution image into 32x32 patches.
To avoid border effects during training, the loss functions only evaluate the central 20x20 crop of input and the network output.
Save the processed data in HDF5 format.

Method:
I implement SRCNN with Keras. use different loss functions, compare results.
SRCNN contains three layers: Patch extraction representation (kernel size 9 x 9), Non-linear mapping (kernel size 1 x 1), Reconstruction(kernel size 5 x 5).
1. patch extraction and representation patches from the Y channel of low-resolution image and represents each patch as a high-dimensional vector
2. Non-linear mapping map each of vectors from last layer into an n2-dimensional one.
3. Reconstruction.
For the data, uses bicubic to amplify low resolution image to target size then fits the nonlinear mapping by the three layers convolution network, the final output is the high resolution image.
Losses:
• L1 error/ Mean Absolute Error (MAE): MAE is the sum of absolute differences between our target and predicted variables
• L2 error/ Mean squared error(MSE)
• SSIM
• Mix
  Mix1 =αLl1 +(1-α)SSIM 
  Mix2 =αLl2 +(1-α)SSIM
  
  
[1] Chao Dong, Chen Change Loy, Kaiming He, Xiaoou Tang. Learning a Deep Convolutional Network for Image Super-Resolution, in Proceedings of European Conference on Computer Vision (ECCV), 2014.
[2] Zhou Wang, A. C. Bovik, H. R. Sheikh and E. P. Simoncelli, "Image quality assessment: from error visibility to structural similarity," in IEEE Transactions on Image Processing, vol. 13, no. 4, pp. 600-612, April 2004..
[3] E. Agustsson and R. Timofte, "NTIRE 2017 Challenge on Single Image Super-Resolution: Dataset and Study," 2017 IEEE Conference on Computer Vision and Pattern Recognition Workshops (CVPRW), Honolulu, HI, 2017, pp. 1122-1131.
[4] Wikipedia contributors. (2020, April 16). Super-resolution imaging. In Wikipedia, The Free Encyclopedia. Retrieved 21:47, May 4, 2020, from https://en.wikipedia.org/w/index.php?title=Super- resolution_imaging&oldid=951384848
[5] Wikipedia contributors. (2020, March 30). YUV. In Wikipedia, The Free Encyclopedia. Retrieved 21:52, May 4, 2020,from https://en.wikipedia.org/w/index.php?title=YUV&oldid=94813057 6
[6] Zhao, H., Gallo, O., Frosio, I., & Kautz, J. (2015). Loss Functions for Neural Networks for Image Processing. ArXiv, abs/1511.08861.
