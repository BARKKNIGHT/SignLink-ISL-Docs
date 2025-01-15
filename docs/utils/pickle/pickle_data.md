# `pickle_data`

Save a single data sample (video tensor and label tensor) to disk as a `.pt` file.

## Description

The function saves a video tensor and its corresponding label tensor to a specified directory as a `.pt` file. The file will be named using a specified index to ensure uniqueness.

#### Function Definition
```python
utils.pickle.pickle_data(X, y, n, path)
```

## Arguments

- **`X`** (`torch.Tensor`):  
  The video tensor to be saved.

- **`y`** (`torch.Tensor`):  
  The label tensor corresponding to the video.

- **`n`** (`int`):  
  The index used to name the saved file. The file will be named `tensor_<n>.pt`.

- **`path`** (`str`):  
  The directory where the tensor file will be saved. If the directory does not exist, it will be created automatically.

## Behavior

- A dictionary containing the video tensor and label tensor is created and saved to disk as a `.pt` file.
- The file is named `tensor_<n>.pt`, where `<n>` corresponds to the provided index.
- If the specified directory does not exist, it is created automatically.

## Example Usage

```python
import torch
import os

# Example tensors
X = torch.randn(3, 224, 224)  # Example video tensor
y = torch.tensor(1)          # Example label tensor

# Save the data
pickle_data(X, y, 0, "./output_tensors")
```

## Saved File Structure

For a `path` of `./output_tensors` and an index `n = 0`:
```
./output_tensors/
    tensor_0.pt
```

The `.pt` file contains a dictionary with two keys:
- `video`: The video tensor.
- `label`: The label tensor.

## Notes

- The `os.makedirs` function ensures the directory exists or is created automatically.
- Files are saved using `torch.save`, which serializes the tensors to the `.pt` format.

## Implementation

```python
def pickle_data(X : torch.tensor, y : torch.tensor, n : int, path : str):
    """
    Saves the input data and labels as a PyTorch tensor file.

    Args:
        X (tensor): The input data to be saved (e.g., video frames, features).
        y (tensor): The labels corresponding to the input data.
        n (int): A numerical identifier that will be used to name the saved file.
        path (str): The directory path where the tensor file will be saved.

    Saves:
        A tensor file named 'tensor_{n}.pt' containing the input data (X) and labels (y) 
        at the specified path. The directory is created if it doesn't exist.

    Example:
        pickle_data(X_data, y_labels, 1, '/path/to/save')
    """
    tensor_data = {
        'video': X,
        'label': y
    }
    os.makedirs(path, exist_ok=True)
    torch.save(tensor_data, os.path.join(path, f'tensor_{n}.pt'))
```
