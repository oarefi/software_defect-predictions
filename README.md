# software_defect-predictions
Software detect prediction using randomforrest classifier and regressor. We used code complexity metric recommendations(LOC, Halstead, and Mccabe) as a benchmark to train our ML classifier to predict wheter software would be defective or not. EDA and data processing included Spearman and Point Biserial correlations and Jaccard similiarty between metrics for relations. Dataset was highly imbalanced so SMOTE was performed. Randomforrest regressor was used in a RandomizedSearchCV for hyperparameter tuning. Confusion matrix and ROC/AUC scores where used to test model performance. An acceptable AUC score of 0.76-0.78 were acheieved. SHAP and Lime were used for feature importance of classifier and they indicated LOC or "Lines of Code" was the most important factor.
