# `show_sequence`

Display a sequence of frames in a grid format.

## Description

The function visualizes a sequence of frames as a grid using `matplotlib`. Each frame is displayed as an image, with the sequence organized into rows and columns for easy visualization. The frames are normalized for display.

## Arguments

- **`sequence`** (`torch.tensor`):  
  A tensor containing frames to be displayed. Each frame should be a 3D tensor of shape `(C, H, W)` representing a color image.

- **`NUM_FRAMES`** (`int`):  
  The total number of frames in the sequence to be displayed.

## Returns

- **`None`**:  
  The function directly displays the frames using `matplotlib`.

## Example Usage

```python
import torch

# Example sequence: 16 frames of size (3, 64, 64)
sequence = torch.randn(16, 3, 64, 64)
NUM_FRAMES = 16

# Display the sequence
show_sequence(sequence, NUM_FRAMES)
```

## Notes

- The grid layout defaults to 4 columns. The number of rows is calculated dynamically based on the number of frames.
- The function normalizes each frame by dividing by its maximum value to ensure proper visualization.
- Ensure that `sequence` contains at least `NUM_FRAMES` frames to avoid indexing errors.
- `matplotlib`'s `GridSpec` is used for flexible grid layouts.

## Visualization Example

For a sequence of 16 frames:
- **Grid Layout**: 4 columns x 4 rows
- Each frame is displayed as an image with no axis markers.

<!-- ![show_sequence](https://barkknight.github.io/SignLink-ISL-Docs/html/static/utils/show_sequence/output.png) -->

![show_sequence](http://localhost:8000/output.png)


## Implementation

```python
import os
from matplotlib import pyplot as plt
import matplotlib.gridspec as gridspec

def show_sequence(sequence, NUM_FRAMES):
    """
    Displays a sequence of frames in a grid format.

    Args:
        sequence (torch.tensor): A tensor containing frames to be displayed. 
                                        Each frame should be a 3D tensor (C, H, W) representing a color image.
        NUM_FRAMES (int): The total number of frames the tensor contains.

    Returns:
        None: The function directly displays the frames using `matplotlib`.

    Example:
        show_sequence(frame_sequence, 16)
    """
    columns = 4
    rows = (NUM_FRAMES + 1) // (columns)
    fig = plt.figure(figsize=(32, (16 // columns) * rows))
    gs = gridspec.GridSpec(rows, columns)
    for j in range(rows * columns):
        plt.subplot(gs[j])
        plt.axis("off")
        frames = sequence[j].permute(1,2,0).numpy()
        frames = frames/ frames.max()
        plt.imshow(frames)
    plt.show()
```