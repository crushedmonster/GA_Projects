# Project 4: West Nile Virus Prediction

###### Authors: Catherine Ang, Mei Lian, Wenna Loo

---

### Background
West Nile virus is most commonly spread to humans through infected mosquitos. Around 20% of people who become infected with the virus develop symptoms ranging from a persistent fever, to serious neurological illnesses that can result in death. In 2002, the first human cases of West Nile virus were reported in Chicago. By 2004 the City of Chicago and CDPH had established a comprehensive surveillance and control program that is still in effect today. Every week from late spring through the fall, mosquitos in traps across the city are tested for the virus. The results of these tests influence when and where the city will spray airborne pesticides to control adult mosquito populations.

---

### Problem Statement
As part of the newly hired data science team working in the division of Societal Cures In Epidemiology and New Creative Engineering (DATA-SCIENCE), we have been tasked to use the mosquito population data collected by the Chicago Department of Public Health (CDPH) to build a model that predicts outbreaks of the West Nile virus. Specifically, our model will use a combination of weather, time, and location features to predict the presence of West Nile virus within mosquito traps set up throughout Chicago. This will help the City of Chicago and CDPH more efficiently and effectively allocate resources towards preventing the transmission of this potentially deadly virus.

---

### Summary 

This project can be identified as a supervised learning task, since the labels are provided (the expected output, i.e., binary representation of whether West Nile Virus was present within mosquito traps). It is also a classification task, since we are predicting a discrete class label. More specifically, this is a binary classification problem, since the ultimate goal is to build a classifier to distinguish between just two classes, whether West Nile Virus was present in these mosquitos. 1 means WNV is present, and 0 means not present. 

The data collected include:
1. Mosquito trap data collected by the surveillance and control system
2. Location data of spraying efforts
3. Weather data

There are a total of two notebooks in this project, namely:
1. [Data Cleaning and Exploratory Data Analysis](/codes/01_Data_Cleaning_and_EDA.ipynb)
2. [Feature Engineering, Modelling and Cost Benefit Analysis](/codes/02_Feature_Engineering_Modelling_Cost_Benefit.ipynb)

---

### Contents
1. Datasets used
2. Data Cleaning and Exploratory Data Analysis
3. Feature Engineering and Modelling
4. Evaluation of Models
5. Cost Benefit Analysis
6. Conclusion and Recommendations
7. Limitations and Further Exploration
8. Python Library Used
 
#### 1. Datasets used
The datasets used for analysis in this project are:
- [`train.csv`](/datasets/train.csv), [`test.csv`](/datasets/test.csv): the training and test set of the main dataset. The training set consists of data from 2007, 2009, 2011, and 2013, while in the test set we are requested to predict the test results for 2008, 2010, 2012, and 2014.
- [`spray.csv`](/datasets/spray.csv): GIS data of spraying efforts in 2011 and 2013
- [`weather.csv`](/datasets/weather.csv): weather data from 2007 to 2014. 

##### Data Dictionary

| Feature | Type | Dataset | Description  |
|:--------|:----:|:-------:|:-------------|
| **Id** | *integer* | test | The id of the record |
| **Date** | *datetime* | train/ test | Date that the WNV test is performed (YYYY-MM-DD)|
| **Address** | *object* | train/ test | Approximate trap address retrieved from GeoCoder |
| **Species** | *object* | train/ test | The species of mosquitos |
| **Block** | *integer* | train/ test | Block number of address |
| **Street** | *object* | train/ test | Street name |
| **Trap** | *object* | train/ test | Id of the trap |
| **AddressNumberAndStreet** | *object* | train/ test | Approximate address returned from GeoCoder |
| **Latitude** | *float* | train/ test | Latitude returned from GeoCoder |
| **Longitude** | *float* | train/ test | Longitude returned from GeoCoder |
| **AddressAccuracy** | *integer* | train/ test | Accuracy returned from GeoCoder |
| **NumMosquitos** | *integer* | train | Number of mosquitoes caught in this trap |
| **WnvPresent** | *integer* | train | Whether West Nile Virus was present in these mosquitos (1 = present; 0 = absent) |
| **Date** | *datetime* | spray | The date of the spray (YYYY-MM-DD)|
| **Time** | *object* | spray | The time of the spray |
| **Latitude** | *float* | spray | The latitude of the spray |
| **Longitude** | *float* | spray | The longitude of the spray |
| **Station** | *integer* | weather | Weather station (1 or 2) |
| **Date** | *datetime* | weather | Date of measurement (YYYY-MM-DD)|
| **Tmax** | *integer* | weather | Maximum daily temperature (in Degrees Fahrenheit, F) |
| **Tmin** | *integer* | weather | Minimum daily temperature (in Degrees Fahrenheit, F) |
| **Tavg** | *object* | weather | Average daily temperature (in Degrees Fahrenheit, F) |
| **Depart** | *object* | weather | Departure from normal temperature (in Degrees Fahrenheit, F) |
| **DewPoint** | *integer* | weather | Average Dew Point temperature (in Degrees Fahrenheit, F) |
| **WetBulb** | *object* | weather | Average Wet Bulb temperature (in Degrees Fahrenheit, F) |
| **Heat** | *object* | weather | Heating Degree Days (season begins with July) |
| **Cool** | *object* | weather | Cooling Degree Days (season begins with January) |
| **Sunrise** | *object* | weather | Time of sunrise (calculated) |
| **Sunset** | *object* | weather | Time of sunset (calculated) |
| **CodeSum** | *object* | weather | Code of significant weather phenomena |
| **Depth** | *object* | weather | Snow/ice depth on the ground in inches, measured at 1200 UTC |
| **Water1** | *object* | weather | Water equivalent in inches, measured at 1800 UTC |
| **SnowFall** | *object* | weather | Total snowfall precipitation for the day (in inches and tenths) |
| **PrecipTotal** | *object* | weather | Total water equivalent precipitation for the day (in inches and tenths).  |
| **StnPressure** | *object* | weather | Average station pressure (in inches of hg) |
| **SeaLevel** | *object* | weather | Average sea level pressure (in inches of hg) |
| **ResultSpeed** | *float* | weather | Resultant wind speed (mph) |
| **ResultDir** | *integer* | weather | Resultant wind direction (degrees) |
| **AvgSpeed** | *object* | weather | Average wind speed (mph) | 

