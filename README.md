#Installation
By clicking here to the chemprop subdirectory, detailed instructions on the installation of chemprop can be found. Specfically, we installed via source for this project.

#Training
A model similar to that used to predict Abaucin can be found here.

If you wish to train a new model on different data, continue on here, replacing paths where appropriate.

If you wish to use the model to predict for antimicrobial activities on other data sets, move to the Prediction subheader. Training data for this data set is made available in the supplementary section of the paper1.

Using the given data sets as an example, to train a Chemprop model with ensembling and RDKit global features, use the following command while in the chemprop conda environment.*

chemprop_train --data_path data/SD_1_training_set.csv --features_generator rdkit_2d_normalized --no_features_scaling --target_columns Activity --dataset_type classification --split_type cv --save_dir models/custom

Details of used parameters can be found in the documentation of the main Chemprop repository.

#Prediction
Activity scores produced by the model were used as the main method of prioritizing molecules. In the paper described, we used the Broad Drug Repurposing Hub as a prediction set (raw data here).*

To perform predictions on this set using models found in the paper:

chemprop_predict --test_path data/SD2_raw_prediction_set.csv --checkpoint_dir models/final_model --preds_path data/predictions.csv --features_generator rdkit_2d_normalized --no_features_scaling

#Additional Tools
Tanimoto Nearest Neighbor Calculations
Tanimoto similarity calculations are performed using Morgan fingerprints (bits = 2048, r = 2). The maximum similarity is returned on, as well as the corresponding SMILES of the 'most similar' molecule. *

python ./chemprop/scripts/nearest_neighbor_tanimoto.py --data_path data/SD2_raw_prediction_set.csv --reference_data_path data/SD_1_training_set.csv --save_path data/SD2_raw_prediction_set_with_similarity.csv

*Data files may need additional manual processing such as header removal or binarization to be correctly formatted for the code.
