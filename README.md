# Cyclistic_Bikes_10012024_case_study

# Ask

## Key Business Task 
To distinguish the patterns of utilization of Cyclistic bikes for Annual Members and Casual Riders respectively, and to devise a marketing strategy to expedite conversion of Casual Riders into purchasing an Annual membership.

## Key Stakeholders

Cyclistic Bike's Marketing Board & Executive Team.

# Prepare

## Downloading Data and Storing it Appropriately.

The dataset used in the analysis is accessed and downloaded from [Motivate International Inc.](https://divvy-tripdata.s3.amazonaws.com/index.html). 12 months worth of data for the year 2023 (202301-divvy-tripdata.zip - 202312-divvy-tripdata.zip) is downloaded, stored locally within the documents folder (Documents\Case_Study_A_080224) of my laptop, and another copy is stored remotely on Google Drive.

```TSQL

install.packages("tidyverse")
install.packages("lubridate")
install.packages("janitor")

library (tidyverse)
library (lubridate)
library (janitor)
```

## Identify how it's Organized

All data is stored in a Comma-separated values (.csv) file format, with 13 columns, demonstrating 13 field names, which are: ride_id, rideable_type, started_at, ended_at, start_station_name, start_station_id, end_station_name, end_station_id, start_lat, start_lng, end_lat, end_lng, and member_casual.

The field names are obtained from Excel Spreadsheets with the following function

```TSQL

=CONCAT(A1,", ",B1,", ",C1,", ",D1,", ",E1,", ",F1,", ",G1,", ",H1,", ",I1,", ",J1,", ",K1,", ",L1,", ",M1)
```

## Determine the credibility of the data.
As this is a study utilizing public, third-party data, we cannot determine its credibility; it may or may not accurately capture a comprehensive consumer snapshot.

# Process

## Check the Data for Errors

R version 4.3.2 is primarily utilized for Data Processing and Analyses. The 12 Comma-seperated Values (.csv) files will be imported into R as data frames utilizing the following code chunk, utilizing the tidyverse, lubridate and janitor libraries.

```TSQL

install.packages("tidyverse")
install.packages("lubridate")
install.packages("janitor")

library (tidyverse)
library (lubridate)
library (janitor)

Jan2023 <- read_csv("Case_Study_A_080224/01_2023.csv")
Feb2023 <- read_csv("Case_Study_A_080224/02_2023.csv")
Mar2023 <- read_csv("Case_Study_A_080224/03_2023.csv")
Apr2023 <- read_csv("Case_Study_A_080224/04_2023.csv")
May2023 <- read_csv("Case_Study_A_080224/05_2023.csv")
Jun2023 <- read_csv("Case_Study_A_080224/06_2023.csv")
Jul2023 <- read_csv("Case_Study_A_080224/07_2023.csv")
Aug2023 <- read_csv("Case_Study_A_080224/08_2023.csv")
Sep2023 <- read_csv("Case_Study_A_080224/09_2023.csv")
Oct2023 <- read_csv("Case_Study_A_080224/10_2023.csv")
Nov2023 <- read_csv("Case_Study_A_080224/11_2023.csv")
Dec2023 <- read_csv("Case_Study_A_080224/12_2023.csv")

```
## Choose your Tools

R version 4.3.2 is primarily utilized for Data Processing, Analyses, Visualization and Sharing.

## Transform the Data so You Can Work with it Effectively

