# Ensembling

Each week the hub combines the valid submitted forecasts into an ensemble forecast, published as the `EuroCOVIDhub-ensemble` model in [`data-processed`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/tree/main/data-processed/EuroCOVIDhub-ensemble). Ensembling and evaluation both rely on the [`EuroForecastHub`](https://github.com/epiforecasts/EuroForecastHub) R package. The code lives in [`code/ensemble`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/tree/main/code/ensemble).

### Inclusion criteria

The ensemble combines forecasts by target variable, location, horizon and quantile. For a model's forecast to be included for a given location and target it must:

- provide the full set of 23 predictive quantiles;
- cover the full one- to four-week-ahead horizon;
- not be flagged for manual exclusion (for example, late submissions).

Manual exclusions are listed by forecast date in [`manual-exclusions.csv`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/code/ensemble/EuroCOVIDhub/manual-exclusions.csv), with a reason recorded for each. A location/target combination is only ensembled if at least three models meet the criteria (`min_nmodels = 3`). The set of models actually used each week is recorded in the [`criteria`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/tree/main/code/ensemble/EuroCOVIDhub/criteria) folder.

### Ensembling methods

The published ensemble is an **unweighted quantile average**. The method (`mean` or `median`) is read from the hub configuration (`ensemble.method` in [`project-config.json`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/project-config.json)) when the ensemble runs. The hub began with the mean ensemble and later switched to the median; `method-by-date.csv` records which method applies on which date.

Both methods are implemented in the `EuroForecastHub` package:

| Type | Method | Function |
|---|---|---|
| Unweighted | Mean | [`create_ensemble_average(method = "mean")`](https://github.com/epiforecasts/EuroForecastHub/blob/main/R/create_ensemble_average.R) |
| Unweighted | Median | [`create_ensemble_average(method = "median")`](https://github.com/epiforecasts/EuroForecastHub/blob/main/R/create_ensemble_average.R) |

Other methods, some of them experimental, are run retrospectively across all past forecast dates by [`create-all-methods-ensembles.R`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/code/ensemble/utils/create-all-methods-ensembles.R), with outputs stored under [`ensembles/data-processed`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/tree/main/ensembles). We keep reviewing these against the default and switch only when one of them consistently does better.

### Ensemble outputs

The weekly ensemble is produced by [`create-weekly-ensemble.R`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/code/ensemble/EuroCOVIDhub/create-weekly-ensemble.R), run automatically by the [`ensemble.yml`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/.github/workflows/ensemble.yml) GitHub Action (twice a week, on the day after submission). Each run:

- saves the published ensemble to [`data-processed/EuroCOVIDhub-ensemble`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/tree/main/data-processed/EuroCOVIDhub-ensemble), formatted to the standard [submission format](Submission-format) and tagged with the number of models contributing to each forecast;
- saves an unfiltered version (`min_nmodels = 0`) as `EuroCOVIDhub-ensemble_all` under [`ensembles/data-processed`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/tree/main/ensembles);
- writes the inclusion criteria for that week to the `criteria` folder and appends the method used to `method-by-date.csv`.

Missed weeks can be regenerated with [`manual-weekly-ensemble.R`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/code/ensemble/EuroCOVIDhub/manual-weekly-ensemble.R) via the [`manual-ensemble.yml`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/.github/workflows/manual-ensemble.yml) workflow, which loops over a supplied list of dates.

# Evaluation

Submitted forecasts and the ensemble are scored each week against observed data. The code lives in [`code/evaluation`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/tree/main/code/evaluation) and uses the [`scoringutils`](https://github.com/epiforecasts/scoringutils) and [`covidHubUtils`](https://github.com/reichlab/covidHubUtils) packages.

### Evaluation methods

Scoring proceeds in two stages, both driven weekly by the [`scoring.yml`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/.github/workflows/scoring.yml) GitHub Action:

1. **Score each forecast** — [`score_models.r`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/code/evaluation/score_models.r) (using [`load_and_score_models.r`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/code/evaluation/load_and_score_models.r)) loads all local forecasts and the weekly truth data, matches each forecast to the eventual observation, and scores it. Before scoring, known data [anomalies](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/data-truth/anomalies/anomalies.csv) are removed from the truth data, and forecasts made in the week immediately following an anomaly are dropped. Only truth data with `final` status is used.

2. **Aggregate scores** — [`aggregate_scores.r`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/code/evaluation/aggregate_scores.r) summarises the raw scores by model over rolling windows of history (10 and 52 weeks by default). It keeps only the forecast targets that the baseline (`EuroCOVIDhub-baseline`) also covers, so every model is compared against the baseline on the same set of targets. By default only models with forecasts in the most recent four weeks are ranked.

The main metric is the **[Weighted Interval Score](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1008618)** (WIS), reported alongside its `sharpness`, `underprediction` and `overprediction` components. Additional metrics include the absolute error of the median (`ae_median`), [bias](https://doi.org/10.1371/journal.pcbi.1006785), interval coverage at the 50% and 95% levels (`cov_50`/`cov_95`), and the number of quantiles supplied (`n_quantiles`). Model performance is reported **relative to the baseline** — a flat projection with expanding uncertainty over time.

### Evaluation outputs

- **[`evaluation/scores.csv`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/evaluation/scores.csv)** — raw per-forecast scores (one row per model, target variable, forecast date, target end date, horizon and location), with columns `wis`, `sharpness`, `underprediction`, `overprediction`, `ae_median`, `bias`, `cov_50`, `cov_95` and `n_quantiles`.
- **[`evaluation/weekly-summary`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/tree/main/evaluation/weekly-summary)** — one aggregated `evaluation-<date>.csv` per week, feeding the [weekly performance reports](https://covid19forecasthub.eu/reports.html).
- **[`evaluation/README`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/blob/main/evaluation/README.md)** — an auto-rendered summary of ensemble performance, including the number of models in the ensemble over time, 50% and 95% coverage, and relative WIS and absolute error over the preceding 10 weeks.

These scores also feed the per-model and per-country reports ([`code/reports`](https://github.com/european-modelling-hubs/covid19-forecast-hub-europe_archive/tree/main/code/reports)) published on the [hub website](https://covid19forecasthub.eu/).
