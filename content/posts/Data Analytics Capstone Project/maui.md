---
title: "Google Data Analytics Capstone Project"
date: 2023-03-10T13:12:47+08:00
draft: false
author: "Gerardo Humawan"
tags: ["data analytics"]
categories: ["data analytics"]

lightgallery: true

toc: 
  #enable: true
  auto: false
---


<!--more-->

## Scenario
As a junior data analyst within Cyclistic's esteemed Marketing Analysis team, I am entrusted with a pivotal role in contributing to the organization's strategic vision. Cyclistic, a prominent bike-share enterprise located in Chicago, is poised to chart its course toward an even more prosperous future, and this trajectory hinges upon the optimization of its annual membership base. Given the significance of this endeavor, our team's foremost objective is to attain a nuanced comprehension of the divergent usage patterns exhibited by casual riders and annual members of Cyclistic's bike-sharing services.

By delving into these discernible usage discrepancies, our team endeavors to forge a fresh and efficacious marketing strategy, aimed at the conversion of transient casual riders into dedicated annual members. The blueprint for this strategy is contingent upon securing the endorsement of Cyclistic's executive leadership. Consequently, the recommendations that will be presented must be underpinned by both compelling data insights and an array of sophisticated data visualizations.

In essence, the crux of our initiative lies in identifying the intrinsic distinctions that demarcate the engagement behaviors of casual riders from those of steadfast annual members. Armed with these granular insights, we are poised to shape a strategic narrative that resonates effectively with each category of riders, thereby fostering a paradigm shift in their consumption habits. The forthcoming data-driven revelations and visualizations will serve as the bedrock upon which our transformative marketing strategy will be constructed, enabling us to take bold steps toward converting casual riders into loyal annual members.

Characters and teams
Cyclistic: A bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.
Lily Moreno: The director of marketing and your manager. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels.
Cyclistic marketing analytics team: A team of data analysts who are responsible for collecting, analyzing, and reporting data that helps guide Cyclistic marketing strategy. You joined this team six months ago and have been busy learning about Cyclistic’s mission and business goals — as well as how you, as a junior data analyst, can help Cyclistic achieve them.
Cyclistic executive team: The notoriously detail-oriented executive team will decide whether to approve the recommended marketing program.  

## 1 Ask
Three questions will guide the future marketing program: 
1. How do annual members and casual riders use Cyclistic bikes differently? 
2. Why would casual riders buy Cyclistic annual memberships? 
3. How can Cyclistic use digital media to influence casual riders to become members? 

Moreno has assigned you the first question to answer: How do annual members and casual riders use Cyclistic bikes differently? 
You will produce a report with the following deliverables: 
1. A clear statement of the business task 
2. A description of all data sources used 
3. Documentation of any cleaning or manipulation of data 4. A summary of your analysis 5. Supporting visualizations and key findings 6. Your top three recommendations based on your analysis 

## 2 Prepare
Utilizing Cyclistic's historical trip data, an in-depth analysis will be conducted to discern prevailing trends. The dataset encompassing the last twelve months of Cyclistic trip records can be accessed from the this link https://divvy-tripdata.s3.amazonaws.com/index.html. It is important to acknowledge that the datasets have been designated under an alternate nomenclature due to the fictitious nature of Cyclistic as a corporate entity. It is noteworthy, however, that these datasets remain suitable for the current case study, thus facilitating comprehensive responses to pertinent business inquiries. This dataset has been made available through the auspices of Motivate International Inc., and its use is authorized by the corresponding license agreement.

It should be emphasized that the dataset is of a public nature, permitting the exploration of distinct usage patterns exhibited by various customer categories within the context of Cyclistic bicycles. However, it is crucial to recognize that data privacy considerations prohibit the utilization of personally identifiable information pertaining to riders. Consequently, any endeavors to correlate pass acquisitions with credit card details, with the intention of ascertaining the residence of casual riders within Cyclistic's service vicinity or their history of purchasing multiple individual passes, are precluded by these privacy constraints.

### 2.1 Key tasks
Acquisition and Organization of Data:

The acquisition of the requisite data has been executed diligently, with copies securely preserved both on my local computer and within the confines of Kaggle's secure environment. This meticulous approach to data storage ensures compliance with best practices in data security and confidentiality.

Data Structure and Organization:

The acquired data is structured in the CSV (comma-separated values) format, facilitating ease of data manipulation and analysis. Within this dataset, a total of 13 distinct columns are present, each corresponding to specific attributes and variables relevant to the Cyclistic bike-sharing operations.

