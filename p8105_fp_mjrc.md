p8105\_fp\_mjcr
================

download data

``` r
#cdc_df = GET("https://chronicdata.cdc.gov/resource/ta23-kdpu.csv") %>%
#  content("parsed") 

cdc_df = read_csv("./data/500_Cities__City-level_Data__GIS_Friendly_Format___2016_release.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_character(),
    ##   Population2010 = col_integer(),
    ##   ACCESS2_CrudePrev = col_double(),
    ##   ACCESS2_AdjPrev = col_double(),
    ##   ARTHRITIS_CrudePrev = col_double(),
    ##   ARTHRITIS_AdjPrev = col_double(),
    ##   BINGE_CrudePrev = col_double(),
    ##   BINGE_AdjPrev = col_double(),
    ##   BPHIGH_CrudePrev = col_double(),
    ##   BPHIGH_AdjPrev = col_double(),
    ##   BPMED_CrudePrev = col_double(),
    ##   BPMED_AdjPrev = col_double(),
    ##   CANCER_CrudePrev = col_double(),
    ##   CANCER_AdjPrev = col_double(),
    ##   CASTHMA_CrudePrev = col_double(),
    ##   CASTHMA_AdjPrev = col_double(),
    ##   CHD_CrudePrev = col_double(),
    ##   CHD_AdjPrev = col_double(),
    ##   CHECKUP_CrudePrev = col_double(),
    ##   CHECKUP_AdjPrev = col_double(),
    ##   CHOLSCREEN_CrudePrev = col_double()
    ##   # ... with 37 more columns
    ## )

    ## See spec(...) for full column specifications.

Clean data

``` r
cdc_df = cdc_df %>%
  select(c(StateAbbr, PlaceName, Population2010, ACCESS2_CrudePrev, ACCESS2_AdjPrev, BPHIGH_CrudePrev, BPHIGH_AdjPrev, BPMED_CrudePrev, BPMED_AdjPrev, CANCER_CrudePrev, CANCER_AdjPrev, CHD_CrudePrev, CHD_AdjPrev, CHECKUP_CrudePrev, CHECKUP_AdjPrev, CHOLSCREEN_CrudePrev, CHOLSCREEN_AdjPrev, COLON_SCREEN_CrudePrev, COLON_SCREEN_AdjPrev, COPD_CrudePrev, COPD_AdjPrev, COREM_CrudePrev, COREM_AdjPrev, COREW_CrudePrev, COREW_AdjPrev, DENTAL_CrudePrev, DENTAL_AdjPrev, DIABETES_CrudePrev, DIABETES_AdjPrev, HIGHCHOL_CrudePrev, HIGHCHOL_AdjPrev, LPA_CrudePrev, LPA_AdjPrev, MAMMOUSE_CrudePrev, MAMMOUSE_AdjPrev, OBESITY_CrudePrev, OBESITY_AdjPrev, PAPTEST_CrudePrev, PAPTEST_AdjPrev, PHLTH_CrudePrev, PHLTH_AdjPrev, STROKE_CrudePrev, STROKE_AdjPrev, Geolocation))
```
