# `__init__`

#### Initializes an object of Trainer Class with necessary parameters to train a model.

#### Function Definition
```python
__init__(self,model,device,optimizer,scheduler,loss_fn,train_dataloader,test_dataloader,save=False)
```

## Parameters

### `model`
- **Type:** `torch.nn.Module`
- **Description:** The neural network model to be trained and evaluated.

### `device`
- **Type:** `torch.device`
- **Description:** Specifies the computation device (`'cpu'` or `'cuda'`).

### `optimizer`
- **Type:** `torch.optim.Optimizer`
- **Description:** Optimizer used for updating model weights during training.

### `scheduler`
- **Type:** `torch.optim.lr_scheduler._LRScheduler`
- **Description:** Learning rate scheduler to adjust the learning rate during training.

### `loss_fn`
- **Type:** `callable`
- **Description:** The loss function to compute the difference between predictions and target labels.

### `train_dataloader`
- **Type:** `torch.utils.data.DataLoader`
- **Description:** DataLoader for the training dataset.

### `test_dataloader`
- **Type:** `torch.utils.data.DataLoader`
- **Description:** DataLoader for the testing/validation dataset.

### `save`
- **Type:** `bool`
- **Default:** `False`
- **Description:** Flag indicating whether to save the model after training.

## Example Usage

```python
from torch import nn, optim
from torch.utils.data import DataLoader
from torch.optim.lr_scheduler import StepLR
from torch.cuda.amp import GradScaler
from trainers.trainer import Trainer
from models.Conv3D import SignLanguageClassifier

# Define components
model = SignLanguageClassifier(len(word_to_idx)).to(device)
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)
loss_fn = nn.CrossEntropyLoss()

scheduler = ReduceLROnPlateau(
    optimizer,
    mode='min',
    factor=0.1,
    patience=5,
    min_lr=1e-6
)

# Initialize
trainer = Trainer(
    model=model,
    device=device,
    optimizer=optimizer,
    scheduler=scheduler,
    loss_fn=loss_fn,
    train_dataloader=train_dataloader,
    test_dataloader=test_dataloader,
    save=True
)
```