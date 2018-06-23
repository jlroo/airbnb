Code

-   [Show All Code](#)
-   [Hide All Code](#)
-   -   [Download Rmd](#)

Chicago Airbnb Analysis {.title .toc-ignore}
=======================

### *CME Group Foundation Business Analytics Lab* {.subtitle}

#### *Jose Luis Rodriguez* {.author}

#### *June 13, 2018* {.date}

* * * * *

Notebook Instructions
---------------------

* * * * *

-   This notebook is use to analyze airbnb data based on the Inside
    Airbnb project by Murray Cox.

#### Notebook Version

    platform       x86_64-apple-darwin15.6.0   
    arch           x86_64                      
    os             darwin15.6.0                
    system         x86_64, darwin15.6.0        
    status                                     
    major          3                           
    minor          5.0                         
    year           2018                        
    month          04                          
    day            23                          
    svn rev        74626                       
    language       R                           
    version.string R version 3.5.0 (2018-04-23)
    nickname       Joy in Playing   

### About

-   Airbnb claims to be part of the “sharing economy” and disrupting the
    hotel industry.

-   However, data shows that the majority of Airbnb listings in most
    cities are entire homes, many of which are rented all year round -
    disrupting housing and communities.

-   [http://insideairbnb.com/index.html](http://insideairbnb.com/index.html)

### Project Layout

    .
    └── Airbnb
        ├── airbnb-notebook.Rmd
        │
        ├── data
        │   ├── 2015
        │   │   ├── airbnb.csv
        │   │   ├── airbnb_calendar.csv
        │   │   ├── airbnb_clean.csv
        │   │   ├── airbnb_loc.csv
        │   │   ├── airbnb_nlp.csv
        │   │   ├── airbnb_reviews.csv
        │   │   ├── airbnb_summary.csv
        │   │   └── airbnb_urls.csv
        │   │
        │   ├── 2017
        │   │   ├── airbnb.csv
        │   │   ├── airbnb_calendar.csv
        │   │   ├── airbnb_reviews.csv
        │   │   └── airbnb_summary.csv
        │   │
        │   ├── location
        │   │   ├── 2015-neighbourhoods.csv
        │   │   ├── 2015-neighbourhoods.geojson
        │   │   ├── 2017-neighbourhoods.csv
        │   │   ├── 2017-neighbourhoods.geojson
        │   │   └── names-zipcode.csv
        │   │
        │   └── raw
        │       ├── 2015-airbnb-listings.csv.gz
        │       ├── 2015-calendar.csv.gz
        │       ├── 2015-neighbourhoods.zip
        │       ├── 2015-reviews.csv.gz
        │       ├── 2017-airbnb-listings.csv.gz
        │       ├── 2017-calendar.csv.gz
        │       ├── 2017-neighbourhoods.zip
        │       └── 2017-reviews.csv.gz
        │
        ├── resources
        │   ├── Airbnb-Proposal.docx
        │   └── Airbnb-Proposal.pdf
        │
        └── scripts

### Load Packages in R/RStudio

We are going to use tidyverse a collection of R packages designed for
data science.

-   Info: [https://www.tidyverse.org](https://www.tidyverse.org)

<!-- -->

    Loading required package: tidyverse
    [30m── [1mAttaching packages[22m ────────────────────────────────────────── tidyverse 1.2.1 ──[39m
    [30m[32m✔[30m [34mggplot2[30m 2.2.1     [32m✔[30m [34mpurrr  [30m 0.2.4
    [32m✔[30m [34mtibble [30m 1.4.2     [32m✔[30m [34mdplyr  [30m 0.7.4
    [32m✔[30m [34mtidyr  [30m 0.8.0     [32m✔[30m [34mstringr[30m 1.3.0
    [32m✔[30m [34mreadr  [30m 1.1.1     [32m✔[30m [34mforcats[30m 0.3.0[39m
    [30m── [1mConflicts[22m ───────────────────────────────────────────── tidyverse_conflicts() ──
    [31m✖[30m [34mdplyr[30m::[32mfilter()[30m masks [34mstats[30m::filter()
    [31m✖[30m [34mdplyr[30m::[32mlag()[30m    masks [34mstats[30m::lag()[39m

* * * * *

Data Import and Inspection
--------------------------

* * * * *

-   read dataset from 2015

``` {.r}
airbnb <- read_csv("data/2015/airbnb.csv")
```

### Inspect head and tail of the dataset

``` {.r}
head(airbnb)
```

``` {.r}
tail(airbnb)
```

``` {.r}
colnames(airbnb)
```

     [1] "id"                               "listing_url"                     
     [3] "scrape_id"                        "last_scraped"                    
     [5] "name"                             "summary"                         
     [7] "space"                            "description"                     
     [9] "experiences_offered"              "neighborhood_overview"           
    [11] "notes"                            "transit"                         
    [13] "thumbnail_url"                    "medium_url"                      
    [15] "picture_url"                      "xl_picture_url"                  
    [17] "host_id"                          "host_url"                        
    [19] "host_name"                        "host_since"                      
    [21] "host_location"                    "host_about"                      
    [23] "host_response_time"               "host_response_rate"              
    [25] "host_acceptance_rate"             "host_is_superhost"               
    [27] "host_thumbnail_url"               "host_picture_url"                
    [29] "host_neighbourhood"               "host_listings_count"             
    [31] "host_total_listings_count"        "host_verifications"              
    [33] "host_has_profile_pic"             "host_identity_verified"          
    [35] "street"                           "neighbourhood"                   
    [37] "neighbourhood_cleansed"           "neighbourhood_group_cleansed"    
    [39] "city"                             "state"                           
    [41] "zipcode"                          "market"                          
    [43] "smart_location"                   "country_code"                    
    [45] "country"                          "latitude"                        
    [47] "longitude"                        "is_location_exact"               
    [49] "property_type"                    "room_type"                       
    [51] "accommodates"                     "bathrooms"                       
    [53] "bedrooms"                         "beds"                            
    [55] "bed_type"                         "amenities"                       
    [57] "square_feet"                      "price"                           
    [59] "weekly_price"                     "monthly_price"                   
    [61] "security_deposit"                 "cleaning_fee"                    
    [63] "guests_included"                  "extra_people"                    
    [65] "minimum_nights"                   "maximum_nights"                  
    [67] "calendar_updated"                 "has_availability"                
    [69] "availability_30"                  "availability_60"                 
    [71] "availability_90"                  "availability_365"                
    [73] "calendar_last_scraped"            "number_of_reviews"               
    [75] "first_review"                     "last_review"                     
    [77] "review_scores_rating"             "review_scores_accuracy"          
    [79] "review_scores_cleanliness"        "review_scores_checkin"           
    [81] "review_scores_communication"      "review_scores_location"          
    [83] "review_scores_value"              "requires_license"                
    [85] "license"                          "jurisdiction_names"              
    [87] "instant_bookable"                 "cancellation_policy"             
    [89] "require_guest_profile_picture"    "require_guest_phone_verification"
    [91] "calculated_host_listings_count"   "reviews_per_month"               

* * * * *

Data Selection
--------------

* * * * *

-   Now lets clean the data and delete some unessary columns for this
    analysis

-   Extract the airbnb\_id to later use and identify the columns to
    remove

-   Since there are 92 features/columns we can split the column names
    vector into different chunks

-   The 92 features/columns are of variating types and measures we can
    split the dataset into diffent sections.

-   Such as features/columns related to links/urls or only text columns
    that we can use later for natural language processing.

-   Same process applies to features/columns related to location

-   Finally we can remove the columns from the new datasets to create a
    final dataset that will be more numeric in nature.

-   All datasets will be linked/related by the airbnb\_id

``` {.r}
airbnb <- rename(airbnb, airbnb_id = id)
airbnb_id <- airbnb$airbnb_id
```

``` {.r}
colnames(airbnb)[1:30]
```

     [1] "airbnb_id"             "listing_url"           "scrape_id"            
     [4] "last_scraped"          "name"                  "summary"              
     [7] "space"                 "description"           "experiences_offered"  
    [10] "neighborhood_overview" "notes"                 "transit"              
    [13] "thumbnail_url"         "medium_url"            "picture_url"          
    [16] "xl_picture_url"        "host_id"               "host_url"             
    [19] "host_name"             "host_since"            "host_location"        
    [22] "host_about"            "host_response_time"    "host_response_rate"   
    [25] "host_acceptance_rate"  "host_is_superhost"     "host_thumbnail_url"   
    [28] "host_picture_url"      "host_neighbourhood"    "host_listings_count"  

``` {.r}
colnames(airbnb)[31:65]
```

     [1] "host_total_listings_count"    "host_verifications"          
     [3] "host_has_profile_pic"         "host_identity_verified"      
     [5] "street"                       "neighbourhood"               
     [7] "neighbourhood_cleansed"       "neighbourhood_group_cleansed"
     [9] "city"                         "state"                       
    [11] "zipcode"                      "market"                      
    [13] "smart_location"               "country_code"                
    [15] "country"                      "latitude"                    
    [17] "longitude"                    "is_location_exact"           
    [19] "property_type"                "room_type"                   
    [21] "accommodates"                 "bathrooms"                   
    [23] "bedrooms"                     "beds"                        
    [25] "bed_type"                     "amenities"                   
    [27] "square_feet"                  "price"                       
    [29] "weekly_price"                 "monthly_price"               
    [31] "security_deposit"             "cleaning_fee"                
    [33] "guests_included"              "extra_people"                
    [35] "minimum_nights"              

``` {.r}
colnames(airbnb)[66:92]
```

     [1] "maximum_nights"                   "calendar_updated"                
     [3] "has_availability"                 "availability_30"                 
     [5] "availability_60"                  "availability_90"                 
     [7] "availability_365"                 "calendar_last_scraped"           
     [9] "number_of_reviews"                "first_review"                    
    [11] "last_review"                      "review_scores_rating"            
    [13] "review_scores_accuracy"           "review_scores_cleanliness"       
    [15] "review_scores_checkin"            "review_scores_communication"     
    [17] "review_scores_location"           "review_scores_value"             
    [19] "requires_license"                 "license"                         
    [21] "jurisdiction_names"               "instant_bookable"                
    [23] "cancellation_policy"              "require_guest_profile_picture"   
    [25] "require_guest_phone_verification" "calculated_host_listings_count"  
    [27] "reviews_per_month"               

### Select only columns related to url links

``` {.r}
airbnb_urls <- select(airbnb, contains("url"))
ulr_columns <- colnames(airbnb_urls)
airbnb_urls <- add_column(airbnb_urls, airbnb_id)
```

``` {.r}
head(airbnb_urls)
```

### Select only columns containg text

``` {.r}
text_columns <- c("host_name","name","amenities", "experiences_offered",
                  "host_verifications","transit","notes", 
                 "neighborhood_overview", "host_about", 
                 "description", "space","summary")
airbnb_nlp <- select(airbnb, text_columns)
airbnb_nlp <- add_column(airbnb_nlp, airbnb_id)
```

``` {.r}
head(airbnb_nlp)
```

### Select only columns related to listing location

``` {.r}
location_columns <- c("zipcode", "latitude", "longitude", "city", "state",
                     "street", "neighbourhood", "neighbourhood_cleansed",
                     "neighbourhood_group_cleansed","host_location", "host_neighbourhood",
                     "market", "smart_location", "jurisdiction_names", "country_code", 
                     "country")
airbnb_loc <- select(airbnb, location_columns)
airbnb_loc <- add_column(airbnb_loc, airbnb_id)
```

``` {.r}
head(airbnb_loc)
```

### Use select and one\_of function to remove the columns from previous datasets (ulr\_columns, text\_columns, location\_columns)

``` {.r}
# unique(as.character(airbnb$scrape_id))
remove_columns <- c(ulr_columns, text_columns, location_columns, "scrape_id", "last_scraped")
airbnb_clean <- select(airbnb, -one_of(remove_columns))
```

### Inspect the new more compacted dataset. By doing this we reduced the size by almost half

``` {.r}
head(airbnb_clean)
```

### Save the new dataset for reference and later use

``` {.r}
write_csv(airbnb_urls, "data/2015/airbnb_urls.csv")
write_csv(airbnb_nlp, "data/2015/airbnb_nlp.csv")
write_csv(airbnb_loc, "data/2015/airbnb_loc.csv")
write_csv(airbnb_clean, "data/2015/airbnb_clean.csv")
```

* * * * *

Data Types and Cleaning
-----------------------

* * * * *

``` {.r}
room_type <- airbnb_clean$room_type %>% 
  tolower() %>% 
  str_replace_all(., " ", "_") %>% 
  str_replace(., "home/apt","place")
airbnb_clean$room_type <- as_factor(room_type)
```

``` {.r}
# unique(airbnb_clean$bed_type)
bed_type <- airbnb_clean$bed_type %>% 
  tolower() %>% 
  str_replace_all(., " ", "_") %>% 
  str_replace(., "pull.*","sofa_bed") %>% 
  str_replace(., "real_.*","bed")
airbnb_clean$bed_type <- as_factor(bed_type)
```

``` {.r}
airbnb_clean <- airbnb_clean %>% 
  mutate(airbnb_id = as.character(airbnb_id)) %>% 
  mutate(host_id = as.character(host_id)) %>% 
  mutate(host_is_superhost = parse_logical(host_is_superhost)) %>% 
  mutate(host_has_profile_pic = parse_logical(host_has_profile_pic)) %>% 
  mutate(host_identity_verified = parse_logical(host_identity_verified)) %>% 
  mutate(is_location_exact = parse_logical(is_location_exact)) %>% 
  mutate(property_type = as_factor(tolower(property_type)))
```

``` {.r}
summary(airbnb_clean)
```

      airbnb_id           host_id            host_since         host_response_time
     Length:5147        Length:5147        Min.   :2008-05-06   Length:5147       
     Class :character   Class :character   1st Qu.:2012-12-27   Class :character  
     Mode  :character   Mode  :character   Median :2014-05-01   Mode  :character  
                                           Mean   :2013-12-14                     
                                           3rd Qu.:2015-04-07                     
                                           Max.   :2015-10-02                     
                                                                                  
     host_response_rate host_acceptance_rate host_is_superhost host_listings_count
     Length:5147        Length:5147          Mode :logical     Min.   :  1.000    
     Class :character   Class :character     FALSE:4660        1st Qu.:  1.000    
     Mode  :character   Mode  :character     TRUE :487         Median :  1.000    
                                                               Mean   :  4.791    
                                                               3rd Qu.:  2.000    
                                                               Max.   :480.000    
                                                                                  
     host_total_listings_count host_has_profile_pic host_identity_verified
     Min.   :  1.000           Mode :logical        Mode :logical         
     1st Qu.:  1.000           FALSE:22             FALSE:1201            
     Median :  1.000           TRUE :5125           TRUE :3946            
     Mean   :  4.791                                                      
     3rd Qu.:  2.000                                                      
     Max.   :480.000                                                      
                                                                          
     is_location_exact     property_type         room_type     accommodates   
     Mode :logical     apartment  :4000   entire_place:2928   Min.   : 1.000  
     FALSE:653         house      : 593   private_room:1972   1st Qu.: 2.000  
     TRUE :4494        condominium: 285   shared_room : 247   Median : 2.000  
                       loft       : 154                       Mean   : 3.275  
                       townhouse  :  42                       3rd Qu.: 4.000  
                       (Other)    :  72                       Max.   :16.000  
                       NA's       :   1                                       
       bathrooms        bedrooms           beds            bed_type     square_feet   
     Min.   :0.000   Min.   : 0.000   Min.   : 1.000   bed     :4845   Min.   :    0  
     1st Qu.:1.000   1st Qu.: 1.000   1st Qu.: 1.000   airbed  : 113   1st Qu.:  575  
     Median :1.000   Median : 1.000   Median : 1.000   futon   :  96   Median : 1000  
     Mean   :1.223   Mean   : 1.279   Mean   : 1.642   sofa_bed:  51   Mean   : 1236  
     3rd Qu.:1.000   3rd Qu.: 2.000   3rd Qu.: 2.000   couch   :  42   3rd Qu.: 1350  
     Max.   :6.000   Max.   :10.000   Max.   :16.000                   Max.   :22000  
     NA's   :18      NA's   :15       NA's   :13                       NA's   :5060   
        price           weekly_price       monthly_price      security_deposit  
     Length:5147        Length:5147        Length:5147        Length:5147       
     Class :character   Class :character   Class :character   Class :character  
     Mode  :character   Mode  :character   Mode  :character   Mode  :character  
                                                                                
                                                                                
                                                                                
                                                                                
     cleaning_fee       guests_included extra_people       minimum_nights   
     Length:5147        Min.   : 0.00   Length:5147        Min.   :  1.000  
     Class :character   1st Qu.: 1.00   Class :character   1st Qu.:  1.000  
     Mode  :character   Median : 1.00   Mode  :character   Median :  1.000  
                        Mean   : 1.59                      Mean   :  2.118  
                        3rd Qu.: 2.00                      3rd Qu.:  2.000  
                        Max.   :16.00                      Max.   :180.000  
                                                                            
     maximum_nights      calendar_updated   has_availability   availability_30
     Min.   :1.000e+00   Length:5147        Length:5147        Min.   : 0.00  
     1st Qu.:9.300e+01   Class :character   Class :character   1st Qu.: 0.00  
     Median :1.125e+03   Mode  :character   Mode  :character   Median : 9.00  
     Mean   :4.183e+05                                         Mean   :10.91  
     3rd Qu.:1.125e+03                                         3rd Qu.:19.00  
     Max.   :2.147e+09                                         Max.   :30.00  
                                                                              
     availability_60 availability_90 availability_365 calendar_last_scraped
     Min.   : 0.00   Min.   : 0.00   Min.   :  0.0    Min.   :2015-10-02   
     1st Qu.: 5.00   1st Qu.:14.00   1st Qu.:123.0    1st Qu.:2015-10-02   
     Median :31.00   Median :58.00   Median :311.0    Median :2015-10-03   
     Mean   :28.57   Mean   :48.29   Mean   :244.9    Mean   :2015-10-02   
     3rd Qu.:47.00   3rd Qu.:77.00   3rd Qu.:349.0    3rd Qu.:2015-10-03   
     Max.   :60.00   Max.   :90.00   Max.   :365.0    Max.   :2015-10-03   
                                                                           
     number_of_reviews  first_review         last_review         review_scores_rating
     Min.   :  0.0     Min.   :2009-03-06   Min.   :2010-08-09   Min.   : 20.00      
     1st Qu.:  1.0     1st Qu.:2014-08-04   1st Qu.:2015-08-23   1st Qu.: 91.00      
     Median :  5.0     Median :2015-05-17   Median :2015-09-18   Median : 96.00      
     Mean   : 14.6     Mean   :2014-12-06   Mean   :2015-08-19   Mean   : 93.99      
     3rd Qu.: 16.0     3rd Qu.:2015-08-01   3rd Qu.:2015-09-25   3rd Qu.:100.00      
     Max.   :298.0     Max.   :2015-10-03   Max.   :2015-10-03   Max.   :100.00      
                       NA's   :1005         NA's   :1005         NA's   :1056        
     review_scores_accuracy review_scores_cleanliness review_scores_checkin
     Min.   : 2.000         Min.   : 2.000            Min.   : 2.000       
     1st Qu.: 9.000         1st Qu.: 9.000            1st Qu.:10.000       
     Median :10.000         Median :10.000            Median :10.000       
     Mean   : 9.555         Mean   : 9.315            Mean   : 9.743       
     3rd Qu.:10.000         3rd Qu.:10.000            3rd Qu.:10.000       
     Max.   :10.000         Max.   :10.000            Max.   :10.000       
     NA's   :1073           NA's   :1075              NA's   :1073         
     review_scores_communication review_scores_location review_scores_value
     Min.   : 2.00               Min.   : 4.000         Min.   : 2.000     
     1st Qu.:10.00               1st Qu.: 9.000         1st Qu.: 9.000     
     Median :10.00               Median :10.000         Median :10.000     
     Mean   : 9.79               Mean   : 9.466         Mean   : 9.376     
     3rd Qu.:10.00               3rd Qu.:10.000         3rd Qu.:10.000     
     Max.   :10.00               Max.   :10.000         Max.   :10.000     
     NA's   :1069                NA's   :1068           NA's   :1069       
     requires_license      license          instant_bookable   cancellation_policy
     Length:5147        Min.   :      102   Length:5147        Length:5147        
     Class :character   1st Qu.:  2093472   Class :character   Class :character   
     Mode  :character   Median :  2233303   Mode  :character   Mode  :character   
                        Mean   : 17724533                                         
                        3rd Qu.:  2314739                                         
                        Max.   :352167776                                         
                        NA's   :5111                                              
     require_guest_profile_picture require_guest_phone_verification
     Length:5147                   Length:5147                     
     Class :character              Class :character                
     Mode  :character              Mode  :character                
                                                                   
                                                                   
                                                                   
                                                                   
     calculated_host_listings_count reviews_per_month
     Min.   : 1.000                 Min.   : 0.020   
     1st Qu.: 1.000                 1st Qu.: 0.900   
     Median : 1.000                 Median : 1.710   
     Mean   : 2.805                 Mean   : 2.173   
     3rd Qu.: 2.000                 3rd Qu.: 3.000   
     Max.   :42.000                 Max.   :14.000   
                                    NA's   :1005     

``` {.r}
host_response_rate <- airbnb_price$host_response_rate
host_response_rate <- as.numeric(str_remove(host_response_rate, "%"))
host_response_rate <- host_response_rate/100
airbnb_price$host_response_rate <- host_response_rate
```

``` {.r}
host_verifications <- str_remove(airbnb_price$host_verifications[1], "\\[")
host_verifications <- str_remove(host_verifications, "\\]")
host_verifications <- str_remove_all(host_verifications, "\'")
host_verifications <- str_split(host_verifications, ",") 

host_verifications
```

### Save clean dataset with different name

``` {.r}
write_csv(airbnb_price, "data/airbnb_price.csv")
```

* * * * *

Descriptive Statistics
----------------------

* * * * *

``` {.r}
summary(airbnb_price[1:10])
```

``` {.r}
summary(airbnb_price[10:20])
```

LS0tCnRpdGxlOiAiQ2hpY2FnbyBBaXJibmIgQW5hbHlzaXMiCmF1dGhvcjogIkpvc2UgTHVpcyBSb2RyaWd1ZXoiCmRhdGU6ICJKdW5lIDEzLCAyMDE4IgpvdXRwdXQ6CiAgaHRtbF9ub3RlYm9vazogZGVmYXVsdApzdWJ0aXRsZTogQ01FIEdyb3VwIEZvdW5kYXRpb24gQnVzaW5lc3MgQW5hbHl0aWNzIExhYgotLS0KCi0tLS0tLS0tLS0tLS0KCiMjIE5vdGVib29rIEluc3RydWN0aW9ucwoKLS0tLS0tLS0tLS0tLQoKKiBUaGlzIG5vdGVib29rIGlzIHVzZSB0byBhbmFseXplIGFpcmJuYiBkYXRhIGJhc2VkIG9uIHRoZSBJbnNpZGUgQWlyYm5iIHByb2plY3QgYnkgTXVycmF5IENveC4KCiMjIyMgTm90ZWJvb2sgVmVyc2lvbgoKYGBgCnBsYXRmb3JtICAgICAgIHg4Nl82NC1hcHBsZS1kYXJ3aW4xNS42LjAgICAKYXJjaCAgICAgICAgICAgeDg2XzY0ICAgICAgICAgICAgICAgICAgICAgIApvcyAgICAgICAgICAgICBkYXJ3aW4xNS42LjAgICAgICAgICAgICAgICAgCnN5c3RlbSAgICAgICAgIHg4Nl82NCwgZGFyd2luMTUuNi4wICAgICAgICAKc3RhdHVzICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIAptYWpvciAgICAgICAgICAzICAgICAgICAgICAgICAgICAgICAgICAgICAgCm1pbm9yICAgICAgICAgIDUuMCAgICAgICAgICAgICAgICAgICAgICAgICAKeWVhciAgICAgICAgICAgMjAxOCAgICAgICAgICAgICAgICAgICAgICAgIAptb250aCAgICAgICAgICAwNCAgICAgICAgICAgICAgICAgICAgICAgICAgCmRheSAgICAgICAgICAgIDIzICAgICAgICAgICAgICAgICAgICAgICAgICAKc3ZuIHJldiAgICAgICAgNzQ2MjYgICAgICAgICAgICAgICAgICAgICAgIApsYW5ndWFnZSAgICAgICBSICAgICAgICAgICAgICAgICAgICAgICAgICAgCnZlcnNpb24uc3RyaW5nIFIgdmVyc2lvbiAzLjUuMCAoMjAxOC0wNC0yMykKbmlja25hbWUgICAgICAgSm95IGluIFBsYXlpbmcgICAKYGBgCgojIyMgQWJvdXQKCiogQWlyYm5iIGNsYWltcyB0byBiZSBwYXJ0IG9mIHRoZSAic2hhcmluZyBlY29ub215IiBhbmQgZGlzcnVwdGluZyB0aGUgaG90ZWwgaW5kdXN0cnkuIAoKKiBIb3dldmVyLCBkYXRhIHNob3dzIHRoYXQgdGhlIG1ham9yaXR5IG9mIEFpcmJuYiBsaXN0aW5ncyBpbiBtb3N0IGNpdGllcyBhcmUgZW50aXJlIGhvbWVzLCBtYW55IG9mIHdoaWNoIGFyZSByZW50ZWQgYWxsIHllYXIgcm91bmQgLSBkaXNydXB0aW5nIGhvdXNpbmcgYW5kIGNvbW11bml0aWVzLgoKKiBodHRwOi8vaW5zaWRlYWlyYm5iLmNvbS9pbmRleC5odG1sCgojIyMgUHJvamVjdCBMYXlvdXQKCmBgYAouCuKUlOKUgOKUgCBBaXJibmIKICAgIOKUnOKUgOKUgCBhaXJibmItbm90ZWJvb2suUm1kCiAgICDilIIKICAgIOKUnOKUgOKUgCBkYXRhCiAgICDilIIgICDilJzilIDilIAgMjAxNQogICAg4pSCICAg4pSCICAg4pSc4pSA4pSAIGFpcmJuYi5jc3YKICAgIOKUgiAgIOKUgiAgIOKUnOKUgOKUgCBhaXJibmJfY2FsZW5kYXIuY3N2CiAgICDilIIgICDilIIgICDilJzilIDilIAgYWlyYm5iX2NsZWFuLmNzdgogICAg4pSCICAg4pSCICAg4pSc4pSA4pSAIGFpcmJuYl9sb2MuY3N2CiAgICDilIIgICDilIIgICDilJzilIDilIAgYWlyYm5iX25scC5jc3YKICAgIOKUgiAgIOKUgiAgIOKUnOKUgOKUgCBhaXJibmJfcmV2aWV3cy5jc3YKICAgIOKUgiAgIOKUgiAgIOKUnOKUgOKUgCBhaXJibmJfc3VtbWFyeS5jc3YKICAgIOKUgiAgIOKUgiAgIOKUlOKUgOKUgCBhaXJibmJfdXJscy5jc3YKICAgIOKUgiAgIOKUggogICAg4pSCICAg4pSc4pSA4pSAIDIwMTcKICAgIOKUgiAgIOKUgiAgIOKUnOKUgOKUgCBhaXJibmIuY3N2CiAgICDilIIgICDilIIgICDilJzilIDilIAgYWlyYm5iX2NhbGVuZGFyLmNzdgogICAg4pSCICAg4pSCICAg4pSc4pSA4pSAIGFpcmJuYl9yZXZpZXdzLmNzdgogICAg4pSCICAg4pSCICAg4pSU4pSA4pSAIGFpcmJuYl9zdW1tYXJ5LmNzdgogICAg4pSCICAg4pSCCiAgICDilIIgICDilJzilIDilIAgbG9jYXRpb24KICAgIOKUgiAgIOKUgiAgIOKUnOKUgOKUgCAyMDE1LW5laWdoYm91cmhvb2RzLmNzdgogICAg4pSCICAg4pSCICAg4pSc4pSA4pSAIDIwMTUtbmVpZ2hib3VyaG9vZHMuZ2VvanNvbgogICAg4pSCICAg4pSCICAg4pSc4pSA4pSAIDIwMTctbmVpZ2hib3VyaG9vZHMuY3N2CiAgICDilIIgICDilIIgICDilJzilIDilIAgMjAxNy1uZWlnaGJvdXJob29kcy5nZW9qc29uCiAgICDilIIgICDilIIgICDilJTilIDilIAgbmFtZXMtemlwY29kZS5jc3YKICAgIOKUgiAgIOKUggogICAg4pSCICAg4pSU4pSA4pSAIHJhdwogICAg4pSCICAgICAgIOKUnOKUgOKUgCAyMDE1LWFpcmJuYi1saXN0aW5ncy5jc3YuZ3oKICAgIOKUgiAgICAgICDilJzilIDilIAgMjAxNS1jYWxlbmRhci5jc3YuZ3oKICAgIOKUgiAgICAgICDilJzilIDilIAgMjAxNS1uZWlnaGJvdXJob29kcy56aXAKICAgIOKUgiAgICAgICDilJzilIDilIAgMjAxNS1yZXZpZXdzLmNzdi5negogICAg4pSCICAgICAgIOKUnOKUgOKUgCAyMDE3LWFpcmJuYi1saXN0aW5ncy5jc3YuZ3oKICAgIOKUgiAgICAgICDilJzilIDilIAgMjAxNy1jYWxlbmRhci5jc3YuZ3oKICAgIOKUgiAgICAgICDilJzilIDilIAgMjAxNy1uZWlnaGJvdXJob29kcy56aXAKICAgIOKUgiAgICAgICDilJTilIDilIAgMjAxNy1yZXZpZXdzLmNzdi5negogICAg4pSCCiAgICDilJzilIDilIAgcmVzb3VyY2VzCiAgICDilIIgICDilJzilIDilIAgQWlyYm5iLVByb3Bvc2FsLmRvY3gKICAgIOKUgiAgIOKUlOKUgOKUgCBBaXJibmItUHJvcG9zYWwucGRmCiAgICDilIIKICAgIOKUlOKUgOKUgCBzY3JpcHRzCmBgYAoKCiMjIyBMb2FkIFBhY2thZ2VzIGluIFIvUlN0dWRpbyAKCldlIGFyZSBnb2luZyB0byB1c2UgdGlkeXZlcnNlIGEgY29sbGVjdGlvbiBvZiBSIHBhY2thZ2VzIGRlc2lnbmVkIGZvciBkYXRhIHNjaWVuY2UuIAoKKiBJbmZvOiBodHRwczovL3d3dy50aWR5dmVyc2Uub3JnCgpgYGB7ciwgZWNobyA9IEZBTFNFfQoKIyBIZXJlIHdlIGFyZSBjaGVja2luZyBpZiB0aGUgcGFja2FnZSBpcyBpbnN0YWxsZWQKaWYoIXJlcXVpcmUoInRpZHl2ZXJzZSIpKXsKICAKICAjIElmIHRoZSBwYWNrYWdlIGlzIG5vdCBpbiB0aGUgc3lzdGVtIHRoZW4gaXQgd2lsbCBiZSBpbnN0YWxsCiAgaW5zdGFsbC5wYWNrYWdlcygidGlkeXZlcnNlIiwgZGVwZW5kZW5jaWVzID0gVFJVRSkKICAKICAjIEhlcmUgd2UgYXJlIGxvYWRpbmcgdGhlIHBhY2thZ2UKICBsaWJyYXJ5KCJ0aWR5dmVyc2UiKQp9CgpgYGAKCi0tLS0tLS0tLS0tLS0KCiMjIERhdGEgSW1wb3J0IGFuZCBJbnNwZWN0aW9uCgotLS0tLS0tLS0tLS0tCgoqIHJlYWQgZGF0YXNldCBmcm9tIDIwMTUKCmBgYHtyfQoKYWlyYm5iIDwtIHJlYWRfY3N2KCJkYXRhLzIwMTUvYWlyYm5iLmNzdiIpCgpgYGAKCiMjIyBJbnNwZWN0IGhlYWQgYW5kIHRhaWwgb2YgdGhlIGRhdGFzZXQKYGBge3J9CgpoZWFkKGFpcmJuYikKCmBgYAoKYGBge3J9Cgp0YWlsKGFpcmJuYikKCmBgYAoKYGBge3J9Cgpjb2xuYW1lcyhhaXJibmIpCgpgYGAKCi0tLS0tLS0tLS0tLS0KCiMjIERhdGEgU2VsZWN0aW9uCgotLS0tLS0tLS0tLS0tCgoqIE5vdyBsZXRzIGNsZWFuIHRoZSBkYXRhIGFuZCBkZWxldGUgc29tZSB1bmVzc2FyeSBjb2x1bW5zIGZvciB0aGlzIGFuYWx5c2lzCgoqIEV4dHJhY3QgdGhlIGFpcmJuYl9pZCB0byBsYXRlciB1c2UgYW5kIGlkZW50aWZ5IHRoZSBjb2x1bW5zIHRvIHJlbW92ZQoKKiBTaW5jZSB0aGVyZSBhcmUgOTIgZmVhdHVyZXMvY29sdW1ucyB3ZSBjYW4gc3BsaXQgdGhlIGNvbHVtbiBuYW1lcyB2ZWN0b3IgaW50byBkaWZmZXJlbnQgY2h1bmtzIAoKKiBUaGUgOTIgZmVhdHVyZXMvY29sdW1ucyBhcmUgb2YgdmFyaWF0aW5nIHR5cGVzIGFuZCBtZWFzdXJlcyB3ZSBjYW4gc3BsaXQgdGhlIGRhdGFzZXQgaW50byBkaWZmZW50IHNlY3Rpb25zLiAKCiogU3VjaCBhcyBmZWF0dXJlcy9jb2x1bW5zIHJlbGF0ZWQgdG8gbGlua3MvdXJscyBvciBvbmx5IHRleHQgY29sdW1ucyB0aGF0IHdlIGNhbiB1c2UgbGF0ZXIgZm9yIG5hdHVyYWwgbGFuZ3VhZ2UgcHJvY2Vzc2luZy4KCiogU2FtZSBwcm9jZXNzIGFwcGxpZXMgdG8gZmVhdHVyZXMvY29sdW1ucyByZWxhdGVkIHRvIGxvY2F0aW9uIAoKKiBGaW5hbGx5IHdlIGNhbiByZW1vdmUgdGhlIGNvbHVtbnMgZnJvbSB0aGUgbmV3IGRhdGFzZXRzIHRvIGNyZWF0ZSBhIGZpbmFsIGRhdGFzZXQgdGhhdCB3aWxsIGJlIG1vcmUgbnVtZXJpYyBpbiBuYXR1cmUuIAoKKiBBbGwgZGF0YXNldHMgd2lsbCBiZSBsaW5rZWQvcmVsYXRlZCBieSB0aGUgYWlyYm5iX2lkCgoKYGBge3J9CmFpcmJuYiA8LSByZW5hbWUoYWlyYm5iLCBhaXJibmJfaWQgPSBpZCkKYWlyYm5iX2lkIDwtIGFpcmJuYiRhaXJibmJfaWQKYGBgCgpgYGB7cn0KY29sbmFtZXMoYWlyYm5iKVsxOjMwXQpgYGAKCmBgYHtyfQpjb2xuYW1lcyhhaXJibmIpWzMxOjY1XQpgYGAKCmBgYHtyfQpjb2xuYW1lcyhhaXJibmIpWzY2OjkyXQpgYGAKCiMjIyBTZWxlY3Qgb25seSBjb2x1bW5zIHJlbGF0ZWQgdG8gdXJsIGxpbmtzCgpgYGB7cn0KYWlyYm5iX3VybHMgPC0gc2VsZWN0KGFpcmJuYiwgY29udGFpbnMoInVybCIpKQp1bHJfY29sdW1ucyA8LSBjb2xuYW1lcyhhaXJibmJfdXJscykKYWlyYm5iX3VybHMgPC0gYWRkX2NvbHVtbihhaXJibmJfdXJscywgYWlyYm5iX2lkKQoKYGBgCgpgYGB7cn0KaGVhZChhaXJibmJfdXJscykKYGBgCgojIyMgU2VsZWN0IG9ubHkgY29sdW1ucyBjb250YWluZyB0ZXh0IAoKCmBgYHtyfQp0ZXh0X2NvbHVtbnMgPC0gYygiaG9zdF9uYW1lIiwibmFtZSIsImFtZW5pdGllcyIsICJleHBlcmllbmNlc19vZmZlcmVkIiwKICAgICAgICAgICAgICAgICAgImhvc3RfdmVyaWZpY2F0aW9ucyIsInRyYW5zaXQiLCJub3RlcyIsIAogICAgICAgICAgICAgICAgICJuZWlnaGJvcmhvb2Rfb3ZlcnZpZXciLCAiaG9zdF9hYm91dCIsIAogICAgICAgICAgICAgICAgICJkZXNjcmlwdGlvbiIsICJzcGFjZSIsInN1bW1hcnkiKQoKYWlyYm5iX25scCA8LSBzZWxlY3QoYWlyYm5iLCB0ZXh0X2NvbHVtbnMpCgphaXJibmJfbmxwIDwtIGFkZF9jb2x1bW4oYWlyYm5iX25scCwgYWlyYm5iX2lkKQoKYGBgCgpgYGB7cn0KaGVhZChhaXJibmJfbmxwKQpgYGAKCiMjIyBTZWxlY3Qgb25seSBjb2x1bW5zIHJlbGF0ZWQgdG8gbGlzdGluZyBsb2NhdGlvbgoKYGBge3J9Cgpsb2NhdGlvbl9jb2x1bW5zIDwtIGMoInppcGNvZGUiLCAibGF0aXR1ZGUiLCAibG9uZ2l0dWRlIiwgImNpdHkiLCAic3RhdGUiLAogICAgICAgICAgICAgICAgICAgICAic3RyZWV0IiwgIm5laWdoYm91cmhvb2QiLCAibmVpZ2hib3VyaG9vZF9jbGVhbnNlZCIsCiAgICAgICAgICAgICAgICAgICAgICJuZWlnaGJvdXJob29kX2dyb3VwX2NsZWFuc2VkIiwiaG9zdF9sb2NhdGlvbiIsICJob3N0X25laWdoYm91cmhvb2QiLAogICAgICAgICAgICAgICAgICAgICAibWFya2V0IiwgInNtYXJ0X2xvY2F0aW9uIiwgImp1cmlzZGljdGlvbl9uYW1lcyIsICJjb3VudHJ5X2NvZGUiLCAKICAgICAgICAgICAgICAgICAgICAgImNvdW50cnkiKQoKYWlyYm5iX2xvYyA8LSBzZWxlY3QoYWlyYm5iLCBsb2NhdGlvbl9jb2x1bW5zKQoKYWlyYm5iX2xvYyA8LSBhZGRfY29sdW1uKGFpcmJuYl9sb2MsIGFpcmJuYl9pZCkKCmBgYAoKYGBge3J9CmhlYWQoYWlyYm5iX2xvYykKYGBgCgojIyMgVXNlIHNlbGVjdCBhbmQgb25lX29mIGZ1bmN0aW9uIHRvIHJlbW92ZSB0aGUgY29sdW1ucyBmcm9tIHByZXZpb3VzIGRhdGFzZXRzICh1bHJfY29sdW1ucywgdGV4dF9jb2x1bW5zLCBsb2NhdGlvbl9jb2x1bW5zKQoKYGBge3J9CiMgdW5pcXVlKGFzLmNoYXJhY3RlcihhaXJibmIkc2NyYXBlX2lkKSkKCnJlbW92ZV9jb2x1bW5zIDwtIGModWxyX2NvbHVtbnMsIHRleHRfY29sdW1ucywgbG9jYXRpb25fY29sdW1ucywgInNjcmFwZV9pZCIsICJsYXN0X3NjcmFwZWQiKQoKYWlyYm5iX2NsZWFuIDwtIHNlbGVjdChhaXJibmIsIC1vbmVfb2YocmVtb3ZlX2NvbHVtbnMpKQoKYGBgCgojIyMgSW5zcGVjdCB0aGUgbmV3IG1vcmUgY29tcGFjdGVkIGRhdGFzZXQuIEJ5IGRvaW5nIHRoaXMgd2UgcmVkdWNlZCB0aGUgc2l6ZSBieSBhbG1vc3QgaGFsZgoKYGBge3J9CgpoZWFkKGFpcmJuYl9jbGVhbikKCmBgYAoKIyMjIFNhdmUgdGhlIG5ldyBkYXRhc2V0IGZvciByZWZlcmVuY2UgYW5kIGxhdGVyIHVzZQoKYGBge3J9CndyaXRlX2NzdihhaXJibmJfdXJscywgImRhdGEvMjAxNS9haXJibmJfdXJscy5jc3YiKQoKd3JpdGVfY3N2KGFpcmJuYl9ubHAsICJkYXRhLzIwMTUvYWlyYm5iX25scC5jc3YiKQoKd3JpdGVfY3N2KGFpcmJuYl9sb2MsICJkYXRhLzIwMTUvYWlyYm5iX2xvYy5jc3YiKQoKd3JpdGVfY3N2KGFpcmJuYl9jbGVhbiwgImRhdGEvMjAxNS9haXJibmJfY2xlYW4uY3N2IikKCmBgYAoKLS0tLS0tLS0tLS0tLQoKIyMgRGF0YSBUeXBlcyBhbmQgQ2xlYW5pbmcKCi0tLS0tLS0tLS0tLS0KCgpgYGB7cn0KYWlyYm5iX2NsZWFuIDwtIHJlYWRfY3N2KCJkYXRhLzIwMTUvYWlyYm5iX2NsZWFuLmNzdiIpCmhlYWQoYWlyYm5iX2NsZWFuKQpgYGAKCgpgYGB7cn0Kcm9vbV90eXBlIDwtIGFpcmJuYl9jbGVhbiRyb29tX3R5cGUgJT4lIAogIHRvbG93ZXIoKSAlPiUgCiAgc3RyX3JlcGxhY2VfYWxsKC4sICIgIiwgIl8iKSAlPiUgCiAgc3RyX3JlcGxhY2UoLiwgImhvbWUvYXB0IiwicGxhY2UiKQoKYWlyYm5iX2NsZWFuJHJvb21fdHlwZSA8LSBhc19mYWN0b3Iocm9vbV90eXBlKQoKYGBgCgoKYGBge3J9CgojIHVuaXF1ZShhaXJibmJfY2xlYW4kYmVkX3R5cGUpCmJlZF90eXBlIDwtIGFpcmJuYl9jbGVhbiRiZWRfdHlwZSAlPiUgCiAgdG9sb3dlcigpICU+JSAKICBzdHJfcmVwbGFjZV9hbGwoLiwgIiAiLCAiXyIpICU+JSAKICBzdHJfcmVwbGFjZSguLCAicHVsbC4qIiwic29mYV9iZWQiKSAlPiUgCiAgc3RyX3JlcGxhY2UoLiwgInJlYWxfLioiLCJiZWQiKQoKYWlyYm5iX2NsZWFuJGJlZF90eXBlIDwtIGFzX2ZhY3RvcihiZWRfdHlwZSkKCmBgYAoKCmBgYHtyfQoKYWlyYm5iX2NsZWFuIDwtIGFpcmJuYl9jbGVhbiAlPiUgCiAgbXV0YXRlKGFpcmJuYl9pZCA9IGFzLmNoYXJhY3RlcihhaXJibmJfaWQpKSAlPiUgCiAgbXV0YXRlKGhvc3RfaWQgPSBhcy5jaGFyYWN0ZXIoaG9zdF9pZCkpICU+JSAKICBtdXRhdGUoaG9zdF9pc19zdXBlcmhvc3QgPSBwYXJzZV9sb2dpY2FsKGhvc3RfaXNfc3VwZXJob3N0KSkgJT4lIAogIG11dGF0ZShob3N0X2hhc19wcm9maWxlX3BpYyA9IHBhcnNlX2xvZ2ljYWwoaG9zdF9oYXNfcHJvZmlsZV9waWMpKSAlPiUgCiAgbXV0YXRlKGhvc3RfaWRlbnRpdHlfdmVyaWZpZWQgPSBwYXJzZV9sb2dpY2FsKGhvc3RfaWRlbnRpdHlfdmVyaWZpZWQpKSAlPiUgCiAgbXV0YXRlKGlzX2xvY2F0aW9uX2V4YWN0ID0gcGFyc2VfbG9naWNhbChpc19sb2NhdGlvbl9leGFjdCkpICU+JSAKICBtdXRhdGUocHJvcGVydHlfdHlwZSA9IGFzX2ZhY3Rvcih0b2xvd2VyKHByb3BlcnR5X3R5cGUpKSkKCmBgYAoKYGBge3J9CmhlYWQoYWlyYm5iX2NsZWFuKQpgYGAKCmBgYHtyfQpzdW1tYXJ5KGFpcmJuYl9jbGVhbikKYGBgCgoKYGBge3J9Cgpob3N0X3Jlc3BvbnNlX3JhdGUgPC0gYWlyYm5iX3ByaWNlJGhvc3RfcmVzcG9uc2VfcmF0ZQpob3N0X3Jlc3BvbnNlX3JhdGUgPC0gYXMubnVtZXJpYyhzdHJfcmVtb3ZlKGhvc3RfcmVzcG9uc2VfcmF0ZSwgIiUiKSkKaG9zdF9yZXNwb25zZV9yYXRlIDwtIGhvc3RfcmVzcG9uc2VfcmF0ZS8xMDAKYWlyYm5iX3ByaWNlJGhvc3RfcmVzcG9uc2VfcmF0ZSA8LSBob3N0X3Jlc3BvbnNlX3JhdGUKCmBgYAoKYGBge3J9Cgpob3N0X3ZlcmlmaWNhdGlvbnMgPC0gc3RyX3JlbW92ZShhaXJibmJfcHJpY2UkaG9zdF92ZXJpZmljYXRpb25zWzFdLCAiXFxbIikKaG9zdF92ZXJpZmljYXRpb25zIDwtIHN0cl9yZW1vdmUoaG9zdF92ZXJpZmljYXRpb25zLCAiXFxdIikKaG9zdF92ZXJpZmljYXRpb25zIDwtIHN0cl9yZW1vdmVfYWxsKGhvc3RfdmVyaWZpY2F0aW9ucywgIlwnIikKaG9zdF92ZXJpZmljYXRpb25zIDwtIHN0cl9zcGxpdChob3N0X3ZlcmlmaWNhdGlvbnMsICIsIikgCgpob3N0X3ZlcmlmaWNhdGlvbnMKCmBgYAoKIyMjIFNhdmUgY2xlYW4gZGF0YXNldCB3aXRoIGRpZmZlcmVudCBuYW1lCgpgYGB7cn0KCndyaXRlX2NzdihhaXJibmJfcHJpY2UsICJkYXRhL2FpcmJuYl9wcmljZS5jc3YiKQoKYGBgCgotLS0tLS0tLS0tLS0tCgojIyBEZXNjcmlwdGl2ZSBTdGF0aXN0aWNzIAoKLS0tLS0tLS0tLS0tLQoKYGBge3J9CnN1bW1hcnkoYWlyYm5iX3ByaWNlWzE6MTBdKQpgYGAKCmBgYHtyfQpzdW1tYXJ5KGFpcmJuYl9wcmljZVsxMDoyMF0pCmBgYAo=
