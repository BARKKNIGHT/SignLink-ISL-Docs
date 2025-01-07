# `data_and_words`

#### Overview
The `data_and_words` function loads file paths and their corresponding labels from a dataset directory structure. Each subdirectory name is treated as a label, and the files within represent the data samples for that label.

#### Function Definition
```python
def data_and_words(path):
```

#### Arguments
- **path** (`str`):
  - Path to the root directory of the dataset. Each subdirectory should represent a label and contain files belonging to that category.

#### Returns
- **tuple**: A tuple containing:
  - **data** (`list`):
    - A list of tuples where each tuple consists of:
      - The file path (`str`) to a data sample (e.g., video).
      - The numeric label (`int`) corresponding to the category.
  - **words_list** (`list`):
    - A list of category names (`str`) corresponding to their numeric labels.
  - **words_dict** (`dict`):
    - A dictionary mapping category names (`str`) to their numeric labels (`int`).

#### Notes
- The numeric labels are assigned in the order of the subdirectories as returned by `os.listdir`.
- Ensure that the directory structure is consistent, with subdirectories representing categories and containing relevant files.

#### Example
```python
# Directory structure:
# root/
# ├── cat/
# │   ├── cat1.mp4
# │   ├── cat2.mp4
# ├── dog/
# │   ├── dog1.mp4
```

## Function call:
```
data, words_list, words_dict = data_and_words("root")
```
## Output:
```
# data: [("root/cat/cat1.mp4", 0), ("root/cat/cat2.mp4", 0), ("root/dog/dog1.mp4", 1)]
# words_list: ["cat", "dog"]
# words_dict: {"cat": 0, "dog": 1}
```

## Implementation
```python
def data_and_words(path):
    """
    Loads file paths and their corresponding labels from a dataset directory structure.

    Args:
        path (str): Path to the root directory of the dataset. 
                    Each subdirectory should represent a label and contain files belonging to that category.

    Returns:
        tuple: A tuple containing:
            - data (list): A list of tuples where each tuple consists of:
                - The file path (str) to a data sample (e.g., video).
                - The numeric label (int) corresponding to the category.
            - words_list (list): A list of category names (str) corresponding to their numeric labels.
            - words_dict (dict): A dictionary mapping category names (str) to their numeric labels (int).

    Notes:
        - The numeric labels are assigned in the order of the subdirectories as returned by `os.listdir`.
        - Ensure that the directory structure is consistent, with subdirectories representing categories
          and containing relevant files.

    Example:
        If the directory structure is:
        root/
        ├── cat/
        │   ├── cat1.mp4
        │   ├── cat2.mp4
        ├── dog/
        │   ├── dog1.mp4

        Calling `data_and_words("root")` will return:
            - data: [("root/cat/cat1.mp4", 0), ("root/cat/cat2.mp4", 0), ("root/dog/dog1.mp4", 1)]
            - words_list: ["cat", "dog"]
            - words_dict: {"cat": 0, "dog": 1}
    """
    words = os.listdir(path)
    words_list = []
    data = []
    for word in words:
        words_list.append(word)
        word_videos_path = os.path.join(path, word)
        videos = os.listdir(word_videos_path)
        for video in videos:
            data.append((os.path.join(word_videos_path, video), len(words_list)-1))

    words_dict = dict({})
    for num, word in enumerate(words_list):
        words_dict[word] = num

    return data, words_list, words_dict
```
