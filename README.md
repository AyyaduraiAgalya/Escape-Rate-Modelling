# Escape Rate in Expanding Maps  

**Course:** Financial Data Science
**Module:** Data Driven Methods
**Result:** 100/100 — *"A brilliant piece of work,"* — Professor's comment
**Tools:** Python, NumPy, Matplotlib, SVD, Linear Regression  

---

## Overview  

This project explores how points “escape” from an expanding map of the unit interval — a classic problem in dynamical systems and chaos theory.  

The system is defined by the one-parameter family of maps:  

\[
f_\beta(x) = \{\beta x\}, \quad \beta > 1
\]

where \(\{x\}\) denotes the fractional part of \(x\).  
For a given hole \(H(c, h)\) inside the interval \((0, 1)\), the **escape rate** quantifies how quickly orbits fall into that hole under repeated iterations of the map.  

---

## Objective  

To numerically and statistically **model the escape rate function**:  

\[
r_{\beta, c, h}(t)
\]

and study how it depends on the parameters \(\beta\), \(c\), and \(h\).  

---

## Methods  

### 1. Numerical Simulation  
- Simulated orbits of \( N = 10^4 \) random initial points under \( f_\beta(x) \).  
- Measured how many points remained in \((0, 1)\) after \(t\) iterations to compute \(r_{\beta, c, h}(t)\).  

### 2. Polynomial (Gaussian) Approximation  
- Applied **polynomial regression** (degree ≤ 5) to approximate \(r_{\beta, c, h}(t)\).  
- Implemented least-squares fitting using **normal equations** and **SVD** (`numpy.linalg.svd`).  

### 3. Linear Regression (Log Scale)  
- Modelled \(\log(r_{\beta, c, h}(t)) = A + Bt\).  
- Estimated the **escape rate** \(B\) as the slope of the fitted line.  
- Compared Gaussian and linear fits to evaluate approximation error.  

### 4. Parameter Experiments  
- Varied \(\beta\), \(c\), and \(h\) to observe how escape behaviour changes with the position and size of the hole.  
- Visualized how \(B(c)\) (escape rate vs hole position) evolves across multiple random configurations.  

---

## ⚡ Floating-Point Precision Insight  

In **Exercise 6.2.3**, for parameters β = 2, c = 0.5, h = 10⁴, a surprising behaviour appeared:  
a sudden drop where nearly all points escaped between the **40th – 60th** iteration — precisely around the **52nd**.  

### Why this happens  

- Computers store floating-point numbers using **64 bits**, of which **52 bits** represent the fractional part (mantissa).  
- Doubling a number (β = 2) shifts its binary representation left by one bit.  
- Each iteration removes the integer part (`{x} = x − [x]`), leaving only the fractional remainder.  
- By the 52nd iteration, the mantissa is filled and precision is lost — the binary fraction becomes roughly `0.100000...`, which equals **0.5** in decimal.  
- Since the hole is centred at 0.5, all points suddenly “escape.”  
- Moving the hole elsewhere prevents escapes because subsequent iterations collapse the binary fraction to 0.  

### Fix  
Using **rational numbers** instead of floating-point numbers preserves exact fractional values and avoids this loss of precision.  

This demonstrates how subtle numerical precision limits can create deterministic-looking behaviour in otherwise chaotic systems.  

---

## Results  

- Successfully captured **exponential decay** of \(r_{\beta, c, h}(t)\) and validated the escape rate model.  
- Observed strong dependence of escape rate on hole position \(c\).  
- Revealed precision-related artefacts for β = 2 and explained them mathematically.  
- Implementations using both **normal equations** and **SVD** produced stable and consistent fits with minimal error.  

---

## Key Concepts Illustrated  

- Chaotic maps & deterministic randomness  
- Overdetermined systems  
- Polynomial regression  
- Normal equations vs Singular Value Decomposition  
- Floating-point precision limits  
- Numerical modelling of dynamical systems  

---

## Highlight  

This project was awarded **100/100** and commended by the professor as:  
> “A brilliant piece of work.”  

It demonstrates how mathematical theory, numerical simulation, and statistical regression can work together to reveal structure in chaotic systems.

---

## How to Run  

### Clone the repository
git clone https://github.com/ayyaduraiagalya/Escape-Rate-Modelling.git
cd Escape-Rate-Modelling

### Install Jupyter Notebook (if not already installed)
pip install notebook

## Launch Jupyter Notebook
jupyter notebook

---

## Author  

**Agalya Ayyadurai**  
MSc Financial Data Science, University of Surrey  
[https://www.linkedin.com/in/agalya-ayyadurai-286517172/]
