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

## ❓ Ask
💡 BUSINESS TASK: Our team has been asked to analyze smart device data to gain insight into consumer behavior trends. The insights we discover will then help guide marketing strategy for the company. 

Specifically, our team needs to answer:
1. What are some trends in smart device usage?
2. How could these trends apply to Bellabeat customers?
3. How could these trends help influence Bellabeat's marketing strategy?

Primary stakeholders: Urška Sršen and Sando Mur, executive team members.

Secondary stakeholders: Bellabeat marketing analytics team.

## 💻 Prepare 
This data was sourced from FitBit Fitness Tracker Data and made available by the user Möbius on Kaggle at https://www.kaggle.com/arashnic/fitbit. This is a public dataset. Kaggle is a platform for data science and machine learning projects.

## 🔬 ROCCC Analysis of Dataset

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

### 📦 Packages used in this project:
- `tidyverse`: a collection of R packages for data science, including:
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

#### 🗂️ How is the data organized?

The data is organized in two different folders, one for the period of `3/12/16-4/11/16` and one for `4/12/16-5/12/16`. Although this data is supposed to be continuous, it seems that data from folder1 is incomplete. On inspection, the range of dates often stop at 4/9 which would leave a noticeable 3 day gap between the two data collections. There are also a different number of users in the dataset. For example, 35 users recorded daily activity in the first data set and only 3 in the second dataset. It seems that the user with ID `2891001357` and ID `6391747486` may have dropped out of the study between the first and second dataset. Therefore, we are only focusing on the second dataset as it is more complete.
  
#### ❓ How does it help you answer your question?

The data provides insights into users’ daily habits related to physical activity, heart rate, and sleep patterns. These insights are crucial for understanding trends and behaviors in smart device usage, which can inform Bellabeat’s marketing strategies and product improvements.

#### 🚩 Are there any problems with the data?

Yes, the summary of the dataset from the project states that there are 30 total users in the dataset. However, there are 33 people tracking their daily activity and the people who are tracking their activity are not also consistently tracking other metrics. Heartrate seconds, minutes slept, and weightlog are being tracked by less than the statistically significiant amount of people to form a valid sample. For this reason, we are eliminating some data such as weight tracking from our analysis.

```r
> n_distinct(daily_activity$Id)
[1] 33
> n_distinct(daily_calories$Id)
[1] 33
> n_distinct(daily_intensities$Id)
[1] 33
> n_distinct(daily_steps$Id)
[1] 33
> n_distinct(daily_sleep$Id)
[1] 24
> n_distinct(weight_log$Id)
[1] 8
```

## ✍🏻 Prepare

I began preparing the data with several goals in mind. I wanted to eliminate duplication and null values. I wanted to ensure that the column names, type and format for date are consistent across tables. As I cleaned the data, I also made sure the column names were lowercase and in snake case for consistency.

The tables I am analyzing after renaming:

```r
daily_activity
daily_calories
daily_intensities
daily_steps
daily_sleep
hourly_calories
hourly_intensities
hourly_steps
minute_calories
minute_intensities
minute_METs
minute_sleep
minute_steps
heartrate_seconds
```

### 👭 Duplication and Null Rows

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

### Formatting

Daily tables of activity were in long format, but the data in csvs that calculated by minutes came in two different versions. There were tables in long format and tables in wide format. I found the tables in wide format difficult to read. For example,

**Minute Calories (Wide)**

```r
> colnames(minute_calories_wide)
 [1] "Id"           "ActivityHour" "Calories00"   "Calories01"   "Calories02"   "Calories03"   "Calories04"   "Calories05"  
 [9] "Calories06"   "Calories07"   "Calories08"   "Calories09"   "Calories10"   "Calories11"   "Calories12"   "Calories13"  
[17] "Calories14"   "Calories15"   "Calories16"   "Calories17"   "Calories18"   "Calories19"   "Calories20"   "Calories21"  
[25] "Calories22"   "Calories23"   "Calories24"   "Calories25"   "Calories26"   "Calories27"   "Calories28"   "Calories29"  
[33] "Calories30"   "Calories31"   "Calories32"   "Calories33"   "Calories34"   "Calories35"   "Calories36"   "Calories37"  
[41] "Calories38"   "Calories39"   "Calories40"   "Calories41"   "Calories42"   "Calories43"   "Calories44"   "Calories45"  
[49] "Calories46"   "Calories47"   "Calories48"   "Calories49"   "Calories50"   "Calories51"   "Calories52"   "Calories53"  
[57] "Calories54"   "Calories55"   "Calories56"   "Calories57"   "Calories58"   "Calories59"
```

