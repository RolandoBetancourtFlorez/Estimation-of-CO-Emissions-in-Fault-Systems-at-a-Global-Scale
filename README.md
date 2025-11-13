# Estimation of CO₂ Emissions in Fault Systems at a Global Scale

This repository contains the full workflow and harmonized geospatial datasets used to estimate diffuse CO₂ emissions in fault systems worldwide. The project integrates geological, tectonic, geophysical, and environmental predictors into a unified 0.10° global grid and applies a Machine Learning framework to generate a global CO₂ degassing map constrained to tectonically active regions.

## Table of Contents
1. Project Description  
2. Key Features  
3. Repository Structure  
4. Setup and Installation  
5. Usage Guide  
6. Methodology and Models  
7. Results Overview  
8. Data Availability  
9. Contributing  
10. Contact  
11. License  

## 1. Project Description
**Title:** Estimation of CO₂ Emissions in Fault Systems at a Global Scale  
**Authors:** Rolando Betancourt¹, Carlos Vargas¹  
¹ Department of Geosciences, Universidad Nacional de Colombia – Bogotá  

**Correspondence:**  
- rbetancourt@unal.edu.co  
- cavargasj@unal.edu.co  

### Abstract
This project quantifies diffuse CO₂ degassing in tectonically active regions using 867 degassing measurements and a suite of harmonized global datasets at 0.10° resolution. Five regression algorithms—SVR, KNN, Decision Tree, Random Forest, Gradient Boosting—and a Stacking Regressor with passthrough=True were trained and evaluated. The stacking model achieved R² = 0.677, outperforming individual models. Predictions were applied pixel-by-pixel within a tectonic applicability mask (fault distance ≤ 40 km or PGA ≥ 0.10 g) to prevent extrapolation into stable cratonic regions. The resulting global CO₂ map highlights active margins such as the Andes and Pacific Ring of Fire. This framework provides a reproducible approach for understanding natural CO₂ emissions along fault systems and their role in the carbon cycle.

## 2. Key Features

### 1. Global CO₂ Degassing Database
- 867 diffuse soil CO₂ flux records  
- Derived from more than 37 scientific publications  
- Covers volcanic and non-volcanic tectonic environments  

### 2. Unified 0.10° Raster Dataset
Harmonized predictors include:
- Bouguer anomaly  
- Heat flow  
- Distance to faults  
- Peak ground acceleration (PGA)  
- Distance to volcanoes  
- Distance to mineralizations and mineral products  
- Soil pH, soil organic carbon, soil temperature  
- Tree cover and available water storage  
- GLHYMPS porosity and permeability  

### 3. Machine Learning Pipeline
- SVR, KNN, Decision Tree, Random Forest, Gradient Boosting  
- Stacking Regressor (best-performing model)  
- GridSearch-based hyperparameter optimization  
- Log-target transform and inverse-distance feature engineering  

### 4. Pixel-by-Pixel Global Prediction
- Efficient 512×512 tiled raster inference  
- Predictions restricted to tectonically active mask  
- Produces global GeoTIFF in physical units (g m⁻² d⁻¹)

### 5. Fully Reproducible Workflow
- From data harmonization → sampling → ML → global prediction  
- Handles NoData, scaling, and block-processing robustly  
- Notebook can run fully offline  

## 3. Repository Structure
```
.
├── CO2_Flux_Analysis_and_Modeling.ipynb
├── 01_Data_Global/             
│   └── Processed/              
├── 03_Figures/                 
├── README.md
├── requirements.txt
└── LICENSE
```

## 4. Setup and Installation

### Clone the repository
```bash
git clone https://github.com/YourUsername/GlobalFaultCO2Flux.git
```

### Install dependencies
```bash
pip install -r requirements.txt
```

### Run the notebook
Open:
```
CO2_Flux_Analysis_and_Modeling.ipynb
```

## 5. Usage Guide

### Data Preparation
- Harmonizes all predictors to 0.10°  
- Converts vectors to distance rasters  
- Samples predictors at degassing sites  
- Log-transforms CO₂ flux  

### Model Training
- Train/validation/test split  
- Hyperparameter optimization  
- Stacking Regressor with passthrough=True  
- Evaluation with R², MSE, MAE  

### Prediction
- Pixel-wise prediction using trained model  
- Local imputation within windows  
- Inverse transform from log-flux to physical units  

### Mask Application
- Predictions restricted to:  
  - distance to faults ≤40 km  
  - OR PGA ≥0.10 g  
- Optional continental clipping  

## 6. Methodology and Models

### Final features used
- Bouguer anomaly  
- Heat flow  
- Annual mean temperature  
- Soil organic carbon  
- Soil pH  
- Distances to faults, volcanoes, mineralizations, mineral products  
- Available water storage  
- Tree cover  
- Porosity  
- Permeability  
- PGA  

### Models
1. Support Vector Regression  
2. K-Nearest Neighbors  
3. Decision Tree  
4. Random Forest  
5. Gradient Boosting  
6. Stacking Regressor (best performance)

**Best Test Performance:**  
R² = 0.677

## 7. Results Overview
- Highest predicted fluxes in:  
  - Andes  
  - Cascades  
  - Japan–Kuril arc  
  - Indonesia  
  - East African Rift  

- Key controls identified:  
  - Heat flow  
  - Annual temperature  
  - Distance to volcanoes  
  - Fault connectivity  
  - Porosity and permeability  

## 8. Data Availability
All harmonized datasets (~18 GB) are hosted in Zenodo.

Zenodo DOI: INSERT LINK HERE

Includes:  
- All 0.10° rasters  
- Distance datasets  
- Sampling table  
- Tectonic applicability mask  

## 9. Contributing
We welcome contributions related to:  
- New CO₂ degassing datasets  
- Additional geophysical predictors  
- Improvements to the ML pipeline  

## 10. Contact
Rolando Betancourt – rbetancourt@unal.edu.co  
Carlos Vargas – cavargasj@unal.edu.co  
Department of Geosciences, Universidad Nacional de Colombia

## 11. License
MIT License.
