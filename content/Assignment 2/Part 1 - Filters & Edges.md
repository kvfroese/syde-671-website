---
tags:
  - public
---
# 1.1 Convolutions from Scratch

When comparing the three runtimes, it is somewhat complicated. The fastest is SciPy’s `convolve2d`, unsurprisingly, as it is meant to be optimized. The 2–for loop version naively seems it would be faster than the 4–for loop version, however the 2–for loop version is only faster when a filter of large size is chosen.

For example, the two finite differences have times of about 5.7 and 8.9 s for the 4 and 2–for loop convolutions respectively, with SciPy having 0.03 s. The $9\times9$ box filter has a time of and 40.5 and 4.4 s for the convolution methods.

With some minimal research, this is due to the 2–for loop’s implementation relying on array slicing, which has some overhead that makes it slower for small slicing.

Inside the convolution is a padding function, that uses symmetric padding calculated from the image and kernel dimensions to produce *same* padding. `convolve2d` can do this easily with a flag.

![[Convolved_Images (Custom).png]]

```python
def conv_for_loops_4(image: np.ndarray, kernel: np.ndarray, padding: str = 'same', normalize: str = 'clip'):
    if padding == 'same':
        image = pad_image(image, kernel)

    in_h, in_w = image.shape
    k_h, k_w = kernel.shape

    out_w, out_h = in_w - k_w + 1, in_h - k_h + 1
    out = np.zeros((out_h, out_w))

    for y in range(out_h): # across row
        for x in range(out_w): # across column
            sum = 0.0
            for ky in range(k_h):
                for kx in range(k_w):
                    kx_flipped = k_w - 1 - kx # 0 -> 3 - 1 - 0 = 2, 1 -> 3 - 1 - 1 -> 2 -> 3 - 1 - 2 = 0
                    ky_flipped = k_h - 1 - ky
                    sum += image[y + ky, x + kx] * kernel[ky_flipped, kx_flipped]
            out[y, x] = sum

    if normalize == 'norm':
        return np.clip((out - np.min(out))/(np.max(out) - np.min(out)), 0, 255)
    elif normalize == 'clip':
        return np.clip(out, 0, 255)
    else:
        return out
```

```python
def conv_for_loops_2(image: np.ndarray, kernel: np.ndarray, padding: str = 'same', normalize: str = 'clip'):
    if padding == 'same':
        image = pad_image(image, kernel)

    in_h, in_w = image.shape
    k_h, k_w = kernel.shape
    flipped_kernel = np.flip(kernel, axis=(0, 1))

    out_w, out_h = in_w - k_w + 1, in_h - k_h + 1
    out = np.zeros((out_h, out_w))

    for y in range(out_h):
        for x in range(out_w):
            first_idx_x = x
            sec_idx_x = x + k_w
            first_idx_y = y
            sec_idx_y = y + k_h

            slice = image[first_idx_y:sec_idx_y, first_idx_x:sec_idx_x]
            sum = np.sum(slice * flipped_kernel)

            out[y, x] = sum

    if normalize == 'norm':
        return np.clip((out - np.min(out))/(np.max(out) - np.min(out)), 0, 255)
    elif normalize == 'clip':
        return np.clip(out, 0, 255)
    else:
        return out
```

# 1.2 Binarization

Using the finite difference filters on the Cameraman image, we can produce a gradient magnitude image that can be binarized. The image below features two methods of binarization:

1. Global thresholding, fairly self-explanatory.
2. Adaptive mean thresholding, calculating a mean with a box filter and then comparing said mean and then subtracting a constant to calculate an adaptive threshold.

Both images are passable, with the adaptive mean being better. The image is very noisy, particularly in the grass. The adaptive mean better preserves the edges of the camera, but produces a strange border effect.

![[Binarized_Images,_No_Blurring (Custom).png]]

# 1.3 Derivative of  a Gaussian

This was done in two days, by blurring the image and then convolving, and vice versa.

The first (image blurred):

![[Binarized_Images,_Image_Blurred (Custom).png]]

The second (filter blurred):

![[Binarized_Images,_Filter_Blurred (Custom).png]]

Both look much better than the original binarized, by keeping the edges cleaner and the image less noisy. The cutoff parameters are less harsh than the original which allows for preservation of some of the finer details in the background.

The two methods look identical from a distance, and mathematically the order shouldn’t matter when continuous. However, the discrete convolution results in some minor differences, with the blurred filter producing something slightly better in my opinion.

![[Image_Blur_vs._Kernel_Blur_Binarization (Custom).png]]

# Bells & Whistles

The gradient magnitude was calculated before easily with the Pythagorean theorem. The gradient angles were calculated with $\operatorname{atan2}$, wexpohich is an extended version of $\arctan$ that allows for better orientation by having piecewise components for sign.

![[HSV,_Filter_Blurred (Custom).png]]