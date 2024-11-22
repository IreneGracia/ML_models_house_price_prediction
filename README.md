This notebook utilises the Ames Housing dataset from the House Prices - Advanced Regression Techniques competition on Kaggle. From this dataset, features X and the target variable Y are extracted for analysis and modelling.

**Data Preparation Process**
1. Initial Data Cleaning:
    * Checked for duplicates and missing values (NaN).
    * Missing values were handled using strategies tailored to the type of feature (e.g., assigning a zero when a NaN signified the feature is absent, or mean/median/mode for numerical features).
    * Identified potential erroneous values (e.g., ?, 999, "", inf, -inf) and decided to retain or remove them based on whether they were plausible values for the dataset.
2. Feature Scaling:
    * A scaling strategy was selected based on feature distributions and the presence of outliers.
3. Feature Encoding:
    * Ordinal Encoding was applied to categorical features whose values are arranged based on a qualitative ranking.
    * Numerical Encoding was applied to numerical features.
    * One-Hot Encoding was used for remaining categorical features.
4. Custom Metric for Scoring:
    * Since the competition uses RMSLE (Root Mean Squared Logarithmic Error) as the evaluation metric, which is not available in sklearn, a custom scorer object was created for cross-validation.
5. Feature Engineering:
    * Experimented with three feature selection techniques and selected Univariate Feature Selection to retain the most significant features for predicting Y.
    * Transformed time-based features, such as MoSold, into cyclical features to capture their periodic nature.
    * Applied target engineering, transforming Y to log(Y), which improves model performance when using linear or parametric models.
6. Pipeline Creation:
    * The entire data preparation process, including cleaning, scaling, encoding, and feature engineering, was consolidated into a reusable data processing pipeline.


**Modeling and Evaluation**
1. Model Iteration:
    * Tested a range of models to identify the best-performing one based on cross-validation using the custom RMSLE scorer.
    * Techniques to enhance performance included:
        * Grid Search to optimize hyperparameters for parametric models.
        * Trying different kernels for SVM models.
        * Implementing Early Stopping for certain models to prevent overfitting.
2. Models Explored:
    * Linear Models: Ridge regression.
    * Non-linear Models: K-Nearest Neighbors (KNN), Support Vector Machines (SVM), Decision Tree Regressor.
    * Ensemble Models: Random Forest Regressor, AdaBoost Regressor, Gradient Boosting Regressor, XGBoost Regressor.
3. Final Model Selection:
    * The XGBoost Regressor with optimized hyperparameters emerged as the best-performing model based on RMSLE scores during cross-validation.


**Prediction**

The test dataset was processed through the data preparation pipeline and predictions were made using the best model (XGBoost). These predictions were then submitted as final house price predictions for the competition.
