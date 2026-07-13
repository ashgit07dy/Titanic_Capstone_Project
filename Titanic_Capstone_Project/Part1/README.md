## Part 1: Environment Setup, Data Ingestion, and Structural Inspection

This phase establishes the computing environment, loads the raw primitives, and performs a top-level architectural check on the dataset's dimensions and foundational data types.

### 1.1 Python Stack Configuration
We instantiate the core data science ecosystem using standard aliases. Additionally, a critical quality-of-life configuration is applied to the Pandas rendering engine to prevent column truncation during multi-feature inspections.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Prevent layout truncation for wide tables
pd.set_option("display.max_columns", None)
1.2 Raw Data Ingestion
The immutable source data (train.csv) is read into an in-memory DataFrame structures.

Python
df = pd.read_csv("train.csv")
Dimensional Baseline: The execution of df.shape maps out an initial canvas of 891 individual passenger profiles (rows) across 12 distinct features (columns).

Surface Scanning: Utilizing df.head(), we perform a visual sanity check on the schema. The raw layout maps out structural features (PassengerId, Ticket), demographic variables (Name, Sex, Age), socioeconomic markers (Pclass, Fare, Cabin, Embarked), and the target class (Survived, SibSp, Parch)