#### 2. Data Cleaning and Exploratory Data Analysis
In this section, we will look into the datasets provided, specifically:

- Analyzing the train and test data, and dropping features not required. 
- Analyzing the spray data, and understanding its trend. 
- Analyzing the weather data, and dropping features not required. 

We observe that not all species carry West Nile virus - CULEX PIPIENS and CULEX RESTUANS species are the two main carriers of WNV, and they comprise 99.5% of the mosquitos captured in the traps. 

Additionally, there is an increasing prevalence of WNV during summer - an increasing trend from June, July till it peaks in August, before declining slightly in September. 

Lastly, while traps have been placed across Chicago, not all hot-spots (i.e. WNV outbreak locations) have traps set up thoroughly.

#### 3. Feature Engineering and Modelling
For this section, we look at creating new features, such as humidity and time-lagged features for the more prominent weather conditions. In addition, we have predicted the number of mosquitos in the test dataset (since this information is missing in the previous test table). 

For the modelling, several classifier models have been developed. As there are huge imbalances in the data collected (i.e. 95% of the data indicates an absence of WNV), an over-sampling method known as SMOTE (Synthetic Minority Over-sampling Technique) is adopted.  

The models used include:
- Logistic Regression
- K-Neighbors Classifier
- Random Forest Classifier
- ExtraTrees Classifier
- AdaBoost Classifier
- Gradient Boosting Classifier

#### 4. Evaluation of Models
The evaluation metrics used include:
- Accuracy score
- ROC-AUC score
- Recall
- Precision
- F1-Score

As the dataset is heavily imbalanced, we have optimized the model further with ROC AUC score, instead of purely Accuracy score. Comparing the AUC and recall scores, the final model selected is the Gradient Boosting Classifier model. While there's a slight overfitting of the data while comparing the train and test accuracy scores, the difference is acceptable. 

#### 5. Cost Benefit Analysis
In this section, we explored the cost/benefit by looking at the threshold of the probability of the predicted output that West Nile Virus=1, the confusion matrix and the respective cost for each of them.

Varying the threshold level would affect the expected cost/benefit. The best threshold level is at 0.33 which will generate savings of $7,363.

#### 6. Conclusion and Recommendations
From our modelling, we have learnt that features such as the number of mosquitos, duration of the Sun, species type and total precipitation are strong predictors of the presence of WNV. With a ROC AUC score of 0.8343, we are confident that our model, which employs the use of Gradient Boosting Classifier, is capable of predicting outbreaks of West Nile virus. 

From our cost benefit analysis, we would recommend CDPH to ramp up on its spraying efforts, considering a threshold value of 0.33 to minimise the probability of its people contracting WNV while maintaining a balance between the spray cost and maximising the expected benefit. For a start, CDPH can focus on regions in the northern part of Chicago, particularly areas near water bodies.

#### 7. Limitations and Further Exploration
While we have employed the SMOTE technique to deal with the imbalanced data - which is capable of mitigating the problem of overfitting caused by random oversampling), one of its downside is that it does not take into consideration neighboring examples from other classes, which may result in an increase in overlapping of classes and thus introducing additional noises. In addition, the dataset is limited to just 2007 to 2014 information, and there are only two years of spraying information. 

Some further explorations include: 
- Employing bagging-based or boosting-based techniques for handling imbalanced data;
- Gathering additional years of pesticides spraying data to examine the effectiveness of the spray;
- Looking into more recent years of trap, weather and spray information (from 2014 onwards);
- Looking at the interaction between temperature and humidity on the growth of mosquitos.


#### 8. Python Library Used
- Pandas
- Numpy
- Seaborn
- Matplotlib
- Sklearn
- Imblearn
- Datetime
- Geopy
