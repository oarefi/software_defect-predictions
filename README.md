# Software Defect Analysis and Prediction

Authors: Ali Arefi (oarefi), Jalaj Rastogi (jrastogi)

## Motivation
Good code is characterized by fewer errors, and as code complexity and dynamism increase, assessing its performance and the likelihood of failure becomes more challenging. We need a fast and efficient way to test and understand code, as well as ensure easier maintainability. McCabe and Halstead metrics can be used to measure code complexity and enable developers to design high-quality software with lower risks of failure. This is especially crucial for safety-critical applications that require compliance with high standards set by industries like automotive, manufacturing, aerospace, medical devices, and power stations. Verisoft provides formulas to calculate ideal values and ranges for these metrics, which are essential for good software design.

## Intent Summary
1. We utilize Verisoft parameters to identify programs that fall within the redesign classification and explore the relationship between redesignated programs and actual failures/defects.
2. We employ a Random Forest Classifier to train a software defect prediction system capable of classifying new points as likely defective or not based on previous training data.
3. Once optimized through validation, we perform feature importance measures to identify the most important features in the model's prediction performance.

## Data Manipulation
1. Extract Data: The datasets used in this project were initially in .arff format and were converted to CSV format for ease of use. A custom function was created to convert the .arff file into a list of lines, with the first line representing the column names and the subsequent lines containing the data rows. This list was then written to a CSV file.
2. Merge Data: The datasets were merged using an outer join. The resulting merged dataframe had 2535 rows and 40 columns. NaN values were replaced with empty strings, and the values from two columns representing defects were concatenated and assigned to a new column called 'defects'.
3. Data Preprocessing: A new feature called 'Redesign Status' was created based on conditions derived from Verisoft's software complexity measurement. The conditions included metrics such as cyclomatic complexity, Halstead volume, Halstead error estimate, Halstead effort, Halstead program time, Halstead difficulty, and total line count. If a software module satisfied the conditions, the 'Redesign Status' was set to 0; otherwise, it was set to 1.

## Data Visualization and Analysis
- Defects and Redesign: Jaccard similarity was used to measure the similarity between features. The analysis showed a 75% similarity between redesignations and defects, indicating a significant chance of catching defective software by applying Verisoft metric recommendations.
- Point Biserial Correlation: Point biserial correlation was used to measure the correlation between binary features (defects) and continuous features. The analysis revealed correlations between features such as total lines of code, redesign status, Halstead volume, Halstead errors, and defects.

## Software Defect Prediction System
- Model: An optimized Random Forest Classifier was built for the software defect prediction system. The model uses decision tree classifiers on various sub-samples of the data to improve predictive accuracy and control overfitting. The model parameters were optimized using RandomizedSearchCV.
- Issues: An unbalanced dataset was encountered, where the number of defects was significantly lower than the number of non-defects. This imbalance posed challenges for the model's learning process and prediction performance.
- Hyperparameter Optimization: The model's hyperparameters were optimized using RandomizedSearchCV, resulting in the best parameters for fitting the feature training samples and target training samples.
- Performance: The model demonstrated relatively good performance in predicting the majority class (non-defects), but struggled to predict the minority class (defects) with high precision. Precision, recall, F1-score, and ROC-AUC analysis were performed to evaluate the model's performance, with an AUC score of 0.76 indicating adequate classification.

## Feature Importance
Feature importance tests were conducted to identify the most important features for prediction. A SHAP value plot showed that total lines of code were positively correlated with the defect classification, while cyclomatic complexity and Halstead difficulty showed a negative correlation. This suggests that the volume of operands and operators, as well as the complexity of the program, play significant roles in defect classification.

## Conclusion
This project investigated the relationships between defected programs, programs marked for redesign, and fundamental software metrics. The findings highlighted the significance of total lines of code, volume of operands and operators, and cyclomatic complexity in predicting defects. The software defect prediction system achieved adequate performance, but further improvements are required to address precision and false positives.
