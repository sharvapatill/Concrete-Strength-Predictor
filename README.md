# Concrete Compressive Strength Predictor

**Author:** Sharva Nitin Patil

A data model that predicts the compressive strength of a concrete mixture from its raw
material composition, built for ENGR 1330 (Computational Thinking and Data Science).

## Background

The compressive strength of concrete is normally measured with a crushing test on a concrete
cylinder, which requires a 28 day cure time before testing. That process is slow and labor
intensive, and mistakes in preparation can force the wait time to increase further. This
project uses a predictive data model instead: given the composition of a mixture, the model
estimates compressive strength directly, without a physical cure and crush cycle.

## What's in the notebook

`Concrete_Strength_Predictor.ipynb` covers:

- A short literature review on concrete mixture design and why a data model helps.
- Exploratory data analysis on the UCI Concrete Compressive Strength dataset (distribution
  of strength, strength vs. each raw material).
- A linear regression model trained to predict compressive strength from the eight mixture
  features (cement, blast furnace slag, fly ash, water, superplasticizer, coarse aggregate,
  fine aggregate, age).
- Model evaluation (RMSE, MAE, R-squared) and a coefficient plot showing which features drive
  strength the most.
- Projected strength for five candidate mixtures.
- An interactive prediction function that takes a mixture as input and returns an estimated
  strength.
- A function to append new observations to the dataset and retrain the model.

## Dataset

This project uses the UCI Machine Learning Repository's **Concrete Compressive Strength**
dataset (1,030 observations, 8 features), included in `data/Concrete_Data.xls`.

Original source: <https://archive.ics.uci.edu/ml/datasets/Concrete+Compressive+Strength>

Reference: I-Cheng Yeh, "Modeling of strength of high performance concrete using artificial
neural networks," *Cement and Concrete Research*, Vol. 28, No. 12, pp. 1797-1808 (1998).

## Setup

```
pip install -r requirements.txt
jupyter lab Concrete_Strength_Predictor.ipynb
```

The notebook already reads `data/Concrete_Data.xls`, so it runs top to bottom with no extra
setup.

## Results

A linear regression baseline achieves an R-squared of about 0.63 on held-out data (RMSE
around 9.8 MPa, MAE around 7.75 MPa). Water content and superplasticizer dose show the
strongest linear relationships with strength. Several features (notably age) show non-linear
relationships with strength in the scatter plots, so a tree-based or non-linear model is a
natural next step to improve on this baseline.

One of the five candidate mixtures (high cement content, 365-day age) falls outside the range
the model was trained on and produces an unrealistic prediction over 150 MPa. This is a known
limitation of linear regression: it extrapolates the same straight-line trend past the data it
was fit on. The notebook flags this directly rather than presenting the number at face value.

## Files

- `Concrete_Strength_Predictor.ipynb` — main analysis and model notebook, pre-run with output
- `data/Concrete_Data.xls` — the UCI dataset
- `requirements.txt` — Python dependencies
