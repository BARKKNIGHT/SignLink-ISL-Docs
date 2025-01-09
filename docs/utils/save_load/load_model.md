# `load_model`

Load the model state from a checkpoint and update the model.

## Description

The function updates the provided model with the state stored in a checkpoint file. This is useful for restoring a model's parameters for further training or evaluation.

#### Function Definition
```python
utils.save_load.load_model(model, checkpoint)
```

## Arguments

- **`model`** (`torch.nn.Module`):  
  The PyTorch model instance to load the state into.

- **`checkpoint`** (`dict`):  
  A dictionary containing the model state, typically loaded using a function like `load_checkpoint`. It should have the key `model_state_dict` which stores the model's parameters.

## Returns

- **`torch.nn.Module`**:  
  The model with the loaded state.

## Example Usage

```python
import torch

# Example model
model = torch.nn.Linear(10, 1)

# Example checkpoint loaded from a file
checkpoint = load_checkpoint('model_checkpoint.pth')

# Load the model state
model = load_model(model, checkpoint)
```

## Notes

- Ensure that the checkpoint dictionary contains a `model_state_dict` key corresponding to the model's state.
- The function uses `model.load_state_dict` to update the model's parameters.

## Implementation

```python
import torch

def load_model(model, checkpoint):
    """
    Loads the model state from a checkpoint and updates the model.

    Args:
        model (torch.nn.Module): The model to load the state into.
        checkpoint (dict): A dictionary containing the model state, typically loaded from a checkpoint file.

    Returns:
        torch.nn.Module: The model with the loaded state.

    Example:
        checkpoint = load_checkpoint('model_checkpoint.pth')
        model = load_model(model, checkpoint)
    """
    model.load_state_dict(checkpoint['model_state_dict'])
    return model
```