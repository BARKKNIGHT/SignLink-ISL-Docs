# `train_step`

## Purpose
Executes a single training epoch for the model using the training dataset. It utilizes automatic mixed precision (AMP) for efficient computation on CUDA-enabled devices. The method computes loss, updates model weights, and tracks training accuracy.

---

## Parameters

### `epoch`
- **Type:** `int`
- **Description:** The current epoch number, used for logging and model saving purposes.

---

## Workflow

1. **Set Model to Training Mode**:  
   `self.model.train()` sets the model in training mode to enable gradient computation.

2. **Initialize Metrics**:  
   - `train_loss`: Tracks cumulative loss across all batches in the epoch.  
   - `total_correct`: Tracks the number of correct predictions.  
   - `total_samples`: Tracks the total number of samples processed.

3. **Iterate Through Training DataLoader**:
   - Moves input (`X`) and labels (`y`) to the specified computation device.
   - Performs forward pass using AMP:
     - Computes model predictions (`y_pred`).
     - Calculates loss using `self.loss_fn`.
   - Scales the loss for AMP and performs backpropagation.
   - Updates model parameters using `self.optimizer`.
   - Resets gradients after each update.

4. **Compute Accuracy**:
   - Converts predictions to class labels.
   - Compares predictions with ground truth labels to compute batch accuracy.
   - Aggregates results for all batches.

5. **Log Metrics**:
   - Computes and prints epoch-level loss and accuracy.

6. **Adjust Learning Rate** (if using `ReduceLROnPlateau` scheduler):
   - Calls `self.scheduler.step()` with the epoch loss.

---

## Key Components

### Automatic Mixed Precision (AMP)
- **Purpose**: Improves training speed and reduces memory usage by using lower precision (FP16) during computations.
- **Implementation**: `autocast('cuda')` and `GradScaler`.

### Accuracy Calculation
- **Formula**:  
  \[
  \text{Accuracy} = \left( \frac{\text{Total Correct Predictions}}{\text{Total Samples}} \right) \times 100
  \]

---

## Example Usage

```python
# Train the model for one epoch
my_object.train_step(epoch=1)
```

---

## Output
Logs the following metrics to the console:
- Epoch number
- Average training loss for the epoch
- Training accuracy (percentage)

**Example Output**:
```
Epoch: 1 | Train Loss: 0.2458 | Accuracy: 89.52
```