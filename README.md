# GPU-Based Machine Learning for Higgs Boson Process Classification

## Introduction
The discovery of the Higgs boson particle at CERN in 2012 marked a monumental accomplishment in modern physics, providing tangible proof of the existence of the Higgs field. Detecting particles like the Higgs boson requires advanced hardware and software, as well as international scientific collaboration. Machine learning techniques have become essential tools in high-energy physics, aiding in achieving experimental goals and facilitating the prediction of the Standard Model.

This repository contains the implementation of a GPU-based machine learning technique for discriminating between a signal process that produces Higgs bosons and a background process that does not. It leverages the RAPIDS framework for parallel processing to improve data processing and model training, evaluation, and testing performance.

## Background

### Machine Learning in High-Energy Physics
Machine learning techniques have been applied in particle physics for some time, traditionally relying on processed inputs generated by reconstruction algorithms. However, newer ML algorithms enable the direct analysis of raw data from particle detectors. ML is now used for various tasks, including event selection, event classification, and background suppression for signal events of interest.

### Computational Demands
One significant challenge in implementing machine learning in theoretical physics is the high computational demand. Particle accelerators produce vast amounts of data, such as the Large Hadron Collider (LHC), which has the largest data rate in the world, exceeding 50 terabytes per second. The high luminosity phase of the LHC (HL-LHC) is expected to generate 15 times more data than the current LHC. To meet this demand, researchers are exploring the use of GPUs for ML applications in particle physics, enabling parallel processing of large datasets.

### Task Specification
In high-energy physics, the Higgs boson is observed through the collision of high-energy protons in the Large Hadron Collider at CERN. **Signal events** represent the decay of the Higgs boson, while **background events** involve particles detected in previous experiments. Machine learning can help differentiate between these processes using large datasets of simulated particle collisions.

## Implementation Steps

### Data
- The [UCI Higgs dataset](https://archive.ics.uci.edu/ml/datasets/HIGGS) is used for training and testing.
- It consists of 11 million instances generated via Monte Carlo simulations.
- Each instance has 29 features, with the first feature as the binary label (1 for signal, 0 for background).

### Exploratory Data Analysis (EDA)
- Explored aspects of the dataset, including missing values, class distribution, feature correlation, and outliers.
- Addressed class imbalance and correlated features.

### Data Preprocessing
- Removed correlated features.
- Addressed outliers while preserving valuable data.
- Synthetic Minority Over-sampling Technique (SMOTE) is applied to address class imbalance.
- Normalized the dataset using cuML normalizer to ensure accuracy and reliability.

### Models
Three models were trained and evaluated for baseline comparison:
- Logistic Regression
- Random Forest Classifier
- XGBoost

### Experiments
- Grid search was applied to the three classifiers with different parameters to ensure optimum results. 
- Logistic Regression is compared between GPU and CPU-based training, with similar accuracy but significantly faster GPU training.
- Random Forest's hyperparameters (n_estimators and max_depth) are fine-tuned. This optimization process involved a careful examination of the delicate balance between achieving higher accuracy and managing computational resource demands.
- XGBoost is trained with and without normalization, demonstrating the necessity of preprocessing.
- Principal Component Analysis (PCA) is explored.

### Dimensionality Reduction (PCA)
- Applied PCA to the dataset to explore dimensionality reduction.
- Retrained models on the reduced data.
- Assessed the impact of PCA on model performance.

### Testing and Model Selection
- Logistic Regression is excluded due to lower performance.
- Random Forest and XGBoost models are tested on the test set, achieving similar accuracy (73% and 74%).
- XGBoost performs slightly better, especially in precision for the signal process class.
- XGBoost model is selected and saved in the "./saved_model" directory.

## Repository Structure
- `datasets/`: contains the fauture vectors resulted from the data preprocessing step.
- `saved_model/`: contains the exported saved model.
- `Analysis and Preprocessing.ipynb`: Contains exploratory data analysis and the preprocessing pipeline applied to the dataset.
- `Training and Testing.ipynb`: Details the training, evaluation, and testing of the models using the preprocessed datasets.

## Conclusion
This project demonstrates the potential of GPU-based machine learning techniques in high-energy physics, specifically for Higgs boson process classification. The results highlight the power of the RAPIDS framework in handling large datasets efficiently. The XGBoost model is recommended for this task, achieving an accuracy rate of 74%.
