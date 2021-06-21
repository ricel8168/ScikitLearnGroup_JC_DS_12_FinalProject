# Bike Sharing in Washington DC using Machine Learning

ScikitLearnGroup_JC_DS_12_FinalProject

Member :
- Ibnu Yusuf Prakoso (iyp36@hotmail.com)
- Kevin Octavio Untoro (kevinoctavio.u@gmail.com)
- Kelvin Lois (kelvinnlois@gmail.com)

Dataset taken from : [Bike Sharing in Washington D.C. Dataset](https://www.kaggle.com/marklvl/bike-sharing-dataset)

### Background

Bike sharing systems are a new generation of traditional bike rentals where the whole process from membership, rental and return back has become automatic. Through these systems, user is able to easily rent a bike from a particular position and return back to another position. Currently, there are about over 500 bike-sharing programs around the world which are composed of over 500 thousands bicycles. Today, there exists great interest in these systems due to their important role in traffic, environmental and health issues.

Apart from interesting real-world applications of bike sharing systems, the characteristics of data being generated by these systems make them attractive for the research. Opposed to other transport services such as bus or subway, the duration of travel, departure and arrival position is explicitly recorded in these systems. This feature turns bike sharing system into a virtual sensor network that can be used for sensing mobility in the city. Hence, it is expected that most of important events in the city could be detected via monitoring these data.

This dataset contains the hourly and daily count of rental bikes between years 2011 and 2012 in Capital bikeshare system in Washington, DC with the corresponding weather and seasonal information.

Dataset Characteristic

- instant: Record index
- dteday: Date
- season: Season (1:winter, 2:spring, 3:summer, 4:fall)
- yr: Year (0: 2011, 1:2012)
- mnth: Month (1 to 12)
- hr: Hour (0 to 23)
- holiday: whether day is holiday or not (extracted from Holiday Schedule)
- weekday: Day of the week
- workingday: If day is neither weekend nor holiday is 1, otherwise is 0.
- weathersit: (extracted from Freemeteo)
    - 1: Clear, Few clouds, Partly cloudy, Partly cloudy
    - 2: Mist + Cloudy, Mist + Broken clouds, Mist + Few clouds, Mist
    - 3: Light Snow, Light Rain + Thunderstorm + Scattered clouds, Light Rain + Scattered clouds
    - 4: Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog
- temp: Normalized temperature in Celsius. The values are derived via (t-tmin)/(tmax-tmin), tmin=-8, t_max=+39 (only in hourly scale)
- atemp: Normalized feeling temperature in Celsius. The values are derived via (t-tmin)/(tmax-tmin), tmin=-16, t_max=+50 (only in hourly scale)
- hum: Normalized humidity. The values are divided to 100 (max)
- windspeed: Normalized wind speed. The values are divided to 67 (max)
- casual: count of casual users
- registered: count of registered users
- cnt: count of total rental bikes including both casual and registered



### Introduction

Nowadays Bike Sharing Systems are growing rapidly, the demand of using the systems are also Increasing. Eventually the volume of Bike Sharing Systems are fluctuating from time to time(e.g. Changing hourly, weekly, monthly, and yearly), therefore the maintenance schedule need to be structured and dynamic. The Maintenance Scheduled is adjusted to the trend of the volume of bicycle use, is expected to maximize the life of the bicycle, minimize customer loss due to a shortage of bicycle stock in the field when demand for bicycles is high and maximize income if the demand for bicycle use can always be met, as well as cost efficient.

### Problems

- Bad Maintenance Schedule can affect the lifespan of Bicycles and could increase potential loss of customers (Bike maintenance are related to stock management, since the bicycles are being withdrawn to go under maintenance). When there are many bicycles that must be repaired simultaneously, it indirectly reduces the stock of bicycles in the field and becomes a potential loss of customers).
- The volume of bicycle use in certain seasons (_winter_) is relatively smaller than in other seasons.
- What does the company need to do when there's "SPIKE" in Bike Sharing Demand ?

### Goals

- Creating a Prediction for Bike Sharing Demand (minimum and maximum) to reduce number of customer loss, reduce cost efficiency and predict how many bikes need to be placed in each station each day.
- Creating an efficient Maintenance Schedule to prevent customer loss

### Data Cleaning & Pre - Processing

