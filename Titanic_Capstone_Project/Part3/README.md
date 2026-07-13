Part 3: Data Integrity, Row Deduplication, and Memory Footprint Optimization
Clean columns don't matter if the underlying rows are redundant or chewing up unnecessary machine resources. Part 3 handles row-level isolation and downcasts underlying object primitives.

3.1 Defensive Row Deduplication
Data duplication often causes subtle data leakage, where identical rows accidentally end up in both training and evaluation splits, skewing accuracy metrics.

We perform an explicit check using df.duplicated().sum().

The dataset returned 0 duplicate rows.

However, the pipeline retains an active df.drop_duplicates() statement as a defensive programming best practice to ensure production stability against future dirty data batches.

3.2 Categorical Downcasting & Memory Reclamation
By default, Pandas stores text strings (Sex column containing male or female) as generic object datatypes. This creates heavy internal pointer arrays that waste RAM.

Since Sex only has two distinct states, we convert it into a highly efficient category type. This shifts storage from costly string buffers to small underlying integer codes paired with a compact lookup map:

Python
# Optimizing the object schema
df["Sex"] = df["Sex"].astype("category")
Memory Recovery Metrics:
Initial DataFrame Footprint: 292,500 bytes

Post-Optimization Footprint: 245,756 bytes

Efficiency Gains: A ~16% absolute reduction in total memory utilization achieved by changing a single column's storage behavior. This optimization pattern is essential when scaling pipelines to gigabyte-scale datasets.