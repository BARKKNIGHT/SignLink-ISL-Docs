# `show_performance_scores`

Displays performance metrics (F1 score, precision, recall) for multiple averaging methods (micro, macro, weighted) and overall accuracy.

## Description

This function calculates and prints performance scores for classification tasks based on three averaging methods: 'micro', 'macro', and 'weighted'. It evaluates F1 score, precision, and recall for each averaging method and also computes the overall accuracy.

#### Function Definition
```python
utils.metrics.show_performance_scores(y_true, y_pred)
```

## Arguments

- **`y_true`** (`array-like`):  
  The true labels for the dataset.

- **`y_pred`** (`array-like`):  
  The predicted labels for the dataset.

## Example Usage

```python
from sklearn.metrics import precision_score, recall_score, f1_score, accuracy_score

# Example true and predicted labels
y_true = [0, 1, 2, 2, 0, 1]
y_pred = [0, 1, 2, 1, 0, 0]

# Show performance scores
show_performance_scores(y_true, y_pred)
```

## Printed Output

The function will print the following for each averaging type (micro, macro, weighted):

- F1 score
- Precision
- Recall

It will also print the overall accuracy at the end.

## Notes

- The function supports multiple averaging methods: `micro`, `macro`, and `weighted`. 
  - **Micro**: Calculates metrics globally by counting the total true positives, false positives, etc.
  - **Macro**: Calculates metrics for each label, then finds their unweighted mean.
  - **Weighted**: Calculates metrics for each label, and finds their average weighted by support (the number of true instances for each label).
- The accuracy score is calculated using `accuracy_score` from `sklearn.metrics`.

## Implementation

```python
from sklearn.metrics import precision_score, recall_score, f1_score, accuracy_score

def show_performance_scores(y_true, y_pred):
    """
    Displays performance metrics (F1 score, precision, recall) for multiple averaging methods and overall accuracy.

    Args:
        y_true (array-like): The true labels for the dataset.
        y_pred (array-like): The predicted labels for the dataset.

    Example:
        show_performance_scores(y_true, y_pred)
    """
    types = ['micro', 'macro', 'weighted']
    for ty in types:
        print(ty)
        precision = precision_score(y_true, y_pred, average=ty) 
        recall = recall_score(y_true, y_pred, average=ty)        
        f1 = f1_score(y_true, y_pred, average=ty) 
        print(f"F1 Score: {f1:.4f}")
        print(f"Precision: {precision:.4f}")
        print(f"Recall: {recall:.4f}")
        print("***************")
    print(f"Acc = {accuracy_score(y_true, y_pred):.4f}")
```
