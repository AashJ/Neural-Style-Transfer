# Neural-Style-Transfer
Image 1: Content Image || Image 2: Style Image || Image 3: Result

<img src="/Images/Initial_Image.JPEG" width="250" height="250"> <img src="/Images/Style.jpg" width="250"> <img src="/Images/StyleTransfer.png" width="250"> 


Neural style transfer is the process of transforming an initial iamge into the 'style' of another image. In September 2015, Gatys et. al. published a paper called 'A Neural Algorithm of Artistic Style' detailing this process. The intuition is rather simple, if we can formulate an algorithm to recreate the 'content' of an image and formulate an algorithm to recreate the 'style' of an image, we can combine the two to perform style transfer.

## Content creation

For all learning algorithms, we must create a loss function which we can optimize. In content creation, our loss function can be something as simple as the mean-squared-error (MSE) function. Instead of comparing the raw pixels of each image, we'll be passing our input image and our current output image through a pretrained VGG network and looking at one of the convolutional layers. As Gayt et. al. puts it, "the input image is transformed into representations that increasingly care about the actual *content* of the image compared to the detailed pixel values." Basically, the VGG network has already learned to 'see' the world, and we exploit this to measure how different two images are. 

Thus, content transfer is simply optimizing the MSE that comes out of a convolutional layer of the VGG network.

## Style creation

Similarly, the style creation algorithm must also have a lost function which it can optimize. We use multiple convolutional layers to capture some of the 'texture' information through the images. On top of this, we correlate the convolutional output with the Gram Matrix. Unfortunately, understanding what the Gram Matrix does exactly requires mathematical knowledge beyond the scope of this writeup, however I'll try to provide some intuition. As the Gram Matrix is the inner product between the matrix and its transpose, we're essentially throwing away all spatial information in our loss function. Therefore, you can think of the Gram Matrix as making sure the loss function only takes into account the 'style' of the image and not the 'content'.

We do have some variation in how we weight each convolutional layer -- these are constants with can, and should, be played around with for each image. 

Simply put, style transfer is optimizing the MSE of the correlation map (Gram Matrix) of multiple convolutional layers of the VGG network.

## Putting them together

After understanding content transfer and style transfer, neural style transfer is easy. There is nothing more to it than combining the style creation and content creation loss functions to create a new loss function. 

What is interesting, however, is the way in which you combine the two. Taking the sum of both does create a 'valid' loss function, however may not create the most 'visually appealing' output. Instead, you would want to play around with the way you weight each loss function. For example, in this notebook, the content loss is divided by 10. Increasing this divisor causes the output image to have less content and more style. Similarly, decreasing this divisor causes the output image to have more content and less style. We're optimizing this loss function as the basis of our algorithm, so it definitely is worth playing around with the constants. 

## Further Thoughts

1. The initial image matters quite a bit. In these examples I always started with a random image and optimized from there. We can instead apply a gaussian filter to each image initially to potentially make the optimization process smoother.

2. The style images that are passed through matter quite a bit. Intuitively, paintings that have a distinct style as their main attraction make good style images. Starry Night seems to be the classic. I've tried other paintings -- ones that were much more content heavy -- and these have failed. I'm unsure why these turn out to be failures, as the multiple convolutional layers and the gram matrix should be a content independent loss function. This requires further experimentation on my part.


## Further Experiments

1. Train a network to perform this style transfer itself. This can be done in one pass through of a CNN. My current process takes quite a bit of time per image, as we're repeating the 'training' process for each style. Instead, we can create a network that has learned to create images of a particular style and then just do one pass through this network.

2. Super resolution: This is [an example](https://github.com/tetrachrome/subpixel) of an implementation of super resolution. This would require training a network to deconvolve images through interpolation. From my understanding, the algorithm learns how to make these interpolations, allowing us to upsample images. This [paper]
 (https://arxiv.org/abs/1603.08155) also details super resolution. Possible applications include photo restoration, compression, etc.


## Acknowledgements.

Most of this notebook comes from Jeremy Howard's fast.ai course (Lesson 8). This is simply my explanation for my own understanding of what is going on, as well as a few experiments and further thoughts.
