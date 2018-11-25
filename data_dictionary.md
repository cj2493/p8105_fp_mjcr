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
