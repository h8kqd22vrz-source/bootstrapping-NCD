# bootstrapping-NCD

## Project Overview
This project implements a quantitative bootstrapping algorithm to construct a **Zero Coupon Yield Curve** from raw market data. It replicates and automates a traditional Excel-based workflow commonly used in South African banking (NCDs and Par Swaps).

## Key Features
* **Dual-Method Discounting:** Handles both Short-End (Simple Interest < 1 Year) and Long-End (NACS/Par Bond > 1 Year) instruments.
* **Automated Interpolation:** Uses `scipy.interpolate` to solve for missing liquid pillars (e.g., 18-month or 30-month gaps) in the term structure.
* **Convexity Correction:** Converts Par Yields to Zero Rates and Discount Factors (DF) to ensure arbitrage-free pricing.
* **Visualization:** Automatically plots the Term Structure of Interest Rates (Yield vs. Zero Curve).

## Technical Implementation
* **Language:** Python 3.10+
* **Libraries:** `Pandas` (Data Manipulation), `NumPy` (Vectorized Calculations), `SciPy` (Linear Interpolation), `Matplotlib` (Visualization).
* **Logic:**
    1.  **Data Ingestion:** Reads raw market rates (Deposit, NCD, Swap).
    2.  **Short-End Pricing:** Calculates DFs using $DF = \frac{1}{1 + r \times t}$.
    3.  **Long-End Bootstrapping:** Solves for DFs iteratively using the Par Bond formula: $1 = \sum (C \times DF_i) + 1 \times DF_T$.
    4.  **Zero Rate Extraction:** Converts DFs to continuous zero rates via $r = -\frac{\ln(DF)}{T}$.

## Why Python over Excel?
* **Auditability:** The bootstrapping logic is explicit in code, reducing the "key person risk" associated with complex, hidden Excel formulas.
* **Flexibility:** Allows for easy switching of interpolation methods (Linear vs. Cubic Spline) without restructuring the entire model.

## Usage
```python
# Load the notebook
jupyter notebook Yield_Curve_Bootstrap.ipynb
