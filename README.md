# End_to_End_Interactive_ML_Pipeline_for_DGE
End_to_End_Interactive_ML_Pipeline_for_DGE
🧬 End-to-End ML Pipeline for Differential Gene Expression (DGE) Classification

This repository contains a comprehensive Jupyter Notebook (End_to_End_Interactive_ML_Pipeline_for_DGE.ipynb) demonstrating a complete machine learning (ML) pipeline for classifying gene expression data as 'Upregulated' (1) or 'Downregulated' (0). The analysis includes initial model development, hyperparameter tuning, multi-model benchmarking, and feature importance analysis, providing robust insights into the data's underlying biological signal.

💡 Project Title & Key Findings

Project Title

Supervised Classification & Feature Dominance Analysis of Differential Gene Expression

Overall Synthesis

The analysis consistently demonstrates perfect or near-perfect classification accuracy across all tested models (Random Forest, Logistic Regression, SVM, XGBoost, and LASSO). This exceptional performance is primarily driven by the overwhelming influence of the logFC (Log Fold Change) feature, which acts as the single most critical determinant for classifying gene regulation status. This is visually confirmed by the perfect separation seen in the PCA plots and analytically proven by LASSO feature selection.

🛠️ Machine Learning Pipeline Steps

Step 1: Setup and Data Preparation

    Target Creation: A binary target variable (target) is created: 1 for genes where logFC > 0 ('Upregulated'), and 0 otherwise ('Downregulated').

    Features (X): ['logFC', 'AveExpr', 't', 'P.Value', 'adj.P.Val', 'B'] are used as predictors.

    Data Split: Data is split into training (80%) and testing (20%) sets.

    Scaling: Features are scaled using StandardScaler.

Step 2: Initial Model Development & Hyperparameter Tuning

    An initial Random Forest Classifier pipeline (StandardScaler + RandomForestClassifier) is built.

    GridSearchCV is used for hyperparameter tuning. The optimal configuration found was:

        rf__n_estimators: 50

        rf__max_depth: None (full tree depth allowed)

        rf__min_samples_leaf: 1

        rf__min_samples_split: 2

Step 3: Multi-Model Benchmarking (Validation)

Several models were tested to validate the strong signal and ensure the result was not specific to a single algorithm.
Model,Test Accuracy,CV Accuracy (5-Fold)
Random Forest (Tuned),1.0,1.0
Logistic Regression,1.0,1.0
LASSO Logistic Regression,1.0,1.0
SVM,1.0,0.99
XGBoost,0.967,0.997
Step 4: Feature Dominance Analysis

    Random Forest Feature Importance: logFC contributed approximately 76% of the total feature importance, dominating all other variables.

    LASSO Feature Coefficients: The LASSO (L1 regularization) model shrunk the coefficients for AveExpr, P.Value, adj.P.Val, and B to zero, analytically proving that logFC is the sole necessary feature for this classification.

Step 5: Visual Confirmation (PCA)

    All PCA Visualizations consistently showed an almost perfect visual separation between the 'Upregulated' and 'Downregulated' gene clusters in a 2D (PC1 vs. PC2) reduced space.

    This visual evidence reinforces the strong signal and reliability of the high accuracy metrics.

⚙️ Technical Requirements

Installation

Install the necessary Python libraries:
Bash

pip install pandas scikit-learn numpy xgboost plotly matplotlib

Note on Plotly Rendering

If interactive Plotly charts are not visible in your VS Code notebook, ensure the Jupyter Notebook Renderers (Microsoft) extension is installed, and for a permanent fix, set the default renderer in your global Plotly configuration file (~/.plotly/config.json) to "notebook_connected".
