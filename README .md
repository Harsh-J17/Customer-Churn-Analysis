# 📊 Telecom Customer Churn Analysis (TCA)

> An Exploratory Data Analysis (EDA) project to uncover the key drivers of customer churn in a telecom company — and recommend actionable retention strategies.

---

## 📁 Project Structure

```
Telecom-Customer-Churn-Analysis/
│
├── TCA.ipynb                    # Main Jupyter Notebook (EDA + Visualizations)
├── Customer Churn.csv           # Dataset (7,043 customer records)
├── TCA_Executive_Summary.docx   # Executive Summary Report
└── README.md                    # Project documentation
```

---

## 🔍 Problem Statement

Customer churn is one of the costliest problems in the telecom industry. This project analyses a dataset of **7,043 customers** across **21 variables** to answer:

- What percentage of customers are churning?
- Which customer segments are most at risk?
- What factors drive churn the most?
- What retention strategies can reduce churn?

---

## 📦 Dataset

| Property         | Details                              |
|------------------|--------------------------------------|
| Source           | IBM Telco Customer Churn Dataset     |
| Total Records    | 7,043 customers                      |
| Total Features   | 21 variables                         |
| Target Variable  | `Churn` (Yes / No)                   |
| Nulls / Duplicates | 0 nulls · 0 duplicate IDs          |

**Feature Categories:**
- **Demographics** — gender, SeniorCitizen, Partner, Dependents
- **Services** — PhoneService, InternetService, OnlineSecurity, TechSupport, StreamingTV, etc.
- **Account Info** — tenure, Contract, PaymentMethod, MonthlyCharges, TotalCharges
- **Target** — Churn (Yes/No)

---

## 🛠️ Tools & Libraries

```python
import pandas as pd          # Data manipulation
import numpy as np           # Numerical operations
import matplotlib.pyplot as plt  # Visualizations
import seaborn as sns        # Statistical plots
```

**Environment:** Python 3.x · Jupyter Notebook

---

## 🧹 Data Cleaning Steps

1. **TotalCharges** — blank values for 11 new customers (tenure = 0) replaced with `0`; column cast from `object` → `float64`
2. **SeniorCitizen** — integer encoding (`0`/`1`) converted to human-readable `"yes"`/`"no"` labels
3. **Validation** — confirmed zero null values and zero duplicate `customerID` entries

---

## 📊 Key Findings & Percentages

### 🔴 Overall Churn Rate
| Status   | Count | Percentage |
|----------|-------|------------|
| Retained | 5,174 | **73.46%** |
| Churned  | 1,869 | **26.54%** |

---

### 👤 Gender vs. Churn
| Gender | Churn Rate |
|--------|-----------|
| Male   | 26.2%     |
| Female | 26.9%     |

> ✅ Gender is **not** a significant churn predictor — nearly identical rates across both groups.

---

### 👴 Senior Citizen vs. Churn
| Segment           | % of Base | Churn Rate |
|-------------------|-----------|------------|
| Senior Citizens   | 16.2%     | **41.7%**  |
| Non-Senior        | 83.8%     | 23.7%      |

> ⚠️ Senior citizens churn at **75.9% higher rate** than non-senior customers.

---

### ⏳ Tenure vs. Churn
| Tenure Bucket     | Churn Rate |
|-------------------|------------|
| 0 – 12 months     | **47.7%**  |
| 13 – 24 months    | 23.5%      |
| 25 – 48 months    | 15.0%      |
| 49 – 72 months    | **9.5%**   |

> ⚠️ New customers (< 12 months) churn **5× more** than long-term customers. The first year is the critical retention window.

---

### 📄 Contract Type vs. Churn
| Contract Type   | % of Customers | Churn Rate |
|-----------------|----------------|------------|
| Month-to-Month  | 55.0%          | **42.7%**  |
| One Year        | 20.9%          | 11.3%      |
| Two Year        | 24.1%          | **2.8%**   |

> ⚠️ A **15× churn gap** exists between Month-to-Month and Two Year contract holders.

---

### 🌐 Internet Service vs. Churn
| Internet Type | Churn Rate |
|---------------|------------|
| Fiber Optic   | **41.9%**  |
| DSL           | 19.0%      |
| No Internet   | 7.4%       |

---

### 🔧 Add-On Services vs. Churn
| Service          | With Service | Without Service |
|------------------|-------------|-----------------|
| Online Security  | 14.6%       | **31.8%**       |
| Tech Support     | 15.2%       | **31.6%**       |
| Online Backup    | 21.6%       | 30.1%           |
| Device Protection| 22.5%       | 29.5%           |

