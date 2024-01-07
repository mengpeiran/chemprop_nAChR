## Installation

By clicking [**here**](/chemprop) to the chemprop subdirectory, detailed instructions on the installation of chemprop can be found. Specfically, we installed via source for this project.

## Training

If you wish to train a new model on different data, continue on here, replacing paths where appropriate. 

If you wish to use the model to predict for antimicrobial activities on other data sets, move to the Prediction subheader. Training data for this data set is made available in the supplementary section of the paper. 

Using the given data sets as an example, to train a Chemprop model with ensembling and RDKit global features, use the following command while in the chemprop conda environment.*

```chemprop_train --data_path data/train_alpha7.csv --dataset_type classification --save_dir model_checkpoint5 --features_generator rdkit_2d_normalized --no_features_scaling --num_folds 10 --split_type scaffold_balanced --split_sizes 0.6 0.2 0.2 --extra_metrics accuracy binary_cross_entropy f1 mcc```

Details of used parameters can be found in the documentation of the main Chemprop repository. 


## Prediction
Activity scores produced by the model were used as the main method of prioritizing molecules. 

To perform predictions on this set using models found in the paper:

```chemprop_predict --test_path data/prediction_set.csv --checkpoint_dir models/final_model --preds_path data/predictions.csv --features_generator rdkit_2d_normalized --no_features_scaling```


