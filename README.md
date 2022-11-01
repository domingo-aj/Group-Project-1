# Group-Project-1
# Start date: 10/23/2022
**DATA EXPLORATION**

**Flight Data**

In order to analyze flight cancellations, a fortunately rare occurrence, we would need information about LOTS of flights. Thankfully, a very large free dataset was found on kaggle.com.

<img width="499" alt="Screen Shot 2022-11-01 at 12 43 04 PM" src="https://user-images.githubusercontent.com/112193116/199294365-09671513-78ff-4172-bac1-c50ae734d2fa.png">

At over 2GBs, the dataset appeared to have every domestic US flight from 2009 - 2018, and had all the information that one could reasonably expect such as expected time of departure/landing, cancellation reason, delay times, etc. There were, however, two issues with this dataset.
The first issue is that while the data has cancellation codes that determine between weather, airline issues, security delays, etc. there is no way to tell which airport caused the cancellation. That is to say, if a flight was weather-cancelled, one could not determine if it was cancelled because there was a storm at the origin airport, or the destination airport. For this reason, we would not be able to link each flight to a specific weather palette.
The second issue has to do with the size of the dataset. As a team, we needed to be able to share our clean filtered data through GitHub. This is not possible with 2GBs. In addition, making api calls for tens of millions of rows of data was not an option.
To answer both of these issues required us to greatly change our strategy. Instead of attempting to link each flight to a particular weather palette, we instead would focus on USA’s 5 largest airports, and group flights and weather palettes by month for the latest 4 years of the dataset. The filtered data focused on the 5 largest airports parsed by year was still a large set of data with millions of rows, but it was just small enough that it could be shared on GitHub.

**Location Data**

When the project was first started, it was thought that we would use data from hundreds of airports across the United States, and that all we had was 3-letter codes. Those 3-letter airport codes would need to be translated into coordinates for calling weather data. To this end, a dataset of airport location data was retrieved from www.partow.net. GAD to csv.ipynb takes care to translate the data from a text file to a csv. This data was then used to manually create a new easy-to-read Airport_Data.csv using Microsoft Excel. Ultimately though, because we decided to only go with the 5 largest airports, this whole process could have been done in a few google maps searches. 

**Weather Data**

For the weather data, we had a few API options. At first, we believed that weatherapi.com would be the way to go because the entire team had experience with this API. We assumed that we would have no problems getting the data we needed and went about getting all of the flight and location data tidied up and ready to get weather data for every single flight. A few days into the project however, one team member noticed that weatherapi.com’s free version does not allow calls for historical weather data, only current data.On top of that, for the amount of flights we had data for, even a professional account didn’t have that many API calls.

<img width="232" alt="image (2)" src="https://user-images.githubusercontent.com/112193116/199294361-681f0ac1-4e80-4331-8ef3-6003bff1928f.png">

On the other hand, visualcrossing allows for historical weather data for free. As described above, the team’s strategy changed a few days in and we decided to get information for days rather than each individual flight. For this amount of data, the team was able to pool our free API calls together and get all of the needed information.

# SUMMARY TABLES

After our data exploration and cleaning, we merged weather data from VISUAL CROSSING WEATHER | API and flight data from Airline Delay and Cancellation Data, 2009 - 2018 | Kaggle into a new dataframe on the columns of “Date” and “Airport”. This allowed us to align the weather specific to the airport and flight cancellation date.

