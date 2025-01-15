# `get_all_file_paths`

Recursively collects all file paths in a specified directory.

## Description

This function traverses a directory and its subdirectories to collect the paths of all files within. It is useful for tasks that require batch processing of files, such as loading datasets or organizing input files for machine learning workflows.

#### Function Definition
```python
utils.pickle.get_all_file_paths(path) -> list
```

## Arguments

- **`path`** (`str`):  
  The root directory to start searching for files.

## Behavior

The function walks through the directory tree using the `os.walk` method, which yields the directory path, subdirectories, and filenames at each level. It appends the full file paths (combination of directory path and filenames) to a list, which is returned as the result.

### Detailed Steps
1. Initialize an empty list `path_list`.
2. Use `os.walk` to iterate through each directory and subdirectory starting from the provided `path`.
3. For each file found, construct its full path using `os.path.join` and append it to `path_list`.
4. Return the `path_list` containing all file paths.

## Example Usage

```python
# Example usage
file_paths = get_all_file_paths('/path/to/directory')
print(file_paths)
```

This code will print a list of all file paths within `/path/to/directory` and its subdirectories.

## Notes

- Ensure the provided `path` is valid and accessible.
- The function will return an empty list if the directory does not contain any files.
- This function does not perform any filtering based on file types or extensions; if filtering is needed, you can modify the code to include a condition, e.g., `if file.endswith('.pt'):`.

## Implementation

```python
import os

def get_all_file_paths(path) -> list:
    """
    Recursively collects all file paths in a specified directory.

    Args:
        path (str): The root directory to start searching for files.

    Returns:
        list: A list of file paths (str) for all files in the directory and its subdirectories.
    """
    path_list = []
    for top, dirs, files in os.walk(path):
        for file in files:       
            path_list.append(os.path.join(top, file))
    return path_list
```

