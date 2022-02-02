Bike_Riding
================
Onyedika Obiakarije
2/1/2022

## Cyclistics Bike-Share Analysis Case Study

This is the first case study of Google Capstone. In this case study, I
will perform an analysis. I will be following the data analysis process:
ask, prepare, process, analyze, share, and act.

### Asking Phases.

**Scenario**

You are a junior data analyst working in the marketing analyst team at
Cyclistic, a bike-share company in Chicago. The director of marketing
believes the company’s future success depends on maximizing the number
of annual memberships. Therefore, your team wants to understand how
casual riders and annual members use Cyclistic bikes differently. From
these insights, your team will design a new marketing strategy to
convert casual riders into annual members. But first, Cyclistic
executives must approve your recommendations, so they must be backed up
with compelling data insights and professional data visualizations.

**Characters and teams**

**Cyclistic:** A bike-share program that features more than 5,800
bicycles and 600 docking stations. Cyclistic sets itself apart by also
offering reclining bikes, hand tricycles, and cargo bikes, making
bike-share more inclusive to people with disabilities and riders who
can’t use a standard two-wheeled bike. The majority of riders opt for
traditional bikes; about 8% of riders use the assertive options.
Cyclistic users are more likely to ride for leisure, but about 30% use
them to commute to work each day.

**Lily Moreno:** The director of marketing and your manager. Moreno is
responsible for the development of campaigns and initiatives to promote
the bike-share program. These may include email, social media, and other
channels.

**Cyclistic marketing analytics team:** A team of data analysts who are
responsible for collecting, analyzing, and reporting data that helps
guide Cyclistic marketing strategy. You joined this team six months ago
and have been busy learning about Cyclistic’s mission and business goals
— as well as how you, as a junior data analyst, can help Cyclistic
achieve them.

**Cyclistic executive team:** The notoriously detail-oriented executive
team will decide whether to approve the recommended marketing program.

**Guiding Questions**

**● What is the problem you are trying to solve?**

Build a profile for annual member and convert casual riders into annual
members.

**● How can your insights drive business decisions?**

My insights will help the marketing team increase annual member.

### Prepare

Data from <https://divvy-tripdata.s3.amazonaws.com/index.html>. The data
I will be using is from December 2020 to November 2021.

**Guiding Questions**

**● Where is your data located?**

Data is located here
<https://divvy-tripdata.s3.amazonaws.com/index.html>.

**● How is the data organized?**

The data set is separated by months with identical label columns.

**● Are there issues with bias or credibility in this data? Does your
data ROCCC?**

I do not think there are any bias because the dataset belongs to their
client.The data is credibility and it is reliable, original,
comprehensive, current and cited.

**● How are you addressing licensing, privacy, security, and
accessibility?**

The data do not have any personal information and the company handle the
licensing.

**● How did you verify the data’s integrity?**

All dataset has identical columns and has the correct type of data.

**● How does it help you answer your question?**

It has relevant data to answer my questions.

**● Are there any problems with the data?**

### Process

``` r
library(tidyverse) #for data wrangling
```

    ## Warning: package 'tidyverse' was built under R version 4.0.5

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.4     v dplyr   1.0.7
    ## v tidyr   1.1.4     v stringr 1.4.0
    ## v readr   2.1.1     v forcats 0.5.1

    ## Warning: package 'ggplot2' was built under R version 4.0.5

    ## Warning: package 'tibble' was built under R version 4.0.5

    ## Warning: package 'tidyr' was built under R version 4.0.5

    ## Warning: package 'readr' was built under R version 4.0.5

    ## Warning: package 'purrr' was built under R version 4.0.5

    ## Warning: package 'dplyr' was built under R version 4.0.5

    ## Warning: package 'forcats' was built under R version 4.0.5

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(lubridate) #for time and date
```

    ## Warning: package 'lubridate' was built under R version 4.0.5

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
library(dplyr) #for bind_row
library(ggplot2) #for visualize
```

``` r
# Set working directories.
setwd("C:/Users/harry/Desktop/Class project/github rep/Google-Capstone-Projects")
```

