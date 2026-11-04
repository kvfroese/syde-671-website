---
tags:
  - public
---
In this section two methods were created for warping, nearest neighbour (NN) and bilinear (BL) interpolation. Both made use of inverse warping.

NN works by choosing a pixel nearest to the target and copying that value,r resulting in a lightweight operation. BL works by taking a neighbourhood of pixels in $2\times2$ window and calculating an average from that window. It is more expensive than NN, but is generally considered to produce a better result due to being less blocky.

The two functions were tested on the same image, visualized below. The images looked identical by eye. The NN method required 0.3 s and BL 0.9 s, and while not a thorough unit test, the cost difference was obvious.

![[bi image 1 0.992.png]]

![[nn image 1 0.330.png]]

To spot the difference, a test grid of squares was created, visualized below. It is clear that the bilinear method produces smoother diagonal lines. However, in high texture images it is difficult to spot the difference.

![[nn.png]]

![[bi.png]]

# Rectification

Bilinear warping was applied to rectify two images of rectangular but perspective-skewed objects. The first was a sticky note that was known to be square but unmeasured in length. The second was a book measured to be $8\times10$ in, in order to preserve the proprotions.

![[rect_2.jpg]]

![[rectified final 2.png]]

![[rect_1 cropped.jpg]]

![[rectified final 1.png]]