**Minute Calories (Narrow)**

```r
> colnames(minute_calories_narrow)
[1] "Id"             "ActivityMinute" "Calories"
```
The wide version of the calories by minute table logs a row for each activity hour and then use the columns to represent calories burned in each specific minute of an hour. For example Calories00 would represent the calories burned in the first minute of the hour. I found this not to be ideal for understanding the data, so I renamed each file from `minute_value_narrow` to `minute_value` and ignored the files `minute_value_wide` except for comparison value.

```r
> minute_calories <- minute_calories_narrow
> rm(minute_calories_narrow)
> minute_intensities <- minute_intensities_narrow
> rm(minute_intensities_narrow)
> minute_METS <- minute_METS_narrow
> rm(minute_METS_narrow)
> minute_steps <- minute_steps_narrow
> rm(minute_steps_narrow)
```

### 🕰️ DateTime

Dates were also inconsistent across tables. Before analysis, I also needed to convert these dates in date or character format to *date time* format.

| Table                       | Date/Time Column | **Current Type** | **Needed Type** | Granularity | Value     |
| --------------------------- | ---------------- | ---------------- | --------------- | ----------- | -----     |
| `daily_activity`            | `ActivityDate`   | character        | Date            | Daily       | 4/12/2016 |
| `daily_calories`            | `ActivityDay`    | character        | Date            | Daily       | 4/12/2016 |
| `daily_intensities`         | `ActivityDay`    | character        | Date            | Daily       | 4/12/2016 |
| `daily_steps`               | `ActivityDay`    | character        | Date            | Daily       | 4/12/2016 | 
| `daily_sleep`               | `SleepDay`       | character        | Date            | Daily       | 4/12/2016 12:00:00 AM |
| `hourly_calories`           | `ActivityHour`   | character        | POSIXct         | Hourly      | 4/12/2016 12:00:00 AM |
| `hourly_steps`              | `ActivityHour`   | character        | POSIXct         | Hourly      | 4/12/2016 12:00:00 AM |
| `hourly_intensities`        | `ActivityHour`   | character        | POSIXct         | Hourly      | 4/12/2016 12:00:00 AM |
| `minute_calories`           | `ActivityMinute` | character        |  POSIXct        | Minute      | 4/12/2016 12:00:00 AM |
| `minute_intensities`        | `ActivityMinute` | character        | POSIXct         | Minute      | 4/12/2016 12:00:00 AM |
| `minute_METS`               | `ActivityMinute` | character        | POSIXct         | Minute      | 4/12/2016 12:00:00 AM |
| `minute_sleep`              | `date`           | character        | POSIXct         | Minute      | 4/12/2016 2:47:30 AM  | 
| `minute_steps`              | `ActivityMinute` | character        | POSIXct         | Minute      | 4/12/2016 12:00:00 AM |
| `heartrate_seconds`         | `Time`           | character        | POSIXct         | Second      | 4/12/2016 7:21:00 AM  |

To convert the MM/DD/YYYY columns from character to Date in the daily dataframes, I used the `lubridate` library to convert the dates to the correct format and then the class function to verify. For time, I want to use POSIXct as it's easier to manipulate and run mathematical operations against.

```r
daily_activity$ActivityDate <- mdy(daily_activity$ActivityDate)
> class(daily_activity$ActivityDate)
[1] "Date"
> daily_calories$ActivityDay <- mdy(daily_calories$ActivityDay)
> class(daily_calories$ActivityDay)
[1] "Date"
> daily_intensities$ActivityDay <- mdy(daily_intensities$ActivityDay)
> class(daily_intensities$ActivityDay)
[1] "Date
> daily_steps$ActivityDay <- mdy(daily_steps$ActivityDay)
> class(daily_steps$ActivityDay)
[1] "Date"
> daily_sleep$SleepDay <- mdy(daily_sleep$SleepDay)
> class(daily_sleep$SleepDay)
[1] "Date"
```
Then I renamed the date columns to always be `ActivityDate`

