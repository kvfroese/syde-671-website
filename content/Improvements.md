---
tags: public
---

# Preliminary Resizing

The image pyramids were not enough, the images were simply too big to comfortably run, and window size became more finicky and less universal. With both, an example image pyramid is:

![[image pyramid.png]]

# Gaussian Blurring

A simple $3\times 3$ Gaussian blur was implemented, instead of simply downsampling. To convolve, multiplication was done in frequency space after a fast Fourier transform. It seemed to minorly help stability and did not affect performance all that much.

# Edge Detection

Edge detection allowed the final two [[Preliminary Failures]] to succeed, at least for one algorithm. A *Scharr kernel* was used.

The example image is difficult to see, but it’s there!![[edge detection.png]]

# Gradient Masking

This improvement generates a gradient mask array the size of the image. It has two components, a circular gradient with some minor parameters to affect spread and size of central radius, and a hard edge to cut off the border area of all images from scoring, with range $[0, 1]$ (0 being ignored).

The way it was incorporated was into the metrics. For the $L_2$ norm it was simply multiplied into the squared difference. However, for the NCC it was more complex.![[mask.png]]