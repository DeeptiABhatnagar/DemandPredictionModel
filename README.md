# DemandPredictionModel
Determine how to optimize pricing by constructing and solving an optimization model

---
# **Dynamic Pricing Optimization for Amusement Park Souvenir**  
### *Demand Modeling • Price Ladder Optimization • Gurobi MILP • Seasonal Forecasting*

---

## **Project Overview**

This repository implements a **dynamic pricing optimization model** for a year‑round souvenir sold at a major amusement park. Using three years of historical weekly price and sales data, the project develops:

- A **linear additive demand prediction model**  
- A **mixed‑integer optimization model** using Gurobi  
- A **discrete price ladder** business rule  
- A **revenue‑maximizing pricing policy** for Weeks 157–164  
- A **visualization of optimal weekly prices**

The workflow mirrors the *Analytics Edge of Retail Optimization* framework as provided.

---

## **1. Demand Model**

The demand model is a linear regression incorporating:

- Current price  
- Lagged prices (1‑week and 2‑week lags)  
- Seasonal dummy variables (13 seasons × 4 weeks each)

$$
d_t = 1.978242858 
- 2.809634145\,p_t 
+ 0.963410728\,p_{t-1} 
+ 0.759639170\,p_{t-2}
+ \sum_{s=2}^{13} \beta_s \cdot \text{Season}_s
$$

This structure captures:

- **Price elasticity**  
- **Consumer memory**  
- **Seasonal demand shifts**

---

## **2. Price Ladder Constraint**

Prices must be selected from a **six‑level discrete ladder**:

| Level | Price |
|-------|--------|
| 1 | 1.00 |
| 2 | 0.95 |
| 3 | 0.85 |
| 4 | 0.75 |
| 5 | 0.60 |
| 6 | 0.50 |

Binary variables $(x_{t,k})$ enforce:

$$
\sum_k x_{t,k} = 1, \quad p_t = \sum_k k \cdot x_{t,k}
$$

---

## **3. Optimization Model**

### **Objective Function**

Maximize revenue over Weeks 157–164:

$$
\max \sum_{t=157}^{164} p_t \cdot d_t
$$

### **Decision Variables**

- $(p_t)$: continuous price  
- $(x_{t,k})$: binary ladder selector  

### **Constraints**

- Exactly one ladder price per week  
- Price definition constraint  
- Demand defined by regression model  

---

## **4. Implementation**

The notebook includes:

- Gurobi model construction  
- Demand expression builder  
- Objective function assembly  
- Ladder constraints  
- Optimization and solution extraction  
- Plotly visualization of optimal prices  

---

## **5. Outputs**

- Optimal weekly prices (Weeks 157–164)  
- Revenue‑maximizing price path plot  
- DataFrame of selected prices  
- Academic analysis of model effectiveness  

---

## **6. Repository Structure**

```
├── notebook.ipynb
├── README.md
├── data/
│   └── historical_prices_sales.csv (optional)
└── plots/
    └── optimal_prices.png
```

---

## **7. Requirements**

- Python 3.10+  
- Gurobi + gurobipy  
- NumPy, Pandas, Plotly  

---

## **8. Academic Context**

This project demonstrates:

- Mixed‑integer optimization for pricing  
- Integration of econometric demand models  
- Seasonal forecasting  
- Business rule enforcement  
- Revenue maximization under constraints  
