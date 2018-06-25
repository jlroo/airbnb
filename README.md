------------------------------------------------------------------------

Notebook Instructions
---------------------

------------------------------------------------------------------------

-   This notebook is use to analyze airbnb data based on the Inside Airbnb project by Murray Cox.

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

-   Airbnb claims to be part of the "sharing economy" and disrupting the hotel industry.

-   However, data shows that the majority of Airbnb listings in most cities are entire homes, many of which are rented all year round - disrupting housing and communities.

-   <http://insideairbnb.com/index.html>

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

We are going to use tidyverse a collection of R packages designed for data science.

-   Info: <https://www.tidyverse.org>

<!-- -->

    ## Loading required package: tidyverse

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 2.2.1     ✔ purrr   0.2.4
    ## ✔ tibble  1.4.2     ✔ dplyr   0.7.4
    ## ✔ tidyr   0.8.0     ✔ stringr 1.3.0
    ## ✔ readr   1.1.1     ✔ forcats 0.3.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

------------------------------------------------------------------------

Data Import and Inspection
--------------------------

------------------------------------------------------------------------

-   read dataset from 2015

``` r
airbnb <- read_csv("data/2015/airbnb.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_character(),
    ##   id = col_integer(),
    ##   scrape_id = col_double(),
    ##   last_scraped = col_date(format = ""),
    ##   host_id = col_integer(),
    ##   host_since = col_date(format = ""),
    ##   host_listings_count = col_integer(),
    ##   host_total_listings_count = col_integer(),
    ##   zipcode = col_integer(),
    ##   latitude = col_double(),
    ##   longitude = col_double(),
    ##   accommodates = col_integer(),
    ##   bathrooms = col_double(),
    ##   bedrooms = col_integer(),
    ##   beds = col_integer(),
    ##   square_feet = col_integer(),
    ##   guests_included = col_integer(),
    ##   minimum_nights = col_integer(),
    ##   maximum_nights = col_integer(),
    ##   availability_30 = col_integer(),
    ##   availability_60 = col_integer()
    ##   # ... with 16 more columns
    ## )

    ## See spec(...) for full column specifications.

    ## Warning in rbind(names(probs), probs_f): number of columns of result is not
    ## a multiple of vector length (arg 1)

    ## Warning: 31 parsing failures.
    ## row # A tibble: 5 x 5 col     row col     expected               actual       file                   expected   <int> <chr>   <chr>                  <chr>        <chr>                  actual 1  1105 license no trailing characters " Site 2"    'data/2015/airbnb.csv' file 2  1188 license no trailing characters " Site 1"    'data/2015/airbnb.csv' row 3  1852 license an integer             L20012682021 'data/2015/airbnb.csv' col 4  2451 license an integer             .            'data/2015/airbnb.csv' expected 5  2533 license an integer             None         'data/2015/airbnb.csv'
    ## ... ................. ... .......................................................................... ........ .......................................................................... ...... .......................................................................... .... .......................................................................... ... .......................................................................... ... .......................................................................... ........ ..........................................................................
    ## See problems(...) for more details.

### Inspect head and tail of the dataset

``` r
head(airbnb)
```

    ## # A tibble: 6 x 92
    ##        id listing_url scrape_id last_scraped name  summary   space        
    ##     <int> <chr>           <dbl> <date>       <chr> <chr>     <chr>        
    ## 1 1874928 https://ww…   2.02e13 2015-10-03   Sunn… Enjoy ou… Your apt. is…
    ## 2  739495 https://ww…   2.02e13 2015-10-03   Love… "This sp… Beautiful ap…
    ## 3 1696051 https://ww…   2.02e13 2015-10-03   Uniq… I'd love… You will hav…
    ## 4 5152597 https://ww…   2.02e13 2015-10-03   Sunn… Clean, c… Our apartmen…
    ## 5 8036094 https://ww…   2.02e13 2015-10-03   Brig… Enjoy a … Depending on…
    ## 6 7395957 https://ww…   2.02e13 2015-10-03   Linc… A privat… Private quee…
    ## # ... with 85 more variables: description <chr>,
    ## #   experiences_offered <chr>, neighborhood_overview <chr>, notes <chr>,
    ## #   transit <chr>, thumbnail_url <chr>, medium_url <chr>,
    ## #   picture_url <chr>, xl_picture_url <chr>, host_id <int>,
    ## #   host_url <chr>, host_name <chr>, host_since <date>,
    ## #   host_location <chr>, host_about <chr>, host_response_time <chr>,
    ## #   host_response_rate <chr>, host_acceptance_rate <chr>,
    ## #   host_is_superhost <chr>, host_thumbnail_url <chr>,
    ## #   host_picture_url <chr>, host_neighbourhood <chr>,
    ## #   host_listings_count <int>, host_total_listings_count <int>,
    ## #   host_verifications <chr>, host_has_profile_pic <chr>,
    ## #   host_identity_verified <chr>, street <chr>, neighbourhood <chr>,
    ## #   neighbourhood_cleansed <chr>, neighbourhood_group_cleansed <chr>,
    ## #   city <chr>, state <chr>, zipcode <int>, market <chr>,
    ## #   smart_location <chr>, country_code <chr>, country <chr>,
    ## #   latitude <dbl>, longitude <dbl>, is_location_exact <chr>,
    ## #   property_type <chr>, room_type <chr>, accommodates <int>,
    ## #   bathrooms <dbl>, bedrooms <int>, beds <int>, bed_type <chr>,
    ## #   amenities <chr>, square_feet <int>, price <chr>, weekly_price <chr>,
    ## #   monthly_price <chr>, security_deposit <chr>, cleaning_fee <chr>,
    ## #   guests_included <int>, extra_people <chr>, minimum_nights <int>,
    ## #   maximum_nights <int>, calendar_updated <chr>, has_availability <chr>,
    ## #   availability_30 <int>, availability_60 <int>, availability_90 <int>,
    ## #   availability_365 <int>, calendar_last_scraped <date>,
    ## #   number_of_reviews <int>, first_review <date>, last_review <date>,
    ## #   review_scores_rating <int>, review_scores_accuracy <int>,
    ## #   review_scores_cleanliness <int>, review_scores_checkin <int>,
    ## #   review_scores_communication <int>, review_scores_location <int>,
    ## #   review_scores_value <int>, requires_license <chr>, license <int>,
    ## #   jurisdiction_names <chr>, instant_bookable <chr>,
    ## #   cancellation_policy <chr>, require_guest_profile_picture <chr>,
    ## #   require_guest_phone_verification <chr>,
    ## #   calculated_host_listings_count <int>, reviews_per_month <dbl>

``` r
tail(airbnb)
```

    ## # A tibble: 6 x 92
    ##        id listing_url scrape_id last_scraped name  summary   space        
    ##     <int> <chr>           <dbl> <date>       <chr> <chr>     <chr>        
    ## 1 2730613 https://ww…   2.02e13 2015-10-03   Swee… A privat… This is a 2n…
    ## 2 5414326 https://ww…   2.02e13 2015-10-03   Beve… My sweet… We call my h…
    ## 3 3666299 https://ww…   2.02e13 2015-10-03   Fami… Family h… The Master b…
    ## 4 8623269 https://ww…   2.02e13 2015-10-03   Lake… It is at… <NA>         
    ## 5 8305169 https://ww…   2.02e13 2015-10-03   Chic… Balcony … Spacious hig…
    ## 6 8253039 https://ww…   2.02e13 2015-10-03   Pvt … Breathta… Access to Be…
    ## # ... with 85 more variables: description <chr>,
    ## #   experiences_offered <chr>, neighborhood_overview <chr>, notes <chr>,
    ## #   transit <chr>, thumbnail_url <chr>, medium_url <chr>,
    ## #   picture_url <chr>, xl_picture_url <chr>, host_id <int>,
    ## #   host_url <chr>, host_name <chr>, host_since <date>,
    ## #   host_location <chr>, host_about <chr>, host_response_time <chr>,
    ## #   host_response_rate <chr>, host_acceptance_rate <chr>,
    ## #   host_is_superhost <chr>, host_thumbnail_url <chr>,
    ## #   host_picture_url <chr>, host_neighbourhood <chr>,
    ## #   host_listings_count <int>, host_total_listings_count <int>,
    ## #   host_verifications <chr>, host_has_profile_pic <chr>,
    ## #   host_identity_verified <chr>, street <chr>, neighbourhood <chr>,
    ## #   neighbourhood_cleansed <chr>, neighbourhood_group_cleansed <chr>,
    ## #   city <chr>, state <chr>, zipcode <int>, market <chr>,
    ## #   smart_location <chr>, country_code <chr>, country <chr>,
    ## #   latitude <dbl>, longitude <dbl>, is_location_exact <chr>,
    ## #   property_type <chr>, room_type <chr>, accommodates <int>,
    ## #   bathrooms <dbl>, bedrooms <int>, beds <int>, bed_type <chr>,
    ## #   amenities <chr>, square_feet <int>, price <chr>, weekly_price <chr>,
    ## #   monthly_price <chr>, security_deposit <chr>, cleaning_fee <chr>,
    ## #   guests_included <int>, extra_people <chr>, minimum_nights <int>,
    ## #   maximum_nights <int>, calendar_updated <chr>, has_availability <chr>,
    ## #   availability_30 <int>, availability_60 <int>, availability_90 <int>,
    ## #   availability_365 <int>, calendar_last_scraped <date>,
    ## #   number_of_reviews <int>, first_review <date>, last_review <date>,
    ## #   review_scores_rating <int>, review_scores_accuracy <int>,
    ## #   review_scores_cleanliness <int>, review_scores_checkin <int>,
    ## #   review_scores_communication <int>, review_scores_location <int>,
    ## #   review_scores_value <int>, requires_license <chr>, license <int>,
    ## #   jurisdiction_names <chr>, instant_bookable <chr>,
    ## #   cancellation_policy <chr>, require_guest_profile_picture <chr>,
    ## #   require_guest_phone_verification <chr>,
    ## #   calculated_host_listings_count <int>, reviews_per_month <dbl>

``` r
colnames(airbnb)
```

    ##  [1] "id"                               "listing_url"                     
    ##  [3] "scrape_id"                        "last_scraped"                    
    ##  [5] "name"                             "summary"                         
    ##  [7] "space"                            "description"                     
    ##  [9] "experiences_offered"              "neighborhood_overview"           
    ## [11] "notes"                            "transit"                         
    ## [13] "thumbnail_url"                    "medium_url"                      
    ## [15] "picture_url"                      "xl_picture_url"                  
    ## [17] "host_id"                          "host_url"                        
    ## [19] "host_name"                        "host_since"                      
    ## [21] "host_location"                    "host_about"                      
    ## [23] "host_response_time"               "host_response_rate"              
    ## [25] "host_acceptance_rate"             "host_is_superhost"               
    ## [27] "host_thumbnail_url"               "host_picture_url"                
    ## [29] "host_neighbourhood"               "host_listings_count"             
    ## [31] "host_total_listings_count"        "host_verifications"              
    ## [33] "host_has_profile_pic"             "host_identity_verified"          
    ## [35] "street"                           "neighbourhood"                   
    ## [37] "neighbourhood_cleansed"           "neighbourhood_group_cleansed"    
    ## [39] "city"                             "state"                           
    ## [41] "zipcode"                          "market"                          
    ## [43] "smart_location"                   "country_code"                    
    ## [45] "country"                          "latitude"                        
    ## [47] "longitude"                        "is_location_exact"               
    ## [49] "property_type"                    "room_type"                       
    ## [51] "accommodates"                     "bathrooms"                       
    ## [53] "bedrooms"                         "beds"                            
    ## [55] "bed_type"                         "amenities"                       
    ## [57] "square_feet"                      "price"                           
    ## [59] "weekly_price"                     "monthly_price"                   
    ## [61] "security_deposit"                 "cleaning_fee"                    
    ## [63] "guests_included"                  "extra_people"                    
    ## [65] "minimum_nights"                   "maximum_nights"                  
    ## [67] "calendar_updated"                 "has_availability"                
    ## [69] "availability_30"                  "availability_60"                 
    ## [71] "availability_90"                  "availability_365"                
    ## [73] "calendar_last_scraped"            "number_of_reviews"               
    ## [75] "first_review"                     "last_review"                     
    ## [77] "review_scores_rating"             "review_scores_accuracy"          
    ## [79] "review_scores_cleanliness"        "review_scores_checkin"           
    ## [81] "review_scores_communication"      "review_scores_location"          
    ## [83] "review_scores_value"              "requires_license"                
    ## [85] "license"                          "jurisdiction_names"              
    ## [87] "instant_bookable"                 "cancellation_policy"             
    ## [89] "require_guest_profile_picture"    "require_guest_phone_verification"
    ## [91] "calculated_host_listings_count"   "reviews_per_month"

------------------------------------------------------------------------

Data Selection
--------------

------------------------------------------------------------------------

-   Now lets clean the data and delete some unessary columns for this analysis

-   Extract the airbnb\_id to later use and identify the columns to remove

-   Since there are 92 features/columns we can split the column names vector into different chunks

-   The 92 features/columns are of variating types and measures we can split the dataset into diffent sections.

-   Such as features/columns related to links/urls or only text columns that we can use later for natural language processing.

-   Same process applies to features/columns related to location

-   Finally we can remove the columns from the new datasets to create a final dataset that will be more numeric in nature.

-   All datasets will be linked/related by the airbnb\_id

``` r
airbnb <- rename(airbnb, airbnb_id = id)
airbnb_id <- airbnb$airbnb_id
```

``` r
colnames(airbnb)[1:30]
```

    ##  [1] "airbnb_id"             "listing_url"          
    ##  [3] "scrape_id"             "last_scraped"         
    ##  [5] "name"                  "summary"              
    ##  [7] "space"                 "description"          
    ##  [9] "experiences_offered"   "neighborhood_overview"
    ## [11] "notes"                 "transit"              
    ## [13] "thumbnail_url"         "medium_url"           
    ## [15] "picture_url"           "xl_picture_url"       
    ## [17] "host_id"               "host_url"             
    ## [19] "host_name"             "host_since"           
    ## [21] "host_location"         "host_about"           
    ## [23] "host_response_time"    "host_response_rate"   
    ## [25] "host_acceptance_rate"  "host_is_superhost"    
    ## [27] "host_thumbnail_url"    "host_picture_url"     
    ## [29] "host_neighbourhood"    "host_listings_count"

``` r
colnames(airbnb)[31:65]
```

    ##  [1] "host_total_listings_count"    "host_verifications"          
    ##  [3] "host_has_profile_pic"         "host_identity_verified"      
    ##  [5] "street"                       "neighbourhood"               
    ##  [7] "neighbourhood_cleansed"       "neighbourhood_group_cleansed"
    ##  [9] "city"                         "state"                       
    ## [11] "zipcode"                      "market"                      
    ## [13] "smart_location"               "country_code"                
    ## [15] "country"                      "latitude"                    
    ## [17] "longitude"                    "is_location_exact"           
    ## [19] "property_type"                "room_type"                   
    ## [21] "accommodates"                 "bathrooms"                   
    ## [23] "bedrooms"                     "beds"                        
    ## [25] "bed_type"                     "amenities"                   
    ## [27] "square_feet"                  "price"                       
    ## [29] "weekly_price"                 "monthly_price"               
    ## [31] "security_deposit"             "cleaning_fee"                
    ## [33] "guests_included"              "extra_people"                
    ## [35] "minimum_nights"

``` r
colnames(airbnb)[66:92]
```

    ##  [1] "maximum_nights"                   "calendar_updated"                
    ##  [3] "has_availability"                 "availability_30"                 
    ##  [5] "availability_60"                  "availability_90"                 
    ##  [7] "availability_365"                 "calendar_last_scraped"           
    ##  [9] "number_of_reviews"                "first_review"                    
    ## [11] "last_review"                      "review_scores_rating"            
    ## [13] "review_scores_accuracy"           "review_scores_cleanliness"       
    ## [15] "review_scores_checkin"            "review_scores_communication"     
    ## [17] "review_scores_location"           "review_scores_value"             
    ## [19] "requires_license"                 "license"                         
    ## [21] "jurisdiction_names"               "instant_bookable"                
    ## [23] "cancellation_policy"              "require_guest_profile_picture"   
    ## [25] "require_guest_phone_verification" "calculated_host_listings_count"  
    ## [27] "reviews_per_month"

### Select only columns related to url links

``` r
airbnb_urls <- select(airbnb, contains("url"))
ulr_columns <- colnames(airbnb_urls)
airbnb_urls <- add_column(airbnb_urls, airbnb_id, .before = 1)
```

``` r
head(airbnb_urls)
```

    ## # A tibble: 6 x 9
    ##   airbnb_id listing_url  thumbnail_url      medium_url    picture_url     
    ##       <int> <chr>        <chr>              <chr>         <chr>           
    ## 1   1874928 https://www… https://a2.muscac… https://a2.m… https://a2.musc…
    ## 2    739495 https://www… https://a0.muscac… https://a0.m… https://a0.musc…
    ## 3   1696051 https://www… https://a2.muscac… https://a2.m… https://a2.musc…
    ## 4   5152597 https://www… https://a2.muscac… https://a2.m… https://a2.musc…
    ## 5   8036094 https://www… https://a2.muscac… https://a2.m… https://a2.musc…
    ## 6   7395957 https://www… https://a2.muscac… https://a2.m… https://a2.musc…
    ## # ... with 4 more variables: xl_picture_url <chr>, host_url <chr>,
    ## #   host_thumbnail_url <chr>, host_picture_url <chr>

### Select only columns containg text

``` r
text_columns <- c("host_name","name","amenities", "experiences_offered",
                  "host_verifications","transit","notes", 
                 "neighborhood_overview", "host_about", 
                 "description", "space","summary")

