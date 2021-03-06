data\_dictionary
================

``` r
url = "https://chronicdata.cdc.gov/500-Cities/500-Cities-City-level-Data-GIS-Friendly-Format-201/k56w-7tny"


read_dict = function(url) {
  
  h = read_html(url)
  
  var_name = h %>%
    html_nodes(".column-summary .column-name") %>%
    html_text()
  
  var_description = h %>%
    html_nodes(".Linkify") %>%
    html_text()
  
  var_type = h %>%
    html_nodes(".type-name") %>%
    html_text()
  
  tibble(
    name = var_name,
    description = var_description,
    type = var_type
  )
}



data_dictionary = read_dict("https://chronicdata.cdc.gov/500-Cities/500-Cities-City-level-Data-GIS-Friendly-Format-201/k56w-7tny")
```

This doesn't read in anything? So for now I copied from the webpage into an excel file (will try to figure this out to get the selector gadget to work before submission)

``` r
data_dictionary = readxl::read_xlsx("./data/data_dictionary.xlsx") 
data_dictionary = data_dictionary %>%
  janitor::clean_names() %>%
  filter(column_name %in% c("StateAbbr", "PlaceName", "Population2010", "ACCESS2_AdjPrev", "BPHIGH_AdjPrev", "BPMED_AdjPrev", "CANCER_AdjPrev", "CHD_AdjPrev", "CHECKUP_AdjPrev", "CHOLSCREEN_AdjPrev", "COLON_SCREEN_AdjPrev", "COPD_AdjPrev", "COREM_AdjPrev", "COREW_AdjPrev", "DENTAL_AdjPrev", "DIABETES_AdjPrev", "HIGHCHOL_AdjPrev", "LPA_AdjPrev", "MAMMOUSE_AdjPrev", "OBESITY_AdjPrev", "PAPTEST_AdjPrev", "PHLTH_AdjPrev", "STROKE_AdjPrev", "Geolocation"))

health_exp_dictionary = tibble(column_name = c("state", "health_exp"),
                               description = c("full name of the state", "total healthcare expenditures per capita by state in 2014"),
                               type = c("Plain Text", "Number"))

data_dictionary = full_join(data_dictionary, health_exp_dictionary)
```

    ## Joining, by = c("column_name", "description", "type")

``` r
region_dict = tibble(column_name = c("region", "division"),
                     description = c("geographical region of the state", "more specific division within the region"),
                     type = c("Plain Text", "Plain Text")
  
)

data_dictionary = full_join(data_dictionary, region_dict)
```

    ## Joining, by = c("column_name", "description", "type")
