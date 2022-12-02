# Weather_Crime_relationship



## Data Set

- weather data set : daily weather data set in Chicago from 2001.01.01. ~ 2018.12.31.
https://www.visualcrossing.com/weather/weather-data-services

- crime data set : crime data set in Chicago from 2001.01.01. to present
https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2/data


### 1. Introduction
The earth is getting hotter. Compared to 1850, the average global surface temperature rose by more than one degree.
If the current average temperature increase rate on Earth is maintained, the frequency and intensity of heat waves in many areas will increase.

Temperature and humidity increase, something that increases together. It's a crime.
The five major crimes in Daegu (2019) > about 20% of all crimes
It's not just Korea.
In 1988, when the record-breaking heat wave hit the U.S. > many crimes across the U.S.

High temperatures can make people feel bad and harm others. 
In addition, there was also a study that showed that each crime was related to other meteorological factors. 
(Violent crimes and sex crimes: temperature, Domestic violence: humidity)

Therefore, we decided on a topic and confirmed the relationship between weather and crime.


### 2. import weather data, crime data
We need enough data to determine the relationship between weather and crime.
So we analyze Chicago, which has such a high crime rate that it is called the "city of crime," as an area.
![image](https://user-images.githubusercontent.com/46551994/205298659-e2aa860e-6456-497e-8c11-46cc331a7466.png)

In the crime dataset, we can get the type of crime, date, arrest, location, etc.

In the weather dataset, we can obtain various weather information such as temperature, sensory temperature, precipitation, humidity, wind speed, sloar energy.


### 3. crime data visualization(EDA)
By month, the crime rate is higher in summer than in other months.
![image](https://user-images.githubusercontent.com/46551994/205298121-e2be8a93-f5df-4f51-a20b-0367f93d8f63.png)

On a daily basis, the crime rate fell at the end of the month and the highest crime rate occurred on the first day.
![image](https://user-images.githubusercontent.com/46551994/205298425-2e2dbbf7-3738-4ab2-ba66-a4f7644b3cbb.png)

There was no significant difference by day of the week, but on average, Friday was slightly higher and Sunday was slightly lower.
![image](https://user-images.githubusercontent.com/46551994/205298460-3dabe117-2ec7-4dc4-9f4d-d97470006014.png)

Lastly, looking at the crime rate by hour, the lowest in the morning and the highest in the afternoon.
![image](https://user-images.githubusercontent.com/46551994/205298497-bf2be884-5113-4ca3-9eff-c4a85005bdcb.png)


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
For Time series analysis, we did two kind of things.
First, we trained regression model with ols, and drew scatter plot based on the prediction of the model.
With this, we can get similar effect as if we conduct time series analysis. As a result, we can visualize the future trend of certain type of crime's severity.
And we also actually did the time series analysis with the ARIMA library.
To determine the parameters which are used in ARIMA model, several tests like Augmented Dicky-Fuller test are done and drew ACF and PACF graph.

### 7. Conclusion
Within weather data set, temperature and solar energy showed significant relationship with crimes.
However, in the case of solar energy, it is obvious that the crime occurs more often after sunset, so we conclude that only temperature has significant relationship with crimes.
According to prior study, certain crime type has high relationship with temperature and humidity.
But according to our analysis, almost every type of crime has high correlation whit temperature, not humidity.
We concluded that this is because climate difference between korea and chicago.
If add some additional features like age, gender and educational background, which are known as relevant with crime, more significant conclusion can be expected.
Also, we expect that this analysis can help a national security agency or private security service to assign their attentions and resources everyday.
