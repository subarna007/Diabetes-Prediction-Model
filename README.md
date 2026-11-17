# Diabetes prediction (Pima Indians dataset)

Predicting whether a patient has diabetes from eight routine clinical measurements, with logistic regression and a support vector machine.

## Data

`diabetes.csv` is the Pima Indians Diabetes dataset (768 women, 268 with diabetes), from Kaggle. Features: pregnancies, glucose, blood pressure, skin thickness, insulin, BMI, diabetes pedigree function and age.

Several columns use 0 for missing values (for example a blood pressure of 0). In both notebooks, zeros in glucose, blood pressure, skin thickness, insulin and BMI are replaced by the column median.

## Method

- 80/20 train/test split (`random_state=1`, 154 test patients)
- `Diabeties Prediction Model.ipynb`: logistic regression with 5-fold cross-validated regularisation (`LogisticRegressionCV`), plus a correlation heatmap and confusion matrix
- `SVM.ipynb`: support vector machine (RBF kernel, default settings)

## Results (test set, 154 patients)

| Model | Accuracy | Sensitivity for diabetes | F1 for diabetes |
|---|---|---|---|
| Logistic regression | 76% | 55% (30 of 55) | 0.62 |
| SVM (RBF) | 79.2% | 51% (28 of 55) | 0.64 |

Both models miss about half of the patients with diabetes. Accuracy looks reasonable mainly because two thirds of the patients do not have diabetes.

## What I would do differently

- Report sensitivity and F1 for the diabetes class as the main metrics, not accuracy.
- Scale the features before the SVM and tune its parameters with cross-validation.
- Choose a decision threshold that catches more diabetic patients, since a missed diagnosis costs more than a false alarm.
- Fit the median imputation on the training set only, so no information from the test set leaks into training.

## Run

```bash
pip install -r requirements.txt
jupyter notebook
```
