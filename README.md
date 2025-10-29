# Cybersecurity Incident Classification

A machine learning solution for automating security incident triage in Microsoft Security Operation Centers (SOCs).

##  Project Overview

This project develops a classification model that accurately categorizes cybersecurity incidents into three categories:
- **True Positive (TP)**: Real security threats requiring immediate action
- **False Positive (FP)**: False alarms that can be safely ignored
- **Benign Positive (BP)**: Non-malicious but noteworthy events

##  Business Impact

- **Reduces SOC analyst workload** by automating incident triage
- **Accelerates threat response time** through precise classification
- **Improves enterprise security posture** by minimizing false positives
- **Enables guided response systems** for appropriate action recommendations

##  Dataset

- **GUIDE Dataset**: 9.5 million cybersecurity incidents
- **45 original features** across evidence, alert, and incident hierarchies
- **Class distribution**: Severe imbalance (43% BP, 34% TP, 21% FP)
- **Target variable**: IncidentGrade (TP, FP, BP)

##  Technical Approach

### Data Preprocessing
- Handled missing values (columns with >90% missing data removed)
- Addressed severe class imbalance using stratified sampling
- Encoded categorical variables (Label Encoding & One-Hot Encoding)
- Created time-based features from timestamps

### Feature Engineering
- Removed ID-like columns to prevent data leakage
- Created temporal features: Hour, DayOfWeek, Month, IsWeekend
- Engineered binary flags for missing technique data

### Model Development
```python
Models Evaluated:
- Logistic Regression (Baseline): 0.385 F1 Macro
- Decision Tree: 0.997 F1 Macro (Overfit)
- Random Forest: 0.982 F1 Macro
- XGBoost: 0.913 F1 Macro
- Tuned Random Forest: 0.903 F1 Macro (Selected)

 Model Performance
Model Comparison
Model	Macro F1 Score	Precision	Recall	Status
Random Forest	0.9817	0.98	0.98	Best Performance
XGBoost	0.9125	0.92	0.90	Good Alternative
Tuned Random Forest	0.9027	0.91	0.90	Conservative Choice
Logistic Regression	0.3850	0.39	0.39	Baseline
Decision Tree	0.9968	1.00	1.00	Overfit

Selected Model: Random Forest
Macro F1 Score: 0.9817
Precision: 0.98 (Macro Avg)
Recall: 0.98 (Macro Avg)
Accuracy: 0.98

Class-wise Performance (Random Forest)
Class	Precision	Recall	F1-Score
Benign Positive (0)	0.98	0.99	0.98
False Positive (1)	0.98	0.97	0.98
True Positive (2)	0.99	0.98	0.99

 Key Insights
Random Forest outperformed all other models with 0.9817 F1 Score
Decision Tree overfitted severely (0.9968 F1 - unrealistic)
ID columns removal prevented data leakage and improved generalization
Class imbalance handling was crucial for balanced performance

 Future Improvements
Experiment with Deep Learning models
Implement SHAP values for better interpretability
Add real-time prediction capabilities
Develop API for integration with SOC platforms

 Acknowledgments
Microsoft for providing the GUIDE dataset
Cybersecurity experts for domain guidance
Open-source community for ML libraries and tools