airbnb_nlp <- select(airbnb, text_columns)

airbnb_nlp <- add_column(airbnb_nlp, airbnb_id, .before = 1)
```

``` r
head(airbnb_nlp)
```

    ## # A tibble: 6 x 13
    ##   airbnb_id host_name  name  amenities   experiences_off… host_verificati…
    ##       <int> <chr>      <chr> <chr>       <chr>            <chr>           
    ## 1   1874928 Rick And … Sunn… "{TV,\"Cab… none             ['email', 'phon…
    ## 2    739495 Janet      Love… "{TV,\"Cab… none             ['email', 'phon…
    ## 3   1696051 Ashley     Uniq… "{TV,\"Cab… none             ['email', 'phon…
    ## 4   5152597 Patrick    Sunn… "{TV,Inter… none             ['email', 'phon…
    ## 5   8036094 Annemarie  Brig… "{Internet… none             ['email', 'phon…
    ## 6   7395957 Rebekah    Linc… "{Internet… none             ['phone', 'revi…
    ## # ... with 7 more variables: transit <chr>, notes <chr>,
    ## #   neighborhood_overview <chr>, host_about <chr>, description <chr>,
    ## #   space <chr>, summary <chr>

### Select only columns related to listing location

``` r
location_columns <- c("zipcode", "latitude", "longitude", "city", "state",
                     "street", "neighbourhood", "neighbourhood_cleansed",
                     "neighbourhood_group_cleansed","host_location", "host_neighbourhood",
                     "market", "smart_location", "jurisdiction_names", "country_code", 
                     "country")

