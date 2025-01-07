# `display_conf_matrix`

Displays the confusion matrix of predicted and true labels.

## Description

This function calculates and visualizes a confusion matrix for the given true and predicted labels. The matrix is plotted using a customizable colormap for better readability. The confusion matrix is returned as a NumPy array, which can be used for further analysis or inference.

#### Function Definition
```python
def display_conf_matrix(y_true, y_pred, num_words=50):
```

## Arguments

- **`y_true`** (`array-like`):  
  The true labels for the dataset.

- **`y_pred`** (`array-like`):  
  The predicted labels for the dataset.

- **`num_words`** (`int`, optional):  
  The number of classes to be displayed in the confusion matrix. Default is `50`. This argument is useful when the number of classes is large, and the matrix might become too cluttered.

## Example Usage

```python
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay

# Example true and predicted labels
y_true = [0, 1, 2, 2, 0, 1]
y_pred = [0, 1, 2, 1, 0, 0]

# Display the confusion matrix
cm = display_conf_matrix(y_true, y_pred)
```

## Returned Value

- **`cm`** (`ndarray`):  
  A NumPy array containing the confusion matrix. This array can be used for further analysis or processing.

## Notes

- The function uses `ConfusionMatrixDisplay` from `sklearn` to visualize the confusion matrix.
- The matrix is displayed using the `viridis` colormap, but this can be customized.
- The `num_words` argument ensures that the confusion matrix can handle a large number of classes.

## Implementation

```python
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay

def display_conf_matrix(y_true, y_pred, num_words=50):
    """
    Displays and returns the confusion matrix for the given true and predicted labels.

    Args:
        y_true (array-like): The true labels for the dataset.
        y_pred (array-like): The predicted labels for the dataset.
        num_words (int, optional): The number of classes to display in the matrix. Default is 50.

    Returns:
        numpy.ndarray: The confusion matrix as a NumPy array.

    Example:
        cm = display_conf_matrix(y_true, y_pred)
    """
    cm = confusion_matrix(y_true, y_pred)
    disp = ConfusionMatrixDisplay(confusion_matrix=cm, display_labels=range(num_words))
    disp.plot(cmap="viridis")  # Customize colormap if needed
    return cm  # Returning cm because there are too many classes and the Confusion Matrix gets messy.
```
