# Temperature and Solar Irradiance Analysis

This repository contains a Jupyter notebook that analyzes the relationship between **temperature** and **solar irradiance** using time-series data.
The notebook focuses on data cleaning, visualization, and basic exploratory analysis to better understand environmental conditions relevant to solar energy systems.

---

## Project Overview

The purpose of this project is to explore how **solar irradiance** and **ambient temperature** vary over time and how they relate to each other.
Such analysis is fundamental in solar energy studies, as both variables directly influence photovoltaic (PV) system performance.

The notebook provides a clear and reproducible workflow for:
- Loading raw environmental data
- Cleaning and preprocessing the dataset
- Visualizing temperature and irradiance trends

---

## Data Description

The dataset used in this notebook contains time-dependent measurements of:
- **Solar irradiance**
- **Ambient temperature**

The data is assumed to originate from meteorological or solar monitoring sources and is processed locally within the notebook.

---

## Data Processing Steps

The notebook includes the following main steps:

1. **Data loading**  
   The dataset is loaded into a structured format suitable for analysis.

2. **Data cleaning**  
   - Handling missing or inconsistent values  
   - Ensuring correct data types  
   - Aligning timestamps if necessary  

3. **Exploratory data analysis (EDA)**  
   - Visualization of temperature over time  
   - Visualization of solar irradiance over time  
   - Basic comparison of trends between the two variables  

---

## Methods and Tools

- **Programming language:** Python
- **Environment:** Jupyter Notebook
- **Libraries used:**
  - `pandas` for data handling
  - `matplotlib` / `seaborn` for visualization
  - `numpy` for numerical operations

---

## Outputs

The notebook generates:
- Cleaned datasets ready for analysis
- Time-series plots for temperature
- Time-series plots for solar irradiance
- Visual insights into their temporal relationship

All results are displayed directly within the notebook.

---

## Intended Use

This notebook is intended for:
- Academic coursework
- Introductory data analysis in solar energy studies
- Understanding environmental variables affecting PV performance

---

## Limitations and Future Work

- The analysis is exploratory and does not include predictive modeling.
- Future work could include:
  - Correlation analysis between temperature and irradiance
  - Statistical modeling or regression
  - Integration with PV power output data

---

## Usage

1. Open `temperature_and_irradiance_fixed.ipynb`
2. Run the notebook cells sequentially
3. Inspect plots and outputs generated in the notebook

---

## Disclaimer

This project is developed for **academic purposes only**.
The results are intended for educational analysis and should not be used as a substitute for professional system design or forecasting.
