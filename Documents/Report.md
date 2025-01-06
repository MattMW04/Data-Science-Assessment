# Portfolio for Data Science COM618:  Diabetes Data Analysis

> **Student Name:** Matthew Wilcox   
>**Student Number:**  Q16048563    
> **Github Repository Link:** [Data-Science-Assessment Github Link](https://github.com/MattMW04/Data-Science-Assessment)

***



## Introduction
Diabetes is a large, growing problem within the Medical community, with Diabetes being the direct cause of 1.6 million deaths in 2021 [^1], with the mortality rates increasing since 2000. Furthermore, 59% of adults (30 and over) were living without medication with Diabetes in 2022. These figures represent a challenge in the medical area with effectively screening for people who have the disease and also a problem in distributing care, leading to these increased mortality rates. This represents that the industry could benefit from some analysis of data on the problem in order to help them make informed decisions quicker to help take preventative measures to stop the disease/ distribute care to people with the disease to stop mortality rates rising further.

[^1]: [WHO Diabetes Fact Sheet](https://www.who.int/news-room/fact-sheets/detail/diabetes)

***
#### Aims/Objectives of the coursework: 
- This Coursework aims to provide an analytic insight into some of the variables that can lead to diabetes. This would be helpful in the Medical Sector as having access to data analysis of this problem could lead to better diagnoses of future patients, which could help set up preventative treatments beforehand to stop strain on medical services, but also allow patients to have access to quality healthcare leading to better quality of life, patient satisfaction and survival rate.

***

## Methods

### Dataset
This Diabetes Dataset was sourced from Kaggle [^2] and contains data from the National Institute of Diabetes and Digestive and Kidney Diseases. This Dataset was used to predict whether a patient had diabetes. This Classes patients in the Outcome variable as either 0 (Non Diabetic) or 1 (Diabetic). This dataset provides insight into many key features (BMI, Glucose, Blood Pressure etc) that can be a large indicator in the cause of diabetes. By leveraging this dataset using different data analysis techniques and data modelling, we can help identify indicators of the disease that can be used for prevention and management of the disease. This dataset has missing values , so will need to be preprocessed to ensure valuable insight can be obtained.

[^2]: [Diabetes Dataset (Kaggle)](https://www.kaggle.com/datasets/mathchi/diabetes-data-set)
***

### Analysis and Results

#### Dataset Preparation

This Dataset had to be prepared for Usage in Data Analysis by cleaning up any null / not included ie included as 0 data points. We first did this by checking for null values by using the ` isnull()` function on the DataFrame, which returned 0. Then by checking for 0 values it was found that there are lots of missing values. These were turned to Nan using `diabetes_data_cleaned[columns_to_clean] = diabetes_data_cleaned[columns_to_clean].replace(0, np.nan)`. The proportion of values that were now null in each column of the dataset was then calculated and displayed , giving this output: 

> Proportion of missing values in the cleaned dataset:
    > Id                           0.000000  
    >Pregnancies                  0.000000  
    >Glucose                      0.650289  
    >BloodPressure                4.515896  
    >SkinThickness               28.901734  
    >Insulin                     48.049133  
    >BMI                          1.408960  
    >DiabetesPedigreeFunction     0.000000  
    >Age                          0.000000  
    >Outcome                      0.000000  
    >dtype: float64  
>
Due to this Output , it was decided that 2 rows: **SkinThickness** and **Insulin** would be dropped. This was because imputing thousands of lines to data to something ie the mean would lead to a big skew in data, making the dataset overall unfit for purpose of data analysis as any output would be massive different to real life. **Id** was also dropped as it serves no analytical value for us.

The other Columns with missing data: **Glucose**, **BloodPressure** and **BMI** had the missing columns filled in as they had a lower proportion of missing values, therefore not effecting the data as much. This was done using the Mean(Average) values using the code below, with the example showing how it was done on the **BMI** column:

```python  
imputer = SimpleImputer(strategy='mean')
diabetes_data_cleaned['BMI'] = imputer.fit_transform(diabetes_data_cleaned[['BMI']])
```  

This was done with the averages as this gives the biggest representation of the overall trend of the column from the data, which will help the replaced values being as accurate as possible.
![Skewness-KurtosisSnap](../Plots/Skewness-Kurtosis.png)
![Skewness-KurtosisOutputSnap](../Plots/Skewness-Kurtosis-Output.png)

These Screenshots represent the checking of Skewness and Kurtosis values in the Dataset. These represent that **DiabetesPedigreeFunction**, **BMI(Outside 3 value of Kurtosis but included as it is high)** and **Age** have high skewness or kurtosis that could suggest outliers that could be handled in later steps.

Overall, this step (Data Preprocessing) has helped the data be more fit for its purpose as it has made the dataset more trimmed and has removed any null/unrepresentative(0) values that may skew any findings. This Step could have Been further improved on by using the Skewness and Kurtosis values in order to identify Outliers and handle them appropriately.

***

#### Exploratory Data Analysis/ Data Visualisation

The EDA of this Dataset aimed to see if we could get any valuable insights from the data.

Independent Variables:   
Glucose, BMI, Blood Pressure, Age, Pregnancies, DiabetesPedigreeFunction

Dependent:   
Outcome

#### Univariate Analysis:

!['Mean-Median-Standard Deviation Code'](../Plots/Mean-Median-STD-Code.png)

!['Mean-Median-Standard Deviation Output'](../Plots/Mean-Median-STD-Output.png)

!['Dataset Summary'](../Plots/Range.png)

These Snapshots represent analysis of the Mean, Median and Standard deviation of each variable, as well as a Dataset summary, where the min and max was used to calculate the range.

Some standouts from this data: 

Glucose: 
The Wide range(44-199) and Significant Standard Deviation suggest extreme cases of Hypoglycemia(low) and hyperglycemia(high), which is a condition that can affect our outcome variable (diabetes or not).

BMI : a mean of 32.6 places the average patient in the obese category.

Pregnancies/Age : Both The range of both columns and the standard deviation of pregnancies (3,32) indicates high variation in age.

!['Outcome Distribution Code'](../Plots/Outcome-Distribution-Code.png)

!['Outcome Distribution '](../Plots/Outcome-Distribution.png)

These Screenshots represent the Outcome distribution of the Dataset, which suggests 65% of the outcome variable is 0(Non-Diabetic), which shows a dataset imbalance. This could effect later classification models, which could lead to us needing to do resampling/undersampling or use more complex models like Random Forest.


!['Histograms '](../Plots/Histograms.png)
These Histograms represent the Skewness of the Variables and help us understand what values are most present.

!['Box Plots '](../Plots/Box-Plots.png)
These Box Plots show that **BloodPressure**, **BMI** and **Age** show a number of outliers (circle outside box plot).

#### Bivariate/Mutivariate Analysis:

!['Average by Outcome Code'](../Plots/Averages-By-Outcome-Code.png)

!['Average by Outcome '](../Plots/Averages-By-Outcome.png)

This represents how each variable may effect the outcome, with the graph showing that on average higher glucose, blood pressure, BMI and Age contribute to the 1/Diabetes Outcome.

!['Correlation Matrix Code '](../Plots/Corr-Matrix-Code.png)

!['Correlation Matrix '](../Plots/Corr-Matrix.png)

This is the Correlation Matrix for the Dataset, which shows how much the different variables effect the others. From this, we can see that Glucose has a large impact on Outcome, following other Diabetes findings. Also, Variables such as BMI , Pregnancies Age have a higher correlation with the causation of Diabetes, with DPF and BloodPressure having the lowest impact. We can also see that BMI and BloodPressure and BMI and Glucose have a fair amount of correlation, which again follows Trends.

!['Glucose vs Outcome Code '](../Plots/Glucose-VS-Outcome-Code.png)

!['Glucose vs Outcome  '](../Plots/Glucose-VS-Outcome.png)

This scatterplot shows an example of a scatter plot done for analysis, which shows us that a higher amount of glucose at the higher end of the scale has a 1(diabetic) outcome.



***

#### Data Modelling:


#### Modelling - Predict Dependent variable (Outcome) based on Dataset

The aim of the Model Use of this data was to analyse if the dataset was fit for purpose of classifying patients, as this will help to earlier catch disease symptoms/ trends and either implement measures to stop it becoming Diabetes, or give them the appropriate Medical care to ensure that the death rate does not rise as highly as it has in recent years. I have used 2 Models to analyse this , Logistic Regression and Random Forest. These have been used due to the Data being Categorical in nature, meaning other Machine learning models may not be fit for purpose.

##### Logistic Regression:

!['Logistic-Regression-Code'](../Plots/Logistic-Regression-Code.png)
!['Logistic-Regression-Output-1st-Iteration'](../Plots/Logistic-Regression-Output-1st.png)
!['Logistic-Regression-Confusion-Matrix-1st-Iteration'](../Plots/Logistic-Regression-CM-1st.png)

This Logistic Regression Model was created using the sklearn library . We first seperated the independent and variables, then split the dataset into the test and training sets, then fit our model with the training data and predicted the test data based on that.
The model was then evaluated as:
Accuracy: 0.76 / 76%
!['Logistic-Regression-Results'](../Plots/Logistic-Regression-Results.png)
The model Misclassified 43 false positives and 91 false negatives, showing the model is less accurate on the 1 outcome due to less support/ training data (187 to 367). This is also shown from the much lower precision, recall and f1-score. When attempting to address this with `log_reg=LogisticRegression(class_weight='balanced')` , this improved the model as such:

!['Logistic-Regression-Results'](../Plots/Logistic-Regression-Results-2nd.png)
!['Logistic-Regression-Feature importance'](../Plots/Logistic-Regression-Output.png)
!['Logistic-Regression-Corr-Matrix'](../Plots/Logistic-Regression-CM.png)

These show that while it did improve performance by 2%  and the performance on the 1 outcomes recall and f1-score, the 0 Outcome ended up with more misclassified rows (false-positives) and decreased the recall.

While this performance is ok, we want to improve it to make it as useful as possible, due to this we will try RandomForest, which is a classifier model that due to its ensemble learning[^3] will deal better with the imbalanced dataset.

[^3]: [Logistic regression vs random forest](https://www.geeksforgeeks.org/logistic-regression-vs-random-forest-classifier/)

##### Random Forest Classifier

For this Model, we have used the RandomForestClassifier from sklearn 

!['Random Forest Classifier Code'](../Plots/RFC-Code1.png)
!['Random Forest Classifier Output'](../Plots/RFC-Output-1.png)
!['Random Forest Classifier Feature Importance'](../Plots/RFC-FI-1.png)
!['Random Forest Classifier Confusion Matrix'](../Plots/RFC-CM-1.png)

This Model performs much better then the Logistic regression model, with only 3 false positives and 7 false negatives and an accuracy of 0.98, also having both outcomes having over 95% recall and f1 score. The feature importance graph shows that pregnancies has the lowest impact, while glucose has the highest on the outcome variable. 

Over a few iterations of the model, we go the highest performance by removing pregnancies and DPF. We removed them due to Pregancies low feature importance and DPF low score in the Correlation matrix from earlier. This led to the following scores.
!['Random Forest Classifier Code'](../Plots/RFC-Code2.png)
!['Random Forest Classifier Output'](../Plots/RFC-Output-2.png)
!['Random Forest Classifier Feature Importance'](../Plots/RFC-FI-2.png)
!['Random Forest Classifier Confusion Matrix'](../Plots/RFC-CM-2.png)

## Evaluation
These results for the final model show that the model is very good at evaluating our data based on 4 variables, glucose, bmi blood pressure and age. These would be good indicators for BMI in the medical field, so this could be a useful model for future research. This model gained 99% accuracy with only 8 rows misclassified and had high scores in precision, recall and f-1 score across both outcomes. The feature importance of glucose being so high tracks with real life diabetes studies and also our EDA from earlier, showing the model is classifying correctly. Overall, this model has been very successful at classifying patients.
***

## Limitations and Challenges

Some of the limitations with this dataset include:
Missing values - having missing values in any dataset isn't ideal as it creates a lack of real life, accurate data. We got around this in our data Preprocessing/ Preparation Phase, however 2 variables were dropped from the table during this and other variables having missing values imputed from the average (mean). Due to this, we may lack understanding of how those other variables contribute, which can affect healthcare and also the imputed values may skew any models trained as they are not true organic values gained from study.
Misbalanced data - This data has more Values for Outcome 0 (1816) then outcome 1 (952). This has effected the analytical power of Models such as LogisticRegression as it struggled to identify the 1 outcome as well as 0 as it had less training rows.

***

## Conclusion

The analysis of this data identified Glucose, BMI , Blood Pressure and Age as significant indicators of diabetes, aligning with medical research. Through preprocessing the original dataset, EDA and machine learning algorithms , using feature selections i created an effective model with Random Forest Classifier, which had 99% accuracy of classification. 
This project showed the importance of quality data obtained through preprocessing visualisation in order to gain early insights into the data. Limitations such as imbalanced outcome amounts and missing values highlighted a challenge in healthcare datasets which may prevent some from gaining meaningful insights. 
Reflecting on this work , I gained experience in handling data , preprocessing it to increase usability, visualise data to analyse trends and creation of classifications models. Future work could be done on : Feature imbalance, Outlier detection and removal and further analysis of data, which would overall contribute to better tools for diagnoses, prevention and management of Diabetes. 
***
Word Count (Excluding references): 2076

***

> ## Reference List (Harvard Style)
>
> [1]  World Health Organization (2021) Diabetes Fact Sheet. Available at: https://www.who.int/news-room/fact-sheets/detail/diabetes  (Accessed: 27 December 2024).   
> [2] Mehmet Akturk (Mathchi) (n.d.) Diabetes Data Set. Available at: https://www.kaggle.com/datasets/mathchi/diabetes-data-set  (Accessed: 27 December 2024).   
> [3] GeeksforGeeks, 2024. Logistic Regression vs Random Forest Classifier. [online] Available at: https://www.geeksforgeeks.org/logistic-regression-vs-random-forest-classifier/ [Accessed 30 December 2024].   
>[4] Pandas Documentation, 2024. pandas.DataFrame.T. [online] Available at: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.T.html [Accessed 30 December 2024].   
>[5] Tryolabs, 2017. Pandas & Seaborn: A guide to handle & visualize data elegantly. [online] Available at: https://tryolabs.com/blog/2017/03/16/pandas-seaborn-a-guide-to-handle-visualize-data-elegantly [Accessed 30 December 2024].   
>[6] Statology, 2024. sklearn regression coefficients. [online] Available at: https://www.statology.org/sklearn-regression-coefficients/ [Accessed 30 December 2024].   
