The only algorithm to be 100% successful on the eighteen selected images, as well as the custom three was using an image pyramid with a *normalized cross correlation* (NCC) metric, as well as the edge detection, masking, and Gaussian blurring explained in [[Improvements]].

When observing the greyscale subimages, it is clear there is a difference in brightness and contrast between the BGR subimages. This makes perfect sense, considering the physical nature of film and its uneven response to different parts of the spectrum due to its chemical makeup. This is especially relevant for earlier films.

NCC is more robust at handling uneven brightnesses, and is not too computationally expensive to be unusable.

![[merged-images.png]]