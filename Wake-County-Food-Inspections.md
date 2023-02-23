# Wake County Restaurants and their Sanitation Scores

## Objective

The aim of this Project is to help Wake County residents make informed decisions
about where they eat by providing them with a list of restaurants with
sanitation scores above 90 (excellent) and a list of restaurants with
sanitation scores below 80 (unacceptable). This will be done by exploring two
data sets that Wake County has made available to the public: the Restaurants in
Wake County data set, and the Food Inspections data set. The list presented to
Wake County citizens will include the names, addresses, and phone numbers of the
aforementioned restaurants.


## Restaurants

The table below contains information about all of the restaurants in Wake
County. Each restaurant has a HSISID, which serves as a unique identifier. Other
information contained in the table includes the restaurants' names, addresses,
phone numbers, and the dates of their opening.


```r
restaurants_file <- "Restaurants_in_Wake_County.csv"
Restaurants <- read_csv(restaurants_file)
```

```
## Rows: 3715 Columns: 15
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (11): HSISID, NAME, ADDRESS1, ADDRESS2, CITY, STATE, POSTALCODE, PHONENU...
## dbl  (4): OBJECTID, PERMITID, X, Y
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
Restaurants
```

```
## # A tibble: 3,715 x 15
##    OBJECTID HSISID     NAME  ADDRE~1 ADDRE~2 CITY  STATE POSTA~3 PHONE~4 RESTA~5
##       <dbl> <chr>      <chr> <chr>   <chr>   <chr> <chr> <chr>   <chr>   <chr>  
##  1  3140310 040920105~ O'Ch~ 101 AS~ <NA>    CARY  NC    27511-~ (919) ~ 1991/0~
##  2  3140311 040920106~ Roas~ 7 S WE~ <NA>    RALE~ NC    27603-~ (919) ~ 1991/0~
##  3  3140312 040920140~ Assa~ 7417 S~ <NA>    FUQU~ NC    27526   (919) ~ 2004/0~
##  4  3140313 040921101~ Sout~ 2600 R~ <NA>    RALE~ NC    27610-~ (919) ~ 1997/0~
##  5  3140314 040920134~ Pine~ 3300 G~ <NA>    CLAY~ NC    27520-~ (919) ~ 2001/1~
##  6  3140315 040920100~ AUBR~ 38 N M~ <NA>    WEND~ NC    27591   (919) ~ 1991/0~
##  7  3140316 040920100~ Boja~ 1013 N~ <NA>    RALE~ NC    27601-~ (919) ~ 1991/0~
##  8  3140317 040920102~ Firs~ 99 N S~ <NA>    RALE~ NC    27603-~ (919) ~ 1991/0~
##  9  3140318 040920108~ 42nd~ 508 W ~ <NA>    RALE~ NC    27603-~ (919) ~ 1991/0~
## 10  3140319 040920102~ Fran~ 2030 N~ <NA>    RALE~ NC    27610-~ (919) ~ 1991/0~
## # ... with 3,705 more rows, 5 more variables: FACILITYTYPE <chr>,
## #   PERMITID <dbl>, X <dbl>, Y <dbl>, GEOCODESTATUS <chr>, and abbreviated
## #   variable names 1: ADDRESS1, 2: ADDRESS2, 3: POSTALCODE, 4: PHONENUMBER,
## #   5: RESTAURANTOPENDATE
```

## Sanitation Scores

The table below contains the sanitation scores of all of the restaurants in Wake
County. Each restaurant is identified by its HSISID, which serves as a key to
access more information about the restaurant in the Restaurants data table.


```r
inspections_file <- "Food_Inspections.csv"
Inspections <- read_csv(inspections_file)
```

```
## Rows: 54894 Columns: 8
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (5): HSISID, DATE_, DESCRIPTION, TYPE, INSPECTOR
## dbl (3): OBJECTID, SCORE, PERMITID
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
Inspections
```

```
## # A tibble: 54,894 x 8
##    OBJECTID HSISID      SCORE DATE_                DESCR~1 TYPE  INSPE~2 PERMI~3
##       <dbl> <chr>       <dbl> <chr>                <chr>   <chr> <chr>     <dbl>
##  1 39043897 04092017542  94.5 2017/04/07 04:00:00~ "Inspe~ Insp~ Anne-K~   18439
##  2 39043898 04092017542  92   2017/11/08 05:00:00~ "manag~ Insp~ Laura ~   18439
##  3 39043899 04092017542  95   2018/03/23 04:00:00~  <NA>   Insp~ Laura ~   18439
##  4 39043900 04092017542  93.5 2018/09/07 04:00:00~ "*NOTI~ Insp~ Laura ~   18439
##  5 39043901 04092017542  93   2019/04/04 04:00:00~ "*NOTI~ Insp~ Joanne~   18439
##  6 39043902 04092017542  93.5 2019/10/07 04:00:00~ "Follo~ Insp~ Naterr~   18439
##  7 39043903 04092017542  92.5 2020/05/19 04:00:00~ "*NOTI~ Insp~ Naterr~   18439
##  8 39043904 04092017542  94   2020/10/09 04:00:00~ "PIC c~ Insp~ Nicole~   18439
##  9 39043905 04092017542  94   2021/03/24 04:00:00~ "PIC c~ Insp~ Nicole~   18439
## 10 39043906 04092017542  92   2021/07/20 04:00:00~ "Bathr~ Insp~ David ~   18439
## # ... with 54,884 more rows, and abbreviated variable names 1: DESCRIPTION,
## #   2: INSPECTOR, 3: PERMITID
```