- Checking Missing Value
    - ![Missing Value](https://github.com/PurwadhikaDev/ScikitLearnGroup_JC_DS_12_FinalProject/blob/main/SS/missing%20value.jpeg)
    
- Checking Outliers
    - ![Outliers Box Plot](https://github.com/PurwadhikaDev/ScikitLearnGroup_JC_DS_12_FinalProject/blob/main/SS/outliers%20boxplot.jpeg)
    - ![Outliers Tabular](https://github.com/PurwadhikaDev/ScikitLearnGroup_JC_DS_12_FinalProject/blob/main/SS/outliers%20tabular.jpeg)

- Pre-processing
    - Creating new Columns to separate the Outliers with the original data. To check whether these Outliers affect the original data.
    - Re-scaling (for Exploratory Data Analysis purpose) certain Variables such as:
        - temp (Temperature)
        - atemp (Feels like - Temperature)
        - Humidity
        - Windspeed
     - Change the Name for the Variable:
         - Season
         - Month
         - Year
         - Holiday
         - Workingday
         - Weathersit
         
### Quick Data Analysis

- From the analysis we get, people in Washington, D.C. are more likely to cycle when the temperature conditions are warm with a temperature range of 20-30s degrees Celsius, it can be interpreted that it is the ideal temperature. Because the average temperature in Washington DC is 17 degrees Celsius.

- Bicycle rental tends to be more crowded on weekdays (Monday - Friday) at 8 and 17 because they are used to go to and from work.
- During the weekend (Saturday and Sunday) bicycle rental is crowded at 13.00 because it is used for recreation.
- Weathersit Clear is the condition in which Washington D.C. residents rent the most bicycles. With an average of 205 bikes per hour.
- In June, July, August are the months that have the Summer season which has the highest temperature among all months of the year. Thus the number of people who rent bicycles in the Summer season is the highest compared to other seasons. With an average of 236 bicycles per hour.
- Between 2011 and 2012, the most bicycle rentals occurred in 2012. Which has increase **64.87%%**) from 2011

- [Full Data Analysis](https://github.com/PurwadhikaDev/ScikitLearnGroup_JC_DS_12_FinalProject/blob/main/Exploratory%20Data%20Analysis%20-%20Bike%20Sharing.ipynb)

### Machine Learning Regression

Machine Learning Regression is made to predict the number of bicycle stocks provided every day. Target Scoring is R-Squared, Median Absolute Error and Residual Negative. The higher the R-Squared value, the smaller the Median Absolute Error obtained.

Feature Selection is performed on Variables:
    - temp
        - Already represented with atemp variable variable
    - dteday
        - Already extracted into Year, Month, Day, Hour features
    - casual
    - registered
        - casual and registered dropped because the target model used is the variable **cnt** which is the sum of **casual** data and **registered** data.

- The Best Base Models:
    - Decision Tree Regressor
    - Random Forest Regressor
    - XGBoost Regressor
    
- Hyperparameter Tuning:
     - Decision Tree Regressor
         - best.params: 'max_depth' : [15], 'max_features' : None, 'min_samples_leaf' : [2], 'min_samples_split' : [12]
    - Random Forest Regressor
        - best.params: 'n_estimators' : [2280], 'max_depth' : [81], 'max_features' : ['None'], 'min_samples_leaf' : [1], 'min_samples_split' : [4]
    - XGBoost Regressor
        - best.params: 'learning_rate' : [0.1], 'max_depth' : [6], 'n_estimators' : [1300]
   

Evaluation Matrix Table
- ![Eva Matrix](https://github.com/PurwadhikaDev/ScikitLearnGroup_JC_DS_12_FinalProject/blob/main/SS/Compare.png)

### Machine Learning Insight

Based on the Evaluation Matrix above, discovered that there are five Machine Learning Models that meet the criteria for Bike Sharing Prediction. With a scoring basis of R-Squared, M(ed)AE, and Residual Negative
- `Base DecisionTree` have the best Residual Negative score, but it's Overfitting. 
- `DecisionTree Tuned Grid 2` have the 2nd best Residual Negative score right after `Base DecisionTree`, but it's MedAE & R-Squared are not good enough.
- `Base RandomForest`, `RandomForest Tuned Bayes` and `RandomForest Tuned Random` have similar Evaluation Matrix score.

[Full Machine Learning](https://github.com/PurwadhikaDev/ScikitLearnGroup_JC_DS_12_FinalProject/blob/main/Machine%20Learning%20-%20Bike%20Sharing.ipynb)

### Conclusion

Best model that we choose is **RandomForest Tuned Random**, because it’s R-Squared is 94.99, it’s MedAE is lower than the average of all MedAE and Residual Negative is 52.95%.

- For Bike Maintenance Schedule, you can use several options/sequences:
    - Daily Light maintenance can be done at 4 am.
        - Example: Checking for Leaky Tires.        
    - Weekly Maintenance is carried out on Sundays at 5 am
        - Example: Chain Lubrication & Brake Cable checking
    - Not recommended to do Maintenance on Monthly Basis 
        - Resulting in many bicycles that must be in maintenance at once.
    - Do a Check in advance on the maintenance day to avoid Customer Loss.
        - There is an event on the day of maintenance.    
    - Equalizing Bike Maintenance Schedule with Bike Storing-Pickup Schedule where excess bicycle stock on field/station is picked up for storage in the Warehouse.
    
- There needs to be an efficient Bicycle Stock management every day such as:
     - Provide more Bikes on Working Day
     - Bike Storing Efficiency
         - To store Bikes when there's low demand to prevent damage to the bicycle itself.

### Future Works & Improvement

To conclude, We understand that Our Machine Learning Prediction on this Project  is not perfect. Because there’s several factors that can improve Our Model Prediction such as:
- Cost/Sales of the Bike Rent
- Duration of Bike Usage
- Distance of Bike Usage
- Numbers of Bike Station and their Specific Location
- Performance Metrics can be modified to be more relevant with business problem.

   