``` r
# load data sets.
Dec_2020 <- read_csv("202011-divvy-tripdata.csv")
```

    ## Rows: 259716 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
Jan_2021 <- read_csv("202012-divvy-tripdata.csv")
```

    ## Rows: 131573 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
Feb_2021 <- read_csv("202101-divvy-tripdata.csv")
```

    ## Rows: 96834 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
Mar_2021 <- read_csv("202102-divvy-tripdata.csv")
```

    ## Rows: 49622 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
Apr_2021 <- read_csv("202103-divvy-tripdata.csv")
```

    ## Rows: 228496 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
May_2021 <- read_csv("202104-divvy-tripdata.csv")
```

    ## Rows: 337230 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
Jun_2021 <- read_csv("202105-divvy-tripdata.csv")
```

    ## Rows: 531633 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
Jul_2021 <- read_csv("202106-divvy-tripdata.csv")
```

    ## Rows: 729595 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
Aug_2021 <- read_csv("202107-divvy-tripdata.csv")
```

    ## Rows: 822410 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
Sep_2021 <- read_csv("202108-divvy-tripdata.csv")
```

    ## Rows: 804352 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
Oct_2021 <- read_csv("202109-divvy-tripdata.csv")
```

    ## Rows: 756147 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
Nov_2021 <- read_csv("202110-divvy-tripdata.csv")
```

    ## Rows: 631226 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# a quick check to see if all column names are named equally
colnames(Dec_2020)
```

    ##  [1] "ride_id"            "rideable_type"      "started_at"        
    ##  [4] "ended_at"           "start_station_name" "start_station_id"  
    ##  [7] "end_station_name"   "end_station_id"     "start_lat"         
    ## [10] "start_lng"          "end_lat"            "end_lng"           
    ## [13] "member_casual"

``` r
colnames(Mar_2021)
```

    ##  [1] "ride_id"            "rideable_type"      "started_at"        
    ##  [4] "ended_at"           "start_station_name" "start_station_id"  
    ##  [7] "end_station_name"   "end_station_id"     "start_lat"         
    ## [10] "start_lng"          "end_lat"            "end_lng"           
    ## [13] "member_casual"

``` r
colnames(Jun_2021)
```

    ##  [1] "ride_id"            "rideable_type"      "started_at"        
    ##  [4] "ended_at"           "start_station_name" "start_station_id"  
    ##  [7] "end_station_name"   "end_station_id"     "start_lat"         
    ## [10] "start_lng"          "end_lat"            "end_lng"           
    ## [13] "member_casual"

``` r
colnames(Sep_2021)
```

    ##  [1] "ride_id"            "rideable_type"      "started_at"        
    ##  [4] "ended_at"           "start_station_name" "start_station_id"  
    ##  [7] "end_station_name"   "end_station_id"     "start_lat"         
    ## [10] "start_lng"          "end_lat"            "end_lng"           
    ## [13] "member_casual"

``` r
# Convert some columns to characters.
Dec_2020 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
Jan_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
Feb_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
Mar_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
Apr_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
May_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
Jun_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
Jul_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
Aug_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
Sep_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
Oct_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
Nov_2021 <- mutate(Dec_2020, start_station_id = as.character(start_station_id),
                   end_station_id = as.character(end_station_id))
```

``` r
#Combining the data sets into Seasons
Winter <- bind_rows(Dec_2020, Jan_2021, Feb_2021) #as q1

Spring <- bind_rows(Mar_2021,Apr_2021, May_2021)  #as q2
  
Summer <- bind_rows(Jun_2021, Jul_2021, Aug_2021) #as q3

Autumn <- bind_rows(Sep_2021, Oct_2021, Nov_2021) #as q4
```

