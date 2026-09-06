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
* Result: Rejected H0 (p = 0.049)
* Summary: Technically significant, but only just below the 0.05 threshold, and the actual difference between conditions is small, mean billing ranges from around $25,155 (Cancer) to $25,807 (Obesity), a gap of about 2.5%. With almost 55,000 rows in the dataset, even a small difference between group means can come out as statistically significant, so I wouldn't treat this as a meaningful real-world pattern.

H2: Test results are associated with insurance provider
* Validation: Compare the proportion of Normal/Abnormal/Inconclusive test results across insurance providers using a stacked bar chart and chi-square test
* Result: Failed to reject H0 (p = 0.339)
* Summary: The split between Normal, Abnormal, and Inconclusive results is almost identical across all five insurers, roughly 32-34% each. No evidence that a patient's insurer has any bearing on their test outcome in this dataset.

H3: Age differs significantly across admission types
* Validation: Compare Age across Admission Type groups using a box plot and one-way ANOVA
* Result: Failed to reject H0 (p = 0.630)
* Summary: Mean age is essentially identical across Elective, Emergency, and Urgent admissions, all around 51.5 years. Age doesn't predict how urgently someone is admitted in this dataset.

H4: Billing amount differs significantly between male and female patients
* Validation: Compare Billing Amount between genders using a box plot and independent t-test
* Result: Failed to reject H0 (p = 0.247)
* Summary: Male and female mean billing amounts are within 0.5% of each other ($25,616 vs $25,476). No evidence of gender-based billing disparity in this dataset.

H5: Medical condition is associated with admission type
* Validation: Compare the distribution of admission types across medical conditions using a heatmap and chi-square test
* Result: Failed to reject H0 (p = 0.057)
* Summary: Borderline, sitting just above the 0.05 threshold, but not significant. Counts are spread fairly evenly across the grid, so I wouldn't read anything into this one.

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

**Understand whether billing, outcomes or care pathways vary by demographic or administrative factors** — box plots of Billing Amount by Medical Condition and by Gender, box plot of Age by Admission Type.

**Determine whether commonly assumed risk factors actually influence billing or outcomes** — stacked bar chart of Test Results by Insurance Provider, heatmap of Medical Condition vs Admission Type.

**Build and compare classification models and check fairness** — a feature importance chart from the Random Forest model a model comparison chart (accuracy/F1) for Logistic Regression vs Random Forest and a bar chart of model accuracy by Insurance Provider.

**Present findings for both technical and non-technical audiences** — the notebook plots with statistical test results alongside them serve the technical side, while the Tableau dashboard's Fairness Signals and Ethics pages serve the non-technical side.

## Analysis Techniques Used

I used mean, median and standard deviation to compare groups across the key variables for each hypothesis. To test whether the differences I found were actually significant I ran a one-way ANOVA for numeric variables against 3+ groups (H1, H3) an independent t-test for numeric variables against 2 groups (H4) and chi-square tests for categorical vs categorical comparisons (H2, H5) all using pingouin.

I also looked at how the numeric features correlated with each other using a correlation matrix to get an overall picture before diving into each hypothesis individually.

For the machine learning side I started with single-feature baseline models before testing whether combining features improved performance then built and compared two classification models. Logistic Regression and Random Forest using a scikit-learn pipeline to handle the categorical columns through one-hot encoding. I then checked the stronger model's accuracy across gender and insurance provider subgroups to see whether it performed consistently across every patient group.

One thing worth pointing out almost none of the hypotheses I tested came back statistically significant including both of the fairness-focused ones. With almost 55,000 rows to work with even a very small real difference can register as statistically significant so I made a point of checking the actual size of each difference alongside the p-value rather than treating significance alone as meaningful.

## Ethical Considerations

Ethics was considered throughout ETL, EDA, modelling, and dashboard interpretation, covering both the data itself and the AI model built on top of it.

### Data Privacy and Governance
Even though the dataset used in this project is fully synthetic, generated using Python's Faker library it is structured to closely resemble real hospital admission records, patient names, ages, conditions, billing and insurance details. Treating a dataset like this carelessly just because it isn't real would defeat the purpose of the project, so I approached it as though it were genuine patient data throughout. In the ETL notebook the Name column a direct identifier, was dropped before any analysis, modelling or dashboard work began rather than at the end of the pipeline on the basis that a sensitive field shouldn't sit in working data any longer than necessary. This reflects the core GDPR principle of data minimisation only keeping what's actually needed for the stated purpose which in this case was hypothesis testing and modelling not identifying individuals.

