# 🏋️‍♂️ Fitness & User Performance Data Analysis (SQL + Python)

## 📌 Overview
This project focuses on analyzing user workout consistency, nutritional adherence, and performance metrics from a fitness application dataset. Using **SQL** for data extraction and aggregation, alongside **Python** for data manipulation and visualization, this analysis provides actionable insights to improve user retention and recommendation algorithms.

---

## 🛠️ Tech Stack & Tools
* **Database / Querying:** SQL (JOINs, CTEs, Aggregations, GROUP BY, Window Functions)
* **Data Processing & Analysis:** Python (Pandas, NumPy)
* **Data Visualization:** Matplotlib / Seaborn
* **Version Control:** Git & GitHub

---

## 🔍 Key Questions Answered
1. **Adherence Analysis:** How does daily protein/caloric intake correlate with workout completion rates?
2. **User Segmentation:** Who are the high-performing users versus at-risk inactive users based on monthly logs?
3. **Program Optimization:** Which workout structures lead to the highest user consistency over a 90-day period?

---

## 📊 Sample SQL Queries & Logic

```sql
-- Segmenting users by workout adherence and protein goal compliance
WITH UserMetrics AS (
    SELECT 
        user_id,
        AVG(daily_protein_grams) AS avg_protein,
        COUNT(DISTINCT workout_date) AS active_days
    FROM user_logs
    WHERE log_date >= DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY)
    GROUP BY user_id
)
SELECT 
    user_id,
    avg_protein,
    active_days,
    CASE 
        WHEN active_days >= 12 AND avg_protein >= 120 THEN 'High Adherence'
        WHEN active_days >= 8 THEN 'Moderate Adherence'
        ELSE 'At Risk'
    END AS user_segment
FROM UserMetrics
ORDER BY active_days DESC;