``` r
#Inspect the data
str(Winter)
```

    ## spec_tbl_df [779,148 x 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ ride_id           : chr [1:779148] "BD0A6FF6FFF9B921" "96A7A7A4BDE4F82D" "C61526D06582BDC5" "E533E89C32080B9E" ...
    ##  $ rideable_type     : chr [1:779148] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
    ##  $ started_at        : POSIXct[1:779148], format: "2020-11-01 13:36:00" "2020-11-01 10:03:26" ...
    ##  $ ended_at          : POSIXct[1:779148], format: "2020-11-01 13:45:40" "2020-11-01 10:14:45" ...
    ##  $ start_station_name: chr [1:779148] "Dearborn St & Erie St" "Franklin St & Illinois St" "Lake Shore Dr & Monroe St" "Leavitt St & Chicago Ave" ...
    ##  $ start_station_id  : chr [1:779148] "110" "672" "76" "659" ...
    ##  $ end_station_name  : chr [1:779148] "St. Clair St & Erie St" "Noble St & Milwaukee Ave" "Federal St & Polk St" "Stave St & Armitage Ave" ...
    ##  $ end_station_id    : chr [1:779148] "211" "29" "41" "185" ...
    ##  $ start_lat         : num [1:779148] 41.9 41.9 41.9 41.9 41.9 ...
    ##  $ start_lng         : num [1:779148] -87.6 -87.6 -87.6 -87.7 -87.6 ...
    ##  $ end_lat           : num [1:779148] 41.9 41.9 41.9 41.9 41.9 ...
    ##  $ end_lng           : num [1:779148] -87.6 -87.7 -87.6 -87.7 -87.6 ...
    ##  $ member_casual     : chr [1:779148] "casual" "casual" "casual" "casual" ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   ride_id = col_character(),
    ##   ..   rideable_type = col_character(),
    ##   ..   started_at = col_datetime(format = ""),
    ##   ..   ended_at = col_datetime(format = ""),
    ##   ..   start_station_name = col_character(),
    ##   ..   start_station_id = col_double(),
    ##   ..   end_station_name = col_character(),
    ##   ..   end_station_id = col_double(),
    ##   ..   start_lat = col_double(),
    ##   ..   start_lng = col_double(),
    ##   ..   end_lat = col_double(),
    ##   ..   end_lng = col_double(),
    ##   ..   member_casual = col_character()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
