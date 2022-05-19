
## Case Study: Cyclistic Bike Share Analysis
#### Author: [@Farzal Khan](https://www.linkedin.com/in/farzalkhan)


![App Screenshot](https://www.spaceotechnologies.com/wp-content/uploads/2018/09/bike-sharing-system.jpg)
## About the company
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that
are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and
returned to any other station in the system anytime.

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments.
One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes,
and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers
who purchase annual memberships are Cyclistic members.

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the
pricing flexibility helps Cyclistic attract more customers, Moreno believes that maximizing the number of annual members will
be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a
very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic
program and have chosen Cyclistic for their mobility needs

## Business Task

The goal of this case study is to provide clear insights for designing marketing strategies aimed at converting casual riders into annual members.  The expectation with me was to find out how the two riders, casual and member, use cyclistic bikes differently, and why would a casual rider buy a membership. Based on the insights the marketing team will design a marketing program.
       
## The Stakeholders

**Lily Moreno**: The director of marketing and my manager. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program.

**Cyclistic executive team**: A notoriously detail-oriented team which will decide whether to approve the recommended marketing program.

## Data Exploration

For this project, I have used **12 months** (Jan 2021 to Dec 2021) of data which is located in the [cyclistic database](https://divvy-tripdata.s3.amazonaws.com/index.html). I followed the guidelines according to the terms and conditions under [Data License Agreement](https://ride.divvybikes.com/data-license-agreement).

The data is unbiased, credible and  is organized as yearly, half-yearly, quarterly, and monthly. The data is reliable, original, and current as it is internally collected and stored safely by Cyclistic. The data is also comprehensive and it contained all the information required for descriptive analysis. Personally identifiable information such as credit card numbers has been removed because of data-privacy issues.

## Data Issues

The attributes provided were sufficient but not complete. It could have contained gender and age information as collected in the earlier dataset (2013-2019) which would help in gaining some additional insights. 

## Data Cleaning

Since the data is organized into 12 different worksheets, one for each month, I decided to use Microsoft Excel for monthly analysis and SQL for yearly analysis by using a union. Total number of records for the year 2021 turned out to be 5.5M which is out of scope of Microsoft Excel. For visualizing yearly statistics I used Tableau.

Steps taken for data cleaning

    1) Identified the source of error in ride_length column which turned out to be negative time values that gave !VALUE error. 
       I rectified the problem by using the MOD() function.

    2) 739170 of the station names and IDs out of 5.5M records are missing which constitutes 13.21% of the total records. 
       Suprisingly, the data missing was only for electric bikes. Since the geographical latitudes and longitudes are present 
       the nulls did not hinder the analysis.

    3) Around 4800 records of geographical latitudes and longitudes are missing, but since it constitutes less than 0.1% 
       of the total records it can be filtered out.

    3) Formatted the date and time correctly
    
    4) Removed extra spaces using the TRIM() function

    5) No duplicates were found using the DISTINCT() function

    6) No mismatched data was found 

    7) Data aligned perfectly with the business logic

## Data Transformation

Next, I seperated the date and time into individual columns using the text to column wizard and formatted accordingly.

I renamed the column 'member-casual' to 'rider_type' to specify the two rider types.

Additionally, I created 3 columns as follows:

    1) start_day_number: By using WEEKDAY() function on the date column
    2) start_day: By using TEXT() function on the start_day_number column
    3) ride_length: By subtracting start_time from end_time under the MOD() function

After performing the above mentioned steps I uploaded the 12 CSVs on the Microsoft SQL Server Management Studio and combined them using UNION ALL function in Transact-SQL. 

The free public version of Tableau could not be linked to SQl, so I exported the combined 12 months data into a CSV . Although the maximum number of records a CSV can process is 1048576, but it can store any number of records. The total turned out to be 5.5M which I uploaded onto Tableau as a text file.

After cleaning and tranforming the data into a proper format it was ready for analysis.

## Analyzing The Data

This part of the analysis aims at discovering any surprises, trends, or relationships, and as such, I created 3 pivot tables in each of the 12 CSVs to find out how the usage of annual member riders differ from that of the casual riders **over a  week**.

1) First table calculates the number of bikes leased by each rider type. The goal was to find out whether casual riders preferred certain days as compared to the member riders.

2) Second table calculates the average length of ride by each rider type. The goal here was to compare which rider type leased the bikes for longer periods on what days.

3) Third pivot table was created to determine whether casual or member riders preferred a certain bike type over others on certain days.

Grand totals of the respective pivot tables gave an idea about the total numbers over each month which was then pulled into a common pivot table for a yearly overview.

## Sharing The Analysis

### Ride Count
<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Total%20Ride%20Count.png" align="center" height="400" width="400" ></a> 

Total bikes leased in the year 2021 were 5.59M out of which 3.06M were leased by member riders and 2.52M by casual riders. Member rides and casual rides constitute 55% and 45% of the total respectively. The fact that the number of casual riders is significant supports the idea of converting casual riders to member riders instead of focusing on adding new member riders.

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Ride%20Count%20Distribution.png" align="center" height="600" width="900" ></a>

For casual riders, the number of bikes leased starts increasing from the month of february and peaks in the month of july. After that, the ride count starts decreasing and is lowest in the month of february.

For member riders, the number of bikes leased starts increasing from the month of february and peaks in the month of august/september. After that, the ride count starts decreasing and is lowest in the month of february.

