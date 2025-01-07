# `preload_tensors`

Loads tensors from a list of file paths and transfers them to the specified device.

## Description

This function loads tensor data from a list of file paths and transfers both the input tensors (e.g., video data) and label tensors to the specified device (e.g., CPU or GPU). It is useful for preparing data for machine learning models. (Only use when dataset smaller than Device RAM)!

#### Function Definition

```python
def preload_tensors(path_list, device):
```

## Arguments

- **`path_list`** (`list`):
  A list of file paths to the tensor files to be loaded.
- **`device`** (`torch.device`):
  The device (CPU or CUDA) to which the tensors will be transferred.

## Behavior

The function iterates over the list of file paths, loading tensor dictionaries from each file. The dictionaries are expected to contain two keys:

- `'video'`: The input tensor (e.g., video frames or features).
- `'label'`: The label tensor corresponding to the input.

Each tensor is transferred to the specified device and stored as a tuple of `(video, label)` in a list.

### Detailed Steps

1. Initialize an empty list `data`.
2. For each file path in `path_list`, load the tensor dictionary using `read_pickle_dict`.
3. Extract the `'video'` and `'label'` tensors and transfer them to the specified device using `.to(device)`.
4. Append the tuple `(video, label)` to `data`.
5. Return the `data` list.

## Example Usage

```python
import torch

def preload_tensors(path_list, device):
    """
    Loads tensors from a list of file paths and transfers them to the specified device.

    Args:
        path_list (list): A list of file paths to the tensor files to be loaded.
        device (torch.device): The device (CPU or CUDA) to which the tensors will be transferred.

    Returns:
        list: A list of tuples, where each tuple contains:
            - video (torch.tensor): The input data (e.g., video frames, features) loaded and transferred to the specified device.
            - label (torch.tensor): The corresponding labels, loaded and transferred to the specified device.
    """
    data = []
    for path in path_list:
        tensor = read_pickle_dict(path)  # Load tensor dict from disk
        video, label = tensor['video'].to(device), tensor['label'].to(device) # Move the tensors to device
        data.append((video, label))
    return data

# Example usage
data = preload_tensors(['/path/to/file1.pt', '/path/to/file2.pt'], torch.device('cuda'))
print(data)
```

## Notes

- Ensure the tensor files are saved in a format compatible with `read_pickle_dict`.
- The tensors in the dictionary must have keys `'video'` and `'label'` for this function to work correctly.
- The function assumes that the tensor files can be loaded into memory; for very large datasets, consider alternative approaches such as lazy loading or batching.

## Implementation

```python
import torch

def preload_tensors(path_list, device):
    """
    Loads tensors from a list of file paths and transfers them to the specified device.

    Args:
        path_list (list): A list of file paths to the tensor files to be loaded.
        device (torch.device): The device (CPU or CUDA) to which the tensors will be transferred.

    Returns:
        list: A list of tuples, where each tuple contains:
            - video (torch.tensor): The input data (e.g., video frames, features) loaded and transferred to the specified device.
            - label (torch.tensor): The corresponding labels, loaded and transferred to the specified device.
    """
    data = []
    for path in path_list:
        tensor = read_pickle_dict(path)  # Load tensor dict from disk
        video, label = tensor['video'].to(device), tensor['label'].to(device) # Move the tensors to device
        data.append((video, label))
    return data
```