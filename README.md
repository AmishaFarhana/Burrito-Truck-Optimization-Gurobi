# 🌯 Burrito Truck Optimization – Gurobi

Optimization project modeling optimal food truck deployment to maximize profit while fully serving customer demand.

Built using **Python + Gurobi**, this project formulates and solves a binary integer programming model under multiple cost scenarios.

---

## 📌 Problem Overview

We determine:

- Which truck locations to open  
- Which truck serves each demand node  
- How to maximize total profit  

Profit is defined as:
Total Revenue – Truck Setup Costs


Where:

- Revenue = (Price – Ingredient Cost) × Burritos Served  
- Truck setup cost is fixed per truck  

---

## 📊 Dataset Structure

Four input files were used:

### 1️⃣ Demand Node Data
- Customer locations
- Coordinates (X, Y)
- Burrito demand per location

### 2️⃣ Truck Node Data
- Potential truck deployment locations
- Coordinates (X, Y)

### 3️⃣ Demand–Truck Feasibility Data
- Distance between truck and demand node
- Scaled demand (how many burritos a truck can serve at a node)
- Only positive scaled demand pairs are considered feasible

### 4️⃣ Problem Parameters
- Burrito price
- Ingredient cost
- Fixed truck setup cost

---

## 🧠 Optimization Model

### Decision Variables

- **zᵢ** → 1 if truck i is opened, 0 otherwise  
- **xᵢⱼ** → 1 if truck i serves demand node j  

All variables are binary.

---

### Objective Function

Maximize:
Σ (profit_per_burrito × scaled_demandᵢⱼ × xᵢⱼ)
− Σ (truck_cost × zᵢ)


---

### Constraints

1️⃣ Each demand node must be served exactly once:
Σ xᵢⱼ = 1


2️⃣ Truck activation constraint:
xᵢⱼ ≤ zᵢ


A truck must be open if it serves any demand node.

---

## ⚙️ Implementation

Built in Python using:

- `pandas`
- `gurobipy`
- `GRB`
- `quicksum`

Key modeling steps:

- Filter only feasible truck-demand pairs (scaled_demand > 0)
- Build binary decision variables only for valid pairs
- Add assignment and activation constraints
- Maximize profit
- Solve using Gurobi optimizer

---

# 📈 Scenario Analysis

We tested five pricing scenarios to analyze sensitivity to ingredient cost changes.

---

## 🟢 Case 1 – Base Case

- Burrito price: $10  
- Ingredient cost: $5  
- Profit per burrito: $5  
- Truck cost: $250  

Break-even:  
50 burritos per truck required  

**Optimal Result:**
- 6 trucks opened  
- Optimal profit: **$3,710**

---

## 🟡 Case 2 – Supply Chain Issue

- Ingredient cost increases to $7  
- Profit per burrito: $3  

Break-even:  
~84 burritos per truck  

**Optimal Result:**
- 5 trucks opened  
- Optimal profit: **$1,714**

---

## 🟢 Case 3 – Cost Reduction Strategy

- Ingredient cost reduced to $4  
- Profit per burrito: $6  

Break-even:  
~42 burritos per truck  

**Optimal Result:**
- 6 trucks opened  
- Optimal profit spikes to **$4,752**

Observation:  
Truck assignments remained largely stable; profit increased due to margin expansion.

---

## 🔴 Case 4 – Near Break-Even Crisis

- Ingredient cost: $9  
- Profit per burrito: $1  

Break-even:  
250 burritos per truck  

**Optimal Result:**
- Only 3 trucks opened  
- Minimal profit: **$27**

Model strategically reduces truck count to limit fixed costs.

---

## 🔴 Case 5 – Loss Scenario

- Ingredient cost: $9.1  
- Profit per burrito: $0.99  

**Optimal Result:**
- 3 trucks opened  
- Loss: **$50**

Model minimizes losses by reducing operational footprint.

---

# 📊 Key Insights

### Break-Even Dynamics

| Profit per Burrito | Burritos Needed to Break Even |
|--------------------|-------------------------------|
| $5                 | 50                            |
| $3                 | 84                            |
| $1                 | 250                           |

Higher ingredient costs significantly increase required demand per truck.

---

### Operational Sensitivity

- Small increases in ingredient cost drastically reduce profit
- Truck count adjusts dynamically to maintain viability
- Cost reduction strategies increase profit but may not change deployment structure

---

# 💡 Business Recommendations

- Explore lower-cost truck models (e.g., $150 setup cost)
- Introduce value meals to increase volume
- Consider nonlinear demand effects (kids meals boosting demand)
- Conduct simulation analysis before operational changes

---

# 🛠 Technologies Used

- Python  
- Gurobi Optimizer  
- Pandas  
- Binary Integer Programming  

---

# 🎯 Skills Demonstrated

- Mixed-Integer Linear Programming (MILP)
- Constraint modeling
- Binary assignment problems
- Scenario analysis
- Sensitivity analysis
- Profit optimization under cost uncertainty
- Operational decision modeling

---

# 🚀 Project Outcome

Successfully formulated and solved a real-world location-allocation optimization problem using Gurobi, incorporating:

- Feasibility filtering  
- Profit maximization  
- Scenario-based decision support  
- Strategic operational insights  

This project demonstrates applied optimization modeling for real business decisions.
