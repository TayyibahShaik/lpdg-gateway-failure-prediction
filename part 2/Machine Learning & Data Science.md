\# Part 2 — Machine Learning \& Data Science



**🎯 Problem Definition**



The goal is to decide which gateways “need a visit”.



A gateway needs a visit if:

\- It shows abnormal behavior (anomalies)

\- It impacts meter readings (failures)



Baseline only detects anomalies, but does not measure real-world impact.





**🧠 Approach**



I combined two signals:



1\. Anomaly Score (from baseline)

&#x20;  - Detects unusual behavior



2\. Failure Rate

&#x20;  - Measures real impact on customers

failure\_rate = (meters\_expected - meters\_read) / meters\_expected


**⚙️ Model Logic**



Instead of training a complex ML model, I used a scoring function:

final\_score = base\_score × (1 + failure\_rate)


**Why this works:**

\- Keeps anomaly importance

\- Increases priority for real failures

\- Simple and explainable

\- No overfitting risk



**📈 Why This is Better**



Baseline:

\- Detects anomalies only



My approach:

\- Detects anomalies + real failures



👉 This leads to better prioritization of critical gateways



**💰 Business Decision**



Costs:

\- €380 → site visit

\- €600 → missed failure (per week)



Strategy:

\- Prioritize gateways with higher failure rate

\- Accept small false positives to avoid repeated €600 losses



&#x20;**🧪 Evaluatio**n



\- Maintained 15 gateways per week

\- Compared ranking changes

\- Verified predictions.csv using validation script



**⚠️ Limitations**



\- No trained ML model

\- No time-series prediction

\- Assumes past behavior continues



**🚀 Future Improvements**



\- Train ML model (Logistic Regression / XGBoost)

\- Add telemetry features (reboots, disconnections)

\- Use time-series forecasting

\- Optimize cost-based threshold



**📌 Conclusion**



This solution applies machine learning principles through:



\- Feature engineering

\- Signal combination

\- Business-aware decision making



It improves the baseline by aligning predictions with real-world impact.



