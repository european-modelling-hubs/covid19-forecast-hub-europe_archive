**This overview is preliminary as certain aspects are yet to be decided for the European Forecast Hub. We will add more details and references to updated documentation soon.**

We here compile an overview of things to keep in mind when transitioning from the German and Polish to the European COVID-19 Forecast Hub.

What stays the same:
* The basic folder structure with a model-specific subfolder in `data-processed` (naming convention `team-model`).
* The **forecast file format** with point forecasts and 23 forecast quantiles and **naming of files** (`YYYY-mm-dd-team-model.csv`).
* **Case and death** forecasts will be collected.
* The use of **epi weeks** running from Sunday to Saturday.
* The **submission via GitHub pull requests** (you just need to fork the covid19-forecast-hub-europe repository).
* All **evaluation criteria** which will be applied to your forecasts (weighted interval score, absolute error, interval coverage rates).

What changes:
* **No daily forecasts** will be accepted.
* **Only incidence forecasts** will be covered (i.e. `k wk ahead inc death` and `k wk ahead inc case`). Cumulative targets will not be covered.
* No hospitalization/ICU forecasts will be accepted (technically this is possible in the DE/PL platform, even though we are currently not showing these forecasts in our visualization).
* The authoritative **truth data source is JHU**.
* Forecasts need to be submitted in a **single file per submission date** (pooling over countries and targets), the naming convention being `YYYY-mm-dd-team_name-model_name.csv`.
* Use of rows with `type = "observed"` has been deprecated as there is only one truth data source. Including them will cause validation checks to fail.
* An **(optional) additional column** called `scenario_id` can be included. If included, this needs to be set to `"forecast"` in all rows for short-term forecasts. Other scenarios (e.g., on vaccination strategies) may be added in the future.
* At least in the beginning **only national level forecasts** will be accepted (i.e. no Bundesländer and voivodeships).
* **Location codes** have been changed to [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). This means you need to use `"DE"` for Germany and `"PL"` for Poland.
* Starting from the fist official submission date on 8 March, the **submission deadline** will be Monday 11:59pm.
* The **metadata format** [has been updated](https://github.com/epiforecasts/covid19-forecast-hub-europe/wiki/Metadata) and will be checked more strictly. Metadata files are compulsory in the European COVID-19 Forecast Hub.