## IDs of Restaurants with Sanitation Scores Above 90

The algorithm below filters the Inspections table for the HSISIDs of all of the
restaurants in Wake County that have sanitation scores above 90, and stores the
result as a list.


```r
ids_above_90 <- Inspections[Inspections$SCORE <= 90, "HSISID"]
ids_above_90 <- as.list(ids_above_90$HSISID)
```

## IDs of Restaurants with Sanitation Scores Below 80

The algorithm below filters the Inspections table for the HSISIDs of all of the
restaurants in Wake County that have sanitation scores below 80, and stores the
result as a list.


```r
ids_below_80 <- Inspections[Inspections$SCORE <= 80, "HSISID"]
ids_below_80 <- as.list(ids_below_80$HSISID)
```

## Restaurants with Sanitation Scores Above 90

The Restaurants table is filtered for names, addresses, and phone numbers of the
restaurants in Wake County that have sanitation scores above 90.



```r
restaurants_above_80 <- Restaurants[Restaurants$HSISID %in% ids_above_90,
                              c("NAME","ADDRESS1", "CITY", "STATE", "POSTALCODE",
                                "PHONENUMBER")]
restaurants_above_80
```

```
## # A tibble: 643 x 6
##    NAME                          ADDRESS1            CITY  STATE POSTA~1 PHONE~2
##    <chr>                         <chr>               <chr> <chr> <chr>   <chr>  
##  1 O'Charleys                    101 ASHVILLE AVE    CARY  NC    27511-~ (919) ~
##  2 Roast Grill                   7 S WEST ST         RALE~ NC    27603-~ (919) ~
##  3 Torero's Mexican Restaurant V 1207-C Kildaire Fa~ CARY  NC    27511   (919) ~
##  4 Han-Dee Hugo's #47            4120 GLENWOOD AVE   RALE~ NC    27612-~ (919) ~
##  5 China Chef                    930 US 64 HWY W     APEX  NC    27523   (919) ~
##  6 Los Tres Magueyes             110 SW MAYNARD RD   CARY  NC    27511-~ (919) ~
##  7 Parkside                      301 W MARTIN ST     RALE~ NC    27601-~ (984) ~
##  8 Barrys Cafe                   2851 Jones Frankli~ RALE~ NC    27606-~ (919) ~
##  9 BOJANGLES #15                 5409 CAPITAL BLVD   RALE~ NC    27616-~ (919) ~
## 10 NC Farm Bureau Cafeteria      5301 GLENWOOD AVE   RALE~ NC    27612-~ (919) ~
## # ... with 633 more rows, and abbreviated variable names 1: POSTALCODE,
## #   2: PHONENUMBER
```

## Restaurants with Sanitation Scores Below 80

The Restaurants table is filtered for names, addresses, and phone numbers of the
restaurants in Wake County that have sanitation scores below 80.



```r
restaurants_below_80 <- Restaurants[Restaurants$HSISID %in% ids_below_80,
                              c("NAME","ADDRESS1", "CITY", "STATE", "POSTALCODE",
                                "PHONENUMBER")]
restaurants_below_80
```

```
## # A tibble: 47 x 6
##    NAME                              ADDRESS1        CITY  STATE POSTA~1 PHONE~2
##    <chr>                             <chr>           <chr> <chr> <chr>   <chr>  
##  1 Middle Creek Park                 151 Middle Cre~ APEX  NC    27502   (919) ~
##  2 Wang's Kitchen                    3416 POOLE RD   RALE~ NC    27610-~ (919) ~
##  3 AMF South Hills Snack Bar         301 NOTTINGHAM~ CARY  NC    27511-~ (919) ~
##  4 Moore Square Magnet Middle School 301 S PERSON ST RALE~ NC    27601-~ (919) ~
##  5 Holly Ridge Middle Sch. Cafeteria 950 HOLLY SPRI~ HOLL~ NC    27540-~ (919) ~
##  6 China King                        1861 Aversboro~ GARN~ NC    27529   (919) ~
##  7 Chinatown Express                 5800 Duraleigh~ RALE~ NC    27612   <NA>   
##  8 Turner Creek Elementary Cafeteria 6801 Turner Cr~ CARY  NC    27519   (919) ~
##  9 HONG KONG CHINESE KITCHEN         5563 WESTERN  ~ RALE~ NC    27606   (919) ~
## 10 Willow Creek Exxon                1133 OLD HONEY~ FUQU~ NC    27526-~ (919) ~
## # ... with 37 more rows, and abbreviated variable names 1: POSTALCODE,
## #   2: PHONENUMBER
```

