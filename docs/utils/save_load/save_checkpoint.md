# `save_checkpoint`

Save the model and optimizer state to a specified file.

## Description

The function saves the state of the model, optimizer, and any other relevant training information to a file. This is useful for checkpointing during training, allowing you to resume training or evaluate the model later.

#### Function Definition
```python
utils.save_load.save_checkpoint(state, filename="checkpoint.pth")
```

## Arguments

- **`state`** (`dict`):  
  A dictionary containing:
  - `model_state_dict`: The state dictionary of the model.
  - `optimizer_state_dict`: The state dictionary of the optimizer.
  - Other relevant training information (e.g., epoch number).

- **`filename`** (`str`, optional):  
  The name of the file where the checkpoint will be saved. Default is `'checkpoint.pth'`.

## Example Usage

```python
import torch

# Example model and optimizer
model = torch.nn.Linear(10, 1)
optimizer = torch.optim.SGD(model.parameters(), lr=0.01)

# Create a checkpoint dictionary
state = {
    'epoch': 10,
    'model_state_dict': model.state_dict(),
    'optimizer_state_dict': optimizer.state_dict()
}

# Save the checkpoint
save_checkpoint(state, 'model_checkpoint.pth')
```

## Saved File Structure

The saved file (e.g., `model_checkpoint.pth`) contains a dictionary with keys like:
- `epoch`: The epoch number at which the checkpoint was created.
- `model_state_dict`: The serialized model parameters.
- `optimizer_state_dict`: The serialized optimizer parameters.

## Notes

- Use `torch.load` to load the saved checkpoint when resuming training or for evaluation.
- The function ensures that training progress is not lost in case of interruptions.

## Implementation

```python
import torch

def save_checkpoint(state, filename="checkpoint.pth"):
    """
    Saves the model and optimizer state to a specified file.

    Args:
        state (dict): A dictionary containing the model state, optimizer state, and any other relevant training information.
        filename (str, optional): The name of the file where the checkpoint will be saved. Default is 'checkpoint.pth'.

    Example:
        save_checkpoint({'epoch': 10, 'model_state_dict': model.state_dict(), 'optimizer_state_dict': optimizer.state_dict()}, 'model_checkpoint.pth')
    """
    torch.save(state, filename)
```

