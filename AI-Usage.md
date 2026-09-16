**Where AI was used**



AI tools were used as a support system during development, mainly for understanding, debugging, and improving the solution.



**1. Understanding the Problem**

AI helped in:

\- Interpreting the challenge requirements

\- Understanding the structure of predictions.csv

\- Clarifying constraints like 15 gateways per week and required columns



**2. Debugging Errors**

AI assisted in resolving issues such as:

\- FileNotFoundError (missing predictions.csv)

\- Incorrect command usage in baseline script (--output vs --out)

\- File path issues while reading datasets

\- Merge errors between datasets



**3. Data Processing**

AI helped with:

\- Calculating failure rate using meter data  

&#x20; (meters\_expected - meters\_read) / meters\_expected

\- Handling missing values safely

\- Merging datasets correctly using gateway\_id and week\_start



**4. Improving the Baseline**

The given baseline used only anomaly detection (3-sigma method).



AI helped extend this by:

\- Adding meter read failure as an additional signal

\- Combining anomaly score with failure rate

\- Re-ranking gateways per week based on updated score



**5. Output Formatting**

AI ensured:

\- Correct column structure

\- Proper sorting and ranking

\- Valid predictions.csv format for submission



**Where AI was NOT used**



\- Final decision on scoring logic

\- Choosing how much weight to give failure rate

\- Understanding why results were not changing

\- Verifying correctness of improvements



These were done through manual reasoning and testing.





**One mistake AI made (and I corrected)**



AI initially suggested using average failure rate across all weeks:



groupby("gateway\_id").mean()



**Problem:**

\- Ignored weekly behavior

\- Did not reflect real-time failures

\- No change in rankings



**Fix:**

Merged data using both gateway\_id and week\_start.



**Result:**

\- Rankings changed correctly

\- Scores became meaningful

\- Improvement was visible



**Summary**



AI was useful for:

\- Debugging

\- Code suggestions

\- Implementation support



However, understanding the problem, validating results, and making final decisions were done independently.



AI was treated as a tool, not a replacement for thinking.

