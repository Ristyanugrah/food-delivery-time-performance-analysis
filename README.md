# Food Delivery Time Performance Analysis

**Data Analytics | Operations Analytics | Delivery Performance**

An end-to-end data analytics project exploring food delivery performance, delivery duration, distance, weather, traffic conditions, preparation time, courier experience, and SLA-based delivery status using Python.

## Project Overview

Delivery speed is an important operational metric for food delivery businesses. Understanding the factors associated with longer delivery times can help businesses identify operational bottlenecks, improve delivery planning, and evaluate service performance.

This project analyzes a food delivery dataset containing 1,000 records and nine variables. It combines exploratory data analysis (EDA), correlation analysis, delivery performance comparisons, and an analyst-defined Service Level Agreement (SLA) framework to investigate on-time and late deliveries.

## Business Problem

Food delivery operations face different challenges depending on delivery distance, weather, traffic conditions, preparation time, and courier characteristics.

The central business question is:

**Which factors are associated with longer delivery times, and how can delivery performance be evaluated using distance-based delivery targets?**

The analysis investigates:

- The distribution of delivery times and potential extreme observations.
- The relationship between delivery distance and delivery duration.
- Differences in delivery time across weather, traffic, time of day, and vehicle type.
- Relationships between preparation time, courier experience, and delivery duration.
- On-time and late delivery performance under an analyst-defined SLA.
- Delivery delays by distance band and by weather–traffic combinations.

## Project Objectives

1. Understand the structure and quality of the food delivery dataset.
2. Clean missing values and prepare data for analysis.
3. Identify patterns and potential outliers in delivery duration.
4. Explore operational factors associated with delivery time.
5. Evaluate delivery performance using distance-based time targets.
6. Identify extreme delivery cases for further investigation.
7. Produce analytical summaries that can support operational decision-making.

## Dataset Overview

The project uses `Food_Delivery_Times.csv`.

| Attribute | Description |
|---|---|
| Number of records | 1,000 |
| Original variables | 9 |
| Analysis type | Exploratory and operational analytics |
| Data format | CSV |
| Main outcome | Delivery time in minutes |

### Key Variables

| Variable | Description |
|---|---|
| `Order_ID` | Unique order identifier |
| `Distance_km` | Delivery distance in kilometers |
| `Weather` | Weather condition |
| `Traffic_Level` | Traffic intensity |
| `Time_of_Day` | Time-of-day category |
| `Vehicle_Type` | Vehicle used for delivery |
| `Preparation_Time_min` | Order preparation time in minutes |
| `Courier_Experience_yrs` | Courier experience in years |
| `Delivery_Time_min` | Delivery duration in minutes |

## Tools and Technologies

- **Python** — Data analysis.
- **Pandas** — Data cleaning, transformation, aggregation, and export.
- **NumPy** — Numerical operations and SLA classification.
- **Matplotlib** — Data visualization.
- **Seaborn** — Statistical visualization.
- **Google Colab** — Notebook development and execution.

## Analytical Workflow

### 1. Data Understanding

- Load the CSV dataset.
- Review the first rows and dataset structure.
- Examine missing values and duplicate records.
- Review numerical summaries and categorical distributions.

### 2. Data Quality Assessment

The notebook checks missing values, duplicate rows, duplicate `Order_ID` values, numerical ranges, and potential outliers using the Interquartile Range (IQR) method.

The initial assessment identified:

- Missing values in `Weather`, `Traffic_Level`, `Time_of_Day`, and `Courier_Experience_yrs`.
- No candidate outliers in `Distance_km`, `Preparation_Time_min`, or `Courier_Experience_yrs` using the specified IQR thresholds.
- Six potential outliers in `Delivery_Time_min`.
- A delivery time range of 8 to 153 minutes.

Potential outliers are retained for investigation rather than automatically removed.

### 3. Data Cleaning

A copy of the original dataset is created before cleaning.

- Missing categorical values are filled with the mode of their respective columns.
- Missing courier experience values are filled with the median.
- The cleaned dataset is checked again for missing values and duplicate rows.

The resulting cleaned dataset contains **1,000 rows and nine columns, with zero missing values**.

Mode and median imputation are practical preprocessing choices, but they may affect category distributions and numerical summaries. This should be considered when interpreting the results.

### 4. Exploratory Data Analysis

The EDA examines:

- Delivery time distribution using histograms and boxplots.
- Delivery distance versus delivery duration.
- Average delivery time by weather.
- Average delivery time by traffic level.
- Average delivery time by time of day.
- Average delivery time by vehicle type.
- Correlations between delivery duration, distance, preparation time, and courier experience.

### 5. SLA-Based Delivery Performance

The notebook defines analyst-selected delivery targets based on distance.

| Delivery distance | Target delivery time |
|---|---:|
| Up to 5 km | 45 minutes |
| More than 5 km to 10 km | 60 minutes |
| More than 10 km to 15 km | 75 minutes |
| More than 15 km to 20 km | 90 minutes |

Delivery status is assigned using the following rules:

- **On-Time:** Actual delivery time is less than or equal to the assigned target.
- **Late:** Actual delivery time exceeds the assigned target.
- **Review Required:** No valid target is assigned.

The target values are analytical assumptions established for this project, not verified company policies or industry-wide standards.

The analysis calculates the on-time rate, late rate, average delivery duration, median delivery duration, average distance, and delay minutes for late orders.

### 6. Operational Analysis

The project compares operational characteristics between on-time and late orders, including:

- Average delivery distance.
- Average preparation time.
- Average courier experience.
- Average delivery duration.

It also investigates late delivery rates by distance band and by combinations of weather and traffic level.

### 7. Extreme Delivery Cases

Delivery times above 116 minutes are flagged for additional investigation.

