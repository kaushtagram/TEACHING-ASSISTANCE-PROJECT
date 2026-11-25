# TEACHING-ASSISTANCE-PROJECT
TEACHING ASSISTANCE PROJECT
# Teaching Assistant Performance Prediction

A machine learning classification project that analyses teaching-assistant evaluation data and predicts performance categories: **Low, Medium, or High**.

## Project Overview

This project explores a dataset of teaching-assistant assignments from the Statistics Department at the University of Wisconsin–Madison.

The objective is to understand the relationship between assignment characteristics and teaching-assistant performance, perform exploratory data analysis (EDA), and develop classification models to predict the performance category.

The project covers data quality assessment, preprocessing, model development, hyperparameter tuning, model comparison, and group-aware nested cross-validation.

## Dataset Description

The dataset contains **151 observations** and five input features.

| Feature | Description |
|---|---|
| ENGLISH SPEAKER | Whether the teaching assistant is an English speaker |
| COURSE INSTRUCTOR | Course instructor identifier |
| COURSE | Course identifier |
| SUMMER/REGULAR SEMSTER | Semester type: Summer or Regular |
| CLASS SIZE | Number of participants in the class |

**Target variable: `CLASS ATTRIBUTE`**

| Class | Meaning |
|---|---|
| 1 | Low |
| 2 | Medium |
| 3 | High |

### Target Distribution

- Low: 49 observations
- Medium: 50 observations
- High: 52 observations

The target classes are approximately balanced.

## Exploratory Data Analysis

The initial analysis examined the distribution of the target variable, categorical feature frequencies, class size, and relationships between the available predictors and the target.

Key data-quality findings:

- No missing values were identified in the supplied columns.
- 41 repeated occurrences of complete rows were identified.
- Four distinct input combinations had conflicting target labels, involving 12 observations.
- Several course categories had very few observations.
- Class size alone did not show a strong relationship with the target class.

The project retained the original dataset for its primary nested cross-validation comparison and examined duplicate removal separately as a sensitivity analysis.

## Data Preprocessing

The following preprocessing techniques were used:

- **One-Hot Encoding:** Converted categorical features into numerical representations.
- **StandardScaler:** Scaled the numerical class-size feature.
- **ColumnTransformer:** Applied different preprocessing steps to categorical and numerical columns.
- **Scikit-learn Pipelines:** Integrated preprocessing and model training to reduce data leakage.
- **Group-aware splitting:** Kept repeated input combinations together during cross-validation to prevent identical feature combinations from appearing in both training and validation folds.

## Machine Learning Models

The following classification algorithms were evaluated:

1. Logistic Regression
2. Decision Tree Classifier
3. Random Forest Classifier
4. Support Vector Machine (SVM)
5. Extra Trees Classifier
6. Gradient Boosting Classifier
7. K-Nearest Neighbours (KNN)

A **Dummy Classifier** was also used as a baseline to assess whether the machine learning models performed better than a simple prediction strategy.

## Model Evaluation

The project used:

- Accuracy
- Macro F1-score
- Class-wise precision and recall
- Confusion matrix
- Classification report

A group-aware nested cross-validation approach was used for the final comparison of the leading models.

### Nested Cross-Validation Results

| Model | Mean Accuracy | Mean Macro F1 |
|---|---:|---:|
| Logistic Regression | **0.426** | **0.425** |
| Random Forest | 0.395 | 0.375 |

Logistic Regression achieved the strongest results among the two models in the final nested comparison.

### Baseline Comparison

The pooled out-of-fold Dummy Classifier baseline achieved:

- Accuracy: 29.1%
- Macro F1-score: 0.228

The pooled out-of-fold Logistic Regression results were approximately:

- Accuracy: 42.4%
- Macro F1-score: 0.42

*Note: The pooled out-of-fold baseline and mean nested cross-validation results use different aggregation methods and should not be interpreted as perfectly like-for-like estimates.*

## Key Findings

- Logistic Regression was the leading candidate in the final nested model comparison.
- The model performed better than the Dummy Classifier baseline.
- Predictive performance remained modest across the three classes.
- The Medium performance category was particularly difficult to identify reliably.
- Repeated observations, conflicting labels, and sparse categorical levels limited the information available for model training.

## Challenges and Limitations

**1. Small dataset**

The dataset contains only 151 observations, limiting the ability of models to generalise to new teaching-assistant assignments.

**2. Repeated observations**

The dataset contains 41 repeated occurrences of complete rows. Their provenance is unknown, so they cannot automatically be treated as data-entry errors.

**3. Conflicting labels**

Twelve observations belong to four input combinations that have different target labels. This suggests that the available features may not capture all the factors influencing the target.

**4. Sparse categories**

Some courses and instructor categories have limited observations, making reliable predictions for those categories difficult.

**5. Moderate predictive performance**

The best model achieved a mean nested-CV accuracy of 42.6%. This is not sufficient to support high-confidence individual predictions.

**6. Feature suitability and fairness**

English-speaker status is included as a predictor. Its appropriateness and potential fairness implications would need to be assessed before any consequential real-world use.

## Technology Stack

- Python
- Jupyter Notebook / Google Colab
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn

## Project Structure

```text
Teaching-Assistance-Performance-Prediction/
│
├── README.md
├── TEACHING_ASSISTANCE_PROJECT.ipynb
└── dataset/
    └── teaching_assistance.csv
```

*The structure above is a suggested GitHub layout. Update the notebook and dataset filenames to match the files you actually upload.*

## How to Run the Project

1. Clone or download this repository.
2. Open the Jupyter Notebook in Google Colab or a local Jupyter environment.
3. Upload the dataset and configure the notebook's dataset path.
4. Install the required Python libraries if they are not already available.
5. Execute the notebook cells in sequence to reproduce the analysis and model evaluation.

## Conclusion

This project demonstrates an end-to-end machine learning classification workflow, from exploratory data analysis and data preprocessing to model comparison and nested cross-validation.

Logistic Regression emerged as the preferred experimental model among the leading candidates evaluated. However, the results highlight the importance of dataset quality, sample size, feature availability, and robust validation.

Further data collection, investigation of conflicting labels, and independent validation are necessary before considering real-world deployment.

**Project Status:** Completed as an academic capstone project. Not recommended for production deployment in its current form.
