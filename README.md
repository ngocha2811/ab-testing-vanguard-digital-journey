# A/B Testing Data Analysis – Vanguard Digital Journey

## 1. Project Overview

This project analyzes the results of an **A/B test conducted on Vanguard’s digital client experience** to evaluate whether a redesigned interface improves user engagement and process completion compared to the existing interface.

The analysis investigates whether the new experience leads to **statistically significant improvements in user behavior**, using several metrics including completion rate, error rate, and time spent during the journey.

The goal is to provide **data-driven insights and recommendations** regarding whether the redesigned interface should be implemented at scale.

---

# 2. Business Problem

Vanguard introduced a redesigned digital interface intended to improve the user experience during an online client process.

To evaluate the effectiveness of the redesign, an **A/B experiment** was conducted:

- **Control Group (A)** – Existing interface  
- **Test Group (B)** – Redesigned interface  

The primary objective of the experiment is to determine whether the redesigned interface improves the **process completion rate**.

Vanguard also defined a **business threshold**: the redesign must increase completion rate by **at least 5 percentage points** to justify the cost of full implementation.

---

## Key Questions

This analysis focuses on answering the following questions:

1. Does the redesigned interface increase the completion rate?
2. Does the improvement exceed the **5% business threshold**?
3. Does the new interface reduce or increase user errors?
4. Does the redesign change the time users spend navigating the process?

---

## Table of Contents

