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