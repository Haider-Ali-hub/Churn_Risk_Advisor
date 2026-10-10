# 📊 Churn Risk Advisor

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://churnriskadvisor-dvvv5nizk3df2fax7m8bwx.streamlit.app/)
[![Python 3.12](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![XGBoost 2.0.3](https://img.shields.io/badge/XGBoost-2.0.3-228B22)](https://xgboost.readthedocs.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An interactive, machine learning-driven web application designed to predict customer churn risk for telecommunications services. Built using an optimized **XGBoost** model and deployed via **Streamlit Community Cloud**, this tool provides both real-time individual risk assessments and large-scale batch scoring capabilities.

🔗 **Live Application:** [Churn Risk Advisor Web App](https://churnriskadvisor-dvvv5nizk3df2fax7m8bwx.streamlit.app/)  
📁 **GitHub Repository:** [Haider-Ali-hub/Churn_Risk_Advisor](https://github.com/Haider-Ali-hub/Churn_Risk_Advisor)

---

## 🌟 Key Features

* **Real-time Single Customer Assessment:** Interactively adjust customer demographic and subscription parameters to instantly view churn probability and risk bands (Low, Moderate, High).
* **Batch Scoring Capability:** Upload CSV datasets (e.g., `sample_customers.csv`) to process up to 50 customer profiles simultaneously with instant risk tiering and downloadable results.
* **Actionable Retention Recommendations:** Automatically provides strategic recommendations and intervention strategies based on predicted churn probabilities.
* **XGBoost ML Engine:** Powered by a pre-trained XGBoost 2.0.3 classifier for accurate probability estimates.

---

## 📸 Screenshots

### 1. Single Customer Scoring Tab
<img width="1365" height="642" alt="one customer tab" src="https://github.com/user-attachments/assets/d865004b-7596-4d4e-a952-e50240356289" />

*Interactive UI for analyzing individual customer profiles, churn probability, and risk tiers.*

### 2. Batch Scoring Tab
<img width="1366" height="642" alt="Batch tab" src="https://github.com/user-attachments/assets/d3e5d5f4-372a-4deb-8910-1b59a67eb968" />

*Batch processing 50+ customer profiles using `sample_customers.csv`.*

---

## 🛠️ Tech Stack

* **Language:** Python 3.12
* **Web Framework:** Streamlit
* **Machine Learning Engine:** XGBoost (`2.0.3`) & Scikit-Learn (`1.6.1`)
* **Data Processing & Analytics:** Pandas & NumPy
* **Model Serialization:** Joblib

---

## 📁 Repository Structure

```text
Churn_Risk_Advisor/
├── app.py                  # Main Streamlit application entry point
├── churn_model.joblib      # Pre-trained XGBoost model artifact
├── model_meta.json         # Feature list and metadata specification
├── sample_customers.csv    # Sample batch input dataset for testing
├── requirements.txt        # Python dependency specifications
└── README.md               # Project documentation
```

---

## 🚀 Local Setup & Installation

Follow these steps to run the application locally on your machine:

### Prerequisites
Ensure you have **Python 3.12** installed on your system.

### 1. Clone the Repository
```bash
git clone https://github.com/Haider-Ali-hub/Churn_Risk_Advisor.git
cd Churn_Risk_Advisor
```

### 2. Set Up Virtual Environment
```bash
# On Windows
python -m venv .venv
.venv\Scripts\activate

# On macOS/Linux
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Run the Streamlit Application
```bash
streamlit run app.py
```
The application will automatically launch in your default browser at `http://localhost:8501`.

---

## ☁️ Deployment Instructions

The application is configured for seamless deployment on **Streamlit Community Cloud**:

1. Fork or push this repository to GitHub.
2. Sign in to [Streamlit Community Cloud](https://share.streamlit.io/).
3. Click **New app** and select your repository:
   * **Repository:** `Haider-Ali-hub/Churn_Risk_Advisor`
   * **Branch:** `main`
   * **Main file path:** `app.py`
4. In **Advanced Settings**, set the **Python version** to `3.12`.
5. Click **Deploy!**.

---

## 👤 Author

* **Haider Ali** - [@Haider-Ali-hub](https://github.com/Haider-Ali-hub)

---

## 📜 License

This project is open-source and available under the [MIT License](LICENSE).
