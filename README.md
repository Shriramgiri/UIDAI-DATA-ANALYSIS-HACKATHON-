# AadhaarLens: From Activity to Action

## Detecting Hidden Service Pressure Across Districts

AadhaarLens uses Exploratory Data Analysis (EDA) to uncover patterns in Aadhaar enrolment, demographic updates, biometric updates, and district-level activity. The project focuses on identifying locations where Aadhaar activity behaves unusually relative to their own normal patterns.

## Problem Statement

**From Aadhaar Activity to Action: Detecting Hidden Service Pressure Across India**

Our objective is to understand Aadhaar activity across time, age groups, states, and districts, with particular focus on:

1. **Demand** — Where is Aadhaar enrolment concentrated, and how does it vary across age groups and time?
2. **Maintenance** — Which districts show high demographic and biometric update intensity relative to enrolment?
3. **Anomalies** — Which districts experience unusually high or low activity relative to their own patterns?

### Core Research Question

> Where is Aadhaar activity behaving differently from the normal pattern, and what does that reveal about potential service pressure across districts?

## Objectives

- Clean and validate the UIDAI Aadhaar activity dataset.
- Standardize geographic fields before analysis.
- Engineer meaningful activity and maintenance features.
- Study enrolment patterns by age group.
- Compare demographic and biometric update behaviour.
- Analyse temporal trends.
- Identify unusual district-level activity using statistical anomaly detection.
- Segment districts based on Aadhaar activity behaviour.
- Translate findings into evidence-based operational priorities.

## Dataset

The project uses the UIDAI Aadhaar activity dataset provided for the hackathon.

### Main fields

| Column | Description |
|---|---|
| `date` | Date of recorded activity |
| `state` | State/UT |
| `district` | District |
| `pincode` | Pincode |
| `age_0_5` | Enrolments for age 0–5 |
| `age_5_17` | Enrolments for age 5–17 |
| `age_18_greater` | Enrolments for age 18+ |
| `demo_age_5_17` | Demographic updates for age 5–17 |
| `demo_age_17_` | Demographic updates for age 18+ |
| `bio_age_5_17` | Biometric updates for age 5–17 |
| `bio_age_17_` | Biometric updates for age 18+ |

The dataset contains aggregated activity counts rather than individual-level records.

## Feature Engineering

### Total enrolment

```text
total_enrolment =
age_0_5 + age_5_17 + age_18_greater
```

### Total demographic updates

```text
total_demo_updates =
demo_age_5_17 + demo_age_17_
```

### Total biometric updates

```text
total_bio_updates =
bio_age_5_17 + bio_age_17_
```

### Total updates

```text
total_updates =
total_demo_updates + total_bio_updates
```

### Total Aadhaar activity

```text
total_activity =
total_enrolment + total_updates
```

### Maintenance intensity

```text
maintenance_intensity =
total_updates / total_enrolment
```

Ratio-based metrics are interpreted carefully when enrolment is zero or very small.

## Exploratory Data Analysis

The project follows a connected analytical sequence:

### 1. Demand Analysis
Identify high-activity states and districts and examine enrolment by age group.

### 2. Temporal Analysis
Study daily and monthly activity and use rolling averages to identify changes and trends.

### 3. Maintenance Analysis
Compare demographic and biometric updates and calculate maintenance intensity relative to enrolment.

### 4. District Behaviour
Compare districts using enrolment and maintenance intensity.

### 5. Anomaly Detection
Calculate district-level z-scores to identify activity that is unusually high or low relative to the district's own pattern.

## Key Visualizations

- Top states by total Aadhaar activity
- Enrolment by age group
- Monthly Aadhaar activity trend
- Daily activity with rolling average
- Demographic vs biometric update scatter plot
- District enrolment vs maintenance intensity
- Top districts by maintenance intensity
- Correlation heatmap
- State × Month activity heatmap
- **District × Month anomaly heatmap**

