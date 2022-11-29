# Weather_Crime_relationship



## Data Set

- weather data set : daily weather data set in Chicago from 2001.01.01. ~ 2018.12.31.
https://www.visualcrossing.com/weather/weather-data-services

- crime data set : crime data set in Chicago from 2001.01.01. to present
https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2/data


### 1. Introduction


### 2. import weather data, crime data


### 3. crime data visualization(EDA)


### 4. preprocessing(merge crime data and weather data, Handling Missing values, Outliers, Normalization)
#### merge crime data and weather data

First, classify crimes according to the type of crime, then crimes caused on the same date are grouped into each array. make their index as each date.
After that, based on the date index, combine existing daily weather data with new crime arrays.
As a result, two data sets were combined, 
each column shows a weather element and a crime type, meaning that each row occurred at the same time.

#### Handling Missing values, Outliers, Normalization

There are missing values exist in both weather and crime elements.
The missing value of ‘solar energy’, Most of them occurs at night when the sun sets. Therefore, we filled in the missing values with ‘0’.
Missing value of crime data means that the incident did not happen at that time. So this is also replaceable with ‘0’, too.

Outlier data is an unnecessary element that reduces the performance of the model, so it must be removed.
To handling outliers, multiply each IQR by 1.5 to add the value at 75% points and subtract it from the value at 25% points to determine the minimum.
A value greater than or less than the determined maximum and minimum is considered an outlier, delete them.


### 5. correlation analysis (+ delete some worthless columns)

In correlation analysis, we can find all correlations between each column.
But there are so many columns, which includes useless, unnecessary one. So we can drop some columns that have lower correlation between -0.3 to 0.3.
Also, 'feelslike' columns has very high correlation (almost 1) with ‘temp’ column, so drop it, too.
After adjusting some columns, you can see most crimes take place at night when there’s no ‘solar energy’
And only ‘THEFT’ ’BATTERY” ’CRIMINAL DAMAGE” ‘ASSAULT’ column have high correlation, more than 0.3, with temperature. Other weather columns did not show the significant correlations with crime datas.


### 6. Time Series Analysis and Forecast (With scatter plot from data with ols, with ARIMA library)


### 7. Conclusion
