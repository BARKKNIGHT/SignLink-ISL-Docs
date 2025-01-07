# `preload_data`

Transfers batches of data from a DataLoader to the specified device, to avoid repeated loading of data between epochs.

## Description

This function takes a PyTorch DataLoader and transfers its batches of data to a specified device (CPU or CUDA). It is useful for preparing data for training or inference on a specific hardware accelerator. (Only use when dataset smaller than Device RAM)!

#### Function Definition
```python
def preload_data(dataloader, device) -> list:
```

## Arguments

- **`dataloader`** (`torch.utils.data.DataLoader`):  
  The DataLoader that provides batches of data.

- **`device`** (`torch.device`):  
  The device (CPU or CUDA) to which the data batches will be transferred.

## Behavior

This function processes each batch from the DataLoader by transferring the input data (`X`) and the corresponding labels (`y`) to the specified device. These processed batches are collected into a list of tuples for further use in training or inference workflows.

## Example Usage

```python
import torch
from torch.utils.data import DataLoader

# Assuming `train_dataloader` is a predefined DataLoader
data = preload_data(train_dataloader, torch.device('cuda'))
for X, y in data:
    print(X.shape, y.shape)
```

## Notes

- Ensure the DataLoader is properly defined and yields batches as tuples of `(X, y)`.
- The `device` must be compatible with the tensors (e.g., ensure CUDA is available for GPU usage).

## Implementation
```python
def preload_data(dataloader, device) -> list:
    """
    Transfers batches of data from a DataLoader to the specified device.

    Args:
        dataloader (torch.utils.data.DataLoader): The DataLoader that provides batches of data.
        device (torch.device): The device (CPU or CUDA) to which the data batches will be transferred.

    Returns:
        list: A list of tuples, where each tuple contains:
            - X (torch.tensor): The input data (e.g., video frames, features) from the batch, transferred to the specified device.
            - y (torch.tensor): The corresponding labels from the batch, transferred to the specified device.

    Example:
        data = preload_data(train_dataloader, torch.device('cuda'))
    """
    data_tensor_list = []
    for X, y in dataloader:
        data_tensor_list.append((X.to(device), y.to(device)))
    return data_tensor_list
```

