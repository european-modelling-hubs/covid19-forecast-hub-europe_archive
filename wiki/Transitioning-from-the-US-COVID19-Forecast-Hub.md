This overview shall help you get started quickly if you are already familiar with the procedures for the [US COVID-19 Forecast Hub](https://github.com/reichlab/covid19-forecast-hub). In case you notice an aspect that is missing please let us know by opening an issue.


What stays the same:
* The **basic folder structure** with a model-specific subfolder in `data-processed` (naming convention `team-model`).
* The **forecast file format** with point forecasts and 23 forecast quantiles.
* **Case and death** forecasts will be collected.
* The use of **epi weeks** running from Sunday to Saturday.
* The **metadata format**.
* The **submission via GitHub pull requests** (you just need to fork the covid19-forecast-hub-europe repository).
* All **evaluation criteria** which will be applied to your forecasts (weighted interval score, absolute error, interval coverage rates).
* The authoritative **truth data source is JHU**.
* The weekly submission deadline on **Monday at 6pm ET** (midnight CET).

What changes:
* We cover **national-level forecasts** for **32 European countries**. The countries to be included and their mapping to **location codes** can be found [here](https://github.com/epiforecasts/covid19-forecast-hub-europe/blob/main/data-locations/locations_eu.csv). Note that location codes are based on the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) standard rather than FIPS codes.
* **Only incidence forecasts** will be covered (i.e. `k wk ahead inc death` and `k wk ahead inc case`). Cumulative targets will not be covered.
* **No hospitalization/ICU forecasts** will be accepted.
* An **(optional) additional column** called `scenario_id` can be included. If included, this needs to be set to `"forecast"` in all rows for short-term forecasts. Other scenarios (e.g., on vaccination strategies) may be added in the future.