airbnb_loc <- select(airbnb, location_columns)

airbnb_loc <- add_column(airbnb_loc, airbnb_id, .before = 1)
```

``` r
head(airbnb_loc)
```

    ## # A tibble: 6 x 17
    ##   airbnb_id zipcode latitude longitude city   state street   neighbourhood
    ##       <int>   <int>    <dbl>     <dbl> <chr>  <chr> <chr>    <chr>        
    ## 1   1874928   60625     42.0     -87.7 Chica… IL    North L… Lincoln Squa…
    ## 2    739495   60625     42.0     -87.7 Chica… IL    W Farra… Lincoln Squa…
    ## 3   1696051   60625     42.0     -87.7 Chica… IL    West Ca… Lincoln Squa…
    ## 4   5152597   60625     42.0     -87.7 Chica… IL    North T… Lincoln Squa…
    ## 5   8036094   60625     42.0     -87.7 Chica… IL    North C… Lincoln Squa…
    ## 6   7395957   60618     42.0     -87.7 Chica… IL    W Hutch… Lincoln Squa…
    ## # ... with 9 more variables: neighbourhood_cleansed <chr>,
    ## #   neighbourhood_group_cleansed <chr>, host_location <chr>,
    ## #   host_neighbourhood <chr>, market <chr>, smart_location <chr>,
    ## #   jurisdiction_names <chr>, country_code <chr>, country <chr>

### Use select and one\_of function to remove the columns from previous datasets (ulr\_columns, text\_columns, location\_columns)

``` r
# unique(as.character(airbnb$scrape_id))

