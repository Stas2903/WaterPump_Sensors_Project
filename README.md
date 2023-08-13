# Introduction: 

    This dataset contains measurements of 52 sensors each minute and the machinig status every minute. The machining status may be either NORMAL, BROKEN or RECOVERING.
    Every time the machine has BROKEN label, it is staying in RECOVERING state for a certain amount of time until the machine is fixed and turned back to NORMAL state. 
    
    Our goal is to explore and analyze the data we have and find some patterns during the EDA and finally train ML models and ANN
    to predict the machining status in accordance with sensors and timelines so that we will be able to use our models to avoid the breadwins of the pumps in the future.


# Objectives: 

    Our goals:

        1. To develop a ML model that predicts the Machine Status
    
        2. To develop a DL model that predicts the Machine Status
    
        3. To find insights into the sensor patterns and the possible reason for breakouts


# Description

    1. Type of problem: classification.

    2. 55 Variables: 53 Numerical, 1 datetime

          > 52 sensors
  
          > 1 timestamp 

    3. Target:

          > machine_status (NORMAL, BROKEN, RECOVERING)

    4. Steps applied:

          1. Importing a dataset
  
          2. Data analysis
  
          3. Feature engineering
  
                1. Dropping unnecessary variables
    
                2. Scaling
    
                      > Standart Scaler
      
                      > Robust Scaler
  
                4. Imputing NaN values   
    
                5. Splitting datasets into train / test datasets
    
                      > Sliding window approach
      
                      > Cross validation

          4. Training ML models
  
          5. fine-tuning of hyperparametes

                > GridSearchCV
  
          6. Training ANN
  
          7. Model evaluation and result analysis

    5. Algorithms used:
  
          1. RandomForest Classifier
  
          2. GradientBoosting Classifier
  
          3. KNeighbours Classifier
  
          4. Support Vector Classifier
  
          5. XGBoost Classifier
  
          6. ANN

    6. Evaluation Metrics:
  
          1. Confusion Matrix
  
          2. Roc-auc
  
          3. Precision
  
          4. Recall
  
          5. Accuracy


# Conclusion

##  Data Analysis

    After completing the data analysis step, we found several insights. 
    
          1. all sensors data are numerical types (float64) and the 'machine_status' variable (target) is categorical
  
          2. more than 93% of all the datasets the machining status was "NORMAL"
  
          3. there are only 7 accidents with broken pumps
  
          4. 'NORMAL' takes more than 93 percent of the 'machine_process' variables, while 'RECOVERING' takes almost 7% and "BROKEN" takes less than 1%
  
          5. 4 out of 7 breakouts were fixed under the next 24 hours. However the second and fifth breakouts took more than 50 hours (2 days). ESPECIALLY the fifth breakout which took more than 5 days to fix
  
          6. the amount of missing values in variable 'sensor_15' is 100% which means that there is no point in maintaining this variable, because it has no prediction power. Other variables have less than 45% of missing values which is acceptible and will be imputed in the feature preprocessing steps.
  
          7. there are plenty of outliers in almost all variables and it might be seen that some variables like "sensor_44" and "sensor_42" are constant, but actually they are not.'
  
          8. some of the independent variables have high correlation, causing so-called multicollinearity while others are not correlative at all.
  
          9. sensors from 0 to 10: all sensors record critically low values during July and the majority of sensors has lower values between April and May. The periods are the same with the second and fifth breakouts which took the longest time to fix. It seems that those breakouts were because of some emergancy because a lot of sensors has dropouts during these periods. while the values from sensords during other breakouts seems to be stable and calm.
  
          10. sensors from 11 to 20: all sensors recorded critically low values during July and the majority of sensors also had lower values in the first half of May. Sensors 10, 11 and 12 also has dropdown in the second half of April. The majority of dropouts seems to happen during the third breakout which took almost 1 day to fix and during the fifth which took 5 days.
  
          11. sensors from 21 to 30: all sensors recorded critically low values in the first half of May. Also there are dropdowns just before the July. The majority of dropouts seems to happen during the third breakout which took almost 1 day to fix and during the fifth which took 5 days.
  
          12. sensors from 31 to 40: sensors 31, 32, 33, 34, 35 and recorded critically low values in the first half of May. Some of the dropouts seemed to happen during the third breakout which took almost 1 day to fix and during the fifth which took 5 days.
  
          13. sensors from 41 to 52: sensor 50 has no records after the July. And sensor 51 has critically high values in the second half of June.

        
   ## Feature Engineering & Selection

    > We used Robust Scaler to handle the difference in magnitude of the variables, because of its simplicity, and because it can theoretically hide the outliers.

    > We used a multivariate type of KNN imputation called KNN imputation. After the imputation of Null values using KNN imputation, the distribution of variables has changed a little bit.

    > For feature selection we used two approaches including: 

          > Filtering methods: 
  
                * Constant variables
    
                * Quassi-Constatant variables 
    
                * Duplicated variables
    
                * Correlated variables 
            
    The filtering methods helped us to reduce the dataset's dimension because we deleted 23 variables which were correlated

    
   ## Training & Evaluating models
   
     > Because we are working with Timeseries data, it is important to preserve the time sequence and that it why we will use the technique of sliding window to divide the dataset to train and test sets.

     > We have tested 5 popular models with the same data and same preprocessing steps to then compare them and choose only fixed amounts to tune the hyperparameters. 

     > After testing 5 models, we chose only 3 best models according to the accuracy metrics 

     > Then, we used cross-validation and started to fine-tune hyperparameters to boost the performance 

     > Lastly, We have evaluated the models we built using several metrics including: 

           1. F1 score
  
           2. Roc-auc 
  
           3. Confusion Matrix 
  
           4. Precision
  
           5. Recall 
  
           6. Accuracy

         
    By analyzing all metrics we can tell that: 

          1. The results for Recall and F1 are really bad and probably happens because of the lack of data of broken machines. We have such low results because the recall and f1 for the broken status is significantly low as there are only 7 broken status.
  
          2. It seems that the models we trained are not really good. Because they do not generalize well and can not effectivelly predict broken labels because of the lack of data.
  
          3. If we had to choose one, I would choose Random Forest because although it does not give the highest results, it gives the most stable and consistent resu

                
   ## Training & Evaluating ANN

        1. The loss has dropped to its minimum about 0.450 almost immidiately and then nothing has changed.

        2. The accuracy has reached its maximum at about 95% almost immediately and then nothing has changed.

        3. It seems that ANN is not the best choice here, because the metrics including accuracy and confusion matrix are not the best and not better compared to the ML models. More specifically, the amount of type I and type II error higher.

        
        We tend to think that it would be better to gain more data and may be try to use different approaches to process the time series data and may be use something else for feature selection.

                
   # THANKS!!! :)