str(Spring)
```

    ## spec_tbl_df [779,148 x 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ ride_id           : chr [1:779148] "BD0A6FF6FFF9B921" "96A7A7A4BDE4F82D" "C61526D06582BDC5" "E533E89C32080B9E" ...
    ##  $ rideable_type     : chr [1:779148] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
    ##  $ started_at        : POSIXct[1:779148], format: "2020-11-01 13:36:00" "2020-11-01 10:03:26" ...
    ##  $ ended_at          : POSIXct[1:779148], format: "2020-11-01 13:45:40" "2020-11-01 10:14:45" ...
    ##  $ start_station_name: chr [1:779148] "Dearborn St & Erie St" "Franklin St & Illinois St" "Lake Shore Dr & Monroe St" "Leavitt St & Chicago Ave" ...
    ##  $ start_station_id  : chr [1:779148] "110" "672" "76" "659" ...
    ##  $ end_station_name  : chr [1:779148] "St. Clair St & Erie St" "Noble St & Milwaukee Ave" "Federal St & Polk St" "Stave St & Armitage Ave" ...
    ##  $ end_station_id    : chr [1:779148] "211" "29" "41" "185" ...
    ##  $ start_lat         : num [1:779148] 41.9 41.9 41.9 41.9 41.9 ...
    ##  $ start_lng         : num [1:779148] -87.6 -87.6 -87.6 -87.7 -87.6 ...
    ##  $ end_lat           : num [1:779148] 41.9 41.9 41.9 41.9 41.9 ...
    ##  $ end_lng           : num [1:779148] -87.6 -87.7 -87.6 -87.7 -87.6 ...
    ##  $ member_casual     : chr [1:779148] "casual" "casual" "casual" "casual" ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   ride_id = col_character(),
    ##   ..   rideable_type = col_character(),
    ##   ..   started_at = col_datetime(format = ""),
    ##   ..   ended_at = col_datetime(format = ""),
    ##   ..   start_station_name = col_character(),
    ##   ..   start_station_id = col_double(),
    ##   ..   end_station_name = col_character(),
    ##   ..   end_station_id = col_double(),
    ##   ..   start_lat = col_double(),
    ##   ..   start_lng = col_double(),
    ##   ..   end_lat = col_double(),
    ##   ..   end_lng = col_double(),
    ##   ..   member_casual = col_character()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
str(Summer)
```

    ## spec_tbl_df [779,148 x 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ ride_id           : chr [1:779148] "BD0A6FF6FFF9B921" "96A7A7A4BDE4F82D" "C61526D06582BDC5" "E533E89C32080B9E" ...
    ##  $ rideable_type     : chr [1:779148] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
    ##  $ started_at        : POSIXct[1:779148], format: "2020-11-01 13:36:00" "2020-11-01 10:03:26" ...
    ##  $ ended_at          : POSIXct[1:779148], format: "2020-11-01 13:45:40" "2020-11-01 10:14:45" ...
    ##  $ start_station_name: chr [1:779148] "Dearborn St & Erie St" "Franklin St & Illinois St" "Lake Shore Dr & Monroe St" "Leavitt St & Chicago Ave" ...
    ##  $ start_station_id  : chr [1:779148] "110" "672" "76" "659" ...
    ##  $ end_station_name  : chr [1:779148] "St. Clair St & Erie St" "Noble St & Milwaukee Ave" "Federal St & Polk St" "Stave St & Armitage Ave" ...
    ##  $ end_station_id    : chr [1:779148] "211" "29" "41" "185" ...
    ##  $ start_lat         : num [1:779148] 41.9 41.9 41.9 41.9 41.9 ...
    ##  $ start_lng         : num [1:779148] -87.6 -87.6 -87.6 -87.7 -87.6 ...
    ##  $ end_lat           : num [1:779148] 41.9 41.9 41.9 41.9 41.9 ...
    ##  $ end_lng           : num [1:779148] -87.6 -87.7 -87.6 -87.7 -87.6 ...
    ##  $ member_casual     : chr [1:779148] "casual" "casual" "casual" "casual" ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   ride_id = col_character(),
    ##   ..   rideable_type = col_character(),
    ##   ..   started_at = col_datetime(format = ""),
    ##   ..   ended_at = col_datetime(format = ""),
    ##   ..   start_station_name = col_character(),
    ##   ..   start_station_id = col_double(),
    ##   ..   end_station_name = col_character(),
    ##   ..   end_station_id = col_double(),
    ##   ..   start_lat = col_double(),
    ##   ..   start_lng = col_double(),
    ##   ..   end_lat = col_double(),
    ##   ..   end_lng = col_double(),
    ##   ..   member_casual = col_character()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
str(Autumn)
```

    ## spec_tbl_df [779,148 x 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ ride_id           : chr [1:779148] "BD0A6FF6FFF9B921" "96A7A7A4BDE4F82D" "C61526D06582BDC5" "E533E89C32080B9E" ...
    ##  $ rideable_type     : chr [1:779148] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
    ##  $ started_at        : POSIXct[1:779148], format: "2020-11-01 13:36:00" "2020-11-01 10:03:26" ...
    ##  $ ended_at          : POSIXct[1:779148], format: "2020-11-01 13:45:40" "2020-11-01 10:14:45" ...
    ##  $ start_station_name: chr [1:779148] "Dearborn St & Erie St" "Franklin St & Illinois St" "Lake Shore Dr & Monroe St" "Leavitt St & Chicago Ave" ...
    ##  $ start_station_id  : chr [1:779148] "110" "672" "76" "659" ...
    ##  $ end_station_name  : chr [1:779148] "St. Clair St & Erie St" "Noble St & Milwaukee Ave" "Federal St & Polk St" "Stave St & Armitage Ave" ...
    ##  $ end_station_id    : chr [1:779148] "211" "29" "41" "185" ...
    ##  $ start_lat         : num [1:779148] 41.9 41.9 41.9 41.9 41.9 ...
    ##  $ start_lng         : num [1:779148] -87.6 -87.6 -87.6 -87.7 -87.6 ...
    ##  $ end_lat           : num [1:779148] 41.9 41.9 41.9 41.9 41.9 ...
    ##  $ end_lng           : num [1:779148] -87.6 -87.7 -87.6 -87.7 -87.6 ...
    ##  $ member_casual     : chr [1:779148] "casual" "casual" "casual" "casual" ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   ride_id = col_character(),
    ##   ..   rideable_type = col_character(),
    ##   ..   started_at = col_datetime(format = ""),
    ##   ..   ended_at = col_datetime(format = ""),
    ##   ..   start_station_name = col_character(),
    ##   ..   start_station_id = col_double(),
    ##   ..   end_station_name = col_character(),
    ##   ..   end_station_id = col_double(),
    ##   ..   start_lat = col_double(),
    ##   ..   start_lng = col_double(),
    ##   ..   end_lat = col_double(),
    ##   ..   end_lng = col_double(),
    ##   ..   member_casual = col_character()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
#Combine all data into one
all_trips <- bind_rows(Winter, Spring, Summer, Autumn)
```