remove_columns <- c(ulr_columns, text_columns, location_columns, "scrape_id", "last_scraped")

airbnb_clean <- select(airbnb, -one_of(remove_columns))
```

### Inspect the new more compacted dataset. By doing this we reduced the size by almost half

``` r
head(airbnb_clean)
```

    ## # A tibble: 6 x 54
    ##   airbnb_id  host_id host_since host_response_time host_response_rate
    ##       <int>    <int> <date>     <chr>              <chr>             
    ## 1   1874928  9767449 2013-11-02 within an hour     100%              
    ## 2    739495  3867687 2012-10-14 within a day       100%              
    ## 3   1696051  3350653 2012-08-23 within a few hours 90%               
    ## 4   5152597 22591305 2014-10-15 within an hour     67%               
    ## 5   8036094  7950629 2013-08-05 within an hour     100%              
    ## 6   7395957 31551384 2015-04-19 within an hour     100%              
    ## # ... with 49 more variables: host_acceptance_rate <chr>,
    ## #   host_is_superhost <chr>, host_listings_count <int>,
    ## #   host_total_listings_count <int>, host_has_profile_pic <chr>,
    ## #   host_identity_verified <chr>, is_location_exact <chr>,
    ## #   property_type <chr>, room_type <chr>, accommodates <int>,
    ## #   bathrooms <dbl>, bedrooms <int>, beds <int>, bed_type <chr>,
    ## #   square_feet <int>, price <chr>, weekly_price <chr>,
    ## #   monthly_price <chr>, security_deposit <chr>, cleaning_fee <chr>,
    ## #   guests_included <int>, extra_people <chr>, minimum_nights <int>,
    ## #   maximum_nights <int>, calendar_updated <chr>, has_availability <chr>,
    ## #   availability_30 <int>, availability_60 <int>, availability_90 <int>,
    ## #   availability_365 <int>, calendar_last_scraped <date>,
    ## #   number_of_reviews <int>, first_review <date>, last_review <date>,
    ## #   review_scores_rating <int>, review_scores_accuracy <int>,
    ## #   review_scores_cleanliness <int>, review_scores_checkin <int>,
    ## #   review_scores_communication <int>, review_scores_location <int>,
    ## #   review_scores_value <int>, requires_license <chr>, license <int>,
    ## #   instant_bookable <chr>, cancellation_policy <chr>,
    ## #   require_guest_profile_picture <chr>,
    ## #   require_guest_phone_verification <chr>,
    ## #   calculated_host_listings_count <int>, reviews_per_month <dbl>

### Save the new dataset for reference and later use

``` r
write_csv(airbnb_urls, "data/2015/airbnb_urls.csv")

