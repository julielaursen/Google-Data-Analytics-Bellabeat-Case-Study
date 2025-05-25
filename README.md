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

| **Criterion**      | **Result** | **Assessment**                                                                                                                                       |
|--------------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Reliable**       | ⚠️ Medium  | This is reliable enough for exploratory analysis but not for clinical research or long-term behavior modeling.                                      |
| **Original**       | ❌ No       | This is **third-party data** collected independently from Fitbit users via Amazon Mechanical Turk, not from Bellabeat’s own user base.             |
| **Comprehensive**  | ❌ No       | The dataset only spans a short period of time and does not include demographic factors.                                                            |
| **Current**        | ❌ No       | The data was collected in 2016. While it can still reveal usage patterns, it may not reflect current trends in smart device engagement.            |
| **Cited**          | ✅ Yes      | Citation: Furberg, R., Brinton, J., Keating, M., & Ortiz, A. (2016). Crowd-sourced Fitbit datasets 03.12.2016-05.12.2016 [Data set]. Zenodo. https://doi.org/10.5281/zenodo.53894 |


## ✅ Why We Consider This Good Data

| Reason                            | Details                                                                                                                                                                                                                          |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 📏 **Statistically Valid Sample** | The dataset includes 30 participants — the **minimum sample size** for the [Central Limit Theorem (CLT)](https://en.wikipedia.org/wiki/Central_limit_theorem) to apply, ensuring foundational validity in statistical inference. |
| 🧠 **Credible Source**            | Collected by researchers at **RTI International**, a respected nonprofit research institute. It has a valid [DOI](https://doi.org/10.5281/zenodo.53894), and is hosted on **Zenodo**, backed by CERN & OpenAIRE.                 |
| ⏱ **Objective Measurements**      | While user-submitted, the data was **device-generated**, reducing the potential for typical biases found in self-report surveys.                                                                                              |
| 🔒 **Privacy-Respecting**         | No personally identifiable information (PII) is included — ensuring ethical data sharing.                                                                                                                                        |
| 🌍 **Open and Accessible**        | Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) and hosted on a public, open-access platform. No proprietary software is required.                                                           |

## ⚠️ Where the Data Falls Short

| Concern                            | Details                                                                                                                                            |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| 📉 **Sample Size is Bare Minimum** | While statistically valid, a sample size of 30 is still **limited**. Larger samples would provide more robust insights.                            |
| 🙈 **Limited Demographics**        | Lack of demographic detail (e.g. age, gender, disability status) makes it hard to **generalize** to broader populations.                           |
| 🧩 **Manual Submission Risks**     | Manual exports introduce potential for **data corruption**, **omission**, **variability in device models**, and **user misunderstandings**, leading to misreporting during export

To begin the analysis, we load all the required R packages in https://github.com/julielaursen/r-fitbit-data. These package are used for data cleaning, manipulation, visualization, and time/date processing. 

### Packages used in this project:
- `tidyverse`: a colletion of R packages for data science, including:
  - `dplyr`: For data wrangling and transformation
  - `ggplot2`: For visualizing trends and patterns
  - `readr`: For reading data files
  - `tidyr`: For reshaping and cleaning data
  - `tibble, stringr, forcats, purrr`: Support functions for tidy data workflows
- `here, skimmer, and janitor`: for simplifying data cleaning tasks

To install the tidyverse package:
  `install.packages("tidyverse")`

To load the tidyverse package: 
  `library(tidyverse)`

Then we read the data, changing each csv file into a data frame that we can execute commands against.

```r
daily_activity <- read_csv("mturkfitbit_export_4.12.16-5.12.16/Fitabase Data 4.12.16-5.12.16/dailyActivity_merged.csv")
heartrate_seconds_merged <- read_csv("mturkfitbit_export_4.12.16-5.12.16/Fitabase Data 4.12.16-5.12.16/heartrate_seconds_merged.csv")
hourly_calories <- read_csv("mturkfitbit_export_4.12.16-5.12.16/Fitabase Data 4.12.16-5.12.16/hourlyCalories_merged.csv")
...

```

#### How is the data organized?

The data is organized in two different folders, one for the period of 3/12/16-4/11/16 and one for 4/12/16-5/12/16. Although this data is supposed to be continuous, it seems that data from folder1 is incomplete. On inspection, the range of dates often stop at 4/9 which would leave a noticeable 3 day gap between the two data collections. There are also a different number of users in the dataset. For example, 35 users recorded daily activity in the first data set and only 3 in the second dataset. It seems that the user with ID `2891001357` and ID `6391747486` may have dropped out of the study between the first and second dataset. Therefore, we are only focusing on the second dataset as it is more complete.
  
#### How does it help you answer your question?

#### Are there any problems with the data?

Yes, the summary of the dataset from the project states that there are 30 total users in the dataset. However, there are 33 people tracking their daily activity and the people who are tracking their activity are not also consistently tracking other metrics. Heartrate seconds, minutes slept, and weightlog are being tracked by less than the statistically significiant amount of people to form a valid sample. For this reason, we are eliminating some data such as weight tracking from our analysis.

```r
> n_distinct(daily_activity$Id)
[1] 33
> n_distinct(hourly_calories$Id)
[1] 33
> n_distinct(heartrate_seconds$Id)
[1] 14
> n_distinct(hourly_intensities$Id)
[1] 33
> n_distinct(hourly_steps$Id)
[1] 33
> n_distinct(minute_sleep$Id)
[1] 24
> n_distinct(weightlog_info$Id)
[1] 8
```

## 2. Prepare

I began cleaning the data with several goals in mind. I wanted to eliminate duplication. I wanted to ensure that the column names, type and format for date are consistent across tables. As I cleaned the data, I also made sure the column names were lowercase and in snake case for consistency.

In minute_sleep there were 543 duplicate rows:
```r
> nrow(minute_sleep[duplicated(minute_sleep),])
[1] 543
```

In daily_sleep there were 3 duplicate rows:
```r
> nrow(daily_sleep[duplicated(daily_sleep),])
[1] 3
```

I then confirmed this by removing duplicates and comparing the rows before and after to ensure the number of rows subtracted equaled the number of rows returned in the previous command

```r
> nrow(minute_sleep)
[1] 188521
> minute_sleep_clean <- minute_sleep %>% distinct()
> nrow(minute_sleep_clean)
[1] 187978
```

```r
> nrow(daily_sleep)
[1] 413
> daily_sleep_clean <- daily_sleep %>% distinct()
> nrow(daily_sleep_clean)
[1] 410
```

Dates were also inconsistent across tables. Before analysis, I also needed to conert these dates in date or character format to *date time* format and then split them to date and time separately.

| Table                       | Date/Time Column | **Current Type** | **Needed Type** | Granularity |
| --------------------------- | ---------------- | ---------------- | --------------- | ----------- |
| `daily_activity`            | `ActivityDate`   | character        | Date            | Daily       |
| `hourly_calories`           | `ActivityHour`   | character        | POSIXct         | Hourly      |
| `hourly_steps`              | `ActivityHour`   | character        | POSIXct         | Hourly      |
| `hourly_intensities`        | `ActivityHour`   | character        | POSIXct         | Hourly      |
| `heartrate_seconds_merged`  | `Time`           | character        | POSIXct         | Second      |





