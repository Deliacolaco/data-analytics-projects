# Student Retention Analytics — Macquarie University

A group analytics project for Macquarie University's Business Intelligence and Reporting (BIR) team. We used de-identified enrolment and retention data from 2020–2025 to understand student progression patterns and identify students at risk of not continuing.

The final solution includes two Qlik Sense dashboards built for different stakeholder groups, plus a predictive model that flags students most likely to drop off.

## My Contribution

I designed and built **Dashboard 2: Institutional Retention & Progress Insights**, the executive-facing dashboard used by University Executives to monitor retention, equity outcomes, and faculty performance at an institutional level.

I also contributed to the report's strategic recommendations, key takeaways, and supported the team across other parts of the project.

## Business Problem

Two different groups at the university needed visibility into student retention, but at completely different levels.

- **Course Directors** needed unit-level visibility, which units were driving fails and withdrawals, and which cohorts were most at risk.
- **University Executives** needed an institution-wide view of retention, faculty performance, equity outcomes, and academic progress to guide policy and resourcing.

The data existed but was spread across systems. Trends often got noticed too late to act on.

## Dataset

Two de-identified datasets covering 2020–2025:
- **Enrolment Data:** 284,818 unit-level records, 43 variables
- **Retention Data:** 52,434 course-level records, 13 variables

Both datasets were merged on a shared course admission key. Key variables included gender, citizenship, equity status, grade, unit status, WAM, credit points, faculty, course, study mode, academic year, and retention outcome.

Raw datasets are not shared publicly. They contain real de-identified university data provided under a data governance agreement.

## Tools

- **My contribution (Dashboard 2):** Qlik Sense
- **Team-wide (data prep + modelling):** Python, Pandas, NumPy, Scikit-learn, XGBoost, Matplotlib

## Approach

The team cleaned both datasets, merged them on the shared key, and collapsed the messy continuation codes into three clear outcomes: Retained, Completed, and Not Retained.

For the predictive model, we used a time-aware split to avoid leakage. Features used data only up to year *t*, with the target being retention in year *t+1*. Training used 2020–2022, validation used 2023, and 2024 was held back as a true test set.

For Dashboard 2, I built each chart against an executive use case. Every filter and KPI had to answer the question "what would a senior leader do with this?"

## Key Findings

- Institutional retention improved steadily from 2020 to 2024, then plateaued in 2025.
- Business and Science & Engineering consistently outperformed other faculties.
- Larger faculties had stronger retention and completion outcomes.
- Equity student retention improved from 68% to 74%, narrowing the gap with non-equity students.
- WAM rose steadily before stabilising in 2025, so retention issues are about engagement, not academic difficulty.
- The XGBoost model reached PR-AUC of 0.465 on the 2024 test set, a 5.6× uplift over baseline.
- Flagging the top 20% of highest-risk students would catch around 66% of future attrition cases.

## Files

- `student-retention-analytics.pdf` — Full project report

## Links

- [View full project write-up](https://deliacolaco.github.io/) (portfolio page)
- [View Dashboard 2 (Qlik Cloud)](https://23cen6dozz61syg.ap.qlikcloud.com/sense/app/9b261911-3aea-4951-99d3-3e603903742e/overview)

## Note

This was a group project completed for BUSA8031 – Business Analytics Project at Macquarie University in 2025. Raw datasets are not publicly shared due to university data governance restrictions. All analysis and outputs are original work.
