---
layout: default
title: "Homework 6 Jekyll Please Work"
permalink: /projects/homework6test
images:
  - "/assets/images/humidity.png"
  - "/assets/images/wind.png"
---

# Homework 6 Jekyll Page (Hopefully this works)

## Humidity VS Temperature

![Chart of Humidity VS Max, mid and min Temperatures](/assets/pngs/humidity.png)

In this visualization, we are being shown the temperature differences between the most and least humid states. Arizona is the least humid state while Louisiana is a close second to the most humid state (I thought Alaska would skew the data a lot since it is just known the be very cold). I wanted to record if there were big temperature differences between humid and not humid states. I used the default colors because they are easy to tell apart and since there are only two points, I thought a color map would not be necessary. This is completely different from my HW 5 visualizations since it is a different data set. I thought the interactivity with the different min, max, and mids would show more trends better and you can choose which one you want to see, because there can be meaningful trends by finding max or min temps.

## Wind Speed VS Temperature

![Chart of Humidity VS Max, mid and min Temperatures](/assets/pngs/wind.png)

I decided to go for a similar type of graph but this time I was comparing wind speeds. Surprisingly, Nebraska is supposed to have a higher average wind speen than Mississippi, but it seems to be even if not Mississippi having higher wind speeds than Nebraska. I think the data is just not representative of the actual states and next time I should just compare the variables within the dataset by grouping them and finding the average. I also tried looking for temperature differences on this one. Similar idea with the color map as well since you can tell which colors are which on this one pretty easily. I did not do any data transformations but I did do some data cleaning for NA values. There is no overlap from this to Homework 5. 

<div class="left">
{% include elements/button.html link="https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/bfro_reports_fall2022.csv" text="The Data" %}
</div>

<div class="right">
{% include elements/button.html link="https://github.com/charlie-xliu/charlie-xliu.github.io/blob/main/_example_projects/JekyllTest.ipynb" text="The Analysis" %}
</div>
