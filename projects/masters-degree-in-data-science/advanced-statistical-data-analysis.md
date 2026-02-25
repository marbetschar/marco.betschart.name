---
title: Advanced Statistical Data Analysis
subtitle: Lecture Notes
subject: Advanced Regression Modelling
authors:
  - name: Andreas Ruckstuhl
    affiliation: ZHAW School of Engineering
---

# Review of Multiple Linear Regression

## Initial Remarks

Regression analysis is used to model the relationship between a response variable $Y$ and one or more explanatory variables $x^{(1)}, \dots, x^{(m)}$, where the relationship is masked by random noise.

### Objectives of Regression Analysis
1. General description of data structure.
2. Assessment of the effect of explanatory variables on the response.
3. Prediction of future observations.

:::{prf:definition} Multiple Linear Regression Model
:label: mlr-equation

The systematic relationship is explored via a function $f(\cdot)$:
$$Y_i = \beta_0 + \beta_1 x^{(1)}_i + \dots + \beta_m x^{(m)}_i + \mathcal{E}_i, \quad i = 1, \dots, n$$ (mlr-equation)

where $\mathcal{E}_i$ are unobservable random variables.
:::

:::{prf:remark}
In a **linear model**, the parameters enter linearly; the predictors themselves do not have to be linear. For example, $y \approx \beta_0 + \beta_1 x^{(1)} + \beta_2 \log(x^{(2)})$ is a linear model, but $y \approx \beta_0 + \beta_1 (x^{(1)})^{\beta_2}$ is not.
:::

### Error Assumptions
The standard assumptions for the error terms $\mathcal{E}_i$ are:
- Stochastically independent.
- Expectation zero and constant variance $\sigma^2$ (homoscedasticity).
- Normally (Gaussian) distributed: $\mathcal{E}_i \sim \mathcal{N}(0, \sigma^2)$.

## Matrix Representation

To simplify notation, the regression equation {eq}`mlr-equation` is written in matrix form:
$$\mathbf{Y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\mathcal{E}}$$

where:
- $\mathbf{Y}$ is an $n \times 1$ vector of responses.
- $\mathbf{X}$ is an $n \times p$ matrix of explanatory variables (including a column of 1s for the intercept).
- $\boldsymbol{\beta}$ is a $p \times 1$ vector of unknown coefficients ($p = m+1$).
- $\boldsymbol{\mathcal{E}}$ is an $n \times 1$ vector of unobserved random variables.

## Tukey's First-Aid Transformations

Standard recommendations used to linearize relationships and stabilize variance when there is no specific domain theory to guide variable transformation.
These should be applied to both explanatory variables and responses unless a valid reason exists to do otherwise:

| Data Type | Recommended Transformation                                                  |
| :--- |:----------------------------------------------------------------------------|
| **Concentrations and Amounts** | $\log(x)$                                                                   |
| **Count Data** | $\sqrt{x}$                                                                  |
| **Counted Fractions / Shares** | $\tilde{x} = \text{logit}(x) = \log\left(\frac{x + 0.005}{1.01 - x}\right)$ |

## Model Fitting and Diagnostics

### Least Squares Estimation
The coefficients $\boldsymbol{\beta}$ are estimated by minimizing the sum of squared residuals.

:::{prf:theorem} Gauss-Markov Theorem
:label: thm-gauss-markov
Under the assumptions of zero mean, constant variance, and uncorrelated errors, the Ordinary Least Squares (OLS) estimator is the **Best Linear Unbiased Estimator (BLUE)**.
:::

The OLS estimator is given by:
$$\hat{\boldsymbol{\beta}} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{Y}$$

### Model Adequacy (Residual Analysis)
Model adequacy is checked using diagnostic plots:
- **Tukey-Anscombe Plot:** Residuals vs. Fitted values to check for non-linearity or heteroscedasticity.
- **Normal Q-Q Plot:** To check the normality assumption of errors.
- **Scale-Location Plot:** To check for constant variance.
- **Residuals vs. Leverage:** To identify influential observations (Cook's Distance).