Data Sorting and Filtering:

In accordance with the analytical scope, the data encompassing the most recent 12-month interval, spanning from January 2021 to December 2021, has been identified as the focal period for analysis. This selection has been predicated on the imperative of utilizing the most contemporaneous dataset to underpin our insights and recommendations.

Credibility Assessment:

An inherent aspect of the data analysis process involves an assessment of data credibility. This entails an evaluation of data sources, collection methodologies, and inherent biases. It is imperative to ensure that the data originates from reliable sources and adheres to rigorous collection standards. In order to gauge the credibility of the provided data, a comprehensive review of its sourcing and methodology will be undertaken, with the intent of validating its suitability for generating accurate and actionable insights. This critical appraisal will be a cornerstone in ensuring the integrity of the ensuing analysis and strategic recommendations.

### 2.2 Merging of Datasets
For data transformation, data processing was performed Python Script and SQL Server. The data from each month, spanning from January to December 2021, was imported and merged into a single table called “2021combined_csv.csv”.The steps involved in this process are as follows:

```python
import os
import glob
import pandas as pd

#find all csv files in the folder
#use glob pattern matching -> extension = 'csv'
#save result in list -> all_filenames
extension = 'csv'
glob.glob('*-divvy-tripdata.csv')

['202101-divvy-tripdata.csv',
 '202102-divvy-tripdata.csv',
 '202103-divvy-tripdata.csv',
 '202104-divvy-tripdata.csv',
 '202105-divvy-tripdata.csv',
 '202106-divvy-tripdata.csv',
 '202107-divvy-tripdata.csv',
 '202108-divvy-tripdata.csv',
 '202109-divvy-tripdata.csv',
 '202110-divvy-tripdata.csv',
 '202111-divvy-tripdata.csv',
 '202112-divvy-tripdata.csv',]

#combine all files in the list
combined_csv = pd.concat([pd.read_csv(f) for f in all_filenames ])
#export to csv
combined_csv.to_csv( "2021combined_csv.csv", index=False, encoding='utf-8-sig')

```        
### 2.3 View datasets
Subsequent to the amalgamation of the 12 individual datasets, the aggregated dataset has been seamlessly imported into the PostgreSQL database infrastructure. This comprehensive dataset comprises a total of 5,595,063 distinct rows. For the purpose of reviewing the entire dataset, the ensuing SQL statement may be employed:

```SQL
  --- Below is the SQL statement for creating new tables and rows ---
CREATE TABLE biketrips
	ride_id varchar,
	rideable_type varchar, 
	started_at timestamp, 
	ended_at timestamp, 
	start_station_name varchar, 
	start_station_id varchar, 
	end_station_name varchar, 
	end_station_id varchar, 
	start_lat varchar, 
	start_lng varchar, 
	end_lat varchar, 
	end_lng varchar, 
	bike_user varchar;

  --- Below is the SQL statement to view the total number of rows ---
Select Count(*) from biketrips;

```
## 3 Process
Cleaning or manipulation of data
Our task requires three libraries — Pandas, Glob, and the OS module and PostgreSQL as our  database.
Key tasks
  1. Check the data for errors.
  2. Choose your tools.
  3. Transform the data so you can work with it effectively.
  4. Document the cleaning process.
Deliverable
  1. Documentation of any cleaning or manipulation of data
### 3.1 Data cleaning process
```SQL
  --- I've used below SQL statement to view all the rows wtih a null values ---
SELECT * FROM biketrips
WHERE start_station_name IS  NULL OR
	    start_station_id IS  NULL OR
	    end_station_name IS  NULL OR 
	    end_station_id IS  NULL OR
	    start_lat  IS  NULL OR
		start_lng IS  NULL OR
		end_lat  IS  NULL OR
		end_lng  IS  NULL OR
		bike_user IS  NULL 
ORDER BY started_at ASC

  --- A total of 1,006,761 rows found with null values ---
```
```SQL
  --- Deleting all rows with null values ---
DELETE FROM biketrips
WHERE 
    started_at IS  NULL OR
    ended_at IS NULL OR
    start_station_name IS  NULL OR
    start_station_id IS  NULL OR
    end_station_name IS  NULL OR 
    end_station_id IS  NULL OR
    start_lat  IS  NULL OR
    start_lng IS  NULL OR
    end_lat  IS  NULL OR
    end_lng  IS  NULL OR
    bike_user IS  NULL ;

```

### 3.5 Add new columns
In order to enhance the precision of the datasets and augment the comprehensiveness of information for the purpose of facilitating data analytics comprehension, the incorporation of new columns has been deemed necessary.

