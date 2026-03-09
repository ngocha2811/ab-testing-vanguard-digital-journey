# A/B Testing Data Analysis – Vanguard Client Experience

# 1. Project Overview

This project analyzes the results of an A/B test conducted on Vanguard clients to evaluate whether a new digital experience improves user engagement and completion rates compared to the existing interface.

The objective of the analysis is to determine if the new version of the user experience leads to **statistically significant improvements in client behavior**, and to provide **data-driven recommendations** based on the results.


## Project Structure

```
ab-testing-vanguard-digital-journey
│
├── data
│   ├── raw_data.csv
│   └── cleaned_data.csv
│
├── notebooks
│   └── ab_testing_analysis.ipynb
│
├── visuals
│   ├── conversion_rate.png
│   └── user_behavior.png
│
├── README.md
└── requirements.txt
```

## Table of Contents

1. [Project Overview](#1-project-overview)  
2. [Business Problem](#2-business-problem)  
3. [Dataset](#3-dataset)  
4. [Data Cleaning](#4-data-cleaning) 
5. [EDA](#5-EDA) 
6. [Metrics Definition](#6-metrics-definition)  
7. [Completion Rate Analysis](#7-completion-rate-analysis)  
8. [Error Rate Analysis](#8-error-rate-analysis)  
9. [Time Spent on the Journey](#9-time-spent-on-the-journey)  
10. [Hypothesis Testing](#10-hypothesis-testing)  
11. [Key Insights](#11-key-insights)  
12. [Business Recommendation](#12-business-recommendation)  
13. [Tools & Technologies](#13-tools-&-technologies)
14. [Author](#13-author)


---

# 2. Business Problem

Vanguard introduced a redesigned digital interface aimed at improving the client experience during an online process.

To evaluate the effectiveness of this change, an A/B test was conducted:

* **Control Group (A):** Existing interface
* **Test Group (B):** New redesigned interface

The primary objective of this analysis is to determine whether the new interface improves the process completion rate and overall user engagement.

In addition, Vanguard aims to assess whether the redesign delivers a minimum improvement of 5% in completion rate, which is required to justify the cost of implementing the new interface at scale.

---

## Key Questions

The analysis focuses on answering the following questions:

1. Does the redesigned interface lead to a higher completion rate compared to the existing interface?

2. Is the improvement in completion rate at least 5%, meeting the company's threshold for cost-effective implementation?

3. How does user behavior differ between the control and test groups, particularly regarding error rates and process efficiency?

4. What data-driven business insights can be derived from the experiment results to inform future product decisions?

---

# 3. Dataset

The dataset contains information about client interactions during the experiment.

## Main Variables

| Variable        | Description                              |
| --------------- | ---------------------------------------- |
| client_id       | Unique client identifier                 |
| group           | Experiment group (Control or Test)       |
| visitor_id       | Identifier for a user session; a client may have multiple visitor IDs |
| visit_id      | Unique identifier for each visit to the platform            |
| process_step          | Step reached in the process flow (start, step_1, step_2, step_3, confirm)           |
| date_time | Timestamp indicating when the user reached a specific process step                |

---

## Project Workflow

The project follows a typical **A/B testing analytical framework**:

1. Data Cleaning
2. Exploratory Data Analysis (EDA)
3. Conversion Rate Analysis
4. Statistical Hypothesis Testing
5. Data Visualization
6. Business Insights and Recommendations

---

# 4. Data Cleaning

Before conducting the analysis, several data preparation steps were performed to ensure data quality and consistency:

- Checked for missing values across all datasets
- Converted variables to appropriate data types (e.g., timestamps)
- Removed duplicate records
- Verified that each `visit_id` corresponds to a single `client_id`
- Validated that each visit belongs to only one experiment group (Control or Test)
- Merged the web activity dataset with the experiment assignment and process step datasets

---

# 5. EDA

Initial exploration was conducted to understand the dataset and compare behavioral patterns between the control and test groups.

The following aspects were analyzed:

- Group size comparison
- Conversion rate comparison
- Distribution of time spent on the platform
- User behavior patterns during the experiment

Key metrics analyzed:

- Conversion rate by group
- Average time spent on the platform
- Process completion rate

### Key Observations

- The control and test groups have similar sizes, indicating a balanced experiment.
- The test group shows slightly higher engagement based on time spent.
- Conversion rates appear different between groups and will be further tested statistically.

---
# 6. Metrics Definition

To evaluate the impact of the redesigned interface, several key performance metrics were defined to measure how users interacted with the process.

### Completion Rate

Completion rate measures the percentage of visits that successfully reach the final step of the process.

Completion Rate = Completed Visits / Total Visits

A visit is considered completed if the user reaches the final step `confirm`.

This is the primary business metric because it represents the success of the digital process.

### Error Rate

Error rate measures the share of visits in which users move backward from a later step to an earlier step during the same visit.

Error Rate = Visits with Errors / Total Visits

Backward navigation may indicate confusion, hesitation, or difficulty understanding the process flow.

### Time per Step

Time spent per step measures how long users take to move from one step to the next during a visit.

This metric helps evaluate the efficiency of the user journey and whether the redesigned interface changes user behavior during the process.

---

# 7. Completion Rate Analysis

Completion rate was analyzed to determine whether the redesigned interface improved the likelihood that users complete the process.

A visit was classified as completed if the maximum process step reached was `confirm`. Completion rates were then calculated separately for the Control and Test groups.

Results show that the Test group achieved a higher completion rate than the Control group.

Control completion rate: 49.64%  
Test completion rate: 58.35%

This represents an improvement of approximately 8.71 percentage points, indicating that users interacting with the redesigned interface were more likely to complete the process.

Statistical testing was conducted to determine whether this difference is statistically significant and whether the improvement exceeds the business threshold of 5 percentage points.

---

# 8. Error Rate Analysis

In addition to completion rate, error rate was analyzed to evaluate whether the redesigned interface introduced additional friction in the user journey.

An error was identified when a user moved from a later step to an earlier step during the same visit. This was detected by calculating the difference between consecutive process steps within each `visit_id`.

If a negative step difference occurred during a visit, the visit was flagged as containing an error.

Results show that the Test group experienced a higher error rate than the Control group.

Control error rate: 20.22%  
Test error rate: 26.84%

This suggests that although the redesigned interface improved completion rates, it also increased the likelihood of backward navigation between steps. Such behavior may indicate moments of confusion or hesitation in the new process flow.

Statistical tests were performed to evaluate whether the difference in error rates between the two groups is significant.

---

# 9. Time Spent on the Journey

To better understand how the redesigned interface affects user behavior, the total time spent on the process journey was analyzed.

The duration of each visit was estimated by calculating the time difference between the first recorded step and the final recorded step within each `visit_id`. This provides an estimate of how long users take to move through the entire process from start to completion.

The dataset was sorted by `visit_id` and `date_time` to ensure the correct sequence of events within each visit. Time differences between timestamps were then used to compute the duration of each journey.

The average journey duration was compared between the Control and Test groups to evaluate whether the redesigned interface changes the overall time required to complete the process.

This analysis helps assess whether the new interface makes the process more efficient or whether users spend more time navigating the journey.

Statistical tests were conducted to determine whether the difference in average journey duration between the two groups is statistically significant.


# 10. Hypothesis Testing

To determine whether the observed differences between the Control and Test groups are statistically significant, several statistical tests were conducted.

The main objective was to evaluate whether the redesigned interface improves the completion rate by at least 5 percentage points compared to the existing interface.

### Completion Rate Test

A two-proportion z-test was used to compare completion rates between the Test and Control groups.

Null hypothesis (H0)  
The improvement in completion rate for the Test group is less than or equal to 5 percentage points compared to the Control group.

Alternative hypothesis (H1)  
The improvement in completion rate for the Test group is greater than 5 percentage points compared to the Control group.

Results from the test indicate that the difference in completion rates is statistically significant and exceeds the 5 percentage point threshold defined by the business objective.

### Error Rate Test

A chi-square test of independence and a two-proportion z-test were used to evaluate differences in error rates between the two groups.

The results indicate that error occurrence is significantly associated with experiment variation, with the Test group showing a higher rate of backward navigation during the process.

### Time spent on the Journey Test

Independent two-sample t-tests were applied to compare the average time spent at each process step between the Control and Test groups.

These tests help identify whether the redesigned interface significantly changes how long users spend progressing through the process.

# 11. Key Insights

Key findings from the analysis include:

- The redesigned interface significantly improves the overall completion rate compared to the existing interface.
- The Test group achieved a completion rate of 58.35%, compared to 49.64% for the Control group, representing an improvement of 8.71 percentage points.
- Statistical testing confirms that the improvement in completion rate is significant and exceeds the 5 percentage point business threshold defined by Vanguard.
- However, the Test group also shows a higher error rate, indicating that users were more likely to move backward between steps during the process.
- Analysis of the time spent on the journey helps evaluate whether the redesigned interface changes how long users take to complete the process.

Overall, the redesigned interface improves the likelihood that users complete the process, but it may introduce additional friction during certain stages of the journey.

---

# 12. Business Recommendation

Based on the results of the A/B test, the redesigned interface demonstrates a meaningful improvement in completion rate and meets the minimum business requirement of a 5 percentage point increase.

### Recommendation

The redesigned interface should be considered for rollout because it significantly increases the number of users who successfully complete the process.

However, the higher error rate suggests that some parts of the redesigned journey may create confusion or hesitation for users. Before full deployment, it may be beneficial to review the steps where users move backward in the process and identify opportunities to improve clarity and usability.

### Future Analysis

Further analysis could provide deeper insights into user behavior, including:

- identifying which process steps generate the most backward navigation
- performance differences by device type
- behavioral patterns across different client segments
- evaluating the long-term impact of the redesigned interface on client engagement and retention

---

# 13. Tools & Technologies

The analysis was conducted using the following tools:

* Python
* Pandas
* NumPy
* SciPy
* Matplotlib
* Seaborn
* Jupyter Notebook
* Tableau


---

# 14. Author

This project was completed as part of the Data Analytics Bootcamp at Ironhack.

Author: Ngoc Ha Nguyen 
LinkedIn: [let's-connect  ](https://www.linkedin.com/in/hannah-ngocha-nguyen)

