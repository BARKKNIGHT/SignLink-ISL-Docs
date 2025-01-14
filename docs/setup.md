# Installation

## Commands

1. Clone the repository:
   ```bash
   git clone https://github.com/Naneet/SignLink-ISL.git
   ```

2. Navigate to the project directory
   ```
   cd SignLink-ISL
   ```

3. Install the required dependencies:
   ```
   pip install -r requirements.txt
   ```

## Usage

To understand the flow of the project and replicate the results, follow the notebooks in the recommended order:

1. **Video Dataset Conversion**
   - Notebook: `Video_dataset_conversion_refined.ipynb`
   - This notebook demonstrates the process of converting video datasets into frame-based tensors
2. **Dataset Augmentation**
   - Notebook: `Dataset_augmentation_pickled.ipynb`
   - Apply various augmentations (e.g., horizontal flip, random crop, random rotation) to pickled dataset.
3. **Training the Models**
   - Notebook: `Complete_INCLUDE_training_notebook.ipynb` / `Subset_50_training-notebook.ipynb`
   - Loads the pickled dataset.
   - Covers the training process using different models like r3d_18 and ResNet18 + GRU/LSTM.
   - Training configurations (e.g., hyperparameters, loss functions, optimizers).
   - Model evaluation metrics and saving trained models.
  
🚨🚨 We will also be creating docs for it soon for better understanding 🚨🚨 :)