The threshold of 116 minutes comes from the upper IQR boundary calculated during the initial outlier assessment. It is used to identify unusual delivery cases, not as a separate SLA target.

### 8. Exporting Analytical Outputs

The notebook exports the following files:

- `delivery_kpi_summary.csv`
- `delivery_distance_analysis.csv`
- `delivery_weather_traffic_analysis.csv`
- `delivery_status_comparison.csv`
- `extreme_delivery_orders.csv`
- `Food_Delivery_Times_Cleaned.csv`

These files can be used for further analysis, reporting, or dashboard development.

## Key Findings

The notebook's EDA summary reports the following findings.

### 1. Delivery Distance Has a Strong Positive Relationship with Delivery Time

The Pearson correlation between delivery distance and delivery time is **0.781**.

This indicates a strong positive linear association in the dataset: longer delivery distances tend to be associated with longer delivery durations.

### 2. Preparation Time Has a Moderate Positive Relationship with Delivery Time

The reported correlation between preparation time and delivery time is **0.307**.

This suggests that longer preparation times tend to be associated with longer overall delivery durations, although correlation alone does not establish causation.

### 3. Courier Experience Has a Very Weak Negative Relationship with Delivery Time

The reported correlation is **-0.089**.

The relationship is very weak, so courier experience alone has limited linear association with delivery duration in this dataset.

### 4. Weather Conditions Are Associated with Different Average Delivery Times

The notebook reports:

- Snowy conditions: **67.11 minutes** on average.
- Clear conditions: **53.15 minutes** on average.

These descriptive differences suggest that weather conditions may be relevant when evaluating delivery performance.

### 5. Traffic Level Is Associated with Delivery Duration

The notebook reports:

- High traffic: **64.81 minutes** on average.
- Low traffic: **52.89 minutes** on average.

This difference indicates that traffic conditions are worth investigating in delivery planning and operational monitoring.

### 6. Differences by Time of Day and Vehicle Type Are Smaller in the Notebook Summary

The notebook reports:

- Evening: 57.48 minutes; Night: 55.21 minutes.
- Car: 58.20 minutes; Scooter: 56.05 minutes.

These comparisons are descriptive and should be interpreted alongside group sizes and variability.

**Note:** The values above are taken from the notebook's prepared insight summary. The final KPI and SLA results should be regenerated from the executed notebook before publication, particularly if the dataset or preprocessing steps change.

## Business Recommendations

Based on the observed patterns, the following actions are proposed for evaluation.

1. **Use distance-aware delivery planning.** Consider delivery distance when estimating delivery times and assigning delivery targets.
2. **Monitor preparation time.** Track the time required to prepare orders and investigate whether preparation bottlenecks contribute to longer end-to-end delivery durations.
3. **Consider weather and traffic conditions.** Use operational monitoring to identify conditions associated with slower delivery performance.
4. **Review late deliveries by distance band.** Compare late rates across the defined distance groups to identify where operational improvements may be most useful.
5. **Investigate extreme delivery cases.** Review orders exceeding 116 minutes to understand whether the delays are associated with distance, weather, traffic, preparation time, or other factors.
6. **Use a consistent SLA definition.** Document the distance-based targets and review them with operational stakeholders before treating them as official performance standards.
7. **Monitor performance over time.** Track on-time rate, late rate, average delivery time, and delay minutes to evaluate operational changes.

These recommendations are proposed actions based on descriptive analysis. Their effectiveness would need to be evaluated using operational data and subsequent performance measurements.

## Limitations

- The dataset contains 1,000 records and may not represent every food delivery operation or location.
- The SLA thresholds are analyst-defined assumptions and have not been validated against company policies.
- Filling missing categorical values with the mode and courier experience with the median can affect the resulting analysis.
- Correlation does not establish causation.
- The notebook's insight summary should be cross-checked against the final executed analysis outputs before reporting definitive conclusions.
- The project does not establish the financial impact of late deliveries or the causal effect of any operational intervention.

## Repository Structure

Suggested repository structure:

```text
food-delivery-time-performance-analysis/
├── README.md
├── food_delivery_time_performance_analysis.ipynb
├── data/
│   └── Food_Delivery_Times.csv
└── outputs/
    ├── delivery_kpi_summary.csv
    ├── delivery_distance_analysis.csv
    ├── delivery_weather_traffic_analysis.csv
    ├── delivery_status_comparison.csv
    ├── extreme_delivery_orders.csv
    └── Food_Delivery_Times_Cleaned.csv
```

The `data/` and `outputs/` folders are suggested structures. Include the files only when they are available and permitted to be shared.

## How to Run the Project

1. Clone or download the repository.
2. Open the notebook in Google Colab or Jupyter Notebook.
3. Install the required libraries if necessary.
4. Upload `Food_Delivery_Times.csv` and update the file path in the notebook if needed.
5. Run the notebook cells sequentially.
6. Review the generated charts, KPI tables, SLA summaries, and exported CSV files.

### Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn
```

## Project Outcome

This project demonstrates a practical workflow for analyzing food delivery operations using Python. It combines data quality assessment, exploratory analysis, correlation analysis, SLA-based classification, and operational comparisons to identify factors associated with delivery duration.

The analysis provides a foundation for delivery performance monitoring and further investigation into operational efficiency.

## Author

**Risty Anugrah Dwi Septiana**  
Data Analyst | Business Intelligence Enthusiast

- **GitHub:** [Ristyanugrah](https://github.com/Ristyanugrah)
- **Portfolio Repository:** [Data Analytics Portfolio](https://github.com/Ristyanugrah/data-analytics-portfolio)
- **Portfolio Website:** [risty-portfolio.vercel.app](https://risty-portfolio.vercel.app/)

---

*This project was developed for data analytics portfolio purposes.*
