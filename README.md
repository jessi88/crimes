### Predict Crimes in Vancouver

**Jessica Bosch**


#### Executive Summary
The goal of this project is to predict the probability of crimes in small spatial blocks of Vancouver and identify the contributing factors.


#### Rationale
Instead of having police officers patrolling randomly throughout the city, machine learning can provide them with target areas, 
i.e., areas with a higher probability of potential crime. 
A visible police presence in these target areas keeps people from committing crimes.


#### Research Question
Can we predict the probability of crimes in Vancouver?


#### Data Sources
- Crime statistics: https://vpd.ca/crime-statistics/. The downloaded data comes with a documentation:
    - The data is to be updated every Sunday morning, with a possible delay of 1 week.
    - The data begins in 2003.

- 2021 Census – Boundary files: https://www12.statcan.gc.ca/census-recensement/2021/geo/sip-pis/boundary-limites/index2021-eng.cfm?year=21
    - Reference Guide: https://www150.statcan.gc.ca/n1/pub/92-160-g/92-160-g2021002-eng.htm


Since most files are over GitHub's file size limit, we can't upload them here.


#### Methodology
First, a rich exploratory data analysis of the crime data is performed, among others, studying the most common crimes and analyzing the crime distribution by neighborhood.
Then, we combine the two data sources via the use of GeoDataFrames. In particular, we build small spatial blocks and temporal blocks of our crima data. 
Our spatial blocks are defined at the dissemination block level based on the 2021 Census – Boundary files. 
We create two different datasets based on two different levels of temporal blocks:
 a) Temporal blocks are defined as one day.
 b) The above temporal blocks are further refined as part of the day (early morning, late morning, afternoon, and night).

For each spatio-temporal block, we create a boolean on whether or not a crime happened. This is our target variable, which is imbalanced and in case b) highly imbalanced. 
More exploratory data analysis is performed on the combined data.

For the task of prediction, we restrict our datasets to the Central Business District, as this neighbourhood has by far the highest amount of reported crimes.
We use three different types of models to predict class probabilities (probability that crime will happen) for each of the two datasets:
 1. Random Forest
 2. XGBoost (eXtreme Gradient Boosting)
 3. Dense Neural Network

We tune hyperparameters for Random Forest and XGBoost. We also explore oversampling as well as threshold tuning for all three model types.


#### Results
**EDA**
- The total number of crimes has a decreasing trend over the years.
- `Theft from Vehicle` and `Other Theft` are the most common reported crimes in Vancouver.
- `Homicide` and `Vehicle Collision or Pedestrian Struck (with Fatality)` are the least common crimes.
- `Central Business District` has by far the highest amount of reported crimes, whereas `Musqueam` has the lowest amount of reported crimes.
- `Theft of Vehicle` has the best improvement since 2003, followed by `Break and Enter Residential/Other`.
- `Theft of Bicycle` has the worst development since 2003.
- Crimes occur throughout the year.
- Summer has the highest amount of criminal activities, while winter has the lowest.
- Most of the crimes occur on Fridays and Saturdays, while the least amount of crimes occurs during the middle of the week.
- Most crimes occur from 12pm to 1am, with an exceptional peak at midnight. There is a significant drop of crimes from 12am to 1am. Crimes stay relatively low from 1am to 7am. Crimes are drastically reported around 8am and gradually increase throughout the day peaking at 6pm. In between, we have a smaller peak at noon.



**Prediction**
- XGBoost and Random Forest (both with hyperparameter optimization) yield similar best results. Though XGBoost is slightly outperforming Random Forest.
- The best XGBoost model yields the following scores on the test set:
    - ROC AUC: 76.1%
    - Balanced accuracy: 69.8%
    - Accuracy: 73.9%
    - Recall: 61.6%
    - Average precision: 39.7%
    - Specificity: 78.1%
    - F1: 54.4%

- XGBoost and Random Forest (both with hyperparameter optimization) outperform the Dense Neural Network (without hyperparameter optimization).
- The dissemination block is the most important feature. Year is the second most important feature. Weekday, day, month, and the part of the day have quite lower importance. Season is not very important.





#### Next Steps
In the future, we plan to:
- incorporate the location of [police stations](https://vpd.ca/community/community-policing-centres/)
- analyze the relationship between demographic, social, and economic neighborhood characteristics and the spatial distribution of crime
- use time series analysis to determine long-term changes and seasonal components of crime
- analyze over-/under-sampling
- forecast the time series using Convolutional Neural Networks, Recurrent Neural Networks, and Long Short-Term Memory Networks
- use the KerasTuner for hyperparameter optimization
- explain the models with SHAP values
- apply the [Cynet model](https://pypi.org/project/cynet/)



#### Outline of Project
- [EDA and Data Preparation](https://github.com/jessi88/crimes/blob/main/predict_crimes_Vancouver_eda.ipynb)
- [Random Forest](https://github.com/jessi88/crimes/blob/main/predict_crimes_Vancouver_random_forest.ipynb)
- [XGBoost](https://github.com/jessi88/crimes/blob/main/predict_crimes_Vancouver_xgboost.ipynb)
- [Dense Neural Network](https://github.com/jessi88/crimes/blob/main/predict_crimes_Vancouver_neural_network.ipynb)


##### Contact and Further Information
jessica.bosch88@gmail.com
