ITD224 Applied Data Science Project  
Name: Tan Puey Leng  
Student ID: 5888749K  
  
1\. Project Background

The organisation is facing declining employee engagement and raising employee attrition. This has lowered employees' morale and reduced productivity. Additional resources were also spent on recruitment and training of new staff. To tackle these problems, the human resource department (HR) requested for our help to improve engagement and retain valuable staff in the organisation using data-driven strategies. My part of the project will focus on staff retention and my business objective is to use machine learning to identify key employee characteristics associated with attrition and inform targeted staff retention strategies.

This project uses the HR Employee Attrition dataset to analyse employee characteristics and develop machine learning models to predict employee attrition. However, the purpose of the models is not to identify employees that are at risk of leaving the organisation. Instead, the models were built so that employee characteristics that are strongly associated with employee attrition could be identified through feature importance analysis. Exploratory data analysis was then used to determine how the identified characteristics were associated with employee attrition. The findings were subsequently translated into potential employee retention strategies.

2\. Work Accomplished

2.1 Data Preparation

Data inspection, data cleaning, exploratory data analysis and data preprocessing were carried out on the dataset before modelling. There were no duplicates and missing values found in the dataset. It was observed that the features 'EmployeeNumber', 'DailyRate', 'MonthlyRate', 'Over18' and 'StandardHours' were redundant and they were removed from the dataset subsequently.

Binary encoding was applied to 'Attrition' and 'Overtime' so that the 'Yes' or 'No' entries will be changed to '1' or '0'. Ordinal encoding was performed on 'BusinessTravel' where entries were manually mapped into a 0 to 2 number scale as there was an escalating relationship in the entries. The rest of the categorical variables were prepared using one-hot encoding to convert all strings into machine readable numerical format before modelling.

An 80/20 stratified train-test split was performed on the dataset to validate the predictive performance of the models on unseen data. Standardisation was applied on all numerical columns after train-test split. The scaler was trained on x_train only so that it learns the mean and variance of the training data. Scaling was then applied to both x_train and x_test using the learned parameters, ensuring no data leakage.

Exploratory data analysis revealed that there was a class imbalance in the target variable 'Attrition'. To address this issue, SMOTENC was applied on the training set to balance the data, ensuring there were equal number of entries for employees who attrited and retained. SMOTENC was used as it can effectively handle both numerical and categorical features. The prepared dataset was then ready to be used for modelling.

2.2 Models

The objective for the modelling was to identify the features strongly associated with employee attrition. Therefore, only algorithms capable of generating feature importance scores or interpretable coefficients were utilised. The selected algorithms for this project were Logistic Regression, Decision Tree and Random Forest.

An automated hyperparameter tuning pipeline was constructed to evaluate the 3 algorithms to find the optimal configuration that gives the best performance. The GridSearchCV module was used to perform thorough hyperparameter tuning. It applied 5-fold cross-validation across the training set to evaluate different parameter combinations without overfitting.

After the best model for each algorithm were generated, the models were compared using accuracy, precision, recall and F1 score. F1 score was chosen as the primary performance indicator as it combines precision and recall into one metric using their harmonic mean. This ensures that the model maintains a balance between correctly identifying employees who are likely to leave and minimising false predictions. The overall best performing model was used to generate the feature importance scores for evaluation.

2.3 Evaluation

Random Forest is the best performing model. It has the highest F1 score of 0.941, while also achieving the highest precision (95.7%) and recall (92.6%) as compared to the other 2 models. The Random Forest model is able to identify true attrition risks (high recall) while minimising false alarms (high precision), making its generated feature importance scores highly reliable for interpretation.

3\. Recommendation and Analysis

3.1 Analysis

'OverTime' was the strongest predictor of employee attrition in the Random Forest model. It was followed by 'StockOptionLevel' and 'YearsAtCompany'.

The 10 most important features were distributed across different categories:

- Employee Demographics & Background: 'Age', 'DistanceFromHome'
- Role & Work Conditions: 'OverTime'
- Compensation & Benefits: 'StockOptionLevel', 'MonthlyIncome'
- Tenure & Career History: 'YearsAtCompany', 'TotalWorkingYears', 'YearsInCurrentRole'
- Satisfaction & Performance: 'JobSatisfaction', 'EnvironmentSatisfaction'

The importance values were relatively low and close to each other which suggested that there was no extremely strong association between any feature and attrition. Instead, attrition is the result of a cumulative combination of factors.

3.2 Recommendations

HR should go through the list of features that are strong predictors of attrition and develop new retention strategies. However, they should understand that the model identified the characteristics that are strong predictors of employee attrition and not necessarily causal drivers. It does not mean that these predictors directly cause employees to leave. Further investigations are required before implementing policies based on individual predictors.

Based on the exploratory data analysis done earlier, some recommendations could be given to HR for their consideration.

3.2.1 Strengthen Overtime Management  

The first recommendation is to strengthen overtime management. Since overtime is strongly associated with attrition, HR could first review workload distribution, overtime requirements and staffing levels. HR should also implement an alert system to track employees who consistently work overtime. If any employee is flagged, HR can request the department manager to justify for the overtime and explore redistribution of workload. Additionally, HR should review the current overtime compensation schemes to ensure they remain fair and competitive.

3.2.2 Review Stock Options Policy  

The second recommendation is to review stock options policy. Exploration data analysis revealed that employees with no stock options had a higher observed attrition rate compared with employees receiving any level of stock options. HR should review the current stock option allocation policy and evaluate whether eligibility criteria could be adjusted to provide some employees currently without stock options with Level 1 stock options as part of their employee retention strategy.

3.2.3 Improve Employee Development  

The last recommendation is to improve employee development. Features like 'YearsAtCompany', 'TotalWorkingYears', 'Age' and 'YearsInCurrentRole' indicate that employees who leave are typically younger and have less tenure than those who remain. HR should implement longer-term mentorship programs that outline clear career progression and growth paths, assuring newer employees of their career development within the company. HR could also implement job rotation or cross-training programs to prevent role fatigue or stagnation.

4\. AI Ethics

4.1 Privacy  

The dataset contains the employee number of the employees, a unique identifier for each employee, and other sensitive information such as their age, gender, marital status, monthly income, job role and department. All the information is linked to identifiable employees and therefore, there is a risk of exposing employees' personal information. HR should ensure that the data is collected, stored and processed securely with restricted access to authorised personnel only. All personally identifiable information should also be removed or anonymised when the information is not required.

4.2 Fairness  

Features like age, gender and marital status could result in unfair treatment if they influence the model's prediction on employee attrition. For example, the model and exploratory data analysis suggests that younger employees are more likely to leave the organisation. HR should not discriminate younger employees or lower the hiring of employees in the younger age group due to the finding. HR also should not use the model to predict employees who are likely to attrite for the purpose of identifying each of the individual employees. The characteristics of employee associated with attrition must also not be disclosed to the rest of the organisation to avoid unfair treatment or discrimination.

4.3 Accuracy and Accountability  

Decisions on whether company-wide policies should be changed must be made with human judgement and additional information. HR is responsible for decisions made using the model. Also, the company should built new models periodically to monitor whether there are any changes with the characteristics associated with attrition, especially after the new policies were rolled out for a period of time and when there is a change in employee patterns. This ensures that there are accuracy and accountability for the decisions supported by the model.

4.4 Transparency  

Although the random forest model can be more difficult to interpret than simpler model like logistic regression, the feature importance helped to improve transparency by giving a score to each feature so that the more important features that contributed to the model can be identified. However, it should be clearly communicated to HR that the model identifies patterns and associations rather than causal explanations.
