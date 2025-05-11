# Google-Data-Analytics-Bellabeat-Case-Study

**Author**: Julie Coleman
**Date**: May, 2025

_The case study follows the six step data analysis process:_

### ❓ [Ask](#1-ask)
### 💻 [Prepare](#2-prepare)
### 🛠 [Process](#3-process)
### 📊 [Analyze](#4-analyze)
### 📋 [Share](#5-share)
### 🧗‍♀️ [Act](#6-act)

## Scenario
Bellabeat is a small high-tech company that manufactures health-focused smart products. Since it was founded in 2013 by Urška Sršen and Sando Mur, Bellabeat has opened offices around the world and now has the potential to become a larger player in the global smart device market. The company has 5 focus products at the time of this analysis: bellabeat app, leaf, time, spring, and bellabeat membership. 

## 1. Ask
💡 BUSINESS TASK: Our team has been asked to analyze smart device data to gain insight into consumer behavior trends. The insights we discover will then help guide marketing strategy for the company. 

Specifically, our team needs to answer:
1. What are some trends in smart device usage?
2. How could these trends apply to Bellabeat customers?
3. How could these trends help influence Bellabeat's marketing strategy?

Primary stakeholders: Urška Sršen and Sando Mur, executive team members.

Secondary stakeholders: Bellabeat marketing analytics team.

## 2. Prepare 
This data was sourced from FitBit Fitness Tracker Data and made available by the user Möbius on Kaggle at https://www.kaggle.com/arashnic/fitbit. This is a public dataset. Kaggle is a platform for data science and machine learning projects.

## ROCCC Analysis of Dataset

| **Criterion**      | **Assessment**                                                                                                                                       |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Reliable**       | ⚠️ TBD                             |
| **Original**       | ❌ Not original. This is **third-party data** collected independently from Fitbit users via Amazon Mechanical Turk, not from Bellabeat’s own user base and not affiliated with Bellabeat.             |
| **Comprehensive**  | ✅ Yes? TBD      |
| **Current**        | ❌ No. The data was collected in 2016. While it can still reveal usage patterns, it may not reflect current trends in smart device engagement.         |
| **Cited**          | ✅ Yes citation: Furberg, R., Brinton, J., Keating, M., & Ortiz, A. (2016). Crowd-sourced Fitbit datasets 03.12.2016-05.12.2016 [Data set]. Zenodo. https://doi.org/10.5281/zenodo.53894       |

## Is this Good Data?

Reasons why for categorizing it as good data:
- This meets the criteria for size validation. According to the **Central Limit Theoreum (CLT)** in the field of probability and statistics, a sample of 30 is the smallest sample size for which the CLT is still valid.
- This data is credible as the dataset was created by researchers affiliated with RTI International, a reputable nonprofit research institute. The dataset had a transparent methodology including participant consent. Although the DOI was not referenced on kaggle, the dataset has a DOI through zenodo, ensuring it can be reliably cited and accessed. Zenodo is operated by CERN and OpenAIRE, providing a trusted platform for research data.
- Although technically self-reported, the data itself is device-generated, making it inherently more objective than traditional self-report surveys.
- No PII was retained in the final dataset, so the dataset does not expose privacy or security concerns.
- This data is licensed for public domain: https://creativecommons.org/publicdomain/zero/1.0/
- The data is accessible in that it is distributed under the Creative Commons Attribution 4.0 (CC BY 4.0) license, hosted on an open-access platform, and requires no proprietary software to open. Zenodo provides a clear title and abstract along with basic metadata.

Reasons for categorizing it as bad data:
- Although the dataset meets the minimum for size validation, it is only the minimum. To increase the reliability of the sample size accurately reflecting the general population, we should increase the sample size.
- Although no PII was retained in the final dataset, it is hard to know if this dataset matches the general population without age, gender, location or other demographic factors. It is also hard to know if this dataset matches the general population as far as disabilities.
- Because submission was manual and not done in a controlled setting, there is potential for data corruption, omission, variability in device models, and user misunderstandings leading to misreporting during export.


More questions to answer:
- How is the data organized? Is it in long or wide format?
- How are you addressing licensing, privacy, security, and accessibility?
  - Accessibility:
- How does it help you answer your question?
- Are there any problems with the data?

To begin the analysis, we load all the required R packages in https://github.com/julielaursen/r-fitbit-data. These package are used for data cleaning, manipulation, visualization, and time/date processing. 

Packages used in this project:
- `tidyverse`: a colletion of R packages for data science, including:
  - `dplyr`: For data wrangling and transformation
  - `ggplot2`: For visualizing trends and patterns
  - `readr`: For reading data files
  - `tidyr`: For reshaping and cleaning data
  - `tibble, stringr, forcats, purrr`: Support functions for tidy data workflows
