---
tags:
  - public
---
The final part of this section was to obtain a complete mosaic. The first image shown was done with Laplacian blending. The second was done with feathering, with a high radius (30). Both were done with bilinear interpolation and least squares eight points.

![[mosaic feather high.png]]

![[mosaic.png]]

The final result is not amazing for either, but workable. Even with adjusting points and the homography method multiple times it was not possible to get it better than this. The feathering blending, by eye, looked slightly better due to being less jarring but there was still significant room for improvement.

# Blending

Alpha channel–based blending was implemented to better merge the two images, by modifying the warping functions by adding use of a boolean mask.

The first was a using a built-in distance transform `distance_transform_edt()` from SciPy (equivalent to `bwdist`). A parameter was used to control the feathering radius, with higher producing a longer transition. This method was very lightweight.

The second method was done with a Laplacian pyramid, identical in concept to the last assignment, but using functions from SciPy due to their better optimization. This method was more expensive, but it could be managed by keeping the pyramid levels low (2).

By eye, the pyramid option looked more natural and subtle, but was a sharper blend, even with adjusting $\sigma$.

![[checkerboard feather.png]]

![[checkerboard laplace.png]]