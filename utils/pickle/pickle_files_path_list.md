# `pickle_files_path_lists`

Recursively collects all file paths in a specified directory.

## Description

The function iterates over a dataloader that yields tuples of video tensors and their corresponding label tensors. Each tuple is saved to disk as a `.pt` file in the specified directory. The directory will be created if it does not already exist.

#### Function Definition
```python
def pickle_files_path_list(path) -> list:
```

## Arguments

- **`path`** (`str`):  
  The directory where the tensor files are located.

## Behavior

## Example Usage

## Notes

## Implementation
