Airbnb Chicago Market Analysis
==============================

### RNotebook Analysis: [airbnb-data-notebook](../master/airbnb-notebook.Rmd)
-----

### Introduction

* This notebook is use to analyze airbnb data based on the Inside Airbnb project by Murray Cox.
* Airbnb claims to be part of the “sharing economy” and disrupting the hotel industry.
* However, data shows that the majority of Airbnb listings in most cities are entire homes, many of which are rented all year round - disrupting housing and communities.



### Additional Resources

* [insideairbnb.com](http://insideairbnb.com/index.html)
* [rpubs.com/jlroo/](http://rpubs.com/jlroo/airbnb)


### Notebook Version

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

### Project Layout

    .
    └── Airbnb
        ├── airbnb-notebook.Rmd
        │
        ├── data
        │   ├── 2015
        │   │   ├── airbnb_raw.csv
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

### R/RStudio Packages

We are going to use tidyverse a collection of R packages designed for data science.

* Info: [https://www.tidyverse.org](https://www.tidyverse.org)

        ## Loading required package: tidyverse

        ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.2.1 ──

        ## ✔ ggplot2 2.2.1     ✔ purrr   0.2.4
        ## ✔ tibble  1.4.2     ✔ dplyr   0.7.4
        ## ✔ tidyr   0.8.0     ✔ stringr 1.3.0
        ## ✔ readr   1.1.1     ✔ forcats 0.3.0

        ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
        ## ✖ dplyr::filter() masks stats::filter()
        ## ✖ dplyr::lag()    masks stats::lag()

