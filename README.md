# Predicting Aqueous Solubility Using Machine Learning

## Overview

Aqueous solubility is a key physicochemical property in drug discovery, medicinal chemistry, and molecular design. Poor solubility can significantly affect the bioavailability and effectiveness of pharmaceutical compounds.

This project applies machine learning techniques to predict the aqueous solubility of organic molecules using molecular descriptors derived from chemical structures.

Multiple regression models were implemented, optimized, and evaluated to determine the most accurate predictive approach. The project follows a complete machine learning workflow including feature generation, feature selection, hyperparameter optimization, model evaluation, and model interpretation.

The analysis was implemented using Python and the machine learning tools available in scikit-learn.

---

## Dataset

The dataset used in this project is the **ESOL aqueous solubility dataset**, a widely used benchmark dataset in cheminformatics and quantitative structure–property relationship (QSPR) modeling. You can find the dataset at: **https://moleculenet.org/datasets-1**

The dataset contains:

* Molecular structures
* Calculated molecular descriptors
* Experimentally measured aqueous solubility values

The target variable is the logarithm of aqueous solubility (logS).

---

## Molecular Descriptors and Feature Generation

The dataset contains several precomputed molecular descriptors describing the physicochemical properties of each molecule, including:

- Molecular Weight
- Number of H-Bond Donors
- Number of Rings
- Number of Rotatable Bonds
- Polar Surface Area

These descriptors were directly used as input features for the machine learning models.

In addition, molecular fingerprints were generated using the cheminformatics toolkit RDKit. Fingerprints provide a numerical representation of molecular structure by encoding the presence or absence of specific chemical substructures.

The combination of molecular descriptors and structural fingerprints allows machine learning models to capture both physicochemical and structural information about the molecules.
---

## Feature Analysis with Lasso Regression

Lasso regression was applied to analyze the sparsity of the feature space and identify which predictors receive non-zero coefficients under L1 regularization.

Using the implementation provided in scikit-learn, the Lasso model assigns zero coefficients to less informative predictors while retaining the most influential features.

In this analysis, 142 features were assigned non-zero coefficients by the Lasso model. This observation provides insight into which molecular descriptors and fingerprint bits contribute to predicting aqueous solubility.

The results were used for exploratory analysis rather than strict feature selection, as the full feature set was retained for training and evaluating the other machine learning models.
---

## Machine Learning Models

Several regression algorithms were implemented and compared:

* Lasso Regression
* Support Vector Regression (SVR)
* Random Forest Regressor
* HistGradientBoosting Regressor

These models represent different machine learning approaches, including:

* linear models
* kernel-based methods
* ensemble learning
* gradient boosting

All models were implemented using scikit-learn.

---

## Hyperparameter Optimization

Hyperparameter tuning was performed using the model selection tools available in scikit-learn.

Two search strategies were applied:

- GridSearchCV
- RandomizedSearchCV

Both methods perform cross-validation internally while evaluating different combinations of hyperparameters.

Grid search systematically evaluates all parameter combinations within a predefined search space, while randomized search samples a fixed number of parameter configurations from a specified distribution.

These approaches allow efficient exploration of the hyperparameter space and help identify model configurations that yield the best predictive performance.

---

## Model Evaluation

Model performance was evaluated on a held-out test dataset using the following metrics:

* Root Mean Squared Error (RMSE)
* Coefficient of Determination (R²)

A comparison of model performance across the evaluated models was visualized using bar plots.

Additional diagnostic plots were generated to analyze prediction behavior:

* Residual plots
* Predicted vs Expected value plots

These plots help identify potential model bias, heteroscedasticity, and systematic prediction errors.

To further assess model generalization, training and test performance were compared to detect possible overfitting. In particular, the Random Forest model was examined for discrepancies between training and test error, as large performance gaps may indicate that the model is capturing noise in the training data rather than learning generalizable patterns.

---

## Model Interpretation

To understand which molecular descriptors drive model predictions, feature importance was calculated using **Permutation Feature Importance**, a model-agnostic interpretability technique.

Permutation importance measures how much model performance decreases when the values of a feature are randomly shuffled.

This method provides insight into which descriptors contribute most to solubility prediction.

---

## Results

Among the evaluated models, **HistGradientBoosting Regressor** achieved the best predictive performance.

Example test performance:

* RMSE ≈ 0.69
* R² ≈ 0.89

Residual analysis indicated that prediction errors were generally centered around zero with no strong systematic bias.

Feature importance analysis revealed that a small subset of molecular descriptors drives the majority of predictive performance.

---

## Project Structure

```text
Solubility_ML/
│
├── Solubility_prediction.ipynb
├── delaney-processed.csv
├── README.md
├── requirements.txt
└── figures/
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/panos1298/Solubility_ML.git
cd Solubility_ML
```

Install the required Python dependencies:

```bash
pip install -r requirements.txt
```

---

## Running the Project

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open the notebook:

```
Solubility_prediction.ipynb
```

Run the notebook cells sequentially to reproduce the analysis and results.

---

## Technologies Used

Python libraries used in this project include:

* RDKit
* scikit-learn
* NumPy
* pandas
* Matplotlib
* Jupyter Notebook

---

## Future Improvements

Potential extensions of this project include:

* advanced model interpretability using SHAP
* additional molecular descriptor sets
* external dataset validation
* model deployment as a prediction API

---

## Author

Panagiotis Koumpouris

Machine Learning / Chemoinformatics project exploring QSAR modeling techniques for molecular property prediction.