``` r
# Remove unnecessary columns
all_trips <- subset(all_trips, select = -c(start_lat, start_lng, end_lat, end_lng))
```

``` r
colnames(all_trips) #Show colnames
```

    ## [1] "ride_id"            "rideable_type"      "started_at"        
    ## [4] "ended_at"           "start_station_name" "start_station_id"  
    ## [7] "end_station_name"   "end_station_id"     "member_casual"

``` r
nrow(all_trips) #no_ of rows
```

    ## [1] 3116592

``` r
dim(all_trips) #Dimensions of the data
```

    ## [1] 3116592       9

``` r
head(all_trips) #load the first 6 row of the data
```

    ## # A tibble: 6 x 9
    ##   ride_id rideable_type started_at          ended_at            start_station_n~
    ##   <chr>   <chr>         <dttm>              <dttm>              <chr>           
    ## 1 BD0A6F~ electric_bike 2020-11-01 13:36:00 2020-11-01 13:45:40 Dearborn St & E~
    ## 2 96A7A7~ electric_bike 2020-11-01 10:03:26 2020-11-01 10:14:45 Franklin St & I~
    ## 3 C61526~ electric_bike 2020-11-01 00:34:05 2020-11-01 01:03:06 Lake Shore Dr &~
    ## 4 E533E8~ electric_bike 2020-11-01 00:45:16 2020-11-01 00:54:31 Leavitt St & Ch~
    ## 5 1C9F4E~ electric_bike 2020-11-01 15:43:25 2020-11-01 16:16:52 Buckingham Foun~
    ## 6 725958~ electric_bike 2020-11-14 15:55:17 2020-11-14 16:44:38 Wabash Ave & 16~
    ## # ... with 4 more variables: start_station_id <chr>, end_station_name <chr>,
    ## #   end_station_id <chr>, member_casual <chr>

``` r
summary(all_trips) #Shows the statistical summary
```

    ##    ride_id          rideable_type        started_at                 
    ##  Length:3116592     Length:3116592     Min.   :2020-11-01 00:00:08  
    ##  Class :character   Class :character   1st Qu.:2020-11-06 20:13:53  
    ##  Mode  :character   Mode  :character   Median :2020-11-10 16:17:15  
    ##                                        Mean   :2020-11-13 05:20:02  
    ##                                        3rd Qu.:2020-11-19 15:59:47  
    ##                                        Max.   :2020-11-30 23:56:22  
    ##     ended_at                   start_station_name start_station_id  
    ##  Min.   :2020-11-01 00:02:20   Length:3116592     Length:3116592    
    ##  1st Qu.:2020-11-06 20:36:08   Class :character   Class :character  
    ##  Median :2020-11-10 16:32:15   Mode  :character   Mode  :character  
    ##  Mean   :2020-11-13 05:39:45                                        
    ##  3rd Qu.:2020-11-19 16:18:54                                        
    ##  Max.   :2020-12-01 17:28:22                                        
    ##  end_station_name   end_station_id     member_casual     
    ##  Length:3116592     Length:3116592     Length:3116592    
    ##  Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character  
    ##                                                          
    ##                                                          
    ## 

