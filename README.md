# HeartFailureDataAnalysis
Data analysis on the connection of variables to Heart failure with a dataset provided from kaggle

## Executive Summary

This project analyzes a clinical dataset publicly available on [Kaggle](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction) to identify high-risk physiological profiles for heart failure, a condition affecting 920,000 people in the UK. By leveraging dimensionality reduction and categorical feature engineering, the analysis isolates a robust diagnostic signal from complex medical data [1, 2].

 - **Key Predictors**: Exercise Angina, Oldpeak, and Age are the strongest indicators of heart failure presence.
 - **Dimensionality Signal**: 3D PCA reveals clear class separability, with three components explaining 70.3% of total variance.
 - **The Age Threshold**: A significant risk inflection point occurs at age 50, with the highest risk-to-healthy ratio found in the 61-70 cohort.
 - **Hypertension Tipping Point**: Stage 2 Hypertension (140+ mmHg) acts as a non-linear tipping point where heart disease prevalence significantly outpaces healthy instances.
 - **The Cholesterol Paradox**: Lower cholesterol (<200 mg/dL) shows a higher proportion of disease in this dataset, likely due to medication bias (statins) or data artifacts.

## Clinical Significance & Background

Heart failure prevalence is rising in the UK due to an aging population and is predicted to double by 2040. According to NICE, the condition affects 1 in 5 people across Europe. While datasets are plentiful, identifying the specific "tipping points" where physiological markers transition from "at risk" to "diseased" is critical for preventative diagnostic frameworks. [2]

## Observations 

### Categorical feature distributions
![categorical feature distributions](https://github.com/HA-141/HeartFailureDataAnalysis/blob/main/Output_Figs/Categorical_feature_dist.png)
Observations: 
* Males more likely to have heart disease
* ASY chest pain type more likely to have heart disease
* High fasting blood sugar more likely to have heart disease
* Higher proportion of ST resting ECG has heart disease
* More proportion of individuals with exercise angina has heart failure
* Flat st_slope has higher chance of heart failure, for up, more likely to be healthy and not much different for down st_slope.


### Deep Dive Categorical distribution observations for continuous features
### Age and the Inflection of Risk
Age-stratified analysis shows that while the 51-60 cohort has the highest volume of cases, the 61-70 cohort exhibits the most severe risk ratio.
![Image of stratified distributions](https://github.com/HA-141/HeartFailureDataAnalysis/blob/main/Output_Figs/Feature_eng_Age_level.png)
The drop-off in data volume after age 70 indicates a survivorship bias, where high-risk individuals may suffer acute events before elective diagnostic recording.

### Blood Pressure: The Stage 2 Tipping Point
Risk does not scale linearly with blood pressure; it plateaus through "Elevated" and "Stage 1" before spiking.
![Image of hypertension distribution](https://github.com/HA-141/HeartFailureDataAnalysis/blob/main/Output_Figs/Feature_eng_BP_level.png)
Stage 2 Hypertension is a critical clinical boundary. The sparse data in the "Severe" category suggests these patients are often treated in emergency settings rather than recorded in standard diagnostic datasets.

### Dimensionality Reduction (PCA)
To untangle overlapping variables, PCA was used to compress the feature space while maintaining the "signal."
![3D PCA](https://github.com/HA-141/HeartFailureDataAnalysis/blob/main/Output_Figs/3D_PCA.png)
The 3D projection captures 70.3% of the variance. The clear spatial clustering between groups proves that heart disease is highly predictable when combining these physiological markers, even when ignoring minor data "noise."

### Positive and negative correlation between certain features and heart disease
![correlation heatmap](https://github.com/HA-141/HeartFailureDataAnalysis/blob/main/Output_Figs/Correlation_heatmap.png)
Select features (in descending order) have a stroing correlation to heart fialure: Exercise Angina, OldPeak, Sex, Age, FastingBS.
Select features (in ascending order have a strong negative correlation to heart failure: ST_Slope, MaxHR, ChestPainType, Cholesterol.
Remaining features show little to no correlation to heart disease.
Correlation heatmap shows that a select few features are stronger indicators for heart failure and should have a higher priority in indentifying during diagnosis, while other features less so.

## Methodology
**Preprocessing**: StandardScaling for variance-sensitive algorithms and categorical binning for age and blood pressure.
**Analysis**: Correlation heatmaps to identify primary drivers and pivot tables for risk-ratio validation.
**PCA**: Multi-component Principal Component Analysis to validate class separability in reduced dimensions.


## Future work and real-world applicability

### Clinical Utility
This analysis can be used as a pre-screening framework for primary care. By identifying "Red Flag" profiles such as stage 2 Blood Pressure and age over 50, practitioners can prioritize high-risk individuals for advanced cardiac imaging or stress tests before symptoms become acute.

### Planned Enhancements
**Advanced Modeling**: Implementing non-linear machine learning models, such as Random Forests or XGBoost, to better capture the "threshold effects" identified in the Blood Pressure and Age categories.
**Time-Series Analysis**: If longitudinal data becomes available, tracking how quickly a patient moves from "Stage 1" to "Stage 2" BP could serve as a predictive early-warning system.
**Diagnosis prediction model**: Use classification models such as Random Forest Classifier, SVMs or KNNs to predict (or classify) a patient on whether they are likely to have heart disease, giving features that have a higher correlation to heart disease a stronger importancr factor in the model

References:

[1] [NICE: Heart Failure Prevalence](https://cks.nice.org.uk/topics/heart-failure-chronic/background-information/prevalence/)

[2] [NHS: Managing Heart Failure at Home](https://www.england.nhs.uk/nhs-at-home/managing-heart-failure-at-home/)

![Dataset is available at Kaggle][https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction]
