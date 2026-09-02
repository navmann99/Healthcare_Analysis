# Healthcare Analytics Project

**Healthcare Analytics Project** is a data analysis tool designed to explore patient admission, billing, and outcome data, with a particular focus on data ethics, privacy, and fairness. The project explores a synthetic healthcare dataset through statistical hypothesis testing and machine learning, and presents the findings through an interactive Tableau dashboard.
# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

## Dataset Content

* The dataset I used was the Healthcare Dataset from Kaggle. Here is the link for the Dataset: https://www.kaggle.com/datasets/prasad22/healthcare-dataset

## Business Requirements

* Understand whether patient billing, outcomes or care pathways vary systematically by demographic or administrative factors such as age, gender, and insurance provider.
* Determine whether commonly assumed risk factors actually influence billing or test outcomes or whether the data shows no real relationship at all.
* Build and compare classification models to predict patient test outcomes and check whether that model performs fairly across different patient subgroups.
* Present findings in a way that's accessible to both technical and non-technical audiences with particular attention to data ethics and governance.

## Hypothesis and how to validate?

H1: Billing amount differs significantly across medical conditions
* Validation: Compare Billing Amount across Medical Condition groups using a box plot and one-way ANOVA
* Result: 
* Summary: 

H2: Test results are associated with insurance provider
* Validation: Compare the proportion of Normal/Abnormal/Inconclusive test results across insurance providers using a stacked bar chart and chi-square test
* Result:
* Summary:

H3: Age differs significantly across admission types
* Validation: Compare Age across Admission Type groups using a box plot and one-way ANOVA
* Result:
* Summary:

H4: Billing amount differs significantly between male and female patients
* Validation: Compare Billing Amount between genders using a box plot and independent t-test
* Result: 
* Summary:

H5: Medical condition is associated with admission type
* Validation: Compare the distribution of admission types across medical conditions using a heatmap and chi-square test
* Result: 
* Summary: 

## Project Plan

* Business Understanding: Defined the project's ethics-focused objectives and identified the key questions relevant to the business requirements.
* Data Understanding: Explored the raw dataset, assessed data quality and identified which fields were sensitive and needed careful handling.
* ETL: Cleaned the raw data, checked for missing values, duplicates, incorrect data types and outliers, corrected any negative billing values, de-identified the dataset by dropping the Name column and engineered a Length of Stay feature.
* EDA: Analysed distributions and relationships between features and outcomes and tested five hypotheses using statistical methods (t-test, chi-square tests and ANOVA), two were specifically framed around fairness.
* Data Visualisation: Created plots mapped to each hypothesis and business requirement plus a correlation matrix and built an interactive Tableau dashboard for further exploration.
* Modelling: Built and compared two classification models (Logistic Regression and Random Forest) to predict Test Results then ran a fairness check on the stronger model's performance across gender and insurance provider subgroups.
* Insights & Recommendations: Summarised the findings from the hypothesis testing and the model and translated them into a governance-focused set of takeaways.

* [Kanban board](your-kanban-board-link-here)

**Project files are organised as followed:**
* (Raw) Primary File: Dataset/Raw/healthcare_dataset.csv
* (Cleaned, De-identified) Transformed File: Dataset/CleanData/healthcare_cleaned_deidentified.csv
* Feature Importance File: Dataset/CleanData/feature_importance.csv
* Model Comparison File: Dataset/CleanData/model_comparison.csv
* Fairness Check File: Dataset/CleanData/fairness_check.csv
* Notebooks: jupyter_notebooks/01_ETL.ipynb, 02_EDA.ipynb, 03_Data_Visualisation.ipynb, 04_Modelling.ipynb

* [Tableau Dashboard](your-tableau-link-here)

## The rationale to map the business requirements to the Data Visualisations

**Understand whether billing, outcomes, or care pathways vary by demographic or administrative factors** — box plots of Billing Amount by Medical Condition and by Gender, box plot of Age by Admission Type.

**Determine whether commonly assumed risk factors actually influence billing or outcomes** — stacked bar chart of Test Results by Insurance Provider, heatmap of Medical Condition vs Admission Type.

**Build and compare classification models, and check fairness** — a feature importance chart from the Random Forest model, a model comparison chart (accuracy/F1) for Logistic Regression vs Random Forest and a bar chart of model accuracy by Insurance Provider.

**Present findings for both technical and non-technical audiences** — the notebook plots with statistical test results alongside them serve the technical side, while the Tableau dashboard's Fairness Signals and Ethics pages serve the non-technical side.
