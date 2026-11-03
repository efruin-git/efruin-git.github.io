### Overview
I wanted to practice some machine learning techniques.  I spent a lot of time in my previous job working on imaging and mammography data, so I thought a user friendly dataset on Kaggle with breast cancer risk factors would be a great source.  I performed multiple machine learning classification procedures, found the best model, and graphed results to interpret the model, using Scikit Learn, pandas, numpy, and matplotlib packages in Python.  The classification methods I used were K-Nearest Neighbors, Support Vector, and Random Forest.

### Data Sets Used
I used a synthetic dataset from Kaggle - [Breast Cancer Prediction Dataset](https://www.kaggle.com/datasets/mobeenfatimah/breast-cancer-prediction-dataset-10000-patient).  The dataset has demographic and health factor measures that can be used to predict whether a patient has breast cancer and the stage of the cancer.  The dataset was created for research purposes.

_From the source page:_

>Overview:  
>This dataset contains 10,000 synthetic patient records designed for machine learning, data science, and educational purposes.
>It includes demographic information, lifestyle factors, medical history, diagnostic findings, and a binary target variable indicating breast cancer diagnosis.
>
>
>Disclaimer:  
>This dataset is synthetically generated and intended solely for educational, research, and machine learning practice.
>It does not contain real patient information and must not be used for clinical diagnosis or medical decision-making.


### Data Preparation
I performed a few key steps to prepare the data for modeling - encoding categorical data, imputing values for missing data, and scaling the features.

Several fields contained categorical data - gender, family history of breast cancer, smoking indicator, alcohol consumption indicator, etc.  The classification models require numerical variables to run.  I used the ordinal encoder from the Scikit Learn and mapped unknown or missing values to -1, so the categorical variables were transformed into ordinal integers ranging from -1 to 5.  Most encoded variables had only two categories and no missing values, so they were encoded as 0's and 1's.

The BMI (body mass index) and tumor size variables were missing some values so I imputed the average from each field.  The K-Nearest Neighbors and Support Vector models required imputed values in order to run.  I tried the Random Forest model both with and without imputed values and got similar results.

After splitting the dataset into training and test sets I scaled the features using the Scikit Learn standard scaler.  There are a few different reasons why feature scaling matters.  One of the big reasons is that it prevents one feature from dominating the others because of larger values.  The feature of BMI generally has values in the 20's, while Age can range from 1 to 100.  Gender, family history of breast cancer, smoking indicator, and other categorical variables were encoded to integers near 0, so BMI and Age would have had disproportionate influence in the model if all the features were not scaled.

The original dataset contained 19 risk factor variables, a patient identification field, biopsy result, cancer stage, and cancer indicator fields.  The biopsy result and cancer stage fields contained categories that indicated cancer directly, so I left them out of my models.  


### Model Results
I fit classification models of K-Nearest Neighbors, Support Vector, and Random Forest.  I used the 19 risk factor variables as the X variables, and the cancer indicator variable as the Y variable.  The dataset had 10,000 rows.  I split it 75%/25% between training and testing data.

With the K-Nearest Neighbors model I got a best model accuracy near 88%, when using 5, 7, 9, and 11 neighbors, and lower accuracy with other numbers of neighbors.  My best result for the Support Vector Classification model was 93% accuracy with the rbf kernel.  I got 92% accuracy with the polynomial kernel, and 88% accuracy with the sigmoid kernel.  When fitting the Random Forest model, I got 95% accuracy with 10 trees and 98% accuracy with 100 trees.  The Random Forest model proved superior for this dataset.

After fitting the initial Random Forest models, I removed some variables with low feature importances and reran the model.  I got very similar results to the initial model, just slightly improved.  Tumor size, BMI, Age, and Mammogram Result were the features with greatest importance.

```
                   Feature  Importance
6            Tumor_Size_cm    0.130338
1                      BMI    0.123999
0                      Age    0.123712
8         Mammogram_Result    0.099698
3                  Smoking    0.092754
2           Family_History    0.090424
7   Lymph_Node_Involvement    0.082802
5         Genetic_Mutation    0.079821
13       Annual_Income_USD    0.043617
10             Cholesterol    0.042300
9           Blood_Pressure    0.039077
11  Exercise_Days_Per_Week    0.023965
4        Physical_Activity    0.015554
12   Breastfeeding_History    0.011939
```









Describe model fitting and results
Determined model accuracy using test set
	- Predicted values using x_test, compared to y_test data
	- Created confusion matrix
For random forest model, refined fields to include and reran classification
	- Explain reasons to remove fields
	- Similar results as before













### Sources:
Fatima, Mobeen (2026).  Breast Cancer Prediction Dataset | 10,000 Patient.  [breast_cancer_prediction.csv].  Kaggle.  https://www.kaggle.com/datasets/mobeenfatimah/breast-cancer-prediction-dataset-10000-patient.  License: CC BY-NC-SA 4.0


### Disclaimer:
I used AI to research and produce some of the code used in my statistical models.  I did not use AI to edit or write any of the analysis.


[back](./)