```r
> daily_calories <- daily_calories %>% rename(ActivityDate = ActivityDay)
> daily_intensities <- daily_intensities %>% rename(ActivityDate = ActivityDay)
> daily_steps <- daily_steps %>% rename(ActivityDate = ActivityDay)
> daily_sleep <- daily_sleep %>% rename(ActivityDate = SleepDay)
```

For non-daily tables, I converted the date to POSIXct and renamed the column to `ActivityDate`

```r
> hourly_calories <- hourly_calories %>% 
+     rename(ActivityDate = ActivityHour) %>%  # rename column to something clean
+     mutate(
+         ActivityDate = as.POSIXct(
+             ActivityDate,
+             format = "%m/%d/%Y %I:%M:%S %p",  # match "4/12/2016 12:00:00 AM"
+             tz = Sys.timezone()              # set local time zone
+         )
+     )
> 
> 
> View(hourly_calories)
> class(hourly_calories$ActivityDate)
[1] "POSIXct" "POSIXt"
```

Now, I was able to easily check the range of dates to make sure we're not starting late or ending early. All cleaned datasheets (except sleep) start at 4/12/16 midnight and end at 5/12/16 15:00 POSIX time except for minute_calories, minute_intensities, minute_METs, and heartrate_seconds, which all end at 15:59, 15:59, 15:59, and 16:20 respectively. daily_sleep also ends at 00:00:00 or midnight the night before and minute_sleep starts at 4/11/2016 20:48 and ends at 5/12/2016 at 9:56.

**To Note**

daily_sleep has the ActivityDate of midnight which equates to 00:00:00. Since all zeros do not show, it looks as if the time is not included in the date, but `table(format(daily_sleep_clean$SleepDay, "%H:%M:%S"))` proves it's there.

Making all the ranges cover the same amount of time, using the dates of midnight on the start day to midnights on the end day, similar to the sleep tables.

```r
hourly_calories <- hourly_calories %>%
  filter(ActivityDate >= as.POSIXct("2016-04-12 00:00:00"),
         ActivityDate <= as.POSIXct("2016-05-12 00:00:00"))
> range(hourly_calories$ActivityDate)
[1] "2016-04-12 CDT" "2016-05-12 CDT"

> hourly_steps <- hourly_steps %>%
+     filter(ActivityDate >= as.POSIXct("2016-04-12 00:00:00"),
+            ActivityDate <= as.POSIXct("2016-05-12 00:00:00"))
> range(hourly_steps$ActivityDate)
[1] "2016-04-12 CDT" "2016-05-12 CDT"

> hourly_intensities <- hourly_intensities %>%
+     filter(ActivityDate >= as.POSIXct("2016-04-12 00:00:00"),
+            ActivityDate <= as.POSIXct("2016-05-12 00:00:00"))
> range(hourly_intensities$ActivityDate)
[1] "2016-04-12 CDT" "2016-05-12 CDT"

> minute_calories <- minute_calories %>%
+     filter(ActivityDate >= as.POSIXct("2016-04-12 00:00:00"),
+            ActivityDate <= as.POSIXct("2016-05-12 00:00:00"))
> 
> range(minute_calories$ActivityDate)
[1] "2016-04-12 CDT" "2016-05-12 CDT"

minute_intensities <- minute_intensities %>%
  filter(ActivityDate >= as.POSIXct("2016-04-12 00:00:00"),
         ActivityDate <= as.POSIXct("2016-05-12 00:00:00"))
> range(minute_intensities$ActivityDate)
[1] "2016-04-12 CDT" "2016-05-12 CDT"

> minute_METS <- minute_METS %>%
+     filter(ActivityDate >= as.POSIXct("2016-04-12 00:00:00"),
+            ActivityDate <= as.POSIXct("2016-05-12 00:00:00"))
> 
> range(minute_METS$ActivityDate)
[1] "2016-04-12 CDT" "2016-05-12 CDT"

> minute_steps <- minute_steps %>%
+     filter(ActivityDate >= as.POSIXct("2016-04-12 00:00:00"),
+            ActivityDate <= as.POSIXct("2016-05-12 00:00:00"))
> 
> range(minute_steps$ActivityDate)
[1] "2016-04-12 CDT" "2016-05-12 CDT"

> heartrate_seconds <- heartrate_seconds %>%
+     filter(ActivityDate >= as.POSIXct("2016-04-12 00:00:00"),
+            ActivityDate <= as.POSIXct("2016-05-12 00:00:00"))
> 
> range(heartrate_seconds$ActivityDate)