> ✅ Customers WITH protective add-ons churn at roughly **half the rate** of those without.

---

### 💳 Payment Method vs. Churn
| Payment Method          | % of Customers | Churn Rate |
|-------------------------|----------------|------------|
| Electronic Check        | 33.6%          | **45.3%**  |
| Mailed Check            | 22.9%          | 19.1%      |
| Bank Transfer (Auto)    | 21.9%          | 16.7%      |
| Credit Card (Auto)      | 21.6%          | **15.2%**  |

> ⚠️ Electronic Check users churn **~3× more** than auto-pay customers.

---

## 📈 Charts Created

| # | Chart Type         | Variable           | Key Insight                                         |
|---|--------------------|--------------------|-----------------------------------------------------|
| 1 | Count Plot         | Churn              | 5,174 retained vs. 1,869 churned                   |
| 2 | Pie Chart          | Churn              | 26.54% churn rate visualised                        |
| 3 | Count Plot         | Gender × Churn     | No gender-based difference                          |
| 4 | Count Plot         | SeniorCitizen      | 16.2% of base are seniors                           |
| 5 | Stacked Bar        | SeniorCitizen × Churn | 41.7% senior churn rate                          |
| 6 | Histogram          | Tenure × Churn     | Early customers churn most                          |
| 7 | Count Plot         | Contract × Churn   | M2M dominates churn                                 |
| 8 | 3×3 Grid           | 9 Services × Churn | Low add-on adoption; add-ons reduce churn           |
| 9 | Count Plot         | PaymentMethod × Churn | Electronic Check highest churn                  |

---

## 🧠 High-Risk Customer Profiles

Based on combined factors, customers most likely to churn:

- 🔴 **New month-to-month customers** (tenure < 12 months) + Electronic Check → est. churn risk **> 55%**
- 🔴 **Senior citizens** on month-to-month contracts → compounded risk from both factors
- 🔴 **Fiber Optic users** with no protective add-on services → churn approaches **45%+**
- 🟡 **Customers with no partner, no dependents, and no add-ons** → lower ecosystem stickiness

---

## 💡 Recommendations

| Priority | Action | Target Segment |
|----------|--------|----------------|
| 🔴 P1 | 90-day onboarding campaign with loyalty discounts | New customers (tenure < 3 months) |
| 🔴 P1 | Incentivise contract upgrades (bill credits, free months) | Month-to-Month holders (55% of base) |
| 🟡 P2 | Auto-pay enrollment campaign with small monthly discount | Electronic Check users (33.6% of base) |
| 🟡 P2 | Senior Care programme with dedicated support | Senior Citizens (16.2% of base) |
| 🟢 P3 | Free 3-month trial of Online Security + Tech Support | Customers without add-ons |
| 🟢 P3 | Investigate Fiber Optic pricing & service quality | Fiber Optic subscribers (41.9% churn) |
| 🟢 P4 | Build a predictive churn ML model | All segments |

---

## 📌 Key Takeaways

1. **26.54%** of customers have churned — roughly 1 in 4
2. **Contract type** is the single strongest churn driver (15× gap: M2M vs 2-year)
3. **Early tenure** is the most vulnerable window — 47.7% churn in first year
4. **Electronic Check** users churn 3× more than auto-pay customers
5. **Add-on services** significantly reduce churn — creating service stickiness
6. **Gender** has negligible impact on churn — not a useful segmentation variable

---

## 🚀 How to Run

```bash
# 1. Clone the repository
git clone https://github.com/your-username/Telecom-Customer-Churn-Analysis.git
cd Telecom-Customer-Churn-Analysis

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# 3. Launch Jupyter Notebook
jupyter notebook TCA.ipynb
```

---

## 📋 Requirements

```
pandas
numpy
matplotlib
seaborn
jupyter
```

---

## 🔮 Future Work

- [ ] Build a **Machine Learning classification model** (Logistic Regression, Random Forest, XGBoost) to predict churn probability per customer
- [ ] Feature engineering — create interaction features (e.g., tenure × contract type)
- [ ] Deploy a **churn risk dashboard** using Streamlit or Power BI
- [ ] Perform statistical significance testing on all churn factors

---

## 👤 Author

**Harsh Jagdale**
- GitHub: [@Harsh-J17](https://github.com/Harsh-J17)
- LinkedIn: [Harsh Jagdale](https://www.linkedin.com/in/harsh-jagdale-b37635332)

---

> ⭐ If you found this project helpful, please give it a star on GitHub!