### Bias and Fairness in the Data
Rather than treating fairness as a separate topic to discuss afterwards I built it directly into two of the five hypotheses tested in the EDA notebook. H2 tested whether a patient's insurance provider was associated with their test outcome and H4 tested whether billing amount differed by gender both are questions that if answered yes would point to a real disparity baked into the data before any model even touches it. Neither came back statistically significant. This matters because any model built on top of biased data will typically reproduce or even amplify that bias so ruling out an obvious source of it at the data stage gave me more confidence that the modelling stage that followed wasn't starting from an already-skewed foundation. I'm careful not to overstate this though a clean result on a synthetic dataset shows the pipeline and the tests work correctly. it doesn't prove real-world healthcare data or insurers are free of these issues.

### Algorithmic Fairness
Data-level fairness and model-level fairness are not the same thing a model can still end up performing unevenly across groups even when its training data shows no obvious bias simply because of how it learns patterns during training. To check for this I took the Random Forest model built in the Modelling notebook the stronger of the two models tested and measured its accuracy separately for each Gender and each Insurance Provider rather than relying on a single overall accuracy figure. The result showed accuracy staying within a tight band at most 2.7 percentage points apart across insurance providers and 0.6 points across gender. Had one subgroup come out substantially lower, for example 15 or 20 points behind the rest that would have meant the model's predictions couldn't be trusted equally for every patient and it would need investigating and likely correcting before being used for anything beyond this project. A gap this small is far more consistent with ordinary sampling variation than a genuine fairness problem in the model.

### Responsible Model Use
Even with a clean fairness result I don't think this model should be presented as anything more than a demonstration of the process. At 41.7% accuracy on a three-class prediction problem only modestly ahead of a 33.5% baseline it simply isn't strong enough to inform any real clinical or administrative decision. Framing a weak model as production-ready, even one that passed its fairness check, would itself be a kind of ethical failure overselling a tool's reliability is its own form of misleading practice separate from bias.

### Legal and Societal Considerations
Part of why I chose this particular dataset was to sidestep a real governance issue, Kaggle has previously hosted healthcare datasets uploaded without clear patient consent or provenance. Using a dataset that is explicitly synthetic and CC0-licensed let me demonstrate the full governance workflow, de-identification, fairness testing at both the data and model level and honest reporting of a weak model without inheriting any of the consent or provenance risk that comes with using scraped or unclear real-world health data.

## Key Findings & Insights

Almost nothing tested in this project showed a statistically meaningful relationship. The one borderline result (H1, billing by medical condition) only just crossed the significance threshold and with almost 55,000 rows even a very small real difference can register as statistically significant the actual gap between the highest and lowest condition was only about $650, roughly 2.5% of the overall average which isn't something I'd act on.

Both fairness-focused hypotheses (H2 and H4) came back with no significant relationship at all which was genuinely one of the more useful findings of the project even though it's a "nothing found" result rather than a positive one. It means the data itself isn't carrying an obvious bias into whatever gets built on top of it.

The modelling results told a similar story. Random Forest reached 41.7% accuracy on a 3-class prediction problem. Only around 8 points above the 33.5% majority-class baseline and Logistic Regression barely beat the baseline at all (33.6%). Neither model found strong predictive signal which lines up with the hypothesis testing there just isn't much real structure in this dataset for a model to learn from.

## Prevention Measures / Recommendations

Based on the analysis this is what I'd recommend:

* Don't treat the borderline H1 result as a real-world finding a ~2.5% difference in billing across medical conditions isn't practically meaningful even though it's technically significant.
* Any pipeline like this reused on real hospital data should re-run all five hypotheses and the fairness check before drawing any conclusions a synthetic dataset can validate that the pipeline works but it can't validate real-world fairness.
* Keep the fairness check as a standard step for any future modelling work on patient data not just this project it's a small amount of extra work for a genuinely important governance signal.
* Continue de-identifying any direct patient identifiers before analysis even on synthetic data so the workflow is safe to reuse on real data without changes.
* Don't present a model this weak (41.7% accuracy on a 3-class problem) as ready for real decision-making even a fair model isn't a useful one if it isn't accurate enough to trust.

## Model

I built and compared two classification models to predict Test Results (Normal/Abnormal/Inconclusive): Logistic Regression and Random Forest, both using a scikit-learn pipeline with one-hot encoding to handle the categorical columns.

Before building the full models, I started with single-feature baselines using Billing Amount and Age individually both landed almost exactly on the 33.5% majority-class baseline and combining them together made no difference at all. This told me early on that these two features alone weren't carrying much signal which set my expectations going into the wider comparison.

