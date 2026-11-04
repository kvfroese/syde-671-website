---
tags:
  - public
---
In this section, a function to compute a homography between two images using two sets points was constructed.

# Images

A point picking tool allowed for manual choice of points, and the ability to visualize the correspondence between the two images.

![[1 points.png]]![[2 points.png]]
# Homography Math

There were two methods use to obtain the obtain the homography. The first was a more expensive singular value decomposition (SVD) and the second was least squares (LS).

The matrices (to three significant figures were)

$$
\begin{align*}
M_\text{SVD, 4}&= \begin{bmatrix}
0.817 & -0.264 &  373 \\
-0.00105 & 0.690 & 44.7 \\
-0.000144 & -0.000266 & 1.00
\end{bmatrix} \\
M_\text{LS, 4}&= \begin{bmatrix}
   0.817 & -0.264 &  373 \\
   -0.00105 & 0.690 & 44.7 \\
   -0.000144 & -0.000266 & 1.00
   \end{bmatrix}
\end{align*}
$$

The two matrices were seemingly identical, though not numerically exact, with four points. This is expected given the determined system.

With four additional points (to make) eight, visualized below, the matrices were

$$
\begin{align*}
M_\text{SVD, 8}&= \begin{bmatrix}
0.0450 & -0.0170 & 385 \\
-0.171 & 0.769 & 67.4 \\
0.000527 & 0.00000703 & 1.00
\end{bmatrix} \\
M_\text{LS, 8}&= \begin{bmatrix}
0.457 & -0.00615 & 382 \\
-0.171 & 0.782 & 64.3 \\
-0.000526 & 0.0000201 & 1.00
\end{bmatrix}
\end{align*}
$$

These two matrices are more different, but still roughly similar with elements noticeably close.

![[1 points more.png]]
## Systems of Equation

Without listing all the systems of equations, the LS eight point system was

$$
\begin{align*}
-476 h_{11} - 617 h_{12} - 1 h_{13} + 371756 h_{31} + 481877 h_{32} + 781 h_{33} &= 0 \\
-476 h_21 - 617 h_{22} - 1 h_{23} + 291788 h_{31} + 378221 h_{32} + 613 h_{33} &= 0 \\
-468 h_{11} - 397 h_{12} - 1 h_{13} + 368316 h_{31} + 312439 h_{32} + 787 h_{33} &= 0 \\
-468 h_21 - 397 h_{22} - 1 h_{23} + 180180 h_{31} + 152845 h_{32} + 385 h_{33} &= 0 \\
-561 h_{11} - 410 h_{12} - 1 h_{13} + 500973 h_{31} + 366130 h_{32} + 893 h_{33} &= 0 \\
-561 h_21 - 410 h_{22} - 1 h_{23} + 226644 h_{31} + 165640 h_{32} + 404 h_{33} &= 0 \\
-563 h_{11} - 650 h_{12} - 1 h_{13} + 499381 h_{31} + 576550 h_{32} + 887 h_{33} &= 0 \\
-563 h_21 - 650 h_{22} - 1 h_{23} + 372143 h_{31} + 429650 h_{32} + 661 h_{33} &= 0 \\
-221 h_{11} - 451 h_{12} - 1 h_{13} + 118898 h_{31} + 242638 h_{32} + 538 h_{33} &= 0 \\
-221 h_21 - 451 h_{22} - 1 h_{23} + 94146 h_{31} + 192126 h_{32} + 426 h_{33} &= 0 \\
-207 h_{11} - 287 h_{12} - 1 h_{13} + 110124 h_{31} + 152684 h_{32} + 532 h_{33} &= 0 \\
-207 h_21 - 287 h_{22} - 1 h_{23} + 57753 h_{31} + 80073 h_{32} + 279 h_{33} &= 0 \\
-420 h_{11} - 283 h_{12} - 1 h_{13} + 304500 h_{31} + 205175 h_{32} + 725 h_{33} &= 0 \\
-420 h_21 - 283 h_{22} - 1 h_{23} + 115500 h_{31} + 77825 h_{32} + 275 h_{33} &= 0 \\
-426 h_{11} - 418 h_{12} - 1 h_{13} + 309702 h_{31} + 303886 h_{32} + 727 h_{33} &= 0 \\
-426 h_21 - 418 h_{22} - 1 h_{23} + 174660 h_{31} + 171380 h_{32} + 410 h_{33} &= 0
\end{align*}
$$