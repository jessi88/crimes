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
- Crime statistics: https://vpd.ca/crime-statistics/
- 2021 Census – Boundary files: https://www12.statcan.gc.ca/census-recensement/2021/geo/sip-pis/boundary-limites/index2021-eng.cfm?year=21

Since most files are over GitHub's file size limit, we can't upload them here.


#### Methodology
First, we extract the data from the two data sources and combine them via the use of GeoDataFrames. 
In particular, we build small spatial blocks and temporal blocks of our crima data:
 - Our spatial blocks are defined at the dissemination block level based on the 2021 Census – Boundary files.
 - Our temporal locks are defined as one day.
 
For each spatio-temporal block, we create a boolean on whether or not a crime happened. This is our target variable.
A rich exploratory data analysis is performed, among others, studying the most common crimes and analyzing the crime distribution by neighborhood.
We use random forests to predict class probabilities (probability that crime will happen). 


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
- We choose to predict crime in the `Central Business District` as it has by far the highest amount of reported crimes.
- Random Forest with the best parameters yields the following scores on the test set:
    - AUC: 0.722
    - Balanced accuracy: 0.653
    - Accuracy: 0.735
    - Recall: 0.488
    - Average precision: 0.362
    - Specificity: 0.819
- The dissemination block is the most important feature. Season and weekday seem not to be important.



#### Next Steps
In the future, we plan to:
- use time series analysis to determine long-term changes and seasonal components of crime
- incorporate the location of [police stations](https://vpd.ca/community/community-policing-centres/)
- analyze the relationship between demographic, social, and economic neighborhood characteristics and the spatial distribution of crime
- apply the [Cynet model](https://pypi.org/project/cynet/)



#### Outline of Project
- [predict_crimes_Vancouver.ipynb](https://github.com/jessi88/crimes/blob/main/predict_crimes_Vancouver.ipynb)



##### Contact and Further Information
jessica.bosch88@gmail.com
