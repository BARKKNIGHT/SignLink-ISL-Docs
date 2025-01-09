# `load_checkpoint`

Load the model and optimizer state from a checkpoint file.

## Description

The function loads the state of the model, optimizer, and any other relevant training information from a checkpoint file. This is useful for resuming training or evaluating a previously saved model.

#### Function Definition
```python
utils.save_load.load_checkpoint(filename="checkpoint.pth") -> dict
```

## Arguments

- **`filename`** (`str`, optional):  
  The name of the file from which the checkpoint will be loaded. Default is `'checkpoint.pth'`.

## Returns

- **`dict`**:  
  A dictionary containing:
  - `model_state_dict`: The state dictionary of the model.
  - `optimizer_state_dict`: The state dictionary of the optimizer.
  - Other relevant training information (e.g., epoch number).

## Example Usage

```python
import torch

# Example model and optimizer
model = torch.nn.Linear(10, 1)
optimizer = torch.optim.SGD(model.parameters(), lr=0.01)

# Load the checkpoint
checkpoint = load_checkpoint('model_checkpoint.pth')

# Restore model and optimizer state
model.load_state_dict(checkpoint['model_state_dict'])
optimizer.load_state_dict(checkpoint['optimizer_state_dict'])
```

## Notes

- The function uses `torch.load` to deserialize the checkpoint file.
- Ensure that the checkpoint file exists and matches the expected format before calling this function.
- Useful for both resuming interrupted training sessions and evaluating saved models.

## Implementation

```python
import torch

def load_checkpoint(filename="checkpoint.pth") -> dict:
    """
    Loads the model and optimizer state from a checkpoint file.

    Args:
        filename (str, optional): The name of the file from which the checkpoint will be loaded. Default is 'checkpoint.pth'.

    Returns:
        dict: A dictionary containing the model state, optimizer state, and any other relevant training information.

    Example:
        checkpoint = load_checkpoint('model_checkpoint.pth')\\
        model.load_state_dict(checkpoint['model_state_dict'])\\
        optimizer.load_state_dict(checkpoint['optimizer_state_dict'])
    """
    checkpoint = torch.load(filename)
    return checkpoint
```
