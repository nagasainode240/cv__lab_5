# CV Lab 5 – Bit Plane Slicing

## Description

This program demonstrates **bit plane slicing** on a grayscale image. It decomposes an 8-bit grayscale image into its 8 individual bit planes (Bit 0 through Bit 7), allowing visualization of each bit's contribution to the overall image.

- **Bit 0** (LSB) — carries the least significant information (mostly noise-like).
- **Bit 7** (MSB) — carries the most significant information (closest to the original image structure).

## Prerequisites

- Python 3.x
- OpenCV (`cv2`)
- NumPy
- Matplotlib

Install dependencies:

```bash
pip install opencv-python numpy matplotlib
```

## Usage

1. Place a grayscale-compatible image named `img1.jpg` in the project directory.
2. Run the script:

```bash
python cvlab5.py
```

Or execute the cells in `cvlab5.ipynb` if using Jupyter Notebook.

## Code Overview

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

# Load image in grayscale
img = cv2.imread('img1.jpg', cv2.IMREAD_GRAYSCALE)

if img is None:
    print('Error : Image not found')
else:
    plt.figure(figsize=(12, 10))

    # Display original image
    plt.subplot(3, 3, 1)
    plt.imshow(img, cmap='gray')
    plt.title('Original Image')
    plt.axis('off')

    # Extract and display each bit plane (0–7)
    for i in range(8):
        bit_plane = (img >> i) & 1      # isolate the i-th bit
        vis_plane = bit_plane * 255      # scale to 0 or 255 for visibility

        plt.subplot(3, 3, i + 2)
        plt.imshow(vis_plane, cmap='gray')
        plt.title(f"Bit Plane {i}")
        plt.axis('off')

    plt.tight_layout()
    plt.show()
```

### How It Works

| Step | Operation | Purpose |
|------|-----------|---------|
| 1 | `cv2.imread(..., IMREAD_GRAYSCALE)` | Load image as single-channel 8-bit |
| 2 | `(img >> i) & 1` | Right-shift by `i` bits, then mask the LSB to isolate bit plane `i` |
| 3 | `bit_plane * 255` | Scale binary (0/1) values to (0/255) for display |
| 4 | `plt.subplot(3, 3, ...)` | Arrange original + 8 bit planes in a 3×3 grid |

## Output

A 3×3 grid of images:

| | Col 1 | Col 2 | Col 3 |
|---|---|---|---|
| **Row 1** | Original | Bit Plane 0 | Bit Plane 1 |
| **Row 2** | Bit Plane 2 | Bit Plane 3 | Bit Plane 4 |
| **Row 3** | Bit Plane 5 | Bit Plane 6 | Bit Plane 7 |

## License

For academic/lab use only.