### Standout Visualization: District-Level Anomaly Heatmap

The anomaly heatmap shows how unusual monthly activity is for selected districts relative to each district's own activity pattern.

| Z-score | Interpretation |
|---:|---|
| `>= +2` | Very high anomaly |
| `+1 to +2` | High |
| `-1 to +1` | Normal |
| `-2 to -1` | Low |
| `<= -2` | Very low anomaly |

This helps identify isolated spikes, repeated high-activity periods, and unusually low periods that may warrant further investigation.

## Methodology

```text
Raw UIDAI Data
      ↓
Data Quality Audit
      ↓
Cleaning & Geographic Standardization
      ↓
Feature Engineering
      ↓
Univariate EDA
      ↓
Bivariate EDA
      ↓
Trivariate / Time-based Analysis
      ↓
Anomaly Detection
      ↓
District Behaviour Analysis
      ↓
Operational Insights
```

## Operational Framework

The analysis can classify districts into analytical categories:

- **Enrolment Priority** — relatively high enrolment demand
- **Maintenance Priority** — relatively high update intensity
- **Dual-Service Pressure** — high demand combined with high maintenance activity
- **Monitor / Investigate** — unusual activity patterns requiring closer examination

These are project-defined analytical categories, not official UIDAI classifications.

## Technology Stack

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn (optional clustering)
- SciPy (optional statistical analysis)
- Google Colab / Jupyter Notebook

## How to Run

### Google Colab / Jupyter Notebook

1. Open Google Colab / Jupyter Notebook
2. Create a new notebook.
3. Upload `UIDAI.csv`.
4. Run the data loading cell.
5. Run cleaning and feature-engineering cells.
6. Run EDA visualizations.
7. Run anomaly detection.
8. Save charts and findings for the final report.

### Basic imports

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

## Important Analytical Considerations

- The data represents **aggregated activity counts**, not individual Aadhaar records.
- Geographic names should be standardized before grouping.
- Raw counts should not be treated as directly comparable measures of population demand when district population sizes differ.
- Correlation does not establish causation.
- Anomalies identify unusual statistical behaviour but do not establish the reason.
- Small enrolment denominators can make ratio-based metrics unstable.
- External population data may be added for per-capita analysis if appropriate.

## Expected Outcome

The project transforms Aadhaar activity records into a connected analytical story:

**Demand → Maintenance → Anomaly → District Behaviour → Operational Priority**

Instead of asking only:

> Which state has the most Aadhaar activity?

AadhaarLens asks:

> **Which districts are behaving differently from their normal patterns, what type of activity is driving that behaviour, and where might operational attention be warranted?**

## Project Structure

```text
AadhaarLens/
│
├── UIDAI.csv
├── AadhaarLens_EDA.ipynb
├── README.md
│
├── outputs/
│   ├── state_activity.png
│   ├── monthly_trend.png
│   ├── age_distribution.png
│   ├── maintenance_intensity.png
│   ├── update_comparison.png
│   └── anomaly_heatmap.png
│
└── report/
    └── AadhaarLens_Final_Report.pdf
```

## Hackathon Impact

The project is designed around:

- **Data Analysis & Insights**
- **Creativity & Originality**
- **Technical Implementation**
- **Visualization & Presentation**
- **Impact & Applicability**

The emphasis is on a small number of connected, interpretable analyses rather than many unrelated charts.

## Limitations

This project identifies patterns and statistical anomalies in the provided dataset. It does not independently establish the causes of those patterns.

Operational recommendations should therefore be treated as **evidence-based prioritisation signals for further investigation**, not definitive explanations or official policy recommendations.

## Team

**Project:** AadhaarLens  
**Theme:** Aadhaar Enrolment & Update Analytics  
**Focus:** EDA-driven detection of hidden service pressure across districts

## License

This repository is intended for hackathon and analytical demonstration purposes. Refer to the applicable UIDAI dataset terms and hackathon rules for data usage and redistribution.
