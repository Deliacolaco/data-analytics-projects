# Gym Customer Segmentation

## Overview
This project applied K-Means++ and Agglomerative clustering in Python 
to segment 2,000 gym members into three distinct customer profiles. 
The goal was to help a gym chain better understand its customer base 
and design more targeted, data-driven marketing strategies for each segment.

---

## Business Problem
A gym chain lacked visibility into differences across its customer base, 
making it difficult to personalise offers or allocate marketing spend 
effectively. The objective was to identify actionable customer segments 
and match each with relevant marketing recommendations.

---

## Dataset
The dataset contains 2,000 gym member records across demographic 
and socioeconomic variables.

**Key variables:**
- Age
- Income
- Gender
- Education
- Occupation
- Marital status
- Settlement size

> Dataset not included due to university assessment restrictions. 
> All analysis and outputs are original work.

---

## Tools Used
- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn

---

## Method
After cleaning and standardising the data, the Elbow Method and 
Silhouette Analysis were used to determine the optimal number of clusters (k=3).

K-Means++ was applied as the primary clustering method due to its 
improved initialisation over standard K-Means. Agglomerative clustering 
was then run independently as a validation check. Both methods produced 
consistent segment structures, supporting confidence in the results.

Each segment was profiled across all demographic and behavioural 
variables to support business interpretation and recommendation development.

**Workflow:**
1. Data cleaning and preparation
2. Exploratory data analysis
3. Feature scaling (StandardScaler)
4. Elbow Method — optimal k selection
5. Silhouette Analysis — cluster quality validation
6. K-Means++ clustering
7. Agglomerative clustering (validation)
8. Segment profiling and interpretation
9. Marketing recommendations

---

## Key Findings

Three distinct customer segments were identified:

### Segment 1 — Youthful, Economically-Conscious Individuals
Younger members with below-average income and high price sensitivity. 
This group represents the highest churn risk and responds best to 
low-cost, flexible membership options.

### Segment 2 — Wealthy Metropolitan Executives
High-income, urban professionals with low visit frequency despite 
active memberships. This group has the highest revenue potential 
and is most receptive to premium services and convenience-focused offers.

### Segment 3 — Knowledgeable Suburban Adults
Mid-career, family-oriented members with consistent attendance and 
strong retention rates. This group forms the gym's most stable 
customer base and responds well to community and family-focused engagement.

---

## Business Recommendations

| Segment | Strategy |
|---|---|
| Youthful, Economically-Conscious | Digital-first budget tiers, referral incentives, flexible contracts |
| Wealthy Metropolitan Executives | Premium wellness packages, off-peak executive services, app-based convenience |
| Knowledgeable Suburban Adults | Family membership bundles, community events, loyalty rewards |

---

## Visual Outputs
- Age and income distribution by segment
- Elbow Method chart (optimal k selection)
- Silhouette Analysis chart (cluster quality)
- Segment profile comparisons

---

## Project Files
- [`report/`](report/) — Full project report (PDF)
- [`code/`](code/) — Python notebook (.ipynb)
- [`assets/`](assets/) — Visual outputs and screenshots