It is observed that the number of rides leased by casual riders surpasses member riders in the months of june, july, and august. The reason I suspect is the increase in tourism in Chicago during this period. Also, the lowest number of rides are in the month of february for both casual and member riders, the reason might be freezing weather conditions. After carefully observing the monthly data, I found out that casual riders hire maximum number of bikes on weekends and member riders on weekdays in each month consistently. From the data it seems that member riders use the bikes for commute purposes which could be office/school/college.

### Ride Length

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Average%20Ride%20Length%20Total.png" align="center" height="400" width="400" ></a>

On average, casual riders spend approximately twice as much time on their bikes as compared to member riders, even though the number of rides leased by casual riders is 10% less than member riders. 

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Average%20Ride%20Length%20Distribution.png" align="center" height="600" width="900" ></a>

The average ride length for casual riders is comparable between february-may and starts declining further until january. It is observed that there is a significant increase in the average ride length for casual riders between january and february.

The average ride length for member riders is comparable between march-september and starts declining further until january. The increase in average ride length between january and february is moderate as compared to casual riders.

The average ride length for casual riders is higher than member riders throughtout the year. Also, it is observed that both casual and member riders ride for the longest periods on sundays.

### Ride Preference

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Ride%20Preference%20Total.png" align="center" height="600" width="900" ></a>

Both casual and member riders prefer classic bikes more than other bike types with docked bikes being the least preferred. Interestingly, docked bikes are almost used negligibly by member riders (only 1 in the whole year). The difference in classic bike usage of member and casual riders is considerable and that of electric bike usage is almost comparable.

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Casual%20Ride%20Preference.png" align="center" height="600" width="900" ></a>

Classic bike usage for casual riders starts increasing from february with the highest rise between may and june, and it peaks in the month of july. After that it starts declining with the largest drop between september and october.

Docked and electric bike usage for casual riders starts increasing from february with the highest rise between april and may, and it peaks in the month of july. After that it starts declining with the largest drop between october and november. Number of electric bike rides is almost comparable between june-october.

On comparison, classic and electric bike usage is similar in the month of january. Casual riders have preferred classic bike throughout the year except for october, novermber, and december. During these months electric bikes are more preferred, and I suspect the reason to be the start of winter season. Usage of all bike types by both rider is the lowest in the month of January and February which are the coldest in Chicago.

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Member%20Ride%20Preference.png" align="center" height="600" width="900" ></a>

Classic bike usage for member riders starts increasing from february with the highest rise between February and March, and it peaks in the month of August. After that it starts declining with the largest drop between October and November. Classic bikes leased by member riders is comparable between July-September.

Electric bike usage for member riders starts increasing from february with the highest rise between September and October, and it peaks in the month of October. After that it starts declining with the largest drop between December and January. Number of electric bike rides is almost comparable between June-September. Docked bikes are never used by member riders.

Member riders have also preferred classic bike throughout the year except for November and December. During these months electric bikes are more preferred reason being the same. Usage of all bike types by both riders is the lowest in the month of January and February which are the coldest in Chicago.

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Ride%20Preference%20Distribution.png" align="center" height="600" width="900" ></a>

Upon monthly comparison, it is observed that classic and docked bikes are used by casual riders more than member riders throughout the year. Casual electric rides exceeded member electric rides between May-September.

For member riders, classic bike usage is evenly distributed between Tuesday-Saturday and electric bike usage is maximum on Friday. Both classic and electric bikes are used lowest on Sunday and Monday. For casual riders, every bike type is used maximum on Saturday.

### Busiest Stations

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Top%2020%20Busiest%20Stations.png" align="center" height="600" width="750" ></a>

Majority of the docking stations are near the coastal area. 'Streeter Dr and Grand Ave' is the most famous docking station with highest number of riders due to excursion places in its vicinity. Difference between number of rides at the top 1st (Streeter Dr & Grand Ave) and top 2nd (Michigan Ave & Oak St) docking stations is significantly large. 

### Peak Hours

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Casual%20Weekday%20Peak%20Hours.png" align="center" height="500" width="1000" ></a>

Casual riders seem to be hiring maximum number of bikes in the evening between 4:00 P.M. - 7:00 P.M. during weekdays probably for leisure activities after office hours.

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Member%20Weekday%20Peak%20Hours.png" align="center" height="500" width="1000" ></a>

Member riders are hiring maximum number of bikes during peak commute hours that is between 7:00 A.M. - 9:00 A.M. in the morning and between 4:00 P.M. - 6:00 P.M. in the evening. Also, member riders seem to be using the bikes to travel towards station since some of the peak cyclistic docking stations are near train stations.

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Casual%20Weekend%20Peak%20Hours.png" align="center" height="500" width="1000" ></a>

During weekends, casual riders hire maximum number of bikes between 12:00 P.M. - 5:00 P.M.. The trend for weekends is a normal distribution unlike weekdays which was spiked during peak commute hours.

<a href="url"><img src="https://github.com/khanfarzal/Cyclistic-Bike-share-Analysis/blob/main/Graphs/Member%20Weekend%20Peak%20Hours.png" align="center" height="500" width="1000" ></a>

Bike hiring trend for member riders on weekends is comparable to that of casual riders, however a bit more consistent between 12:00 P.M. - 3:00 P.M. It seems that both riders types hire bikes for leisure and fun purposes during weekends.

### Recommendations

1. Design Half-Yearly and Quarter- Yearly membership plans
2. Slash the annual membership rates from June-September when casual rider traffic is maximum 
3. Design flash sale of membership plans near top 20 busiest stations on weekends during peak hours
