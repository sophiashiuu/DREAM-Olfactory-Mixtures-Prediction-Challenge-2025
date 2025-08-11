# DREAM Olfactory Mixtures Prediction Challenge 2025
## 📌 Background & Motivation
Predicting human olfactory perception from chemical structure is a major challenge in computational neuroscience. While molecular descriptors capture structural information, translating this into accurate perceptual predictions remains difficult.

Our goal was to:

Predict perceptual ratings for single molecules (Task 1) and mixtures (Task 2).

Use Random Forest Regression for its balance of interpretability, robustness, and ability to handle high-dimensional molecular data.

Integrate diverse molecular features to improve generalization to unseen compounds and mixtures.

Feature Sources:

Mordred descriptors

Morgan fingerprints

OpenPOM perceptual vectors

## 🛠 Methods
Task 1: Single-Molecule Prediction
* Data Integration:
*   Merged TASK1_Stimulus_definition.csv with Mordred_Descriptors.csv on molecule.
*   Combined with TASK1_training.csv on stimulus.

* Feature Selection:
*   Removed non-numeric and metadata columns (stimulus, molecule, dilution, etc.).

* Preprocessing:
*   Replaced infinite values with NaN, missing values with 0.
*   Scaled features with StandardScaler.

* Model:
*   RandomForestRegressor wrapped in MultiOutputRegressor.
*   Hyperparameters: n_estimators=100, random_state=42.
*   Train-validation split: 80/20.

* Evaluation Metric: 
*   Root Mean Squared Error (RMSE).

Task 2: Mixture Prediction
* Data Integration:
*   Merged Mordred_Descriptors.csv and Morgan_fingerprints.csv on molecule.
*   Added SMILES strings and OpenPOM_Dream_RATA.csv perceptual data.

* Component Aggregation:
*   Linked component-level features to stimuli.
*   Averaged numeric features per mixture.
*   Missing values → zeros.

* Preprocessing:
*   Scaled features using training set statistics.

* Model:
*   Same setup as Task 1.
*   Train-validation split: 90/10.

* Evaluation Metrics:
*   RMSE
*   Mean Cosine Distance
*   Mean Pearson Correlation

## 📊 Tools & Libraries
* Python 3.11

* pandas, numpy — data wrangling

* scikit-learn — modeling & evaluation

## 📈 Results & Discussion
Task 1 was easier to model due to direct molecule-descriptor mapping while Task 2 required aggregation of multiple molecular representations for mixtures. At the end, we came to terms that combining diverse molecular features improved generalization.

Major challenge: missing features for some components, handled via zero imputation.

## Future work:
Capture interactions between mixture components.
Go beyond simple averaging for mixture representation.
