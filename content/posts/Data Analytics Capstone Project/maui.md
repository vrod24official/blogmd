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
You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations. 

Characters and teams
Cyclistic: A bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.
Lily Moreno: The director of marketing and your manager. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels.
Cyclistic marketing analytics team: A team of data analysts who are responsible for collecting, analyzing, and reporting data that helps guide Cyclistic marketing strategy. You joined this team six months ago and have been busy learning about Cyclistic’s mission and business goals — as well as how you, as a junior data analyst, can help Cyclistic achieve them.
Cyclistic executive team: The notoriously detail-oriented executive team will decide whether to approve the recommended marketing program.  
##  Ask
Three questions will guide the future marketing program: 
1. How do annual members and casual riders use Cyclistic bikes differently? 
2. Why would casual riders buy Cyclistic annual memberships? 
3. How can Cyclistic use digital media to influence casual riders to become members? 
   
Moreno has assigned you the first question to answer: How do annual members and casual riders use Cyclistic bikes differently? 
You will produce a report with the following deliverables: 
1. A clear statement of the business task 
2. A description of all data sources used 
3. Documentation of any cleaning or manipulation of data 4. A summary of your analysis 5. Supporting visualizations and key findings 6. Your top three recommendations based on your analysis 
## 2 Data sources

## 3 Cleaning or manipulation of data

### 3.1 Merge datasets

```python
import os
import glob
import pandas as pd

#find all csv files in the folder
#use glob pattern matching -> extension = 'csv'
#save result in list -> all_filenames
extension = 'csv'
all_filenames = [i for i in glob.glob('*.{}'.format(extension))]
#print(all_filenames)

#combine all files in the list
combined_csv = pd.concat([pd.read_csv(f) for f in all_filenames ])
#export to csv
combined_csv.to_csv( "combined_csv.csv", index=False, encoding='utf-8-sig')

```        
### 3.2 View datasets

### 3.3 Delete NULL

### 3.4 Add new columns

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

