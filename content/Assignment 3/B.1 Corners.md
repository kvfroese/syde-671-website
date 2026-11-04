---
tags:
  - public
---
In this section, the provided `harris.py` code was used to obtain corners for the image, visualized below. The corner detection is not bad per se, but it produces very clustered points with high corner density.

![[harris.png]]

The Harris corner coordinates were obtained from the Harris response, visualized below[^1].

![[harris response.png]]

Adaptive non-maximal suppression was implemented to use the Harris response. Its parameters were set to have a threshold of 10, number of retained points to 250, and tolerance of 0.9. None of these are provably the best, but worked well with the images used. 

![[anms.png]]

[^1]: Intensity has been adjusted to be easier to visualize due to high dynamic range.