```SQL - 
  --- added new column (ride_length) and populate ---
  --- the new column is about the ride durations in each rows ---
  --- data extracted from subtracting started_at from ended_at columns ---
ALTER TABLE biketrips ADD COLUMN ride_length INTERVAL;
UPDATE biketrips o1
	SET ride_length = o2.ended_at - o1.started_at
FROM biketrips o2
WHERE o1.ride_id = o2.ride_id;

  --- since the output is in timeformat, data was changed to seconds (number format) ---
ALTER TABLE biketrips ADD COLUMN ride_length NUMERIC;
UPDATE biketrips o1
	SET ride_length = EXTRACT(EPOCH FROM (o2.ended_at - o1.started_at)) 
FROM biketrips o2
WHERE o1.ride_id = o2.ride_id

  ---columns with negative and zero values was deleted for more cleaning process--
  --- below is SQL statement to view zero and less than zero values ---
select * from biketrips where ride_length = 0
select * from biketrips where ride_length < 0
  --- SQL statement for deleting zero and less than zer values ---
delete from biketrips where ride_length = 0
delete from biketrips where ride_length < 0

```

``` SQL 
  --- added new column (day_of_week) ---
  --- the new column shows what day of the week the activity occurred ---
ALTER TABLE biketrips ADD COLUMN day_of_week TEXT;
    UPDATE biketrips o1
        SET day_of_week = TO_CHAR(o1.started_at, 'Day')
    FROM biketrips o2
    WHERE o1.ride_id = o2.ride_id;
```

``` SQL 
  --- added new column (month) ---
  --- the new column shows which month the activity occurred ---
ALTER TABLE biketrips ADD COLUMN month TEXT;
    UPDATE biketrips o1
        SET month = TO_CHAR(o1.started_at, 'Month')
    FROM biketrips o2
    WHERE o1.ride_id = o2.ride_id;
```

``` SQL 
  --- added new column (time_block) ---
  --- the new column shows what part of the day the activity occurred --- 
ALTER TABLE biketrips
ADD COLUMN time_block VARCHAR(20);
UPDATE events
SET time_block = CASE
  WHEN EXTRACT(HOUR FROM event_time) >= 6 AND EXTRACT(HOUR FROM event_time) < 12 THEN 'Morning'
  WHEN EXTRACT(HOUR FROM event_time) >= 12 AND EXTRACT(HOUR FROM event_time) < 18 THEN 'Afternoon'
  WHEN EXTRACT(HOUR FROM event_time) >= 18 AND EXTRACT(HOUR FROM event_time) <= 23 THEN 'Evening'
  ELSE 'Night'
END;

```

## 4. Analyze
In the Analyze phase, we delve into the data to uncover insights and address the key findings related to how annual members and casual riders use Cyclistic bikes differently. The focus is on understanding their behavior, preferences, and patterns to inform marketing strategies aimed at converting casual riders into annual members. To address the key findings, the following analyses were performed in postgreSQL server.

### 4.1 Casual riders vs annual members (percentage)

```SQL
SELECT bike_user AS membership_type, 
COUNT (bike_user) AS total_ride, 
SUM (COUNT (bike_user)) OVER () AS total_membership,
CONCAT (CAST (COUNT (bike_user) * 100.0/ SUM (COUNT (bike_user)) OVER () AS DECIMAL (10,2)), '%') membership_percentage
FROM biketrips
WHERE bike_user IS NOT NULL
GROUP BY bike_user;
```
![](/images/image1.png)



```SQL

select
rideable_type AS bike_type,
bike_user AS membership_type,  
COUNT (rideable_type) AS individual_membership_count, 
SUM (COUNT (rideable_type)) OVER (Partition by rideable_type) AS total_membership,
CONCAT (CAST (COUNT (rideable_type) * 100.0/ SUM (COUNT (rideable_type)) OVER (Partition by rideable_type) AS Decimal (10,2)), '%') AS membership_percentage
FROM biketrips
WHERE bike_user IS NOT NULL
GROUP BY rideable_type, bike_user
ORDER BY rideable_type;

```

![Percentage](/images/total_percent.png "Percentage")

**Median ride length  or trip duration**

![Median ride length or trip duration](/images/median.png "Median Ride Length")


**Busiest day for rides**

**Median ride length per day**

**Total rides per day**

![Total rides per day](/images/total_rides_day.png "Total rides per day")


## Summary of analysis

## Visualizations and key findings


## Three recommendations based on analysis

