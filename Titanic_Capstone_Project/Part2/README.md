Part 2:

Advanced Missing Data Diagnosis and Targeted Imputation Tactics
Data gaps can severely bias predictive models or crash linear estimators. This part implements a structural auditing step to flag, analyze, and selectively resolve missing data points based on mathematical safety thresholds.

2.1 Null-Value Matrix Profiling
We run an aggregation query (df.isnull().sum()) combined with relative percentage weights to expose the exact depth of missing data across all columns:

Age: Missing 177 records (~19.87% of the total dataset).

Cabin: Missing 687 records (~77.10% of the total dataset).

Embarked: Missing 2 records (~0.22% of the total dataset).

2.2 Execution of the Imputation Strategy
We avoid broad-stroke fills and instead apply custom statistical rules tailored to each feature's datatype and distribution.

A. The >20% Structural Risk Rule (Cabin)
The pipeline implements an explicit defensive threshold: any feature missing more than 20% of its data is flagged as a structural hazard. Because Cabin is missing 77.10% of its data, guessing values through mean or mode would introduce artificial patterns and pollute the data. The pipeline flags this column to be excluded from baseline modeling or handled separately via pattern extraction.

B. Variance-Preserving Median Imputation (Age)
Since the age distribution contains distinct life-stage groups and natural bounds, the arithmetic mean is highly sensitive to extreme outlier age groups. To keep the imputation robust:


# Safeguarding against outlier distortion

df["Age"] = df["Age"].fillna(df["Age"].median())
By filling the 177 gaps with the median, we preserve the central tendency of the distribution without artificially pulling the distribution towards a skewed average.

C. Categorical Frequency Alignment (Embarked)
With only 2 missing values out of 891 records, dropping the rows would be wasteful, and complex modeling is unnecessary. The pipeline calculates the mode (the most frequently occurring arrival port) and fills the two blanks immediately to achieve 100% data completeness for this feature.
