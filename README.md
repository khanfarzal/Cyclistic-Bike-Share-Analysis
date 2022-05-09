
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

    1) Identified the source of error in ride_length column which turned out to be negative time values that gave !VALUE error. I rectified the problem by using the MOD() function.

    2) 739170 of the station names and IDs out of 5.5M records are missing which constitutes 13.21% of the total records. Suprisingly, the data missing was only for electric bikes. Since the geographical latitudes and longitudes are present the nulls did not hinder the analysis.

    3) Around 4800 records of geographical latitudes and longitudes are missing, but since it constitutes less than 0.1% of the total records it can be filtered out.

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

