# 🚀 LPDG Innovation Hub Challenge 2026

## 📌 Overview

This project identifies the **top 15 gateways per week** that require site visits to prevent failures in a radio network carrying meter readings.

The solution improves the provided **baseline (3-sigma anomaly detection)** by incorporating **meter read failure rates**, making the results more aligned with real-world impact and business cost.


## 🎯 Problem Statement
- Each gateway connects multiple meters.
- When a gateway fails, meter readings stop.
- Failures are not immediately visible.
- Only **15 site visits per week** are allowed.

### 💰 Cost Trade-off:
- €380 → cost of a site visit  
- €600 → cost of missing a failed gateway  

👉 Goal: **Select the most critical gateways to minimize loss**

## 📂 Project Structure
project/
├── solution.py ✅
├── predictions.csv
├── README.md
├── DECISIONS.md
├── AI-USAGE.md
└── .gitignore

---

## ⚠️ Dataset Notice

The dataset is **not included** in this repository due to challenge restrictions.

To run this project:
- Place the dataset inside a folder named `data/`

### Expected structure:
├── telemetry/
├── meter_read_success.csv
├── gateway_master.csv
├── field_visits.csv
└── engineer_review_2026-02.xlsx

## ⚙️ How to Run

### 🔹 Step 1: Place Dataset

Make sure your dataset is inside:
   data/

### 🔹 Step 2: Run the Solution

bash
```python Solution.py --data data --out predictions.csv```

📊 Output

The script generates:
```predictions.csv```

**✔ Output Details:**
120 rows (8 weeks × 15 gateways)
Required columns:
week_start
rank
gateway_id
score
reason

🧠 Approach
🔹 Baseline
Uses 3-sigma anomaly detection
Detects abnormal gateway behavior
🔹 Improvement

The solution enhances the baseline by adding meter failure impact.

📌 Key Idea:
failure_rate = (meters_expected - meters_read) / meters_expected

**📌 Final Score combines:**
Anomaly frequency (flagged hours)
Anomaly severity (z-score)
Unread meters (impact)
Failure rate (%)

👉 This ensures both technical anomalies + real-world impact are considered.
