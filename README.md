📝 Project Overview
This project focuses on automatic call classification for Insurance.
Using 21,915 call records, including both operational metrics and full speech-to-text transcriptions, the goal was to classify each call into:

0 – No dissatisfaction
1 – Dissatisfaction

The process evaluates:

Models trained only using BTS metrics
Models trained using only call transcriptions
Hybrid models combining metrics + text
SHAP value analysis to understand which metrics drive dissatisfaction
An Active Learning workflow to improve performance with fewer labeled examples


🚀 Key Features
✔️ Data Unification Pipeline

Import of multiple dataset sources:

JSON transcriptions
Call metrics (CSV)
Consolidated database (XLSB)


Merging by unique call IDs
Export to unified dataset:
Dataset unificado VERTI.csv

✔️ Preprocessing & Cleaning

Dropping single-value columns
Normalizing flow-related features by call duration
Balancing extreme class imbalance (5.2% dissatisfaction)
Preparing matrices for metrics-only and text-only modeling

✔️ Metrics-Only Model (Neural Network)
Architecture:
Input (32)
Dense(256, relu)
Dropout(0.25)
Dense(1, sigmoid)

Performance (Validation):

ROC AUC: 0.827
Accuracy: 0.76
Class 1 (dissatisfaction):

Precision: 0.14
Recall: 0.74
F1: 0.24



✓ Strong recall for the minority class
✓ Good ranking ability (AUC)

🧠 Active Learning Approach
To compensate for the extreme imbalance, we implemented an iterative sampling strategy:

Initial training set: 900 samples
Validation: 300
Test: 300
Unlabeled pools:

20,027 negatives
388 positives



Workflow:

Train model
Evaluate misclassified samples
Adjust positive/negative sampling ratio
Add 200 samples per iteration
Repeat for 5 iterations

Model metrics tracked:

loss
binary_accuracy
false_negatives
false_positives

Final Test Results:

Accuracy: 0.68
Balanced precision/recall across classes
Optimal threshold: 0.5246


📊 Evaluation Tools
The project includes:
✔️ ROC Curves
With threshold optimization using:
sqrt(tpr * (1 – fpr))
✔️ Classification Reports
Per iteration and per model version
✔️ Training Curves

Loss
Accuracy
Error distributions

✔️ SHAP Value Analysis
Used to rank metrics influencing dissatisfaction

🛠️ Tech Stack

































CategoryToolsDatapandas, numpy, json, unidecodeMLTensorFlow, Keras, Scikit-learnTextTransformersExplainabilitySHAPVisualizationMatplotlib, SeabornUtiltqdm, os, re, copy
