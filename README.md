# HeartFailureDataAnalysis
Data analysis on the connection of variables to Heart failure with a dataset provided from kaggle

## Executive Summary

This project analyzes a clinical dataset to identify high-risk physiological profiles for heart failure, a condition affecting 920,000 people in the UK. By leveraging dimensionality reduction and categorical feature engineering, the analysis isolates a robust diagnostic signal from complex medical data [1, 2].

 - **Key Predictors**: Exercise Angina, Oldpeak, and Age are the strongest indicators of heart failure presence.
 - **Dimensionality Signal**: 3D PCA reveals clear class separability, with three components explaining 70.3% of total variance.
 - **The Age Threshold**: A significant risk inflection point occurs at age 50, with the highest risk-to-healthy ratio found in the 61-70 cohort.
 - **Hypertension Tipping Point**: Stage 2 Hypertension (140+ mmHg) acts as a non-linear tipping point where heart disease prevalence significantly outpaces healthy instances.
 - **The Cholesterol Paradox**: Lower cholesterol (<200 mg/dL) shows a higher proportion of disease in this dataset, likely due to medication bias (statins) or data artifacts.

## Clinical Significance & Background

Heart failure prevalence is rising in the UK due to an aging population and is predicted to double by 2040. According to NICE, the condition affects 1 in 5 people across Europe. While datasets are plentiful, identifying the specific "tipping points" where physiological markers transition from "at risk" to "diseased" is critical for preventative diagnostic frameworks. [2]

## Deep Dive Observations
### 1. Age and the Inflection of Risk
Age-stratified analysis shows that while the 51-60 cohort has the highest volume of cases, the 61-70 cohort exhibits the most severe risk ratio.
[Insert image_3e1f16.png here]
The drop-off in data volume after age 70 indicates a survivorship bias, where high-risk individuals may suffer acute events before elective diagnostic recording.

### 2. Blood Pressure: The Stage 2 Tipping Point
Risk does not scale linearly with blood pressure; it plateaus through "Elevated" and "Stage 1" before spiking.
[Insert image_3ea65a.png here]
Stage 2 Hypertension is a critical clinical boundary. The sparse data in the "Severe" category suggests these patients are often treated in emergency settings rather than recorded in standard diagnostic datasets.

### 3. Dimensionality Reduction (PCA)
To untangle overlapping variables, PCA was used to compress the feature space while maintaining the "signal."
[Insert image_3f7814.jpg here]
The 3D projection captures 70.3% of the variance. The clear spatial clustering between groups proves that heart disease is highly predictable when combining these physiological markers, even when ignoring minor data "noise."

## Methodology
**Preprocessing**: StandardScaling for variance-sensitive algorithms and categorical binning for age and blood pressure.
**Analysis**: Correlation heatmaps to identify primary drivers and pivot tables for risk-ratio validation.
**PCA**: Multi-component Principal Component Analysis to validate class separability in reduced dimensions.

## Detailed observations
wip

## Future work and real-world applicability
wip

References

[1] [NICE: Heart Failure Prevalence](https://cks.nice.org.uk/topics/heart-failure-chronic/background-information/prevalence/)

[2] [NHS: Managing Heart Failure at Home](https://www.england.nhs.uk/nhs-at-home/managing-heart-failure-at-home/)
