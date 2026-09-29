# image-processing-lab6
# Frequency Domain Filtering with Python

This project demonstrates image filtering in the **frequency domain** using Python, NumPy, Matplotlib, and Scikit-Image.

The notebook focuses on applying the **Fourier Transform** to image processing and demonstrates how spatial filtering operations can be performed as multiplication in the frequency domain.

## Overview

In image processing, filtering can be performed in either the spatial domain or the frequency domain.

According to the convolution theorem:

```text
Convolution in the spatial domain
=
Multiplication in the frequency domain
```

The general process used in this lab is:

1. Load the image.
2. Compute the 2D Fast Fourier Transform using `fft2()`.
3. Create the frequency-domain filter.
4. Multiply the image spectrum by the filter.
5. Apply the inverse Fourier Transform using `ifft2()`.
6. Visualize the filtered result.

## Tasks Implemented

### 1. Laplacian Filtering in the Frequency Domain

The Laplacian filter is used for edge detection and high-frequency enhancement.

The frequency-domain representation used in the notebook is:

```text
H(u,v) = -4π²(u² + v²)
```

The image is transformed using the 2D FFT, multiplied by the Laplacian frequency response, and then transformed back into the spatial domain.

The notebook displays:

- Original image
- Laplacian spectrum
- Laplacian filtered output

### 2. Sobel Filtering in the Frequency Domain

The assessment task implements Sobel edge detection using two directional kernels.

#### Sobel X

```text
[-1   0   1]
[-2   0   2]
[-1   0   1]
```

#### Sobel Y

```text
[-1  -2  -1]
[ 0   0   0]
[ 1   2   1]
```

Since the Sobel filters are originally `3 × 3` spatial kernels, they must first be converted into frequency-domain filters.

The implementation:

1. Creates a zero-filled array matching the image size.
2. Places the Sobel kernel in the center.
3. Applies `ifftshift()` to move the kernel center to the FFT origin.
4. Applies `fft2()` to obtain the kernel's frequency response.
5. Multiplies the response by the FFT of the image.
6. Applies `ifft2()` to return to the spatial domain.
7. Combines the X and Y responses to produce the final edge magnitude.

The Sobel magnitude is calculated as:

```python
sobel_magnitude = np.sqrt(
    sobel_x_image**2 + sobel_y_image**2
)
```

## Output

The Sobel implementation produces four visualizations:

- Original Cameraman image
- Sobel X response
- Sobel Y response
- Combined Sobel magnitude

The combined magnitude highlights edges regardless of their direction.

## Technologies Used

- Python
- NumPy
- Matplotlib
- Scikit-Image
- Jupyter Notebook

## Main Libraries

```python
import numpy as np
import matplotlib.pyplot as plt

from skimage import data
from skimage.transform import resize

from numpy.fft import fft2, ifft2, fftshift, ifftshift
```

## Key Concepts

This lab covers several important digital image processing concepts:

- Spatial domain vs. frequency domain
- Fourier Transform
- 2D Fast Fourier Transform
- Inverse Fourier Transform
- Frequency-domain filtering
- High-pass filtering
- Edge detection
- Laplacian filtering
- Sobel filtering
- Kernel padding
- FFT shifting
- Pointwise frequency multiplication

## General Frequency-Domain Filtering Process

```python
# Compute image FFT
F = fft2(image)

# Create or transform a frequency-domain filter
H = ...

# Apply the filter
G = F * H

# Convert back to spatial domain
filtered = ifft2(G).real
```

One important principle demonstrated in this lab is that filtering is performed through **pointwise multiplication** in the frequency domain rather than direct spatial convolution.

## Project Structure

```text
Frequency-Domain-Filtering/
│
├── Lab6_Frequency_Domain_COMPLETED.ipynb
└── README.md
```

## Running the Notebook

### 1. Install the required libraries

```bash
pip install numpy matplotlib scikit-image jupyter
```

### 2. Start Jupyter Notebook

```bash
jupyter notebook
```

### 3. Open the notebook

```text
Lab6_Frequency_Domain_COMPLETED.ipynb
```

Run the cells sequentially to reproduce the filtering results.

## Learning Outcomes

After completing this lab, the following concepts should be understood:

- How image information is represented using frequencies.
- How FFT converts an image from the spatial domain to the frequency domain.
- How filters can be applied through frequency-domain multiplication.
- How spatial kernels such as Sobel can be converted into frequency responses.
- How `fft2()`, `ifft2()`, `fftshift()`, and `ifftshift()` are used in image processing.
- How Laplacian and Sobel filters detect image edges.

## Notes

Low frequencies generally represent smooth image regions and overall intensity variations, while high frequencies represent rapid intensity changes such as edges, textures, and noise.

For computation, FFT data should remain in its natural ordering. Functions such as `fftshift()` are mainly useful when displaying frequency spectra.

After applying `ifft2()`, the real component is used because very small imaginary values can appear due to numerical floating-point calculations.

## Author

Computer Science / Digital Image Processing Lab Project
