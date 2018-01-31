# Neural-Style-Transfer
Image 1: Content Image || Image 2: Style Image || Image 3: Result

Neural style transfer is the process of transforming an initial iamge into the 'style' of another image. In September 2015, Gatys et. al. published a paper called 'A Neural Algorithm of Artistic Style' detailing this process. The intuition is rather simple, if we can formulate an algorithm to recreate the 'content' of an image and formulate an algorithm to recreate the 'style' of an image, we can combine the two to perform style transfer.

## Content Transfer

For all learning algorithms, we must create a loss function which we can optimize. In content transfer, our loss function can be something as simple as the mean-squared-error (MSE) function. Instead of comparing the raw pixels of each image, we'll be passing our input image and our current output image through a pretrained VGG network and looking at one of the convolutional layers. As Gayt et. al. puts it, "the input image is transformed into representations that increasingly care about the actual *content* of the image compared to the detailed pixel values." Basically, the VGG network has already learned to 'see' the world, and we exploit this to measure how different two images are. 

Thus, content transfer is simply optimizing the MSE that comes out of a convolutional layer of the VGG network.

## Style Transfer

Similarly, the style transfer algorithm must also have a lost function which it can optimize. 

## Further Thoughts & Experiments


## Acknowledgements.

Most of this notebook comes from Jeremy Howard's fast.ai course (Lesson 8). This is simply my explanation for my own understanding of what is going on, as well as a few experiments and further thoughts.
