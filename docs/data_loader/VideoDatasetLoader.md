# `VideoDatasetLoader`

Helps loading video dataset into memory.

## Overview

The class `VideoDatasetLoader` is used to load a video dataset and label into memory, which can be used for training the model.

#### Class Definition
``python
VideoDatasetLoader(data, temp_data_folder, NUM_FRAMES=10, transform_frame=None,transform_video=None, video_fps=25, resolution='1920:1080')
``

## Arguments

- **`data`** (`list`):  
  It takes a list of tuples, where index zero is the path to the video and index 1 is the label of the video.
- **`temp_data_folder`** (`str`):
  A temporary folder where ffmpeg can store the frames of the video. The folder gets clear automatically.
- **`NUM_FRAMES`** (`int`):
  Number of frames to be extracted from the video. It refers to number of frames the tensor will have.
- **`transform_frame`** (`torchvision.transforms`):
  Transformations to be done on the individual frames.
- **`transform_video`** (`torchvision.transforms`):
  Transformations to be done on the whole video.
- **`video_fps`** (`int`):
  The fps at which the video will be saved by ffmpeg.
- **`resolution`** (`str`):
  Resolution at which ffmpeg will save the frames.

## Returns
- **`tuple`**: A tuple containing:
  - **`video_frames`** (`torch.tensor`):
     Returns a tensor with `NUM_FRAMES` number of frames from a video stacked.
  - **`label`** (`int`):
    Returns the label of the `video_frames`.

## Example Usage

train_dataset = VideoDataset(data=train_data, temp_data_folder=r"D:\ISL_temp", transform_frame=None, transform_video=None, NUM_FRAMES=24, video_fps=25, resolution='1280:720')