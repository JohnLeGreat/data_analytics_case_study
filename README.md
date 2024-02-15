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

We will need to check the data frames for any disrespancies in formatting (making sure the type formatting is consistent across all columns in the dataframes). We will be utilizing the str() function to inspect the data frames.

```TSQL

str(Jan2023)
str(Feb2023)
str(Mar2023)
str(Apr2023)
str(May2023)
str(Jun2023)
str(Jul2023)
str(Aug2023)
str(Sep2023)
str(Oct2023)
str(Nov2023)
str(Dec2023)

```

After primary inspection, data formatting appears to be consistent across all data frames, with appropriate data types.\
Three outputs for the data frames, Jan2023, Jun2023, and Dec2023 will be demonstrated for reference. \
(Key: chr: character, num: numeric, POSIXct: date-time)

```TSQL
>str(Jan2023)
spc_tbl_ [190,301 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ ride_id           : chr [1:190301] "F96D5A74A3E41399" "13CB7EB698CEDB88" "BD88A2E670661CE5" "C90792D034FED968" ...
 $ rideable_type     : chr [1:190301] "electric_bike" "classic_bike" "electric_bike" "classic_bike" ...
 $ started_at        : POSIXct[1:190301], format: "2023-01-21 20:05:42" "2023-01-10 15:37:36" ...
 $ ended_at          : POSIXct[1:190301], format: "2023-01-21 20:16:33" "2023-01-10 15:46:05" ...
 $ start_station_name: chr [1:190301] "Lincoln Ave & Fullerton Ave" "Kimbark Ave & 53rd St" "Western Ave & Lunt Ave" "Kimbark Ave & 53rd St" ...
 $ start_station_id  : chr [1:190301] "TA1309000058" "TA1309000037" "RP-005" "TA1309000037" ...
 $ end_station_name  : chr [1:190301] "Hampden Ct & Diversey Ave" "Greenwood Ave & 47th St" "Valli Produce - Evanston Plaza" "Greenwood Ave & 47th St" ...
 $ end_station_id    : chr [1:190301] "202480.0" "TA1308000002" "599" "TA1308000002" ...
 $ start_lat         : num [1:190301] 41.9 41.8 42 41.8 41.8 ...
 $ start_lng         : num [1:190301] -87.6 -87.6 -87.7 -87.6 -87.6 ...
 $ end_lat           : num [1:190301] 41.9 41.8 42 41.8 41.8 ...
 $ end_lng           : num [1:190301] -87.6 -87.6 -87.7 -87.6 -87.6 ...
 $ member_casual     : chr [1:190301] "member" "member" "casual" "member" ...
 - attr(*, "spec")=
  .. cols(
  ..   ride_id = col_character(),
  ..   rideable_type = col_character(),
  ..   started_at = col_datetime(format = ""),
  ..   ended_at = col_datetime(format = ""),
  ..   start_station_name = col_character(),
  ..   start_station_id = col_character(),
  ..   end_station_name = col_character(),
  ..   end_station_id = col_character(),
  ..   start_lat = col_double(),
  ..   start_lng = col_double(),
  ..   end_lat = col_double(),
  ..   end_lng = col_double(),
  ..   member_casual = col_character()
  .. )
 - attr(*, "problems")=<externalptr> 
>str(Jun2023)
spc_tbl_ [719,618 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ ride_id           : chr [1:719618] "6F1682AC40EB6F71" "622A1686D64948EB" "3C88859D926253B4" "EAD8A5E0259DEC88" ...
 $ rideable_type     : chr [1:719618] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
 $ started_at        : POSIXct[1:719618], format: "2023-06-05 13:34:12" "2023-06-05 01:30:22" ...
 $ ended_at          : POSIXct[1:719618], format: "2023-06-05 14:31:56" "2023-06-05 01:33:06" ...
 $ start_station_name: chr [1:719618] NA NA NA NA ...
 $ start_station_id  : chr [1:719618] NA NA NA NA ...
 $ end_station_name  : chr [1:719618] NA NA NA NA ...
 $ end_station_id    : chr [1:719618] NA NA NA NA ...
 $ start_lat         : num [1:719618] 41.9 41.9 42 42 42 ...
 $ start_lng         : num [1:719618] -87.7 -87.7 -87.7 -87.7 -87.7 ...
 $ end_lat           : num [1:719618] 41.9 41.9 41.9 42 42 ...
 $ end_lng           : num [1:719618] -87.7 -87.7 -87.6 -87.7 -87.7 ...
 $ member_casual     : chr [1:719618] "member" "member" "member" "member" ...
 - attr(*, "spec")=
  .. cols(
  ..   ride_id = col_character(),
  ..   rideable_type = col_character(),
  ..   started_at = col_datetime(format = ""),
  ..   ended_at = col_datetime(format = ""),
  ..   start_station_name = col_character(),
  ..   start_station_id = col_character(),
  ..   end_station_name = col_character(),
  ..   end_station_id = col_character(),
  ..   start_lat = col_double(),
  ..   start_lng = col_double(),
  ..   end_lat = col_double(),
  ..   end_lng = col_double(),
  ..   member_casual = col_character()
  .. )
 - attr(*, "problems")=<externalptr> 
>str(Dec2023)
spc_tbl_ [224,073 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ ride_id           : chr [1:224073] "C9BD54F578F57246" "CDBD92F067FA620E" "ABC0858E52CBFC84" "F44B6F0E8F76DC90" ...
 $ rideable_type     : chr [1:224073] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
 $ started_at        : POSIXct[1:224073], format: "2023-12-02 18:44:01" "2023-12-02 18:48:19" ...
 $ ended_at          : POSIXct[1:224073], format: "2023-12-02 18:47:51" "2023-12-02 18:54:48" ...
 $ start_station_name: chr [1:224073] NA NA NA NA ...
 $ start_station_id  : chr [1:224073] NA NA NA NA ...
 $ end_station_name  : chr [1:224073] NA NA NA NA ...
 $ end_station_id    : chr [1:224073] NA NA NA NA ...
 $ start_lat         : num [1:224073] 41.9 41.9 41.9 42 41.9 ...
 $ start_lng         : num [1:224073] -87.7 -87.7 -87.6 -87.7 -87.6 ...
 $ end_lat           : num [1:224073] 41.9 41.9 41.9 41.9 41.9 ...
 $ end_lng           : num [1:224073] -87.7 -87.6 -87.6 -87.7 -87.6 ...
 $ member_casual     : chr [1:224073] "member" "member" "member" "member" ...
 - attr(*, "spec")=
  .. cols(
  ..   ride_id = col_character(),
  ..   rideable_type = col_character(),
  ..   started_at = col_datetime(format = ""),
  ..   ended_at = col_datetime(format = ""),
  ..   start_station_name = col_character(),
  ..   start_station_id = col_character(),
  ..   end_station_name = col_character(),
  ..   end_station_id = col_character(),
  ..   start_lat = col_double(),
  ..   start_lng = col_double(),
  ..   end_lat = col_double(),
  ..   end_lng = col_double(),
  ..   member_casual = col_character()
  .. )
 - attr(*, "problems")=<externalptr> 

```
To merge multiple data frames into a single data frame, merged_df2023 with the date starting 01-01-2023 and ending 31-12-2023, we will be utilizing the rbind() function.