write_csv(airbnb_nlp, "data/2015/airbnb_nlp.csv")

write_csv(airbnb_loc, "data/2015/airbnb_loc.csv")
```

------------------------------------------------------------------------

Data Types and Cleaning
-----------------------

------------------------------------------------------------------------

``` r
head(airbnb_clean)
```

    ## # A tibble: 6 x 54
    ##   airbnb_id  host_id host_since host_response_time host_response_rate
    ##       <int>    <int> <date>     <chr>              <chr>             
    ## 1   1874928  9767449 2013-11-02 within an hour     100%              
    ## 2    739495  3867687 2012-10-14 within a day       100%              
    ## 3   1696051  3350653 2012-08-23 within a few hours 90%               
    ## 4   5152597 22591305 2014-10-15 within an hour     67%               
    ## 5   8036094  7950629 2013-08-05 within an hour     100%              
    ## 6   7395957 31551384 2015-04-19 within an hour     100%              
    ## # ... with 49 more variables: host_acceptance_rate <chr>,
    ## #   host_is_superhost <chr>, host_listings_count <int>,
    ## #   host_total_listings_count <int>, host_has_profile_pic <chr>,
    ## #   host_identity_verified <chr>, is_location_exact <chr>,
    ## #   property_type <chr>, room_type <chr>, accommodates <int>,
    ## #   bathrooms <dbl>, bedrooms <int>, beds <int>, bed_type <chr>,
    ## #   square_feet <int>, price <chr>, weekly_price <chr>,
    ## #   monthly_price <chr>, security_deposit <chr>, cleaning_fee <chr>,
    ## #   guests_included <int>, extra_people <chr>, minimum_nights <int>,
    ## #   maximum_nights <int>, calendar_updated <chr>, has_availability <chr>,
    ## #   availability_30 <int>, availability_60 <int>, availability_90 <int>,
    ## #   availability_365 <int>, calendar_last_scraped <date>,
    ## #   number_of_reviews <int>, first_review <date>, last_review <date>,
    ## #   review_scores_rating <int>, review_scores_accuracy <int>,
    ## #   review_scores_cleanliness <int>, review_scores_checkin <int>,
    ## #   review_scores_communication <int>, review_scores_location <int>,
    ## #   review_scores_value <int>, requires_license <chr>, license <int>,
    ## #   instant_bookable <chr>, cancellation_policy <chr>,
    ## #   require_guest_profile_picture <chr>,
    ## #   require_guest_phone_verification <chr>,
    ## #   calculated_host_listings_count <int>, reviews_per_month <dbl>

``` r
airbnb_clean$room_type <- airbnb_clean$room_type %>% 
  tolower() %>% 
  str_replace_all(., " ", "_") %>% 
  str_replace(., "home/apt","place") %>% 
  as_factor()
```

``` r
airbnb_clean$bed_type <- airbnb_clean$bed_type %>% 
  tolower() %>% 
  str_replace_all(., " ", "_") %>% 
  str_replace(., "pull.*","sofa_bed") %>% 
  str_replace(., "real_.*","bed") %>% 
  as_factor()
```

``` r
airbnb_clean$host_response_rate <- airbnb_clean$host_response_rate %>% 
  str_remove(. , "%") %>% 
  as.numeric()/100
```

    ## Warning in function_list[[k]](value): NAs introduced by coercion

``` r
airbnb_clean$host_acceptance_rate <- airbnb_clean$host_acceptance_rate %>% 
  str_remove(. , "%") %>% 
  as.numeric()/100
```

    ## Warning in function_list[[k]](value): NAs introduced by coercion

``` r
airbnb_clean$property_type  <- airbnb_clean$property_type %>%  
  str_replace(., " \\& ", "_") %>% 
  str_replace(., "\\/", "_") %>% 
  as_factor()
```

``` r
airbnb_clean$price <- airbnb_clean$price %>% 
  str_remove(., "\\$") %>% 
  str_remove(., ",") %>% 
  as.numeric()

airbnb_clean$weekly_price <- airbnb_clean$weekly_price %>% 
  str_remove(., "\\$") %>% 
  str_remove(., ",") %>% 
  as.numeric()

