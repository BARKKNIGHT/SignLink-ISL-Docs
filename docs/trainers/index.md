# Trainers

This section contains classes necessary for training models using dataloaders or pickled data.

## Contents

### [Trainer Class](./trainer/init.md)  
Class for training with ```torch.utils.data.DataLoader``` dataset loader.

### [Trainer_Batch_Slice Class](./trainer_batch_slice/init.md)
Class for training with ```pickled_data``` dataset and enables adaptive slicing of batch tensors into equal parts for training in ```vram``` constrained environments.

### [Trainer_Pickle Class](./trainer_pickle/init.md)  
Class for training with  ```pickled_data``` dataset.

### [Trainer_Pickle_Preload Class](./trainer_pickle_preload/init.md)  
Class for training with  ```pickled_data``` dataset and invloves tools like ```utils.pickle.preload_tensors(path_list, device)``` to prefetch data into vram to improve performance by reducing ```I/O``` fetching between epochs. ⚠️⚠️ Only for Environments where the entire dataset fits the vram constraints⚠️⚠️.


