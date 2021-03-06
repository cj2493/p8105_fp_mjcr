p8105\_fp\_mjcr
================

Download data:

``` r
#cdc_df = GET("https://chronicdata.cdc.gov/resource/ta23-kdpu.csv") %>%
#  content("parsed") 

cdc_df = read_csv("./data/500_Cities__City-level_Data__GIS_Friendly_Format___2016_release.csv")
```

Select variables we may be interested in:

``` r
cdc_df = cdc_df %>%
  select(c(StateAbbr, PlaceName, Population2010, ACCESS2_AdjPrev, BPHIGH_AdjPrev, BPMED_AdjPrev, CANCER_AdjPrev, CHD_AdjPrev, CHECKUP_AdjPrev, CHOLSCREEN_AdjPrev, COLON_SCREEN_AdjPrev, COPD_AdjPrev,COREM_AdjPrev, COREW_AdjPrev, DENTAL_AdjPrev, DIABETES_AdjPrev, HIGHCHOL_AdjPrev, LPA_AdjPrev, MAMMOUSE_AdjPrev, OBESITY_AdjPrev, PAPTEST_AdjPrev, PHLTH_AdjPrev, STROKE_AdjPrev, Geolocation)) %>% 
  mutate(state = abbr2state(StateAbbr)) %>%
  select(state, everything())
```

Merge data on state expenditure on healthcare:

``` r
#link: https://www.kff.org/other/state-indicator/health-spending-per-capita/?currentTimeframe=0&sortModel=%7B%22colId%22:%22Location%22,%22sort%22:%22asc%22%7D

#Importing the raw expenditure data set and cleaning
healthcare_exp_df = read_csv("./data/health_care_expenditure.csv", 
                             skip = 4, n_max = 51, col_names = F) %>%
  rename(state = "X1", health_exp = "X2") %>%
  mutate(health_exp = str_replace(health_exp, "\\$", ""),
         health_exp  = as.numeric(health_exp))


#Add state healthcare expenditure data to CDC data
cdc_df = left_join(cdc_df, healthcare_exp_df, by = "state")

cdc_df = cdc_df %>% mutate(state = abbr2state(StateAbbr))
```

Merge data regions per state:

``` r
regions_df = read_csv("https://raw.githubusercontent.com/cphalpert/census-regions/master/us%20census%20bureau%20regions%20and%20divisions.csv") %>%
  janitor::clean_names() %>%
  select(-state_code)
  

cdc_df = left_join(cdc_df, regions_df, by = "state")
```

Export merged data:

``` r
write_csv(cdc_df, path = "./data/cdc_df.csv")
```

List of health practice variables and health outcome variables:

``` r
#health_practices = BPMED_AdjPrev, CHECKUP_AdjPrev, CHOLSCREEN_AdjPrev, COLON_SCREEN_AdjPrev, COREM_AdjPrev, COREW_AdjPrev, DENTAL_AdjPrev, LPA_AdjPrev, MAMMOUSE_AdjPrev, PAPTEST_AdjPrev

#health_outcomes = BPHIGH_AdjPrev, CANCER_AdjPrev, CHD_AdjPrev, COPD_AdjPrev, DIABETES_AdjPrev, HIGHCHOL_AdjPrev, OBESITY_AdjPrev, PHLTH_AdjPrev, STROKE_AdjPrev

#miscellaneous = StateAbbr, PlaceName, Population2010, ACCESS2_AdjPrev, Geolocation, state, health_exp, region, division
```