airbnb_clean$monthly_price <- airbnb_clean$monthly_price %>% 
  str_remove(., "\\$") %>% 
  str_remove(., ",") %>% 
  as.numeric()

airbnb_clean$security_deposit <- airbnb_clean$security_deposit %>% 
  str_remove(., "\\$") %>% 
  str_remove(., ",") %>% 
  as.numeric()

airbnb_clean$extra_people <- airbnb_clean$extra_people %>% 
  str_remove(., "\\$") %>% 
  str_remove(., ",") %>% 
  as.numeric()

airbnb_clean <- rename(airbnb_clean, extra_people_fee = extra_people)

airbnb_clean$cleaning_fee <- airbnb_clean$cleaning_fee %>% 
  str_remove(., "\\$") %>% 
  str_remove(., ",") %>% 
  as.numeric()
```

``` r
updated_days <- function(item){
  if(str_detect(item, "today"))
        item <- 0
  if(str_detect(item, "yesterday"))
        item <- 1
  if(str_detect(item, "never"))
        item <- 9999
  if(str_detect(item, "(a week ago)|(1 week ago)"))
        item <- 7
  if(str_detect(item, "days"))
    item <- str_extract(item, "\\d+") %>% 
      as.numeric()
  if(str_detect(item, "weeks"))
    item <- str_extract(item, "\\d+") %>% 
      as.numeric() * 7
  if(str_detect(item, "months"))
    item <- str_extract(item, "\\d+") %>% 
      as.numeric() * 30 
  return(item)
}


calendar_updated_days <- map_dbl(airbnb_clean$calendar_updated, updated_days)

airbnb_clean$calendar_updated_days <- if_else(calendar_updated_days %in% 9999, 
         airbnb_clean$calendar_last_scraped - airbnb_clean$host_since, 
         airbnb_clean$calendar_last_scraped - (airbnb_clean$calendar_last_scraped - calendar_updated_days)) %>% as.double()

airbnb_clean$calendar_updated <- NULL
```

``` r
airbnb_clean$host_response_time <- airbnb_clean$host_response_time %>% 
  str_replace("N/A", "NA") %>% 
  str_replace(".*(an hour)",  "60") %>% 
  str_replace(".*(few hours)",  as.character(60*12)) %>% 
  str_replace(".*(a day)",  as.character(60*24)) %>% 
  str_replace(".*(few days).*",  as.character(60*(5*24))) %>% 
  factor(., levels = c("60", "720", "1440", "7200"))
```

### Change variable to correct datatypes

``` r
airbnb_clean <- airbnb_clean %>% 
  mutate(airbnb_id = as.character(airbnb_id)) %>% 
  mutate(host_id = as.character(host_id)) %>% 
  mutate(property_type = as_factor(tolower(property_type))) %>% 
  mutate(cancellation_policy = factor(tolower(cancellation_policy),
                                      levels = c("flexible", "moderate", 
                                                 "strict", "super_strict_30")))
```

#### Change variable to logical (TRUE/FALSE)

``` r
airbnb_clean <- airbnb_clean %>% 
  mutate(host_is_superhost = parse_logical(host_is_superhost)) %>% 
  mutate(host_has_profile_pic = parse_logical(host_has_profile_pic)) %>% 
  mutate(host_identity_verified = parse_logical(host_identity_verified)) %>% 
  mutate(is_location_exact = parse_logical(is_location_exact)) %>% 
  mutate(requires_license = parse_logical(requires_license)) %>% 
  mutate(instant_bookable = parse_logical(instant_bookable)) %>% 
  mutate(has_availability = parse_logical(has_availability)) %>% 
  mutate(require_guest_profile_picture = parse_logical(require_guest_profile_picture)) %>% 
  mutate(require_guest_phone_verification = parse_logical(require_guest_phone_verification))
