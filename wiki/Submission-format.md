Each forecast should be stored as a comma-separated value (csv) file in your `data-processed/team-model` folder.

The csv file must use a standardised file name, and contain specific variable names and values which identify the forecast you are submitting. This allows us to evaluate and compare across forecasts. The automatic check validates both the filename and file contents to ensure the file can be used in the visualization and ensemble forecasting.

## File name
Each forecast file within the subdirectory should have the following name format:

`YYYY-MM-DD-team-model.csv`

##### Forecast date
The date `YYYY-MM-DD` is the forecast date. This should be the last day of the submission period (Monday).

##### team-model
The `team` and `model` in this file name must match the name of the `data-processed` directory this file is in.

## File format
### Required variables
The csv file must be contain only the following columns (in any order). No additional columns are allowed.

| column | column type | description |
| -------- | -------- | ------- |
| [`forecast_date`](#forecast-date) | date | Date as **YYYY-MM-DD**, last day (Monday) of submission window |
| Optional: [`scenario_id`](#scenario_id) | string | If included, must be "**forecast**" |
| [`target`](#target) | string | "**_#_ wk ahead inc case**", "**_#_ wk ahead inc death**" or "**_#_ wk ahead inc hosp**" where _#_ is usually between -2 and 4 (see [Targets and Horizons](targets-and-horizons)) |
| [`target_end_date`](#target-end-date) | date | Date as **YYYY-MM-DD**, the last day (Saturday) of the target week |
| [`location`](#location) | string | An **ISO-2** country code |
| [`type`](#type) | string | One of **"point"** or **"quantile"**|
| [`quantile`](#quantile) | numeric | For quantile forecasts, one of the 23 quantiles in `c(0.01, 0.025, seq(0.05, 0.95, by = 0.05), 0.975, 0.99` |
| [`value`](#value) | numeric | The **predicted count**, a non-negative integer number of new cases or deaths in the forecast week |

### Notes on each variable
##### forecast_date
This should correspond with the date in the filename: see [above](#Forecast-date).

##### scenario_id

This optional column identifies whether a model is predicting a forecast, or using a scenario. In the case of the Forecast Hub, the value of `scenario_id` should be **"forecast"**, indicating that the values are true forecasts, i.e. reflect probabilities of observing future values in the [truth data](Targets-and-horizons#truth-data)

For actual scenario modelling, please refer to the [European Covid-19 Scenario Hub page](https://covid19scenariohub.eu/).

##### target
Values in the `target` column must be a character (string) and be one of the following specific targets:

- **"_#_ wk ahead inc case"**
- **"_#_ wk ahead inc hosp"**
- **"_#_ wk ahead inc death"**

###### "_#_ wk ahead"
"_#_" will usually be a number between -2 and 4.

For the week ahead horizon, we use Epidemiological Weeks (EW) defined by the [US CDC](https://wwwn.cdc.gov/nndss/document/MMWR_Week_overview.pdf). Each week starts on Sunday and ends on Saturday. See [here](Targets-and-horizons#date-format) for more detail on EW weeks, and the [template file](https://github.com/epiforecasts/covid19-forecast-hub-europe/blob/main/template/date-to-epiweek.csv) for csv files converting between dates and EW weeks.

###### "inc"
All forecasts should be for the incident (weekly count) number of cases predicted by the model during the week that is N weeks after `forecast_date`.

Predictions for this target will be evaluated compared to the number of new reported cases, as recorded by [JHU](Targets-and-horizons#Truth-data).

##### target_end_date
Values in the `target_end_date` column must be a date in the format `YYYY-MM-DD`.

This is the date for the forecast `target` and will be the Saturday at the end of the week time period. We provide a [template csv](https://github.com/epiforecasts/covid19-forecast-hub-europe/blob/main/template/forecast-dates.csv) to convert between an Epidemiological Week and its end date.

##### location
Values in the `location` column must be one of the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) (ISO-2) geocodes. We provide a [geocode file](https://github.com/epiforecasts/covid19-forecast-hub-europe/blob/main/data-locations/locations_eu.csv) to convert between country names and ISO-2 code (column "iso2c"), or if using R, you can use the [countrycode package](https://cran.r-project.org/web/packages/countrycode/index.html).

##### type
Values in the `type` column are one of

-  **“point”**
-  **“quantile”**

This value indicates whether that row corresponds to a point forecast or a quantile forecast. Point forecasts are used in visualization, while quantile forecasts are used in visualisation and in ensemble construction, as long as all the quantiles given above are present. Both are considered in the evaluation, but with a focus on models that do provide quantiles.

Forecasts must include exactly 1 “point” forecast for each unique combination of `location` and `target` (usually 1 to 4 week ahead incident cases or deaths).

##### quantile
For quantile forecasts, this value indicates the quantile for the `value` in this row, in the format "0.###"". Teams should provide the following 23 quantiles:

    c(0.01, 0.025, seq(0.05, 0.95, by = 0.05), 0.975, 0.99)

i.e.
```
0.010 0.025 0.050 0.100 0.150 0.200 0.250 0.300 0.350 0.400 0.450 0.500 0.550 0.600 0.650 0.700 0.750 0.800 0.850 0.900 0.950 0.975 0.990
```

Together with the single point forecast, this means that there should be 24 rows for every location-target pair.

If `type` is “point”, the `quantile` column value should be set to “NA”.

##### value

Values should be non-negative, integer counts.

- For a “point” prediction, `value` is simply the value of that point prediction for the `target` and `location` associated with that row.
- For a “quantile” prediction, `value` is the inverse of the cumulative distribution function (CDF) for the `target`, `location`, and `quantile` associated with that row.
