##Semi-supervised Approach for Dominant Gene Selection and Classification

## SADGSC: Running the Code

The main script (`main_SADGSC.m`) runs the Semi-Supervised Dominant Gene Selection and Classification (SADGSC) algorithm.

### Key Parameters and Variables

- `cv_num` : Number of cross-validation folds (default: 5)
- `lambda1–lambda6` : Regularization and weighting parameters controlling sparsity, noise suppression, reconstruction error, and other model effects
- `percentages` : Proportion of unlabeled data used in semi-supervised training (e.g., [0.9, 0.7, 0.5]) (0.9 means 10% labeled)
- `dataset_files` : List of dataset `.mat` files to process

### Workflow

1. Load datasets and prepare feature and target matrices.
2. Normalize the data and add bias term.
3. For each dataset and labeled data percentage:
   - Generate cross-validation splits (`generateCVSet`).
   - Mask a portion of the labels for semi-supervised learning (`mask_target_entries`).
   - Train the model using `[out, ~] = model(...)`.
   - Predict outputs and assign labels using `assignLabelsToHighestValue`.
   - Evaluate performance: Average Precision, Weighted F1 Score, AUC.
4. Average results across CV folds and save to Excel (`WeightedF1Scores.xlsx`).

### Example Usage
```matlab
cv_num = 5;
percentages = [0.9, 0.7, 0.5];
dataset_files = {'breast_can.mat'};
lambda1 = 1; lambda2 = 1; lambda3 = 100;
lambda4 = 10; lambda5 = 1; lambda6 = 0.01;

% Run main script
run('main_SADGSC.m')