``` r
#drop values with NA
all_trips <- na.omit(all_trips)

# Filter out started_at data that are less than ended_at data, avoiding negative value
all_trips <- all_trips %>% filter(all_trips$started_at < all_trips$ended_at)

#Create a new column and name it ride_length
all_trips$ride_length <- all_trips$ended_at - all_trips$started_at

#Format the colummn to hour, minutes, and seconds
all_trips$ride_length <- hms::hms(seconds_to_period(all_trips$ride_length))

#Convert ride_length to number for easy calculation.
all_trips <- mutate(all_trips, ride_length = as.numeric(ride_length))

#Create a new column called day_of_week
all_trips$day_of_week <- wday(all_trips$started_at, label = TRUE)

#Save file as a CSV
#all_trips %>% write.csv("clean_ride.csv")
```

**Guiding Questions**

**● What tools are you choosing and why?**

I am using R. I am using R because of the amount of data and to expand
my knowledge in R.

**● Have you ensured your data’s integrity?**

Yes, the dataset has identical columns.

**● What steps have you taken to ensure that your data is clean?**

I converted some columns, so that I would be able to merge it. Next, I
remove the NA data and unnecessary columns. I filter out the started_at
data that are less than the ended_at data, then I create two new columns
and named them ride_length and day_of_week.Next, I formatted the
ride_length column to hour, minutes, and seconds.

**● How can you verify that your data is clean and ready to analyze?**

**● Have you documented your cleaning process so you can review and
share those results?**

Yes, all document are store in R markdown.

### Analyze

``` r
# Descriptive analysis on ride_length
mean(all_trips$ride_length) #average ride
```

    ## [1] 1203.182

``` r
quantile(all_trips$ride_length, .25) #Q1
```

    ## 25% 
    ## 388

``` r
quantile(all_trips$ride_length, .50) #Median
```

    ## 50% 
    ## 692

``` r
#median(all_trips$ride_length) #midpoint
quantile(all_trips$ride_length, .75) #Q3
```

    ##  75% 
    ## 1285

``` r
max(all_trips$ride_length) #longest ride
```

    ## [1] 2156040

``` r
min(all_trips$ride_length) #shortest ride
```

    ## [1] 1

``` r
sd(all_trips$ride_length)  #Standard Deviation 
```

    ## [1] 8762.412

``` r
summary(all_trips$ride_length)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##       1     388     692    1203    1285 2156040

``` r
#Compare ride_length of member_casual
 aggregate(all_trips$ride_length ~ all_trips$member_casual, FUN = sum)
```

    ##   all_trips$member_casual all_trips$ride_length
    ## 1                  casual            1756029792
    ## 2                  member            1448034648

``` r
# aggregate(all_trips$ride_length ~ all_trips$member_casual, FUN = mean)
# aggregate(all_trips$ride_length ~ all_trips$member_casual, FUN = median)
# aggregate(all_trips$ride_length ~ all_trips$member_casual, FUN = max)
# aggregate(all_trips$ride_length ~ all_trips$member_casual, FUN = min)
```

``` r
#Average ride_length by each day for member_casual column.
aggregate(all_trips$ride_length ~ all_trips$member_casual + all_trips$day_of_week, FUN = mean)
```

    ##    all_trips$member_casual all_trips$day_of_week all_trips$ride_length
    ## 1                   casual                   Sun             2459.6935
    ## 2                   member                   Sun              882.9196
    ## 3                   casual                   Mon             1725.7497
    ## 4                   member                   Mon              745.4346
    ## 5                   casual                   Tue             1728.4028
    ## 6                   member                   Tue              761.2670
    ## 7                   casual                   Wed             1535.9677
    ## 8                   member                   Wed              754.6756
    ## 9                   casual                   Thu             1827.8159
    ## 10                  member                   Thu              779.3516
    ## 11                  casual                   Fri             1919.1907
    ## 12                  member                   Fri              816.4063
    ## 13                  casual                   Sat             2236.8528
    ## 14                  member                   Sat              934.1594

``` r
#Number of rides by ride type
all_trips %>% 
  mutate(weekday = wday(started_at, label = TRUE)) %>%  #weekday field
  group_by(member_casual, weekday) %>%                  #group by usertype and weekday
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>%  #average duration
  arrange(member_casual, weekday)  %>%                  #Sort
  #visualization
  ggplot(aes(x = weekday, y = number_of_rides, fill = member_casual)) +
  geom_col(position = "dodge")
