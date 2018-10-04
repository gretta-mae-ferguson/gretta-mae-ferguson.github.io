---
layout: post
title: "Metis Project 1"
---
# Using data for effective canvassing

Just one week into the Metis Data Science Bootcamp, I have already learned so much. This week we learned how to import data 
from the web using pandas and APIs. We also learned how to create data visualizations using python with matplotlib and seaborn. 

## Problem Statement

For our first project, we worked in teams of 4 to create a street canvassing strategy for "WTWY", a women's tech bootcamp 
which was hosting a fundraising gala in NYC. Our client's main concern was identifying at which subway stations to place 
canvassers so that they could maximize attendance and funds raised. We therefore wanted to recommend a strategy that would 
maximize both the quantity of exposure - i.e. reaching *many* people - and the quality of exposure - i.e. reaching the *right* 
people. 

## Approach

Our group took a 4 pronged approach to answering this question. We wanted to identify:
1. Stations with high **transit** (train) traffic 
2. Stations with high **pedestrian** traffic 
3. Stations in areas with high median **income**, since affluent individuals are more likely to donate
4. Stations in areas with a lot of **tech** companies, since professionals in the tech industry are more likely to care about this cause

For each of these four areas, we assigned each station a score between 1 (for the highest performing station) to 0. Our final 
recomendation would be to canvass at those stations which had the highest sum of the four scores, which we called our Benson 
score.

## Data Analysis

For each of the four areas, we had to identify the datasets we would leverage for the analysis and then generate a Benson 
score for each station

#### TRANSIT
MTA provides publicly available data on the locations of subway stations and the number of entries and exits per 4 hour 
period at each turnstile. We needed to roll this data together and calculate the total entries and exits by station. We ran
into a few nuances in the data that we managed to work around such as:
- multiple stations being named the same thing
- entry/exit counters resetting
- non-standard time periods across turnstiles

#### PEDESTRIAN
WalkScore.com takes in an address and provides a "walkscore" based on how walkable the area is, given proximity of restaurants,
shopping, parks, etc. Areas with high walkscores also tend to have high foot traffic, we we used this score as a proxy for the 
amount of pedestrian traffic near a station. We fed the locations (lattitude and longitude) of each station into the 
WalkScore.com API to generate the score.

#### INCOME
US Census data provides median income by zip code. We used OpenMap to generate zip code from the lattitude and longitude of 
each station then we joined that to the US Census data to come up with median income surrounding each station.

#### TECH
We found a list of the top tech companies in New York and the number of employees at those companies. We then created a spacial
normal distribution around each tech company, scaled by that companies number of employees. Then for each station, we 
calculated the sum across all of these distributions, to come up with the "total tech score" for each station. Then we 
normalized these scores so that the station with the maximum "total tech score" was scaled down to a value of 1, which gave us
our Benson scores.

## Results

Finally we created charts and graphs to visualize the data along with a presentation to convey our findings. 

The top 5 stations we recommended visiting (in order) were:
1. Grand Central - 42nd St
2. WTC Cortlandt
3. 34 St - Herald Sq
4. Unin Sq - 14th St
5. 34 St - Penn Station

Unfortunately, I have not yet managed to get the graphics to work on this blog, but check back next week and I will 
show you some cool stuff!

![final output]({{https://github.com/gretta-mae-ferguson/gretta-mae-ferguson.github.io/blob/master/images/Screen%20Shot%202018-09-28%20at%202.58.49%20AM.png?raw=true}})
