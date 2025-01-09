# `random_split`

#### Overview
The `random_split` function is used to split a dataset into training and testing sets based on a specified ratio. It ensures that the split is random and reproducible using a fixed seed.

#### Function Definition
```python
utils.data_words.random_split(data_dict, train_ratio=0.8, seed=42)
```

#### Arguments
- **data_dict** (`dict`):
  - A dictionary where keys are labels (e.g., strings) and values are lists of paths (e.g., file paths or data samples corresponding to those labels).

- **train_ratio** (`float`, optional):
  - The proportion of data to include in the training set. Defaults to `0.8`.

- **seed** (`int`, optional):
  - Random seed for reproducibility of the data split. Defaults to `42`.

#### Returns
- **tuple**: Returns two lists, `train_data` and `test_data`.
  - **train_data** (`list`):
    - A list of tuples, where each tuple contains a path and its corresponding label index, e.g., `[(path1, label_index1), (path2, label_index2), ...]`.
  - **test_data** (`list`):
    - A list of tuples, similar to `train_data`, but for the testing set.

#### Notes
- Paths for each label are shuffled before splitting to ensure randomness.

## Example
```python
data_dict = {
    "cat": ["cat1.jpg", "cat2.jpg", "cat3.jpg"],
    "dog": ["dog1.jpg", "dog2.jpg"]
}
word_to_idx = {"cat": 0, "dog": 1}

train_data, test_data = random_split(data_dict, train_ratio=0.7)
```

### Output
```python
train_data: [("cat1.jpg", 0), ("dog1.jpg", 1), ...]
test_data: [("cat3.jpg", 0), ("dog2.jpg", 1)]
```

## Implementation
```python
def random_split(data_dict, word_to_idx, train_ratio=0.8, seed=42):
    """
    Splits a dataset into training and testing sets based on the specified ratio.

    Args:
        data_dict (dict): A dictionary where keys are labels (e.g., strings), and values are lists of paths 
                          (e.g., file paths or data samples corresponding to those labels).
        train_ratio (float, optional): The proportion of data to include in the training set. Defaults to 0.8.
        seed (int, optional): Random seed for reproducibility of the data split. Defaults to 42.

    Returns:
        tuple: Two lists, `train_data` and `test_data`.
            - train_data: A list of tuples, where each tuple contains a path and its corresponding label index, 
                          e.g., [(path1, label_index1), (path2, label_index2), ...].
            - test_data: A list of tuples, similar to `train_data`, but for the testing set.

    Notes:
        - This function assumes a global or pre-defined dictionary `word_to_idx` mapping label names to integer indices.
        - Paths for each label are shuffled before splitting to ensure randomness.

    Example:
        data_dict = {
            "cat": ["cat1.jpg", "cat2.jpg", "cat3.jpg"],
            "dog": ["dog1.jpg", "dog2.jpg"]
        }
        word_to_idx = {"cat": 0, "dog": 1}

        train_data, test_data = random_split(data_dict, train_ratio=0.7)
        # train_data: [("cat1.jpg", 0), ("dog1.jpg", 1), ...]
        # test_data: [("cat3.jpg", 0), ("dog2.jpg", 1)]
    """
    np.random.seed(seed)
    train_data = []
    test_data = []

    for label, paths in data_dict.items():
        # Shuffle the paths
        paths = np.array(paths)
        np.random.shuffle(paths)

        # Split into training and testing
        split_idx = int(len(paths) * train_ratio)
        train_paths = paths[:split_idx].tolist()
        test_paths = paths[split_idx:].tolist()

        # Append the paths with their labels
        train_data.extend([(path, word_to_idx[label]) for path in train_paths])
        test_data.extend([(path, word_to_idx[label]) for path in test_paths])

    return train_data, test_data
```