```TSQL

merged_df2023 <- rbind(Jan2023, Feb2023, Mar2023, Apr2023, May2023, Jun2023, Jul2023, Aug2023, Sep2023, Oct2023, Nov2023, Dec2023)

```
## Document the Cleaning Process

For data cleaning prior to our next Analyses step, we will need to utilize the janitor library, namely the clean_names () and remove_empty() function, which function is to clean data frames names for consistency and to remove empty rows or columns, respectively.

```TSQL

merged_df2023 <- clean_names (merged_df2023)

merged_df2023 <- remove_empty (merged_df2023, which = c("rows","cols"))

```
# Analyse

## Aggregate your Data so it's Useful and Accessible

To get the day of the week of where the trips have occurred, we will be utilizing the wday() function.

```TSQL
day_of_week <- wday(merged_df2023$started_at)
```
To get the trip duration / ride length, we will be utilizing the difftime () function.

```TSQL
ride_length <- difftime(merged_df2023$ended_at, merged_df2023$started_at, unit ="min")
```

To get the month of the year of where the trips have occurred, we will be utilizing the format(as.Date()) function.

```TSQL
month <- format(as.Date(merged_df2023$started_at), '%m')
```

T0 get the starting hour, we will be utilizing the format(as.POSIXct()) function.

```TSQL
starting_hour <- format(as.POSIXct(merged_df2023$started_at), '%m')
```
## Perform some calculations

To calculate and tabulate the mean of ride_length and max of ride_length, for the annual member and casual rider groups respectively, we will be using the mean() and max() function respectively, grouped by member_casual.
```TSQL
merged_df2023 %>%
  group_by (member_casual) %>%
  summarise (ave_ride_length = mean(ride_length), max_ride_length = max (ride_length))
```
The following output is recorded:
```TSQL
# A tibble: 2 × 3
  member_casual ave_ride_length max_ride_length
  <chr>         <drtn>          <drtn>         
1 casual        28.22453 mins   98489.067 mins 
2 member        12.51317 mins    1559.667 mins 
```
From the data, we know that on average, casual riders tend to use Cylistic Bikes for a longer duration of time then the annual members.

To calculate and tabulate the mean of ride_length and max of ride_length, for each day of the week, we will be using the mean() and max() function respectively, grouped by day_of_week.
```TSQL
merged_df2023 %>%
  group_by (day_of_week) %>%
  summarise (ave_ride_length = mean(ride_length), max_ride_length = max (ride_length))
```
The following output is recorded:
```TSQL
# A tibble: 2 × 3
 day_of_week ave_ride_length max_ride_length
        <dbl> <drtn>          <drtn>         
1           1 22.40607 mins   62867.10 mins  
2           2 16.99238 mins   83382.58 mins  
3           3 15.92316 mins   64171.70 mins  
4           4 15.60619 mins   98489.07 mins  
5           5 16.01644 mins   92569.92 mins  
6           6 17.94457 mins   79775.02 mins  
7           7 22.39733 mins   64009.25 mins  
```
From the data, we know that on average, Cyclistic Bikes tend to get used more often on the weekends, namely Fridays, Saturdays and Sundays, recording on average 17.94, 22.39 and 22.40 mins respectively.

To calculate the mode of day_of_week, we will be utilizing the following code chunk.
```TSQL
getmode <- function(v) {
  uniqv <- unique(v)
  uniqv[which.max(tabulate(match(v, uniqv)))]
}

weekday_mode <- getmode(merged_df2023$day_of_week)

print(weekday_mode)
```
The following output in recorded:
```TSQL
[1] 7
```
From the results, we know that Cyclistic Bikes get used the most on Saturdays.