```

    ## `summarise()` has grouped output by 'member_casual'. You can override using the `.groups` argument.

![](Ride_Sharing_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
#Average duration
all_trips %>% 
  mutate(weekday = wday(started_at, label = TRUE)) %>% 
  group_by(member_casual, weekday) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(member_casual, weekday)  %>% 
  ggplot(aes(x = weekday, y = average_duration, fill = member_casual)) +
  geom_col(position = "dodge")
```

    ## `summarise()` has grouped output by 'member_casual'. You can override using the `.groups` argument.

![](Ride_Sharing_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

``` r
#Distributed within the weekday
all_trips %>% 
  group_by(day_of_week) %>%
  summarise(count = length(ride_id),
            '%' = (length(ride_id) / nrow(all_trips)) * 100,
            'member' = (sum(member_casual == "member") / length(ride_id)) * 100,
            'casual' = (sum(member_casual == "casual") / length(ride_id)) * 100,
            'Member x Casual Perc Diferrent' = member - casual)
```

    ## # A tibble: 7 x 6
    ##   day_of_week  count   `%` member casual `Member x Casual Perc Diferrent`
    ##   <ord>        <int> <dbl>  <dbl>  <dbl>                            <dbl>
    ## 1 Sun         391584  14.7   59.1   40.9                            18.2 
    ## 2 Mon         408768  15.3   74.2   25.8                            48.4 
    ## 3 Tue         312036  11.7   74.5   25.5                            49.0 
    ## 4 Wed         322392  12.1   74.7   25.3                            49.4 
    ## 5 Thu         350700  13.2   71.1   28.9                            42.3 
    ## 6 Fri         403296  15.1   67.2   32.8                            34.3 
    ## 7 Sat         474216  17.8   54.9   45.1                             9.89

``` r
ggplot(all_trips, aes(day_of_week, fill=member_casual)) + 
  geom_bar() +
  labs(x="Weekday", title = "Distibution by weekday")  
```

![](Ride_Sharing_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

``` r
  #coord_flip()
```

``` r
#Distributed by ride type
all_trips %>% 
  group_by(rideable_type) %>%
  summarise(count = length(ride_id),
            '%' = (length(ride_id) / nrow(all_trips)) * 100,
            'member' = (sum(member_casual == "member") / length(ride_id)) * 100,
            'casual' = (sum(member_casual == "casual") / length(ride_id)) * 100,
            'Member x Casual Perc Diferrent' = member - casual)
```

    ## # A tibble: 2 x 6
    ##   rideable_type   count   `%` member casual `Member x Casual Perc Diferrent`
    ##   <chr>           <int> <dbl>  <dbl>  <dbl>                            <dbl>
    ## 1 docked_bike   1805208  67.8   69.6   30.4                             39.2
    ## 2 electric_bike  857784  32.2   62.1   37.9                             24.2

``` r
ggplot(all_trips, aes(rideable_type, fill=member_casual)) + 
  geom_bar() +
  labs(x="Riderable type", title = "Distibution by type of bikes") 
```

![](Ride_Sharing_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

**Guiding Questions**

**● How should you organize your data to perform analysis on it?**

All data sets should be combine into one data set.

**● Has your data been properly formatted?**

Yes, my data has been properly formatted. All the column has their
collect data type.

**● What surprises did you discover in the data?**

Casual have more ride than members.

**● What trends or relationships did you find in the data?**
