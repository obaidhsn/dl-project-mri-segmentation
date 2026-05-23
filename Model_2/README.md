# BraTS 2020 3D AIR-UNet Segmentation

This project trains and evaluates 3D AIR-UNet based models for BraTS 2020 brain tumor segmentation. The target regions are whole tumor (WT), tumor core (TC), and enhancing tumor (ET).

## Setup

Install the required packages:

```bash
pip install -r requirements.txt
```

If using CUDA, install the PyTorch version that matches your CUDA setup from the official PyTorch instructions.

## Files

- `dataset_exploration.ipynb`: downloads/prepares the BraTS dataset and explores the data.
- `Model_2_AIR_MAIN.ipynb`: trains the main full-volume 3D AIR-UNet model on resized `128 x 128 x 128` MRI volumes.
- `Model_2_AIR_Patch.ipynb`: trains the auxiliary patch-based 3D AIR-UNet model focused more on TC and ET.
- `Model_2_AIR_Ensemble.ipynb`: loads both trained checkpoints, combines their probability maps, evaluates train/validation/test metrics, and saves/visualizes final 3D predictions.
- `requirements.txt`: Python package dependencies.

## Run Order

1. Run `dataset_exploration.ipynb` to download the BraTS 2020 data.
2. Run `Model_2_AIR_MAIN.ipynb` to train the main full-volume model.
3. Run `Model_2_AIR_Patch.ipynb` to train the patch-based model.
4. Run `Model_2_AIR_Ensemble.ipynb` to combine both models and generate final metrics/predictions.

## Outputs

- Model checkpoints are saved in `checkpoints/`.
- Processed cached tensors are saved in `data/processed/`.
- Final ensemble masks and visualization outputs are saved in `predictions/paper3_ensemble_3d_masks/`.

## Notes

The ensemble uses the full-volume model mainly for global structure and the patch model as a small refinement for TC and ET. Validation-based thresholds are selected before reporting final test metrics.
