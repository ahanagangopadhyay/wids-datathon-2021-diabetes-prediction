This repository contains codes for our submission to the 4th Annual Women in Data Science (WiDS) Datathon 2021 hosted on Kaggle. Our solution ranked in the top 24% of the submissions (180th out of 762 teams) with an AUC-ROC score of 0.86697 on the public leaderboard.

**Problem statement:**

It is important to get a rapid understanding about the overall health of a patient brought to a hospital. Covid-19 has made this all the more crucial as healthcare workers around the world struggle with hospitals overloaded with patients in critical conditions. Intensive Care Units (ICUs) often do not have medical histories of incoming patients. Patients themselves may be in distress, confused or unresponsive, and as such unable to provide information about any existing chronic conditions,such as heart disease, diabetes, etc. Medical records may take days to transfer, especially for a patient from another medical provider or system.

Knowledge about chronic conditions such as diabetes can inform clinical decisions about patient care and ultimately improve patient outcomes. This year's challenge was to use data from the first 24 hours of intensive care to determine whether a patient admitted to an ICU has been diagnosed with a particular type of diabetes, Diabetes Mellitus. This included data about patient demographics as well as clinical measurements from the first 24 hours of intensive care.

**Challenges:**

- The provided dataset has large amounts of missing data, with more than 90% of the features having missing values.
- The dataset is imbalanced, where aound 23% of the patients have Diabetes Mellitus.


**Our approach:**

- We took an ensemble learning approach, using a variety of classifiers like LightGBM, XGBoost, CatBoost and Deep Neural Networks. Final predictions were a weighted sum of the individual predictions, where the weights were chosen through validation.
- We experimented with different methods of data cleaning and imputation, some of which are outlined below:
  > Dropping features having more than a certain percentage of missing values
  > Dropping one of a pair of numerical features if pair-wise correlation is greater than a threshold
  > Dropping features with less than a certain number of unique values
  > Considering missing values in categorical features as a separate category instead of replacing with the mode of the feature, which we saw improved our predictions
  > Imputing missing age with average age of people in the United States
  > Imputing missing features like height and weight according to gender instead of using overall means
  > Imputing missing blood oxygen levels with standard values
  > Calculating missing BMI using height and weight
  > Adding new features, e.g. markers for low levels of creatinine, markers for high levels of billirubin/glucose/BMI, range/ratio features corresponding to min and max records       for lab tests, flags for liver disorders
- For some base learners, we used SMOTE oversampling to balance the dataset.
- For all classifiers, we implemented hyperparameter tuning with stratified K-fold cross-validation to select the best model.