1. [Project Overview](#1-project-overview)  
2. [Business Problem](#2-business-problem)  
3. [Dataset](#3-dataset)  
4. [Project Structure](#4-project-structure) 
5. [Project Workflow](#5-project-workflow) 
6. [Data Cleaningn](#6-data-cleaning)  
7. [Exploratory Data Analysis (EDA)](#7-exploratory-data-analysis-(EDA))
8. [Metrics Definition](#8-metrics-definition)
9. [Completion Rate Analysis](#9-completion-rate-analysis) 
10. [Error Rate Analysis](#10-error-rate-analysis)  
11. [Time Spent on the Journey](#11-time-spent-on-the-journey)  
12. [Hypothesis Testing](#12-hypothesis-testing)  
13. [Key Insights](#13-key-insights)  
14. [Business Recommendation](#14-business-recommendation)  
15. [Tools & Technologies](#15-tools-&-technologies)
16. [Author](#16-author)

# 3. Dataset

The dataset contains records of client interactions during the experiment.

Each record represents a user reaching a specific step of the process at a given time.

### Main Variables

| Variable | Description |
|--------|-------------|
| client_id | Unique identifier for each client |
| group | Experiment group (Control or Test) |
| visitor_id | Identifier for a user session |
| visit_id | Unique identifier for each visit |
| process_step | Step reached in the process (`start`, `step_1`, `step_2`, `step_3`, `confirm`) |
| date_time | Timestamp indicating when the step was reached |

---

# 4. Project Structure

```
ab-testing-vanguard-digital-journey
│
├── data
│   ├── raw_data.csv
│   └── cleaned_data.csv
│
├── notebooks
│   ├── cleaning.ipynb
│   ├── ab_testing_analysis.ipynb
│   └── eda.ipynb
│
├── README.md
└── requirements.txt
```

---

# 5. Project Workflow

The project follows a standard **A/B testing analysis workflow**:

1. Data Cleaning  
2. Exploratory Data Analysis (EDA)  
3. Metric Definition  
4. Statistical Hypothesis Testing  
5. Visualization  
6. Business Insights and Recommendations  

---

# 6. Data Cleaning

Several preprocessing steps were performed to ensure data quality:

- checked for missing values
- removed duplicate records
- converted timestamps to datetime format
- validated that each `visit_id` belongs to a single experiment group
- verified that each visit corresponds to one client
- merged experiment data with web activity logs

These steps ensured that the dataset accurately reflects the experiment structure.

---

# 7. Exploratory Data Analysis (EDA)

Initial exploration was conducted to understand the dataset and identify behavioral patterns between the Control and Test groups.

### Key analyses

- group size comparison
- distribution of user journeys
- completion rate comparison

### Observations

- Control and Test groups have similar sizes, indicating a balanced experiment.
- The Test group appears to have a higher completion rate.
- Differences in user navigation patterns were observed between groups.

These patterns were further evaluated using statistical testing.

---

# 8. Metrics Definition

Three metrics were used to evaluate the impact of the redesigned interface.

## Completion Rate

Completion rate measures the percentage of visits that successfully reach the final step (`confirm`).

```
Completion Rate = Completed Visits / Total Visits
```

This is the **primary business metric** because it represents successful completion of the process.

---

## Error Rate

Error rate measures how often users move backward to a previous step during a visit.

```
Error Rate = Visits with Errors / Total Visits
```

Backward navigation may indicate confusion or friction in the process flow.

---

## Time Spent on the Journey

Time spent on the journey measures how long users take to move between steps during a visit.

This metric helps evaluate the **efficiency of the user journey** and whether the redesigned interface changes user behavior.

---

# 9. Completion Rate Analysis

Completion rate was calculated by identifying visits that reached the final step (`confirm`).

### Results

Control completion rate: **49.64%**  
Test completion rate: **58.35%**

Observed improvement:

**+8.71 percentage points**

This suggests that users interacting with the redesigned interface were more likely to complete the process.

---

# 10. Error Rate Analysis

Errors were identified when users navigated backward to a previous process step during the same visit.

### Results

Control error rate: **20.22%**  
Test error rate: **26.84%**

The Test group shows a **higher error rate**, suggesting that some steps in the redesigned journey may introduce confusion or hesitation.

---

# 11. Time Spent on the Journey

The duration of each journey was calculated by measuring time differences between consecutive process steps within each `visit_id`.

Average time spent navigating between steps was then compared between the Control and Test groups.


| Variation | Average Journey Time (seconds) |
|----------|-------------------------------|
| Control  | 83.65 |
| Test     | 84.20 |

---

# 12. Hypothesis Testing

Statistical tests were conducted to determine whether observed differences between groups are significant.

Significance level: **α = 0.05**

---

## Completion Rate Test

Two-proportion z-test

**Hypotheses**

H₀: p(Test) − p(Control) ≥ 5%  
H₁: p(Test) − p(Control) < 5%

**Results**

- z-statistic = **9.75**  
- p-value = **1.00**

**Interpretation**

The improvement in completion rate is **not statistically smaller than the required 5% threshold**, meaning the redesigned interface **meets Vanguard’s business requirement**.

---

## Error Rate Test

Two-proportion z-test

**Hypotheses**

H₀: p(Test) ≥ p(Control)  
H₁: p(Test) < p(Control)

**Results**

- z-statistic = **20.33**  
- p-value = **1.00**

**Interpretation**

There is **no statistical evidence that the redesigned interface reduces the error rate**.  
Descriptive results suggest the Test interface may introduce additional navigation friction.

---

## Time Spent Test

Independent two-sample t-test

**Hypotheses**

H₀: μ(Test) = μ(Control)  
H₁: μ(Test) ≠ μ(Control)

**Results**

- t-statistic = **0.64**  
- p-value = **0.52**

**Interpretation**

There is **no statistically significant difference** in the time users spend navigating between steps.

---

# 13. Key Insights

The analysis reveals several important findings:

- The redesigned interface significantly increases completion rates.
- Completion improved from **49.64% to 58.35%**, exceeding the **5% business threshold**.
- However, the Test group doesn't shows a **higher error rate**, suggesting some steps may be less intuitive. that test group doesnt have lower error rate.
- The redesign does **not significantly change the time spent navigating the process**.

Overall, the new interface improves process completion but may introduce additional navigation friction.

---

# 14. Business Recommendation

The redesigned interface demonstrates a **meaningful improvement in completion rate** and meets Vanguard’s business requirement.

### Recommendation

The redesigned interface should be considered for rollout because it increases the number of successful process completions.

However, the higher error rate suggests that certain steps may require further usability improvements.

Before full deployment, Vanguard should:

- analyze which steps generate the most backward navigation
- improve clarity in those steps
- conduct additional usability testing

---

# 15. Tools & Technologies

The analysis was conducted using:

- Python  
- Pandas  
- NumPy  
- SciPy  
- Matplotlib  
- Seaborn  
- Jupyter Notebook  

---

# 16. Author

This project was completed as part of the **Data Analytics Bootcamp at Ironhack**.

**Ngoc Ha Nguyen**  
LinkedIn:  
https://www.linkedin.com/in/hannah-ngocha-nguyen