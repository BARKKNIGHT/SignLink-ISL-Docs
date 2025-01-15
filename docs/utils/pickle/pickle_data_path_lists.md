# `pickle_data_path_lists`

Save data from a dataloader to disk as separate tensor files.

## Description

The function iterates over a dataloader that yields tuples of video tensors and their corresponding label tensors. Each tuple is saved to disk as a `.pt` file in the specified directory. The directory will be created if it does not already exist.

#### Function Definition
```python
utils.pickle.pickle_data_path_lists(path, dataloader)
```

## Arguments

- **`path`** (`str`):  
  The directory where the tensor files will be saved. If the directory does not exist, it will be created automatically.

- **`dataloader`** (`iterable`):  
  An iterable (e.g., a PyTorch DataLoader) that yields tuples `(X, y)`.  
  - `X`: The video tensor.  
  - `y`: The corresponding label tensor.

## Behavior

- Each item in the dataloader is saved as a separate `.pt` file in the specified directory.
- Filenames are formatted as `tensor_<index>.pt`, where `<index>` corresponds to the index of the item in the dataloader.

## Example Usage

```python
from torch.utils.data import DataLoader
import torch
import os

# Example dataloader
data = [ 
    (torch.randn(3, 224, 224), torch.tensor(0)), 
    (torch.randn(3, 224, 224), torch.tensor(1))
]
dataloader = DataLoader(data, batch_size=1)

# Save tensors to disk
pickle_data_path_lists("./output_tensors", dataloader)
```

## Saved File Structure

For a `path` of `./output_tensors` and a dataloader containing 3 samples:
```
./output_tensors/
    tensor_0.pt
    tensor_1.pt
    tensor_2.pt
```

Each `.pt` file contains a dictionary with two keys:
- `video`: The video tensor.
- `label`: The label tensor.

## Notes

- The `os.makedirs` function ensures the directory exists or is created automatically.
- Files are saved using `torch.save`, which serializes the tensors to the `.pt` format.

## Implementation

```python
def pickle_data_path_lists(path : str, dataloader):
    """
    Save data from a dataloader to disk as separate tensor files.

    Args:
        path (str): Directory where the tensor files will be saved.
        dataloader (iterable): An iterable that yields tuples (X, y), where
            X is the video tensor and y is the corresponding label tensor.

    Each item from the dataloader will be saved as a .pt file in the specified
    directory, with filenames formatted as 'tensor_<index>.pt'.
    The directory will be created if it does not already exist.
    """
    for n, (X, y) in enumerate(dataloader):
        tensor_data = {
            'video': X,
            'label': y
        }
        os.makedirs(path, exist_ok=True)
        torch.save(tensor_data, os.path.join(path, f'tensor_{n}.pt'))
```
