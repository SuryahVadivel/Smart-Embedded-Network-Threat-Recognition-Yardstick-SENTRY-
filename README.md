# Project SENTRY: Smart Embedded Network Threat Recognition Yardstick 🛡️

**A Machine Learning-driven Intrusion Classification System for IoT Edge Devices.**

## 📖 Overview
The Internet of Things (IoT) landscape is exploding, but these resource-constrained devices often lack robust security. **Project SENTRY** is an Intrusion Detection System (IDS) designed to detect sophisticated cyberattacks on IoT networks.

Using the **RT-IoT2022 Benchmark Dataset**, we developed a model that balances high accuracy with the efficiency required for edge deployment. Our solution distinguishes between normal telemetry and 11 specific attack types, including rare threats like `NMAP_FIN_SCAN` and `Metasploit_SSH`.

## 📊 The Data
We utilized the **RT-IoT2022 Dataset** sourced from the UCI Machine Learning Repository.
* **Source:** Real-time IoT testbed (ThingSpeak-LED, MQTT-Temp, Wipro-Bulb).
* **Volume:** 123,117 Network Flows.
* **The Challenge:** Extreme Class Imbalance.
    * 76% of data was a single attack type (`DOS_SYN_Hping`).
    * Critical attacks like `NMAP_FIN_SCAN` represented < 0.02% of the data.

## 🛠️ Methodology
Our pipeline focused on **Feature Optimization** to reduce computational overhead for edge devices.

1.  **Data Cleaning:** Target-conditional median imputation and removal of zero-variance features.
2.  **Feature Engineering:** Created a custom **"Burstiness"** feature (`fwd_pkts_payload.tot / flow_duration`) to distinguish high-rate DoS attacks from normal traffic.
3.  **Dimensionality Reduction:**
    * Compared PCA (19 components) vs. Random Forest Feature Selection.
    * **Selected:** Top-25 Features via Random Forest Importance (retained interpretability).
4.  **Modeling:** Evaluated Logistic Regression, XGBoost, and Random Forest.

## 🏆 Key Results
We optimized for **Macro F1-Score** to ensure rare attacks were detected just as reliably as common ones.

| Model | Feature Set | Accuracy | Macro F1-Score | Detection of Rarest Attack (`NMAP_FIN`) |
| :--- | :--- | :--- | :--- | :--- |
| **Random Forest** | **Top 25 (Selected)** | **99.72%** | **0.973** | **0.91** |
| XGBoost | Top 25 | 99.76% | 0.958 | 0.71 |
| MLP (Neural Net) | Hybrid (PCA+Cat) | 98.8% | 0.930 | 0.77 |
| Logistic Regression | Top 25 | 98.0% | 0.810 | 0.34 |

**Conclusion:** The **Random Forest** model using only 25 features was the optimal solution. It outperformed Deep Learning (MLP) and Gradient Boosting (XGBoost) in robustness, achieving a **0.91 F1-score on the rarest attack class**, where other models faltered.

## 🚀 Usage
### Prerequisites
* Python 3.8+
* Jupyter Notebook

### Installation
1. Clone the repository:
   ```bash
   git clone [https://github.com/manoranjith-a/intrusion-classification-system.git](https://github.com/manoranjith-a/intrusion-classification-system.git)

2. Install dependencies:
`pip install -r requirements.txt`

### Running the Project
Open the Jupyter Notebook:
`jupyter notebook intrusion-classification-system.ipynb`
The notebook utilizes the ucimlrepo library to fetch the dataset directly. No manual data download is required.

### 👥 Team Members
1. Manoranjith Anandan
2. Melissa Cai Shi
3. Bakr Katkhuda
4. Kumar Rishu
5. Suryah Vadivel

### 📜 License & Acknowledgments
Dataset: RT-IoT2022 on UCI Machine Learning Repository.

Course: Advanced Machine Learning Capstone.