Random Forest was the clear winner of the two full models reaching 41.7% accuracy, compared to Logistic Regression's 33.6%, which barely beat the baseline. I'm recommending Random Forest, but with a real caveat, 41.7% on a 3-class problem is still a weak result overall and I wouldn't present this model as genuinely predicting patient outcomes without making that limitation very clear. It's best read as a demonstration that the pipeline works not as something ready for real decision-making.

Feature importance from the Random Forest model showed Billing Amount, Age and Length of Stay as the strongest predictors by a wide margin with none of the one-hot encoded categorical features individually mattering much this fits with the EDA notebook finding no significant relationship for Insurance Provider (H2) or Medical Condition (H5).

I also checked the Random Forest model's accuracy separately across Gender and Insurance Provider subgroups. Accuracy stayed within a tight band, 41.4%-42.0% by gender and 40.0%-42.7% by insurance provider showing no evidence the model performs systematically worse for any particular group.

## Dashboard Design

I'm building the dashboard in Tableau Public.

1. **Overview** — key stats (patient count, average billing, average length of stay) and a summary of the dataset.
2. **Billing & Conditions** — the chart for H1, my most significant (if practically weak) finding.
3. **Fairness Signals** — the charts for H2 and H4, framed for a non-technical reader, does your insurer or gender affect your results or your bill?
4. **Admissions** — the charts for H3 and H5.
5. **Model Insights** — feature importance and model comparison charts, plus the fairness-by-subgroup chart.
6. **Data Ethics & Governance** — a plain-English page summarising the Ethical Considerations section above, written for a general hospital-administrator audience rather than a technical one.

## Limitations

The dataset is synthetic (Faker-generated) so the near-total absence of significant relationships is a property of this particular dataset, not something I can generalise beyond it.

106 rows had a negative Billing Amount which I treated as sign errors and corrected to positive values using .abs(). That's a documented assumption rather than a certainty a different explanation, for example genuine refunds, would change how those rows should have been handled.

Model performance is modest (41.7% accuracy on a 3-class problem) and shouldn't be relied on for any real decision-making it demonstrates the modelling and fairness-checking process, not a production-ready classifier.

The fairness check only covers Gender and Insurance Provider since these were the two subgroups tested as hypotheses earlier in the project. Other potentially relevant subgroups such as age band or medical condition weren't checked for model fairness in this version.

## Development Roadmap

* I'd like to test the same hypotheses and fairness check against a real properly governed healthcare dataset to build my confidence in knowing whether findings from a synthetic dataset actually generalise or whether they're an artefact of the data being simulated.
* I want to get more practice extending fairness checks to additional subgroups such as age band or medical condition rather than just the two I tested here so this becomes second nature rather than something I have to think through from scratch each time.
* I'd like to improve my understanding of why a model underperforms rather than just accepting a weak result trying additional feature engineering or alternative algorithms on this dataset would help me build that diagnostic skill.
* I want to develop my ability to communicate technical findings to a non-technical audience building the Ethics & Governance dashboard page in a way a hospital administrator could genuinely follow would be good practice for that.
* Going forward, I want de-identification and fairness-checking to become a habit I apply automatically on any project involving personal or sensitive-looking data not something I only remember to do because a project is explicitly framed around ethics.

## Bugs and Fixes

I didn't encounter many bugs within this project since the fraud detection project (porject 2) was still fresh in my head I remembered a lot of the mistakes not to repeat this time around. The main issue I ran into was Jupyter kernel problems while running the Modelling notebook which I had to restart and re-run from the top to resolve. 

## AI Assistance

* I used Claude AI mainly for the machine learning and fairness-check sections, to help me understand how to check model performance across subgroups and interpret what the results meant.
* It helped me structure the ethics section of this README around the actual hypothesis and fairness-check results rather than writing generic statements.
* I used it a little to plan the project and notebook structure, reusing the same approach as my fraud detection project.
* I mainly used it as a guide to check I was going in the right direction rather than relying on it to do the work for me.

## Main Data Analysis Libraries

* Pandas — used throughout ETL, EDA and Modelling
* Numpy — numerical operations
* Matplotlib — charts in the EDA and Data Visualisation notebooks
* Seaborn — charts in the EDA and Data Visualisation notebooks
* Pingouin — normality checks, t-tests, chi-square tests and ANOVA
* Scikit-learn — Logistic Regression, Random Forest, pipelines and evaluation metrics

## Credits & Acknowledgements

* Dataset: [prasad22/healthcare-dataset](https://www.kaggle.com/datasets/prasad22/healthcare-dataset) (Kaggle, CC0-1.0)