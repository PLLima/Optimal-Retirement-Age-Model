# Retirement-Modelisation
Trying to push the state of the art of retirement age and capital models!

## 1. Project Overview
This project models the dynamic evolution of a country's population age structure and analyzes the fiscal sustainability of a **Pay-As-You-Go (PAYG)** pension scheme.

Based on the theoretical framework of **Hock and Weil (2012)**, we implement a continuous-time dynamical system (ODE) that captures the feedback loop between:
1.  **Demographic Aging:** Rising life expectancy and changing retirement ratios.
2.  **Economic Burden:** Increased tax rates required to fund pensions.
3.  **Endogenous Fertility:** How higher taxes reduce disposable income, leading to lower fertility rates and further aging (a "demographic death spiral").

The model is calibrated using demographic data approximating **Austria** (TFR $\approx$ 1.5) to simulate realistic "Low Fertility Trap" scenarios.

## 2. Theoretical Framework (Part I)
The core simulation relies on a system of Ordinary Differential Equations (ODEs) representing three population stocks:
* **$A_Y(t)$**: Youth Dependents (0–20 years)
* **$A_M(t)$**: Working-Age Population (20–65 years)
* **$A_O(t)$**: Retirees (65+ years)

### Key Mechanisms
* **McKendrick-Von Foerster Transitions:** Flows between cohorts are modeled using probabilistic transition rates ($\lambda = 1/T$).
* **Fiscal Feedback:** The tax rate $\tau(t)$ adjusts instantly to balance the pension budget based on the dependency ratio.
* **Fertility Response:** The fertility rate $n(t)$ is endogenous, calculated as:
    $$n(t) = \psi (1 - \tau(t))$$
    where $\psi$ represents cultural preferences and child-rearing costs.

## 3. Repository Structure
The simulation is built in **MATLAB** using modular **Live Functions (.mlx)**.

| File Name | Description |
| :--- | :--- |
| **`run_analysis.mlx`** | **MAIN DRIVER.** Open and run this file to execute the full simulation and generate all figures (Population Stocks, Ratios, Tax/Fertility). |
| `get_parameters.mlx` | Configuration file containing all model parameters (Demographic durations, Economic policy $\alpha, \beta$, and calibrated Fertility $\theta, \xi$). |
| `model_dynamics.mlx` | The mathematical engine. Contains the ODE definitions and the algebraic feedback loops (Tax $\to$ Fertility). |
| `visualize_results.mlx` | Plotting utility to generate standardized figures for reports. |
| `stability_analysis.mlx` | **Analytical Script.** Performs Jacobian matrix analysis and generates Phase Plane plots to prove the stability of equilibrium points. Also, it forces the model into a "Zero Growth" state to verify mass conservation and replacement level calibration. |

## 4. How to Run the Simulation
**Prerequisites:** MATLAB R2023a or later (for Live Script compatibility).

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/PLLima/Optimal-Retirement-Age-Model.git
    ```
2.  **Open MATLAB.**
3.  **Run the Main Simulation:**
    * Open `run_analysis.mlx`.
    * Click the **"Run All"** button in the Live Editor tab.
    * *Output:* Interactive figures showing 150-year projections of population and tax rates.
4.  **Run Stability Analysis:**
    * Open `stability_analysis.mlx`.
    * Click **"Run All"**.
    * *Output:* Calculated Eigenvalues and a Phase Plane vector field plot confirming the stability node.

## 5. Numerical Experiments & Results
This simulator allows for the testing of various demographic scenarios. The default configuration (`run_analysis.mlx`) runs **Experiment 3**.

| Exp | Scenario | Key Parameters | Outcome |
| :--- | :--- | :--- | :--- |
| **1** | **Population Explosion** | $\psi \approx 0.04$ ($n > \lambda_M$) | Exponential growth ($10^{15}$), unstable demographic path. |
| **2** | **Stationary State** | Tuned $\theta$ so $n = \lambda_M$ | Perfect Zero Growth. Ratios and Stocks stabilize. |
| **3** | **Low Fertility Trap** | $\theta = 0.057$ (Austria TFR $\approx$ 1.5) | Declining population, Tax Rate $\tau$ stabilizes at high equilibrium (~23%), Fertility remains below replacement. |

## 6. Assumptions & Limitations
* **Unisex Model:** The model uses a "representative agent" and births per worker, abstracting from gender ratios.
* **Balanced Budget:** We assume the government cannot borrow; pension deficits must be covered immediately by tax increases.
* **Inelastic Labor:** All working-age individuals are assumed to be employed (no unemployment modeled).
* **Closed Economy:** Migration is disabled by default (though implemented in the code logic).

## 7. References
1.  **Hock, H., & Weil, D. N. (2012).** *On the dynamics of the age structure, dependency, and consumption.* Journal of Population Economics, 25(3), 1019-1043.
2.  **Hock, H., & Weil, D. N. (2007).** Modeling the effects of population aging on consumption in the presence of intergenerational transfers. In R. Clark, N. Ogawa, & A. Mason (Eds.), *Population Aging, Intergenerational Transfers and the Macroeconomy* (pp. 101-127). Edward Elgar Publishing.
3.  **Feichtinger, G., Prskawetz, A., & Veliov, V. M. (2004).** *Age-structured optimal control in population economics.* Theoretical Population Biology, 65(4), 373-387.
