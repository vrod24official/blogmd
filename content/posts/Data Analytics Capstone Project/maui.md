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
## 1 Business task
the quick brown fox jumps over the lazy dog
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

