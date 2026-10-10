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

---

## 📝 Written Analysis & Findings (Write It Section)

### Part 1: Training-Serving Skew & Parity Test
* **Probabilities Comparison:** 
  * `Wrong (Week 3 build_features)`: **0.548**
  * `Right (prepare_input)`: **0.274**
* **Explanation:** When `get_dummies(drop_first=True)` is called on a single row, pandas treats the single present category as the baseline/first category and drops it. As a result, all encoded `Contract` columns become `0`, tricking the model into treating the customer as having a high-risk *Month-to-month* contract instead of a *Two-year* contract, effectively doubling the predicted churn probability[cite: 5].
* **Parity Test Result:** `Parity test passed on 7043 customers` with a maximum absolute difference of `0.0000` ($< 10^{-15}$), proving zero training-serving skew[cite: 5].
* **What-If Driver Analysis:** Switching the contract to **Two year** lowers the risk probability the most (from 0.812 to 0.231). However, this represents a statistical association learned from historical data rather than a guaranteed causal effect; forcing a dissatisfied customer into a long-term contract without addressing underlying issues may lead to default or early cancellation rather than true retention[cite: 6].

### Part 2: Local Application Testing Insights
* **Surprising App Behavior:** Moving the **Contact threshold slider** dynamically updates the assigned Risk Band (Low, Watch, High) instantly across the UI without recalculating or changing the underlying predicted churn probability itself[cite: 10].
* **Problematic Real-World User Input:** A user might enter a extremely high `MonthlyCharges` (e.g., $118) along with a `0` month tenure. Since `TotalCharges` is derived automatically as `tenure * monthly` (0 USD), the model receives an unrealistically skewed ratio that may distort probability scoring for fresh onboarding profiles[cite: 9, 10].

### Part 3: Deployment Verification
* **Public Live URL:** [https://churnriskadvisor-dvvv5nizk3df2fax7m8bwx.streamlit.app/](https://churnriskadvisor-dvvv5nizk3df2fax7m8bwx.streamlit.app/)
* **Deployment Experience:** The initial deployment succeeded seamlessly because `requirements.txt` strictly pinned `scikit-learn` version `1.6.1` matching the training environment, preventing model unpickling/deserialization errors[cite: 6, 7, 11].

---

## ❓ Check Your Understanding

1. **Why does `get_dummies(drop_first=True)` break predictions when scoring a single customer?**  
   Calling `drop_first=True` on a single-row dataframe drops the only present categorical value because pandas views it as the first category[cite: 5]. This zeroes out essential features, causing the model to misinterpret inputs (e.g., misreading a Two-year contract as Month-to-month)[cite: 5].

2. **What does the parity test compare, and why must it cover every training row rather than a few?**  
   The parity test compares predictions generated during model training against predictions produced by the serving encoder (`prepare_input`)[cite: 5]. It must cover every training row to guarantee that no edge case, rare category combination, or missing column setup introduces hidden training-serving skew[cite: 3, 5].

3. **Should the model be loaded with `st.cache_resource` or `st.cache_data`? Why?**  
   It must be loaded with `@st.cache_resource`[cite: 8]. Heavy, stateful objects like machine learning models or database connections should be cached as shared global resources once per server instance rather than re-parsed or duplicated per user session/data mutation[cite: 8].

4. **Why does the app derive `TotalCharges` instead of asking the user to type it?**  
   Deriving `TotalCharges` (`tenure * MonthlyCharges`) prevents user input errors, logical inconsistencies (e.g., specifying high tenure but $0 total charges), and simplifies the UI[cite: 9].

5. **Why must `requirements.txt` pin the exact `scikit-learn` version used in training?**  
   Scikit-learn model artifacts (`.joblib` / `.pkl`) depend on internal class structures and byte code. Pinning the exact training version prevents `InconsistentVersionWarning` or unpickling/deserialization failures during deployment on cloud servers[cite: 4, 7, 11].

6. **The what-if shows a two-year contract lowers risk from 0.79 to 0.27. Would offering one make the customer stay? How could a company find out?**  
   Not necessarily. Observational ML models capture correlations, not direct causality[cite: 6, 10]. To determine if contract extensions actually drive retention, the company must run a controlled randomized experiment (A/B testing) offering promotional long-term contracts to a target cohort[cite: 3, 6].
