# css4p01
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Mon Oct 21 15:05:21 2024

@author: boitumelo
"""
#reading csv file
import pandas as pd
dataf=pd.read_csv("movie_dataset.csv")
print(dataf)

#displaying the data
pd.set_option('display.max_rows',None)

print(dataf)


#Fixing the NANs in the two colounms
x = dataf["Revenue (Millions)"].mean()

dataf["Revenue (Millions)"].fillna(x, inplace = True) 

x1 = dataf["Metascore"].mean()

dataf["Metascore"].fillna(x, inplace = True) 


# Fixing the names to have _
dataf.columns = dataf.columns.str.replace("Revenue \(Millions\)", "Revenue_Millions")
dataf.columns = dataf.columns.str.replace("Runtime \(Minutes\)", "Runtime_Minutes")


#Question 1
sorted_dataf = dataf.sort_values(by='Rating', ascending=False)  # Change 'Rating' to your actual rating column name
print(sorted_dataf)
print(dataf.info())

#Question 2 : Getting the value of mean

avg_revenue=dataf["Revenue_Millions"].mean()

#Question 3
# Filtering data
year = dataf[(dataf["Year"] >= 2015) & (dataf["Year"] <= 2017)]
#year=(dataf[dataf["Year"]> range (2016,2017)])
print(year)

avg_revenueyear=year["Revenue_Millions"].mean()

#question 4
year2016 = dataf[(dataf["Year"] >= 2016)]
print(year2016)
movienum=len(year2016["Title"])

#question 5
christophern = dataf[dataf['Director']=='Christopher Nolan']
directorC=len(christophern["Title"])

#question 6
ratings= dataf[(dataf["Rating"] >= 8.0)]
print(ratings)
ratings8=len(ratings["Title"])

#question 7
christophern_median = christophern["Rating"].median()

christophern["Rating"].fillna(x, inplace = True) 

#question 8
year2006 = dataf[(dataf["Year"] == 2006)]
print(year2006)
year2008 = dataf[(dataf["Year"] == 2008)]
print(year2008)
year2007 = dataf[(dataf["Year"] == 2007)]
print(year2007)

avg_2016=year2016["Rating"].mean()
avg_2006=year2006["Rating"].mean()
avg_2008=year2008["Rating"].mean()
avg_2007=year2007["Rating"].mean()

#question 9
movie2006_number=len(year2006["Title"])
print(movie2006_number)
movie2016_number=len(year2016["Title"])
print(movie2016_number)
percentage_increase = ((movie2016_number - movie2006_number) / movie2006_number) * 100  
print(percentage_increase)

#question 10
from collections import Counter
actor_list = dataf["Actors"].str.split(', ').sum()
actor_count = Counter(actor_list)
most_common_actor = actor_count.most_common(1)[0]

#question 11
from collections import Counter
genre_list = dataf["Genre"].str.split(',').sum()
unique_genre_set = set(genre_list)  
unique_genre_count = len(unique_genre_set)
print(unique_genre_count)
























