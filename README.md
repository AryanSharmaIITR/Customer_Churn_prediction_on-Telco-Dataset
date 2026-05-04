# 📊 Customer Churn Prediction on Telco Dataset

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat-square&logo=jupyter)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-green?style=flat-square&logo=scikit-learn)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

**An End-to-End Machine Learning Project for Predicting Customer Churn in Telecommunications**

[Features](#-features) • [Dataset](#-dataset) • [Models](#-models) • [Results](#-results) • [Quick Start](#-quick-start) • [Usage](#-usage)

</div>

---

## 🎯 Overview

This project implements a comprehensive machine learning pipeline to predict customer churn in a telecommunications company. Using advanced data science techniques, feature engineering, and multiple ML algorithms, we identify high-risk customers with actionable insights powered by **SHAP explainability analysis**.

Customer churn is one of the most critical metrics for telecom companies. By accurately predicting which customers are likely to leave, businesses can implement targeted retention strategies, ultimately reducing customer acquisition costs and maximizing lifetime value.

**Key Achievement**: Optimized Random Forest model achieving competitive recall scores through hyperparameter tuning with Optuna, enabling effective identification of at-risk customers.

---

## 🌟 Features

✅ **Comprehensive EDA & Data Cleaning**
- Exploratory data analysis with 70+ visualizations
- Outlier detection and handling using IQR method
- Missing value imputation with statistical approaches
- Data validation and quality checks

✅ **Advanced Feature Engineering**
- Binary encoding for categorical variables
- One-hot encoding for multi-class features
- Feature selection based on statistical significance
- Standardization and scaling of numerical features

✅ **Multiple ML Models**
- **Logistic Regression**: Baseline interpretable model
- **Random Forest**: Ensemble learning with optimization
- **Bagging Classifier**: Bootstrap aggregating with Decision Trees
- Hyperparameter optimization using **Optuna** framework

✅ **Model Explainability**
- SHAP values for feature importance analysis
- Individual prediction explanations (waterfall plots)
- Feature impact visualization (beeswarm plots)
- Actionable insights for business stakeholders

✅ **Robust Evaluation**
- Cross-validation with stratified k-fold
- Classification metrics: Precision, Recall, F1-Score
- ROC-AUC analysis and threshold optimization
- Comprehensive classification reports

---

## 📊 Dataset

**Source**: Telco Customer Churn Dataset (Excel format)

**Dataset Characteristics**:
- **Samples**: 7,043 customer records
- **Features**: 30+ attributes covering:
  - Demographics (age, gender, dependents)
  - Account information (tenure, contract type, billing)
  - Service features (internet, phone, streaming services)
  - Financial metrics (monthly charges, total charges, CLTV)

**Target Variable**:
- Binary classification: Churn (Yes/No)
- Class distribution: Imbalanced (73% retained, 27% churned)

**Files**:
- `Telco_customer_churn.xlsx` - Raw dataset
- `Preprocessed_Dataset.xlsx` - Cleaned and engineered features
- `Model_with_Threshold.pkl` - Serialized optimized model
- `dataset_detail.pkl` - Data pipeline artifacts

---

## 🤖 Models & Performance

### Model Comparison

| Model | Accuracy | Precision | Recall | F1-Score |
|-------|----------|-----------|--------|----------|
| Logistic Regression | Baseline | — | — | — |
| Random Forest | High | High | **Optimized** | Competitive |
| Bagging Classifier | Competitive | — | — | — |

### Hyperparameter Optimization

Used **Optuna** framework to optimize Random Forest parameters across 50 trials:
- `n_estimators`: 100-500
- `max_depth`: 3-30
- `min_samples_split`: 2-20
- `min_samples_leaf`: 1-10
- `max_features`: sqrt, log2, None

**Optimization Goal**: Maximize Recall (minimize false negatives in churn prediction)

---

## 🔍 Key Insights

### Top Churn Drivers (from SHAP Analysis):
1. **Contract Type**: Month-to-month contracts show highest churn risk
2. **Tenure**: Customers with low tenure (< 3 months) are at greater risk
3. **Monthly Charges**: Higher charges correlate with increased churn
4. **Internet Service**: Fiber optic users show different churn patterns
5. **Streaming Services**: Limited streaming services correlate with loyalty

### Data Quality Findings:
- **Missing Values**: ~11 records had missing Total Charges
- **Duplicates**: Removed 0 duplicate records
- **Outliers**: Detected and handled in Total Charges using IQR method
- **Data Type Issues**: Corrected Total Charges from object to numeric

---

## 📁 Project Structure

```
Customer_Churn_prediction_on-Telco-Dataset/
│
├── README.md                          # Project documentation
├── LICENSE                            # MIT License
├── .gitignore                         # Git ignore rules
│
├── NoteBook/
│   ├── EDA.ipynb                      # Exploratory Data Analysis (77 cells)
│   └── Model.ipynb                    # Model Building & Optimization (36 cells)
│
└── artifacts/
    ├── dataset_detail.pkl             # Data preprocessing pipeline
    └── Model_with_Threshold.pkl       # Production-ready model
```

---

## 🚀 Quick Start

### Prerequisites

```bash
python >= 3.8
pip install -r requirements.txt
```

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/Customer_Churn_prediction_on-Telco-Dataset.git
cd Customer_Churn_prediction_on-Telco-Dataset

# Install dependencies
pip install pandas numpy scikit-learn matplotlib seaborn optuna shap jupyter

# Launch Jupyter
jupyter notebook
```

### Run the Analysis

1. **Start with EDA**: Open `NoteBook/EDA.ipynb`
   - Explore data distributions
   - Understand feature relationships
   - Identify patterns and anomalies

2. **Build Models**: Open `NoteBook/Model.ipynb`
   - Train baseline models
   - Optimize hyperparameters
   - Generate SHAP explanations

---

## 💻 Usage

### Making Predictions

```python
import pickle
import pandas as pd

# Load the optimized model
with open('artifacts/Model_with_Threshold.pkl', 'rb') as f:
    model = pickle.load(f)

# Load your preprocessed data
X_new = pd.read_excel('Dataset/Preprocessed_Dataset.xlsx')

# Make predictions
churn_predictions = model.predict(X_new)
churn_probabilities = model.predict_proba(X_new)

# Get high-risk customers
high_risk = X_new[churn_probabilities[:, 1] > 0.5]
```

### Interpreting Results

```python
import shap

# Create explainer for a customer prediction
explainer = shap.TreeExplainer(model)
shap_values = explainer(X_new)

# Visualize why a specific customer is likely to churn
shap.plots.waterfall(shap_values[0])  # First customer
```

---

## 📈 Model Training Pipeline

```
Raw Dataset
    ↓
Data Cleaning & Validation
    ↓
Feature Engineering & Selection
    ↓
Train-Test Split (70-30)
    ↓
Feature Scaling (StandardScaler)
    ↓
Model Training (LR, RF, Bagging)
    ↓
Hyperparameter Optimization (Optuna)
    ↓
Model Evaluation & SHAP Analysis
    ↓
Production Model Serialization
```

---

## 🛠️ Technologies & Libraries

| Category | Technologies |
|----------|--------------|
| **Data Processing** | Pandas, NumPy |
| **Visualization** | Matplotlib, Seaborn |
| **Machine Learning** | scikit-learn, Optuna |
| **Explainability** | SHAP |
| **Notebooks** | Jupyter |
| **Data Format** | Excel (xlsx) |

---

## 📊 Evaluation Metrics

- **Accuracy**: Overall correctness of predictions
- **Precision**: True positives among predicted positives (minimize false alarms)
- **Recall**: True positives among actual positives (minimize missed churners)
- **F1-Score**: Harmonic mean of precision and recall
- **ROC-AUC**: Area under the receiver operating characteristic curve
- **Cross-Validation**: k-fold with stratified sampling

---

## 🎓 Learning Outcomes

This project demonstrates:
- ✅ End-to-end ML pipeline development
- ✅ Data preprocessing and feature engineering best practices
- ✅ Ensemble learning and model optimization
- ✅ Handling imbalanced datasets
- ✅ Model explainability and interpretability
- ✅ Hyperparameter tuning with Bayesian optimization
- ✅ Production-ready code structure

---

## 🔮 Future Enhancements

- 🔄 Implement deep learning models (Neural Networks)
- 📊 Add customer segmentation analysis
- 🎯 Deploy model as REST API (Flask/FastAPI)
- 🔔 Real-time prediction pipeline
- 📱 Interactive dashboard with Streamlit/Dash
- 🌐 Web application for stakeholder access
- 🧪 Advanced ensemble methods (XGBoost, LightGBM)
- 📈 Temporal analysis and trend forecasting

---

## 📝 Notebooks Overview

### `EDA.ipynb` - Exploratory Data Analysis
Comprehensive analysis covering:
- Data ingestion and shape exploration
- Missing value and duplicate detection
- Data type validation and conversion
- Outlier detection and handling
- Univariate and bivariate analysis
- Categorical feature distribution analysis
- Feature selection and engineering

### `Model.ipynb` - Model Development
Complete ML pipeline including:
- Data loading and train-test splitting
- Feature scaling with StandardScaler
- Logistic Regression baseline
- Random Forest with Optuna optimization
- SHAP feature importance analysis
- Bagging Classifier implementation
- Model comparison and evaluation

---

## 🤝 Contributing

Contributions, bug reports, and feature requests are welcome! 

```bash
# Fork the repository
# Create a feature branch (git checkout -b feature/improvement)
# Commit changes (git commit -am 'Add improvement')
# Push to branch (git push origin feature/improvement)
# Create a Pull Request
```

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

Copyright © 2026 Aryan Sharma

---

## 👤 Author

**Aryan Sharma**

---

## 📧 Contact & Support

For questions, suggestions, or collaboration opportunities:
- 📧 Email: [your-email@example.com]
- 💼 LinkedIn: [your-linkedin-profile]
- 🐙 GitHub: [your-github-profile]

---

## 🙏 Acknowledgments

- Telco Customer Churn Dataset community
- scikit-learn and open-source ML community
- SHAP library for explainability insights
- Optuna framework for hyperparameter optimization

---

<div align="center">

**If you found this project helpful, please ⭐ star the repository!**

Made with ❤️ by Aryan Sharma

</div>