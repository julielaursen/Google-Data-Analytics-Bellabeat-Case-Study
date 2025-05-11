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
| **Cited**          | TBD         |

TBD:

I will answer the following questions
- How is the data organized? Is it in long or wide format?
- Are there issues with bias or credibility in this data?
  - Yes, according to the **Central Limit Theoreum (CLT)** in the field of probability and statistics, a sample of 30 is the smallest sample size for which the CLT is still valid. To increase the reliability of the sample size accurately reflecting the general population, we should increase the sample size.
- How are you addressing licensing, privacy, security, and accessibility?
  - Licensing: this data is public domain. https://creativecommons.org/publicdomain/zero/1.0/
  - Privacy:
  - Security:
  - Accessibility:
- How did you verify the data’s integrity?
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
