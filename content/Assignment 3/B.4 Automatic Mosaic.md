---
tags:
  - public
---

In this final section, an automatic mosaic was obtained. It used an implementation of the 4-point RANSAC algorithm. Aside from that it used

- Bilinear warping
- Laplacian blending
- Singular value decomposition

The final mosaic is visualized below, and for comparison the original mosaic is placed as well. By eye the automatic mosaic is much better, though there is still strangeness at the corners, particularly due to the colour being slightly off.

![[3 image mosaic.png]]

![[mosaic.png]]

It was also tested with four images (from pictures obtained online). It produce an uncanny effect due to the vignette around each photo that was not noticeable until combined. It also really started to shrink the middle images, making certain detail harder to see. However, due to the image being a more zoomed out photo from the start blending artifacts were harder to spot (aside from the vignette).

![[4 image mosaic.png]]