# Titanic Data Cleaning & Exploratory Analysis Pipeline

 Welcome to this repository. This project focuses on cleaning, optimizing, and performing an initial statistical check on the classic Titanic dataset. Instead of jumping straight into building machine learning models, the goal here was to build a rock-solid, clean dataset (`cleaned_data.csv`) while keeping an eye on things like memory footprints and feature distributions.

Project Objective: To architect a production-ready, clean, and resource-efficient data preprocessing pipeline using the classic Titanic dataset. This pipeline bridges the gap between raw, messy data ingestion and model-ready feature arrays.📊 The Macro MetricsData Retention: 100% row integrity maintained (891 rows $\times$ 12 columns). Zero ghost rows or duplicates detected during auditing.Missing Data Resolution: 179 missing entries resolved systematically. Missing values in Age (19.87%) were resolved via median imputation to protect against outlier drift, while Embarked (0.22%) was resolved using mode imputation.Feature Risk Flagged: Cabin was systematically flagged as a high-risk structural hazard due to a 77.10% null-rate, dropping it from baseline considerations to prevent data pollution.Computational Efficiency: Achieved an immediate ~16% reduction in RAM footprint (saving over 46,000 bytes) by transforming low-cardinality string objects (Sex) into optimal categorical memory blocks.Statistical Alert: Diagnosed a severe right-skewness profile in Fare (Skewness: 4.78), signaling a mandatory requirement for logarithmic or power transformations before feeding the feature into linear estimators.

Core Engineering Pipeline Architecture[Raw Train.csv] 
       │
       ▼
[Part 1: Ingestion & Schema Audit] ──► 891 rows × 12 columns verified
       │
       ▼
[Part 2: Tactical Imputation]      ──► Median (Age) | Mode (Embarked) | Flag (>20% Cabin)
       │
       ▼
[Part 3: Memory Reclamation]       ──► String Object ──► Categorical Downcast (~16% RAM saved)
       │
       ▼
[Part 4: Distribution Diagnostics] ──► Skewness Profiling (Fare: 4.78) & Describe Matrix
       │
       ▼
[Cleaned_Data.csv]                 ──► Automated Round-Trip Integrity Verification Passed!


Final VerdictThis pipeline establishes that data preprocessing isn't just about deleting empty rows—it’s about balancing mathematical accuracy (variance-preserving imputation), compute efficiency (categorical downcasting), and algorithmic safety (skewness diagnostics). The resulting asset, cleaned_data.csv, is completely verified and statistically profiled for any downstream Machine Learning workflow.
