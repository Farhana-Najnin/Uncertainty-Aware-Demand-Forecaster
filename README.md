# 📦 Uncertainty-Aware Retail Demand Forecaster 🚀

This repository contains the **updated and extended version** of my earlier project:

🔗 **Previous Project (Baseline Version):**  
https://github.com/Farhana-Najnin/Retail-Demand-Forecaster

The original project focused on **point demand forecasting**.  
This version extends that work by **explicitly modeling forecast uncertainty and translating predictions into inventory decisions and cost outcomes**.

---

## 🧠 High-Level Idea

Demand forecasting is only valuable when it supports **real business decisions**.

This project demonstrates a complete, decision-oriented pipeline that:
1. Forecasts future demand with **uncertainty**
2. Converts forecasts into **inventory ordering decisions**
3. Simulates realistic inventory behavior
4. Evaluates outcomes using **business cost metrics**, not accuracy alone

---

## 🔄 What Changed From the Previous Project

| Aspect | Previous Project | This Project |
|------|-----------------|-------------|
| Forecast Output | Single point forecast | **P50 & P90 uncertainty-aware forecasts** |
| Uncertainty Modeling | Not included | **Explicit percentile-based uncertainty** |
| Business Layer | Not modeled | **Inventory simulation with costs** |
| Evaluation | MAE only | **MAE + cost-based metrics** |
| Interface | Script-based | **Interactive Streamlit dashboard** |
| Sharing | Local execution | **Temporary public demo via ngrok** |

---

## 🧩 How the System Works (End-to-End)

### 1️⃣ Time-Series Forecasting

**Model Used:** Prophet

Prophet is used to model historical retail demand because it:
- Handles trend and seasonality
- Is designed for business time-series data
- Provides prediction intervals needed for uncertainty modeling

Each **store–product combination** is treated as an independent time series.

---

### 2️⃣ Forecast Uncertainty (P50 & P90)

From Prophet’s predictive distribution, two forecasts are extracted:

- **P50 (50th percentile)**  
  Median forecast representing a balanced estimate of future demand.

- **P90 (90th percentile)**  
  Conservative forecast representing higher potential demand to reduce stock-out risk.

These forecasts are **used directly as inventory ordering signals**, not just plotted.

---

### 3️⃣ Inventory Simulation Engine

A custom inventory simulation module models:
- Daily demand fulfillment
- Lead time between ordering and receiving stock
- Inventory on hand and pipeline inventory

**Costs calculated:**
- Holding cost
- Stock-out cost
- Total operational cost
- Stock-out event count

This makes the impact of forecasting decisions measurable.

---

### 4️⃣ Decision Comparison: P50 vs P90

Inventory simulations are run separately using:
- P50-based ordering
- P90-based ordering

This allows direct comparison of:
- Cost efficiency vs service level
- Conservative vs balanced strategies
- Risk–cost trade-offs

---

### 5️⃣ Evaluation Metrics

The system evaluates performance using:
- Mean Absolute Error (MAE)
- Holding cost
- Stock-out cost
- Total cost
- Stock-out events

This ensures evaluation is **decision-aware**, not purely statistical.

---

## 🖥️ Interactive Streamlit Dashboard

An interactive **Streamlit dashboard** allows users to:
- Adjust forecast horizon
- Configure inventory parameters (lead time, holding cost, stock-out cost)
- Switch between P50 and P90 ordering policies
- Visualize forecasts and inventory KPIs in real time

Streamlit was chosen for rapid experimentation and interpretability.

---

## 🔄 How the Streamlit App Handles Requests (No GET/POST APIs)

This project does **not** use a traditional REST API.  
There are **no manually defined HTTP GET or POST endpoints**.

Streamlit follows a **script re-execution model**:

- When a user opens the app:
  - The browser sends a standard HTTP GET request
  - Streamlit executes `app.py` from top to bottom

- When a user interacts with UI widgets:
  - Streamlit captures the new values
  - Automatically **re-runs the entire script**
  - Updates charts and metrics

All HTTP handling is managed internally by Streamlit.

---

### 📥 Data Loading & Caching

- Retail data is loaded using **Hugging Face Datasets**
- Converted to Pandas DataFrames
- Cached using `@st.cache_data` to avoid repeated downloads

Model artifacts are cached using `@st.cache_resource` to prevent reloads during UI interactions.

---

## 🌐 Public Demo (Temporary)

The Streamlit app runs locally on port `8501`.  
**ngrok** is used to expose it via a secure, temporary public URL.

🔗 **Live Demo (temporary):**  
👉 https://endurable-thwartedly-somer.ngrok-free.dev

⚠️ The URL is session-based and will expire when the runtime stops.

---

## 🏗️ Application Flow
User Browser
→
ngrok Public URL
→
ngrok Tunnel
→
Streamlit Server (localhost:8501)
→
Forecasting + Inventory Simulation



---

## 📊 Dataset Used

**Dataset:** `t4tiana/store-sales-time-series-forecasting`  
**Source:** Hugging Face Datasets

The dataset contains daily retail sales across multiple stores and product families.

---

## 🛠️ Tech Stack

- Python
- Prophet
- Pandas, NumPy
- Scikit-learn
- Matplotlib
- Streamlit
- ngrok
- Hugging Face Datasets

---

## 🎯 Who This Project Is For

- Retail & supply-chain analysts
- Data scientists interested in decision-aware ML
- Learners exploring uncertainty in forecasting

---

## 📌 Key Takeaway

> Accurate forecasts are useful.  
> **Uncertainty-aware forecasts drive better decisions.**

This project demonstrates how modeling uncertainty leads to more informed and realistic inventory planning.

---
