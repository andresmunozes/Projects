
# Lung Cancer Prediction Using Gene Expression Data

This repository contains the end-to-end workflow for a data analysis project aimed at predicting lung cancer from gene expression data. The project is divided into two main phases: data extraction and predictive modeling.

## Project Goal
The primary objective of this project was to develop a machine learning pipeline to classify lung tissue samples as "Normal" or "Tumor" with the highest possible accuracy, while using a minimal set of a minimal set of genes. The analysis begins with a raw dataset of over 51,000 genes and seeks a computationally efficient solution suitable for potential diagnostic applications.

## Repository Structure
This project is organized into two main directories:

* **/01_Data_extraction/**: Contains the Jupyter Notebook (`data_extraction.ipynb`) responsible for the ETL (Extract, Transform, Load) process. This notebook handles the initial data cleaning, curation, and preparation, generating the final datasets used for modeling.
* **/02_Prediction_model/**: Contains the Jupyter Notebook (`prediction_model.ipynb`) where the machine learning models are developed. This includes feature selection using Mutual Information, training a Random Forest model, and evaluating its performance to identify the most efficient set of predictive genes.

## How to Run
To reproduce this analysis, follow the steps in order:

1.  **Run the Data Extraction Notebook:**
    * Navigate to the `01_Data_extraction` folder.
    * Execute the `data_extraction.ipynb` notebook. This will generate the necessary input files (`x_df_raw_cleaned.csv` and `y_df.csv`) for the next step.

2.  **Run the Prediction Model Notebook:**
    * Navigate to the `02_Prediction_model` folder.
    * Execute the `prediction_model.ipynb` notebook to perform feature selection, train the models, and see the final results.

## Key Findings
The main finding of this project is that an extremely efficient predictive model, using the expression of only **2 key genes**, can classify lung cancer with **100% accuracy** on the test dataset. This represents a 99.996% reduction in feature complexity without sacrificing predictive power, suggesting the viability of a focused and cost-effective diagnostic approach.

## Tools and Technologies
* **Language:** Python
* **Core Libraries:** Pandas, Scikit-learn, Matplotlib, Seaborn
* **Feature Selection:** Mutual Information
* **Classification Model:** Random Forest
* **Visualization:** t-SNE

## Data Source
The raw gene expression data used in this project was obtained from the NCBI Gene Expression Omnibus (GEO) database under the accession number **GSE81089**. The original data can be accessed via the following link:

* **Source:** [https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE81089]