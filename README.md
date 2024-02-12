# Cyclistic_Bikes_10012024_case_study

# Ask

## Key Business Task 
To distinguish the patterns of utilization of Cyclistic bikes for Annual Members and Casual Riders respectively, and to devise a marketing strategy to expedite conversion of Casual Riders into purchasing an Annual membership.

## Key Stakeholders

Cyclistic Bike's Marketing Board & Executive Team.

# Prepare

## Downloading Data and Storing it Appropriately.

The dataset used in the analysis is accessed and downloaded from [Motivate International Inc.](https://divvy-tripdata.s3.amazonaws.com/index.html). 12 months worth of Data is downloaded, stored locally in the documents folder (Documents\Case_Study_A_080224) of my laptop, and another copy is stored remotely on Google Drive.

```TSQL

install.packages("tidyverse")
install.packages("lubridate")
install.packages("janitor")

library (tidyverse)
library (lubridate)
library (janitor)
```
