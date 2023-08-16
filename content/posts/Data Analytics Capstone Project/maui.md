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

## 1 Scenario
As a junior data analyst within Cyclistic's esteemed Marketing Analysis team, I am entrusted with a pivotal role in contributing to the organization's strategic vision. Cyclistic, a prominent bike-share enterprise located in Chicago, is poised to chart its course toward an even more prosperous future, and this trajectory hinges upon the optimization of its annual membership base. Given the significance of this endeavor, our team's foremost objective is to attain a nuanced comprehension of the divergent usage patterns exhibited by casual riders and annual members of Cyclistic's bike-sharing services.

By delving into these discernible usage discrepancies, our team endeavors to forge a fresh and efficacious marketing strategy, aimed at the conversion of transient casual riders into dedicated annual members. The blueprint for this strategy is contingent upon securing the endorsement of Cyclistic's executive leadership. Consequently, the recommendations that will be presented must be underpinned by both compelling data insights and an array of sophisticated data visualizations.

In essence, the crux of our initiative lies in identifying the intrinsic distinctions that demarcate the engagement behaviors of casual riders from those of steadfast annual members. Armed with these granular insights, we are poised to shape a strategic narrative that resonates effectively with each category of riders, thereby fostering a paradigm shift in their consumption habits. The forthcoming data-driven revelations and visualizations will serve as the bedrock upon which our transformative marketing strategy will be constructed, enabling us to take bold steps toward converting casual riders into loyal annual members.

Characters and teams
Cyclistic: A bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.
Lily Moreno: The director of marketing and your manager. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels.
Cyclistic marketing analytics team: A team of data analysts who are responsible for collecting, analyzing, and reporting data that helps guide Cyclistic marketing strategy. You joined this team six months ago and have been busy learning about Cyclistic’s mission and business goals — as well as how you, as a junior data analyst, can help Cyclistic achieve them.
Cyclistic executive team: The notoriously detail-oriented executive team will decide whether to approve the recommended marketing program.  

## 2 Ask
Three questions will guide the future marketing program: 
1. How do annual members and casual riders use Cyclistic bikes differently? 
2. Why would casual riders buy Cyclistic annual memberships? 
3. How can Cyclistic use digital media to influence casual riders to become members? 

Moreno has assigned you the first question to answer: How do annual members and casual riders use Cyclistic bikes differently? 
You will produce a report with the following deliverables: 
1. A clear statement of the business task 
2. A description of all data sources used 
3. Documentation of any cleaning or manipulation of data 4. A summary of your analysis 5. Supporting visualizations and key findings 6. Your top three recommendations based on your analysis 

## 3 Prepare
Utilizing Cyclistic's historical trip data, an in-depth analysis will be conducted to discern prevailing trends. The dataset encompassing the last twelve months of Cyclistic trip records can be accessed from the this link https://divvy-tripdata.s3.amazonaws.com/index.html. It is important to acknowledge that the datasets have been designated under an alternate nomenclature due to the fictitious nature of Cyclistic as a corporate entity. It is noteworthy, however, that these datasets remain suitable for the current case study, thus facilitating comprehensive responses to pertinent business inquiries. This dataset has been made available through the auspices of Motivate International Inc., and its use is authorized by the corresponding license agreement.

It should be emphasized that the dataset is of a public nature, permitting the exploration of distinct usage patterns exhibited by various customer categories within the context of Cyclistic bicycles. However, it is crucial to recognize that data privacy considerations prohibit the utilization of personally identifiable information pertaining to riders. Consequently, any endeavors to correlate pass acquisitions with credit card details, with the intention of ascertaining the residence of casual riders within Cyclistic's service vicinity or their history of purchasing multiple individual passes, are precluded by these privacy constraints.

### 3.1 Key tasks
Acquisition and Organization of Data:

The acquisition of the requisite data has been executed diligently, with copies securely preserved both on my local computer and within the confines of Kaggle's secure environment. This meticulous approach to data storage ensures compliance with best practices in data security and confidentiality.

Data Structure and Organization:

The acquired data is structured in the CSV (comma-separated values) format, facilitating ease of data manipulation and analysis. Within this dataset, a total of 13 distinct columns are present, each corresponding to specific attributes and variables relevant to the Cyclistic bike-sharing operations.

Data Sorting and Filtering:

In accordance with the analytical scope, the data encompassing the most recent 12-month interval, spanning from January 2021 to December 2021, has been identified as the focal period for analysis. This selection has been predicated on the imperative of utilizing the most contemporaneous dataset to underpin our insights and recommendations.

Credibility Assessment:

An inherent aspect of the data analysis process involves an assessment of data credibility. This entails an evaluation of data sources, collection methodologies, and inherent biases. It is imperative to ensure that the data originates from reliable sources and adheres to rigorous collection standards. In order to gauge the credibility of the provided data, a comprehensive review of its sourcing and methodology will be undertaken, with the intent of validating its suitability for generating accurate and actionable insights. This critical appraisal will be a cornerstone in ensuring the integrity of the ensuing analysis and strategic recommendations.

### 3.2 Merging of Datasets
Through the utilization of a straightforward Python script, the data pertaining to the 12 consecutive months has been successfully amalgamated into a singular, unified dataset.

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
### 3.3 View datasets
Subsequent to the amalgamation of the 12 individual datasets, the aggregated dataset has been seamlessly imported into the PostgreSQL database infrastructure. This comprehensive dataset comprises a total of 5,595,063 distinct rows. For the purpose of reviewing the entire dataset, the ensuing SQL statement may be employed:

```sql
  --- Below is table structure SQL statement that has been established, accompanied by the requisite rows, 
      in advance of the commencement of the data sets' importation process. ---

CREATE TABLE biketrips (
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
	bike_user varchar
)

  --- Below is the SQL statement to view the total number of rows ---
Select Count(*) from biketrips;
```

### 3.4 Data cleaning process
```sql
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

  --- A total of 1,006,761 rows found with null values --
```
```sql
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

## 4. Exploratory Analysis

Insert image/picture:

![Average ride length or trip duration](/images/avg_ride_length.png "AVG Ride Length")

**Total trips**

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

