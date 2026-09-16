**Decision 1: Using Baseline 3-Sigma Method**

I started with the provided baseline\_3sigma.py as a foundation.



Alternative:

Build a model completely from scratch.



Why not:

The baseline is already close to production and provides a strong anomaly signal. Using it allowed me to focus on improving decision quality rather than rebuilding everything.





**Decision 2: Defining "Needs a Visit"**

I defined a gateway needing a visit based on:

\- High anomaly hours (from baseline)

\- High meter read failure rate



Alternative:

Use anomaly detection alone.



Why not:

Anomalies do not always translate to real-world impact. Meter read failures directly indicate customer impact and revenue loss.



**Decision 3: Feature Engineering (ML Thinking)**

I created an additional feature:

\- failure\_rate = (meters\_expected - meters\_read) / meters\_expected



This acts as a strong indicator of gateway health.



Alternative:

Use raw meter readings directly.



Why not:

Raw values are not normalized and are harder to interpret. Failure rate gives a consistent and comparable metric.



**Decision 4: Score Combination Strategy**

I combined anomaly score and failure rate using:



score = base\_score × (1 + failure\_rate)



Alternative:

\- Add fixed weights

\- Use complex ML models (e.g., Random Forest)



Why not:

\- Addition can underweight strong signals

\- Complex models require proper training, validation, and risk overfitting



This multiplicative approach behaves like a simple ML model by scaling importance based on failure severity.



**Decision 5: Time-Aware Merging (Critical Fix)**

I merged datasets using:

gateway\_id + week\_start



Alternative:

Aggregate failure rate across all weeks.



Why not:

This ignores temporal behavior and led to no change in rankings. Weekly alignment ensures the model reacts to recent failures.



**Decision 6: Choosing Machine Learning Approach (Part 2)**

I selected Machine Learning as my focus area.



Approach:

Instead of training a full model, I applied ML principles:

\- Feature engineering (failure\_rate)

\- Feature combination (score scaling)

\- Ranking as decision output



Reason:

This approach improves the baseline while remaining simple, explainable, and reliable without requiring heavy training pipelines.



Alternative:

Train a supervised ML model.



Why not:

\- Requires labeled data (not clearly defined in problem)

\- Risk of overfitting

\- Less explainable for operations team



**What My Solution Cannot Do**



\- It does not learn from labeled failures

\- It cannot predict unseen patterns beyond existing signals

\- It assumes past behavior continues into future weeks

\- It may miss sudden unexpected failures





**What I Would Improve with More Time**



\- Apply machine learning principles more formally by introducing a trained model once reliable labels are defined  

\- Add telemetry-based features such as disconnections, reboot counts, and offline duration  

\- Incorporate time-series trends to detect failures earlier instead of reacting after anomalies  

\- Optimize decision thresholds using the €380 (visit cost) vs €600 (failure cost) trade-off  

\- Evaluate the model on unseen weeks and gateways to ensure generalization