![combined_flight_weather_data](https://user-images.githubusercontent.com/112193116/199295029-47905b87-2aab-46cf-a695-702913127f8e.png)

![cancelled_flight_weatherdata](https://user-images.githubusercontent.com/112193116/199295026-06bcad8f-37f9-4155-9982-9f462900a442.png)

![monthly_averages_data1](https://user-images.githubusercontent.com/112193116/199295032-c7a3f689-9ead-4d4c-b6ea-3b8aaea17347.png)

![monthly_averages_data2](https://user-images.githubusercontent.com/112193116/199295034-57cc5d91-e2a7-4186-852c-6cfd9023280b.png)

# LOCATION

**Heatmap Weighted by Cancellation Numbers**

The map presented below shows the number of cancellations in each airport.

![Cancel_heatmap](https://user-images.githubusercontent.com/112193116/199296102-10d1078b-f85f-4842-93ba-f0828d7252f3.png)

**Heatmap Weighted by Canceled and Non-Cancelled Numbers**

The map presented below shows the number of canceled,non-cancelled and total flights in each airport.The inner circle at each airport is weighted by the total canceled flights and the outer rectangle is weighted by the total non-cancelled flights.

![cancel_noncancel_heatmap](https://user-images.githubusercontent.com/112193116/199296106-c7494123-6457-4caf-b69e-165b3ac909fc.png)

**Flight Cancellations by Airport**

The sample data below reflects the percentage of flight cancellations caused by weather factors for five major US airports. The percentage of cancellations is greatest in Chicago (ORD) compared to other airports at 33.8% of all sample data retrieved. 

**Total Canceled Flights:**

ORD: 13,418 Flight Cancellations

LAX: 2,372 Flight Cancellations

DFW: 10,181 Flight Cancellations

DEN: 5,989 Flight Cancellations

ATL: 7,701 Flight Cancellations

![percent_cancel_airport](https://user-images.githubusercontent.com/112193116/199296279-17393bee-74de-4d9f-84ae-90789551b048.png)

# PRECIPITATION 

**Avg. Precipitation (in) by # Monthly Cancellations**

1.Visibility is a critical factor in flight safety. If the precipitation is too heavy, then the pilot’s visibility can be impaired. When the amount of precipitation (in) is too high, it is too dangerous to takeoff, resulting in a flight cancellation.

2.There was an increased # in monthly flight cancellations when the avg. precipitation was low, between 0.0 - 1.0 (in). 

3.The regressions line and the r-value indicate that precipitation was not a significant factor in the number of monthly flight cancellations. From the sampled data, we fail to reject the null hypothesis. Therefore, precipitation will result in no impact on flight cancellations.

4.The correlation between both factors is -0.04

5.The r-squared is: 0.001249106831586809

**Average Precipitation vs. Total Cancellations by Month**

The chart shows the average precipitation in comparison to the total canceled flights by month for the sample data set. The number of cancellations per month from January 2015 to December 2018 shows consistent spikes during the month January across all years. The average precipitation (in) from January 2015 to December 2018 shows a relatively consistent range falling between 0 - 1.0 (in) with the exception of spikes above 2 inches between July - December of 2015 and March to August of 2017.

**Cancellations Due to Precipitation**

The sample data below reflects the breakdown of precipitation types (Rain, snow, rain/snow) that caused cancellations for five major US airports. The precipitation type that caused the greatest amount of flight cancellations in the sample data was rain at 52.7%, followed by rain/snow at 30.4%.

Precipitation type and the canceled numbers.

Rain: 14,592
Rain + Snow: 8,420
Snow: 4,676

# TEMPERATURE

**Avg. Max Temp (F) by Avg. Precipitation (In)**

As the average max temperature (F) increased, the average precipitation (In) increased. 

1.The correlation between both factors is 0.23

2.The r-squared is: 0.053597775234979474

3.The regressions line and the r-value indicate that there is a relationship between average max temp (F) and avg. precipitation (In). 

**Avg. Max Temp (F) by Monthly Cancellations**

1.The correlation between both factors is -0.52

2.The r-squared is: 0.26932427288672406

3.During warmer weather, there were less total canceled flights by month. From the sampled data, we can reject the null hypothesis. Therefore, average maximum temperature will result in an impact on monthly flight cancellations.

**Average Temperature vs Total Cancellations by Month**

The chart shows the average maximum temperature in comparison to the total canceled flights by month for the sample data set. The number of cancellations per month from January 2015 to December 2018 shows consistent spikes during the month January across all years. The average temp (F) from the sample data set peaks each year in July at approximately ~85 (F).

# WIND SPEED

**Avg. Wind Speed (mph) by Monthly Cancellations**

1.There were more months with flight cancellations when the average wind speed was between 15 mph and 20 mph.  As wind speed increased, the number of monthly canceled flights decreased.

2.The regressions line and the r-value indicate that avg. wind speed was not a significant factor in the number of monthly flight cancellations. From the sampled data, we fail to reject the null hypothesis. Therefore, wind speed will result in no impact on flight cancellations.

3.The correlation between both factors is 0.07

4.The r-squared is: 0.005518412470719093

**Average Wind Speed vs Total Cancellations by Month**

The chart shows the average wind speed (mph) in comparison to the total canceled flights by month for the sample data set. The number of cancellations per month from January 2015 to December 2018 shows consistent spikes during the month January across all years. The average wind speed (mph) from the sample data shows no correlation. 

# TIME

**Cancellation Number by Months For Each Year**

The below line graph shows the flight cancellation numbers along the months of the years (2015-2018). From the graph,the cancellations seem to be very high in the month of Feb (2015).

**Cancellation / Non-Cancellation Numbers by Months For Each Year**

Over the course of January 2015 - December 2018, there were a few instances in which canceled flights outnumbered non-cancelled flights. The below graph shows both the trends of cancellation and non-cancellations throughout the months of the year.

**Weather Flight Cancellations From 2015 - 2018**

The below bar chart indicates the cancellations across the years of 2015-2018 from the sample data set. 2015 had the highest number of weather-specific flight cancellations at 34% compared to other years. 

2015 Canceled Flights: 13,503

2016 Canceled Flights: 7,434

2017 Canceled Flights: 8,591

2018 Canceled Flights: 10,133

**Heatmap Calendar 5 Top US Airport Weather Cancellations by Day**

This heat map displays volume of weather related cancellations over the course of a calendar year and broken down by day. Overall, we can see the lower concentrations of cancellations are in the summer, and a higher concentration of cancellations in the earlier part of the year (Jan - Mar). To investigate if there are more weather-related cancellations in different areas, we zoom in on each airport.

**DFW Cancellation Calendar Heatmap**

The heatmap calendar for DFW, a centrally located southern airport, we see higher concentrations of weather related cancellations in the winter months (Dec - Feb). Max cancellations for one day at DFW across 2015-2018 is 480.

**ATL Cancellation Calendar Heatmap**

 The heatmap calendar for ATL, we can observe concentrations of weather related cancellations in December and January. Max cancellations for one day at ATL across 2015-2018 is 536.
 
**DEN Cancellation Calendar Heatmap**

The heatmap calendar for DEN, we can observe concentrations of weather related cancellations in December and January. Max cancellations for one day at DEN across 2015-2018 is 596.

**ORD Cancellation Calendar Heatmap**

The heatmap calendar for ORD, we can observe concentrations of weather related cancellations between the months of Nov-Jan. Max cancellations for one day at ORD across 2015-2018 is 505.

**LAX Cancellation Calendar Heatmap**

The heatmap calendar for LAX shows the lowest numbers of weather related cancellations, we can observe concentrations of cancellations between the months of Dec-Mar. However, the max cancellations for one day at LAX across 2015-2018 is 53, showing that LAX experiences the least amount of weather related cancellations by day.

# Chi-Square Test on Flight Cancellations from Weather

Since the chi-square value of 12603.59 at a confidence level of 95% exceeds the critical value of 62.83, we conclude that the differences seen in the number of cancellations by months of year are statistically significant.












