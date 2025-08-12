# NeurIPS_Open-Polymer-Prediction-2025 (Work in progress)
A Machine Learning Approach to Polymer Property Prediction: Interpretable Models

## 1. Introduction and Problem Formulation
Polymer informatics represents a critical intersection of materials science and machine learning, where quantitative structure-property relationships (QSPRs) are established to predict key material characteristics. In this technical exposition, I present a comprehensive methodology for predicting five fundamental polymer properties from SMILES representations:  
`Density (ρ)` - Mass per unit volume, critical for material selection  
`Thermal Conductivity (Tc)` - Heat transfer capability   
`Glass Transition Temperature (Tg)` - Amorphous phase transition point  
`Radius of Gyration (Rg)` - Molecular size characterization  
`Fractional Free Volume (FFV)` - Packing efficiency metric  

The approach systematically addresses following core challenges:  
Molecular representation - Transforming SMILES into informative features (2D descriptors + 3D descriptors + Morgan fingerprint)
Model interpretability - Understanding structure-property relationships

## 2. Data Preprocessing Pipeline
### 2.1 SMILES Validation and Standardization
All SMILES strings underwent RDKit's molecular validation to remove invalid SMILES
### 2.2 Molecular descriptors generation
For each valid SMILES, their 2D and 3D descriptors where extracted.
### 2.3 Fingerprint Generation
I generated Morgan fingerprints for all the SMILES using RDKit with radius=3 and n_bits=2048.
### 2.4 Chemical space visualization
Chemical space analysis was performed to get a general idea about how similar the polymers are.Both descriptors and fingerprints were used and TSNE was employed for clustering. 


## 3. Machine Learning Modeling
### 3.1 Model Architecture Selection
I evaluated traind an XGBoost (objective function = reg:squarederror and n_estimators=500) model with 5 fold CV for each properties.

### 3.2 Hyperparameter Optimization
Hyperparameter Optimization was performed using Optuna which uses Bayesian optimization for finding best set of parameters.

Search space:  
n_estimators (100-500),  
max_depth (3-10),  
Learning rate (1e-3 to 0.5)


## 4. Model Interpretation
### 4.1 SHAP Analysis & feature importance 
Key findings:

### 4.2 Partial Dependence Plots

## 5. Performance Evaluation
Cross-validated Results:

|Property|RMSE|R²|Key Features|
|:---:|:---:|:---:|:---:|
|||||


## 6. Conclusion and Future Work
This approach demonstrates that careful feature engineering combined with ensemble methods can achieve strong predictive performance for polymer properties.   
Future directions:  
Building a Graph Neural Network for training molecular graph (nodes->atoms, edge->bonds)
Nodes attributes containing atom based properties and edge attributes comtaining bond type, distance and bond based properties. Where each molecular graph will be accompanied with molecular features.
Architecture with a popper pooling/embedding method will give the model more granularity and context about the polymers, hence a good model with better learning.

