There is no obligation to submit forecasts for all suggested targets or horizons, and it is up to you to decide which you are comfortable forecasting with your model.

Please take care when submitting the forecasts to be clear which target and horizon you are using: use this page and the [formatting guide](Forecast-format).

## Targets
#### Targets
We are currently focused on the forecast target of:
* **Weekly new COVID-19 hospitalisations**

In addition we are continuing to solicit forecasts of:
* **Weekly new COVID-19 cases**
* **Weekly new COVID-19 deaths**

You can submit forecasts for only cases or hospitalisations or deaths, or multiple targets.
The current priority for the Hub is on hospitalisations.

We only use **incident** forecasts: the count of new hospitalisations (or cases/deaths) per week. We do not use cumulative (running total) forecasts. This varies from other forecast hubs.

#### Truth data

We evaluate forecasts against:

- Hospitalisation data synthesised by [Our World in Data](https://ourworldindata.org/covid-hospitalizations)
- Case and death data collated by the [ECDC](https://www.ecdc.europa.eu/en/publications-data/data-national-14-day-notification-rate-covid-19)

We recommend using these datasets as the basis for forecasts. 

Because data can be subject to ongoing revisions, we assume that data for any given week is stable when downloaded 4 weeks later and ignore any further revisions from that moment. This means that all forecasts are only evaluated against data produced 4 weeks after the forecast target date (even if that data point is later revised).

More information on the data sources, and on the truth files we make available to forecasters, is available in the [data-truth](https://github.com/epiforecasts/covid19-forecast-hub-europe/tree/main/data-truth) directory.

Note there are some differences between the format of the source data sets and what we require in a forecast.
* **Spatial unit:** Subnational data are available in some countries, but we require national-level forecasts.
* **Time unit:** Source data are reported daily, but we require [weekly](#Date-format) forecasts.
* **Counts:** JHU data are cumulative, but we require a forecast of the new (incident) count over the time horizon of each target. We derive incident data by taking weekly differences of the cumulative data.
* **Values:** JHU data may in some cases differ slightly from individual national datasets, and JHU data can be revised retrospectively. We still recommend using the data provided for forecasting so that we share a common dataset with which to compare across models.

#### Additional data sources
We do not use or evaluate against these data, but the following might be useful for modelling targets:

Data | Description | Source | Link
--- | --- | --- | ---
Vaccination | Number of vaccine doses distributed by manufacturers, number of first, second and unspecified doses administered | ECDC | [Data on COVID-19 vaccination in the EU/EEA](https://www.ecdc.europa.eu/en/publications-data/data-covid-19-vaccination-eu-eea)
Variants of concern | Volume of COVID-19 sequencing, the number and percentage distribution of VOC for each country, week and variant submitted since 2020-W40  | ECDC | [Data on SARS-CoV-2 variants in the EU/EEA](https://www.ecdc.europa.eu/en/publications-data/data-virus-variants-covid-19-eueea)
Testing |  Weekly testing rate and weekly test positivity | ECDC | [Data on testing for COVID-19 by week and country](https://www.ecdc.europa.eu/en/publications-data/covid-19-testing)

## Horizon and frequency
#### Horizon
For forecasts, we focus on horizons of between 1 and 4 weeks ahead. 
Teams can submit forecasts for any combination of horizons up to 20 weeks ahead but caution that teams should only submit forecasts for horizons that they are happy to be compared to truth data, i.e taken as true predictions. 
In addition to future data, teams can submit their estimates of the final (4 weeks after the date) value of past truth data.
This reflects the fact that data may be revised in the future.
Corresponding horizons are indicated by a zero or negative values (e.g. "-1 wk ahead" for the data one week before the forecast date).

Ideally we would like teams to provide values both for past weeks (where revisions are to be expected) and future weeks up to 4 weeks ahead.

##### Date format
Forecast horizons should use the Epidemiological Week (EW) format, defined by the [US CDC](https://ndc.services.cdc.gov/wp-content/uploads/MMWR_Week_overview.pdf). Each week starts on Sunday and ends on Saturday.  For example:
* A **1 week ahead** hospitalisation forecast submitted on Monday 6th March 2023 should cover the seven days including Sunday 5th March to Saturday 11th March. In this example, the forecast file would include:
  - `forecast_date = "2023-03-06"`
  - `target = "1 wk ahead inc hosp"`
  - `target_end_date = "2023-03-11"`
* A **4 week ahead** hospitalisation forecast submitted on Monday 6th March 2023 would include the period Sunday 26th March to Saturday 1st April 2023. In this example:
  - `forecast_date = "2023-03-06"`
  - `target = "4 wk ahead inc hosp"`
  - `target_end_date = "2023-04-01"`
* A **0 week past** hospitalisation nowcast submitted on Monday 6th March 2023 would include the period Sunday 26th February to Saturday 5th March 2023. In this example:
  - `forecast_date = "2023-03-06"`
  - `target = "0 wk ahead inc hosp"`
  - `target_end_date = "2023-03-05"`
* A **2 week past** hospitalisation nowcast submitted on Monday 6th March 2023 would include the period Sunday 12th February to Saturday 18th February 2023. In this example:
  - `forecast_date = "2023-03-06"`
  - `target = "-2 wk ahead inc hosp"`
  - `target_end_date = "2023-02-18"`

Note that weeks start on a Sunday, but we require submission by the Monday evening of that week.

Date conversion helpers include:
* Packages in R: [lubridate](https://lubridate.tidyverse.org/reference/week.html), [MMWRweek](https://cran.r-project.org/web/packages/MMWRweek/)
* Packages in Python: [pymmwr](https://pypi.org/project/pymmwr/), [epiweeks](https://pypi.org/project/epiweeks/)
* We provide a [csv template](https://github.com/epiforecasts/covid19-forecast-hub-europe/tree/main/template/forecast-dates.csv) with the start and end dates for one-week-ahead forecasts at the respective forecast dates (which we assume to be Mondays, in line with the weekly submission deadlines)

#### Frequency
Forecasts should be submitted once per week only.
* Submission can be at any time/day of the week.
* We recommend submitting on Monday: if the forecast date is on a Saturday, Sunday or Monday then the “1 week ahead forecast” is for the week ending the Saturday following. If the forecast date is any other day of the week, then the “1 week ahead forecast” is for the week ending the second Saturday following. For example, for a forecast made on 30 July, 31 July, 1 August or 2 August, the “1 week ahead forecast” is for the week ending 7 August, and for a forecast date of 3-9 August the “1 week ahead forecast” is for the week ending 14 August. Whilst submitting on a weekday other than Monday therefore puts teams at a disadvantage in terms of the information available, we do accept forecasts on any other dates, and we will monitor whether the submission date makes any difference in the quality of forecasts.

## Location
You can submit a forecast for a single country, or any combination of the target countries ([EU](https://en.wikipedia.org/wiki/Member_state_of_the_European_Union), [EFTA](https://en.wikipedia.org/wiki/European_Free_Trade_Association) and the UK). We use [ISO-2](../wiki/Forecast-format#location) codes to identify countries.

Currently we do not accept sub-national forecasts. Sub-national country datasets can be incompatible with each over and over time, making comparisons between forecasts unclear.
