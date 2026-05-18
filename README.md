# 🩺 Sepsis-XAI: Explainable Early Sepsis Prediction System

[![Streamlit App](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=Streamlit&logoColor=white)](http://localhost:8501)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-111111?style=for-the-badge&logo=scikitlearn&logoColor=white)](https://xgboost.readthedocs.io/)
[![SHAP](https://img.shields.io/badge/SHAP-3498DB?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTEyIDJDMiAxMiAyIDEyIDEyIDIyczEwLTggMTAtOC0yLTEwLTEwLTEweiIvPjwvc3ZnPg==&logoColor=white)](https://shap.readthedocs.io/)

Early detection of sepsis in intensive care units (ICUs) is one of the most critical challenges in modern healthcare. **Sepsis-XAI** is an advanced Clinical Decision Support System (CDSS) that leverages machine learning to predict early-stage sepsis and uses state-of-the-art **eXplainable AI (XAI)** methodologies to translate black-box model decisions into transparent, actionable, and trusted clinical insights for practitioners.

This project is built directly in alignment with the academic findings presented in our included paper: **`Sepsis_Prediction_Research_Paper_final.pdf`**.

---

## 🌟 Key Features

*   **⚡ High-Fidelity Machine Learning Engine**: Powered by an optimized XGBoost classifier trained on processed clinical telemetry (Heart Rate, Temperature, Blood Pressure, Respiratory Rate, Lactate, Oxygen Saturation, etc.).
*   **🔍 Explainable AI (SHAP Integration)**: Provides clear, patient-specific explanations utilizing SHAP tree-explainers, translating mathematical weights into intuitive clinical terms (identifying precisely which vital signs are elevating or lowering the risk).
*   **🛠️ Counterfactual Intervention Planning**: Answers the crucial clinical question: *"What vital signs must be stabilized, and by how much, to reduce this patient's sepsis risk below a safe threshold?"*
*   **⏳ Temporal Risk Timeline Simulation**: Simulates the next 6 hours of patient progression under two distinct scenarios:
    1.  *No Treatment* (Condition worsens over time)
    2.  *With Treatment* (Condition steadily improves via targeted intervention)
*   **🛡️ Uncertainty & Confidence Calibration**: Includes a calibrated risk confidence estimator to display the model's reliability alongside the prediction, preventing over-reliance on marginal predictions.
*   **📑 Clinical Rule Engine**: Cross-references patient vitals against traditional clinical guidelines (e.g., SIRS, SOFA markers like high temperature, high respiratory rates, low MAP, and acidosis) to complement the ML predictions.
*   **📊 Premium Interactive Dashboard**: A highly polished, responsive Streamlit interface that supports existing patient lookup, worst-case selection, and new patient CSV uploads.
*   **📥 Instant Clinical Report Export**: Compiles all analytics, vital-sign counterfactual comparisons, and simulated risk pathways into a professional, downloadable **PDF Clinical Report** for hospital record-keeping.

---

## 🏗️ Project Architecture

```directory
Sepsis-XAI/
├── Sepsis_Prediction_Research_Paper_final.pdf  # Academic research backing the project
└── sepsis-xai/
    ├── data/
    │   └── clean_data.csv                      # Cleaned clinical features & patient data
    ├── models/
    │   └── xgb_model.pkl                       # Serialized XGBoost classification model
    ├── outputs/
    │   └── plots/                              # Generated explainability diagrams (SHAP, etc.)
    └── src/
        ├── app.py                              # Core Streamlit multi-tab clinical dashboard
        ├── train.py                            # Model training script
        ├── preprocess.py                       # Preprocessing and normalization pipelines
        ├── explain_shap.py                     # SHAP explainability processing script
        ├── counterfactuals.py                  # Static counterfactual intervention calculator
        ├── temporal_counterfactuals.py         # Time-horizon step-by-step clinical bounds planner
        ├── risk_timeline.py                    # 6-hour patient health timeline simulation
        ├── uncertainty.py                      # Calibrated confidence & uncertainty estimators
        └── rules.py                            # SIRS/SOFA clinical rule cross-checking logic
```

---

## 🚀 Getting Started

### Prerequisites

*   Python 3.10+
*   Git (for cloning)

### Installation & Setup

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/Abdul-Khader117/Sepsis-Prediction-XAI.git
    cd Sepsis-Prediction-XAI
    ```

2.  **Create and activate a virtual environment**:
    ```bash
    # Windows
    python -m venv venv
    .\venv\Scripts\Activate.ps1
    
    # macOS/Linux
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Install dependencies**:
    ```bash
    pip install streamlit pandas joblib shap matplotlib numpy reportlab xgboost scikit-learn
    ```

---

## 💻 Running the Application

To start the interactive Streamlit clinical dashboard:

```bash
streamlit run sepsis-xai/src/app.py
```

Once executed, Streamlit will boot the local server. Open your browser and navigate to:
👉 **[http://localhost:8501](http://localhost:8501)**

---

## 📑 Dashboard Breakdown & Methodology

### 1. Patient Risk Summary
*   Categorizes risk dynamically: **🟢 LOW (<30%)**, **🟠 MEDIUM (30%-70%)**, or **🔴 HIGH (>=70%)**.
*   Displays predictive confidence to ensure transparency when making high-stakes decisions.
*   Enables sorting and tracking of the top 10 highest-risk patients currently in the ward.

### 2. SHAP (SHapley Additive exPlanations)
*   Visualizes both local patient-level waterfall plots and global feature impact.
*   Clearly maps how abnormal vitals (like fever, hyperventilation, or poor tissue perfusion) push the risk towards sepsis.

### 3. Counterfactual Interventions
*   Iteratively calculates vital sign adjustments to bring the patient back to a stable state.
*   Features before/after treatment risk progression charts and clinical target parameters.

### 4. Future Risk Timelines
*   Projects the patient’s next 6 hours of health progression.
*   Triggers severe clinical alerts if the predicted risk is set to cross the **80% threshold** inside the 6-hour horizon.

---

## 🤝 Contact & Citation

Developed by **Abdul Khader**. If you use this CDSS or build upon the clinical methods in your academic research, please refer to the attached paper: `Sepsis_Prediction_Research_Paper_final.pdf`.