```

``` r
head(airbnb_clean)
```

    ## # A tibble: 6 x 54
    ##   airbnb_id host_id  host_since host_response_time host_response_rate
    ##   <chr>     <chr>    <date>     <fct>                           <dbl>
    ## 1 1874928   9767449  2013-11-02 60                               1   
    ## 2 739495    3867687  2012-10-14 1440                             1   
    ## 3 1696051   3350653  2012-08-23 720                              0.9 
    ## 4 5152597   22591305 2014-10-15 60                               0.67
    ## 5 8036094   7950629  2013-08-05 60                               1   
    ## 6 7395957   31551384 2015-04-19 60                               1   
    ## # ... with 49 more variables: host_acceptance_rate <dbl>,
    ## #   host_is_superhost <lgl>, host_listings_count <int>,
    ## #   host_total_listings_count <int>, host_has_profile_pic <lgl>,
    ## #   host_identity_verified <lgl>, is_location_exact <lgl>,
    ## #   property_type <fct>, room_type <fct>, accommodates <int>,
    ## #   bathrooms <dbl>, bedrooms <int>, beds <int>, bed_type <fct>,
    ## #   square_feet <int>, price <dbl>, weekly_price <dbl>,
    ## #   monthly_price <dbl>, security_deposit <dbl>, cleaning_fee <dbl>,
    ## #   guests_included <int>, extra_people_fee <dbl>, minimum_nights <int>,
    ## #   maximum_nights <int>, has_availability <lgl>, availability_30 <int>,
    ## #   availability_60 <int>, availability_90 <int>, availability_365 <int>,
    ## #   calendar_last_scraped <date>, number_of_reviews <int>,
    ## #   first_review <date>, last_review <date>, review_scores_rating <int>,
    ## #   review_scores_accuracy <int>, review_scores_cleanliness <int>,
    ## #   review_scores_checkin <int>, review_scores_communication <int>,
    ## #   review_scores_location <int>, review_scores_value <int>,
    ## #   requires_license <lgl>, license <int>, instant_bookable <lgl>,
    ## #   cancellation_policy <fct>, require_guest_profile_picture <lgl>,
    ## #   require_guest_phone_verification <lgl>,
    ## #   calculated_host_listings_count <int>, reviews_per_month <dbl>,
    ## #   calendar_updated_days <dbl>

### Save clean dataset with different name

``` r
saveRDS(airbnb_clean, "data/2015/airbnb_clean.rds")
```

------------------------------------------------------------------------

Descriptive Statistics
----------------------

------------------------------------------------------------------------

``` r
airbnb_clean <- readRDS("data/2015/airbnb_clean.rds")
```

``` r
summary(airbnb_clean[1:18])
```

    ##   airbnb_id           host_id            host_since        
    ##  Length:5147        Length:5147        Min.   :2008-05-06  
    ##  Class :character   Class :character   1st Qu.:2012-12-27  
    ##  Mode  :character   Mode  :character   Median :2014-05-01  
    ##                                        Mean   :2013-12-14  
    ##                                        3rd Qu.:2015-04-07  
    ##                                        Max.   :2015-10-02  
    ##                                                            
    ##  host_response_time host_response_rate host_acceptance_rate
    ##  60  :2175          Min.   :0.100      Min.   :0.0000      
    ##  720 :1493          1st Qu.:0.900      1st Qu.:0.8000      
    ##  1440: 934          Median :1.000      Median :0.9600      
    ##  7200:  98          Mean   :0.925      Mean   :0.8682      
    ##  NA's: 447          3rd Qu.:1.000      3rd Qu.:1.0000      
    ##                     Max.   :1.000      Max.   :1.0000      
    ##                     NA's   :447        NA's   :565         
    ##  host_is_superhost host_listings_count host_total_listings_count
    ##  Mode :logical     Min.   :  1.000     Min.   :  1.000          
    ##  FALSE:4660        1st Qu.:  1.000     1st Qu.:  1.000          
    ##  TRUE :487         Median :  1.000     Median :  1.000          
    ##                    Mean   :  4.791     Mean   :  4.791          
    ##                    3rd Qu.:  2.000     3rd Qu.:  2.000          
    ##                    Max.   :480.000     Max.   :480.000          
    ##                                                                 
    ##  host_has_profile_pic host_identity_verified is_location_exact
    ##  Mode :logical        Mode :logical          Mode :logical    
    ##  FALSE:22             FALSE:1201             FALSE:653        
    ##  TRUE :5125           TRUE :3946             TRUE :4494       
    ##                                                               
    ##                                                               
    ##                                                               
    ##                                                               
    ##      property_type         room_type     accommodates      bathrooms    
    ##  apartment  :4000   entire_place:2928   Min.   : 1.000   Min.   :0.000  
    ##  house      : 593   private_room:1972   1st Qu.: 2.000   1st Qu.:1.000  
    ##  condominium: 285   shared_room : 247   Median : 2.000   Median :1.000  
    ##  loft       : 154                       Mean   : 3.275   Mean   :1.223  
    ##  townhouse  :  42                       3rd Qu.: 4.000   3rd Qu.:1.000  
    ##  (Other)    :  72                       Max.   :16.000   Max.   :6.000  
    ##  NA's       :   1                                        NA's   :18     
    ##     bedrooms           beds       
    ##  Min.   : 0.000   Min.   : 1.000  
    ##  1st Qu.: 1.000   1st Qu.: 1.000  
    ##  Median : 1.000   Median : 1.000  
    ##  Mean   : 1.279   Mean   : 1.642  
    ##  3rd Qu.: 2.000   3rd Qu.: 2.000  
    ##  Max.   :10.000   Max.   :16.000  
    ##  NA's   :15       NA's   :13

``` r
summary(airbnb_clean[19:37])
```

    ##      bed_type     square_feet        price         weekly_price    
    ##  bed     :4845   Min.   :    0   Min.   :  10.0   Min.   :   70.0  
    ##  airbed  : 113   1st Qu.:  575   1st Qu.:  75.0   1st Qu.:  425.0  
    ##  futon   :  96   Median : 1000   Median : 110.0   Median :  630.5  
    ##  sofa_bed:  51   Mean   : 1236   Mean   : 149.5   Mean   :  814.6  
    ##  couch   :  42   3rd Qu.: 1350   3rd Qu.: 175.0   3rd Qu.:  950.0  
    ##                  Max.   :22000   Max.   :4900.0   Max.   :10000.0  
    ##                  NA's   :5060                     NA's   :2525     
    ##  monthly_price   security_deposit  cleaning_fee    guests_included
    ##  Min.   :  310   Min.   :  95.0   Min.   :  5.00   Min.   : 0.00  
    ##  1st Qu.: 1358   1st Qu.: 100.0   1st Qu.: 20.00   1st Qu.: 1.00  
    ##  Median : 2000   Median : 200.0   Median : 40.00   Median : 1.00  
    ##  Mean   : 2652   Mean   : 307.2   Mean   : 47.87   Mean   : 1.59  
    ##  3rd Qu.: 3150   3rd Qu.: 350.0   3rd Qu.: 65.00   3rd Qu.: 2.00  
    ##  Max.   :30000   Max.   :4000.0   Max.   :400.00   Max.   :16.00  
    ##  NA's   :3035    NA's   :3387     NA's   :2100                    
    ##  extra_people_fee minimum_nights    maximum_nights       has_availability
    ##  Min.   :  0.00   Min.   :  1.000   Min.   :         1   Mode:logical    
    ##  1st Qu.:  0.00   1st Qu.:  1.000   1st Qu.:        93   TRUE:5147       
    ##  Median :  0.00   Median :  1.000   Median :      1125                   
    ##  Mean   : 12.61   Mean   :  2.118   Mean   :    418271                   
    ##  3rd Qu.: 20.00   3rd Qu.:  2.000   3rd Qu.:      1125                   
    ##  Max.   :300.00   Max.   :180.000   Max.   :2147483647                   
    ##                                                                          
    ##  availability_30 availability_60 availability_90 availability_365
    ##  Min.   : 0.00   Min.   : 0.00   Min.   : 0.00   Min.   :  0.0   
    ##  1st Qu.: 0.00   1st Qu.: 5.00   1st Qu.:14.00   1st Qu.:123.0   
    ##  Median : 9.00   Median :31.00   Median :58.00   Median :311.0   
    ##  Mean   :10.91   Mean   :28.57   Mean   :48.29   Mean   :244.9   
    ##  3rd Qu.:19.00   3rd Qu.:47.00   3rd Qu.:77.00   3rd Qu.:349.0   
    ##  Max.   :30.00   Max.   :60.00   Max.   :90.00   Max.   :365.0   
    ##                                                                  
    ##  calendar_last_scraped number_of_reviews  first_review       
    ##  Min.   :2015-10-02    Min.   :  0.0     Min.   :2009-03-06  
    ##  1st Qu.:2015-10-02    1st Qu.:  1.0     1st Qu.:2014-08-04  
    ##  Median :2015-10-03    Median :  5.0     Median :2015-05-17  
    ##  Mean   :2015-10-02    Mean   : 14.6     Mean   :2014-12-06  
    ##  3rd Qu.:2015-10-03    3rd Qu.: 16.0     3rd Qu.:2015-08-01  
    ##  Max.   :2015-10-03    Max.   :298.0     Max.   :2015-10-03  
    ##                                          NA's   :1005

``` r
summary(airbnb_clean[38:54])
```

    ##   last_review         review_scores_rating review_scores_accuracy
    ##  Min.   :2010-08-09   Min.   : 20.00       Min.   : 2.000        
    ##  1st Qu.:2015-08-23   1st Qu.: 91.00       1st Qu.: 9.000        
    ##  Median :2015-09-18   Median : 96.00       Median :10.000        
    ##  Mean   :2015-08-19   Mean   : 93.99       Mean   : 9.555        
    ##  3rd Qu.:2015-09-25   3rd Qu.:100.00       3rd Qu.:10.000        
    ##  Max.   :2015-10-03   Max.   :100.00       Max.   :10.000        
    ##  NA's   :1005         NA's   :1056         NA's   :1073          
    ##  review_scores_cleanliness review_scores_checkin
    ##  Min.   : 2.000            Min.   : 2.000       
    ##  1st Qu.: 9.000            1st Qu.:10.000       
    ##  Median :10.000            Median :10.000       
    ##  Mean   : 9.315            Mean   : 9.743       
    ##  3rd Qu.:10.000            3rd Qu.:10.000       
    ##  Max.   :10.000            Max.   :10.000       
    ##  NA's   :1075              NA's   :1073         
    ##  review_scores_communication review_scores_location review_scores_value
    ##  Min.   : 2.00               Min.   : 4.000         Min.   : 2.000     
    ##  1st Qu.:10.00               1st Qu.: 9.000         1st Qu.: 9.000     
    ##  Median :10.00               Median :10.000         Median :10.000     
    ##  Mean   : 9.79               Mean   : 9.466         Mean   : 9.376     
    ##  3rd Qu.:10.00               3rd Qu.:10.000         3rd Qu.:10.000     
    ##  Max.   :10.00               Max.   :10.000         Max.   :10.000     
    ##  NA's   :1069                NA's   :1068           NA's   :1069       
    ##  requires_license    license          instant_bookable
    ##  Mode :logical    Min.   :      102   Mode :logical   
    ##  FALSE:7          1st Qu.:  2093472   FALSE:4584      
    ##  TRUE :5140       Median :  2233303   TRUE :563       
    ##                   Mean   : 17724533                   
    ##                   3rd Qu.:  2314739                   
    ##                   Max.   :352167776                   
    ##                   NA's   :5111                        
    ##       cancellation_policy require_guest_profile_picture
    ##  flexible       :2021     Mode :logical                
    ##  moderate       :1487     FALSE:4890                   
    ##  strict         :1623     TRUE :257                    
    ##  super_strict_30:  16                                  
    ##                                                        
    ##                                                        
    ##                                                        
    ##  require_guest_phone_verification calculated_host_listings_count
    ##  Mode :logical                    Min.   : 1.000                
    ##  FALSE:4832                       1st Qu.: 1.000                
    ##  TRUE :315                        Median : 1.000                
    ##                                   Mean   : 2.805                
    ##                                   3rd Qu.: 2.000                
    ##                                   Max.   :42.000                
    ##                                                                 
    ##  reviews_per_month calendar_updated_days
    ##  Min.   : 0.020    Min.   :   0.00      
    ##  1st Qu.: 0.900    1st Qu.:   2.00      
    ##  Median : 1.710    Median :   7.00      
    ##  Mean   : 2.173    Mean   :  28.87      
    ##  3rd Qu.: 3.000    3rd Qu.:  28.00      
    ##  Max.   :14.000    Max.   :1687.00      
    ##  NA's   :1005
