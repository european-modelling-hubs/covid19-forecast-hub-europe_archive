Each team stores their forecasts in a separate folder within the `data-processed` folder of this repository.

Before submitting your first forecast, please create and name your own folder in the format:

**`team-model`**

Where:

* `team` is the team name
* `model` is the name of your model

Both `team` and `model` should be less than 15 characters and not include hyphens. If submitting multiple models, please create a `team-model` folder for each.

### Metadata

Participating teams must provide a [metadata file](Metadata), including some information about the team and methods. The metadata file should be placed in the [`model-metadata/` folder](https://github.com/covid19-forecast-hub-europe/covid19-forecast-hub-europe/tree/main/model-metadata) and named similarly to your sub-directory:

`team-model.yml`

### Forecasts

The `team-model` directory is where you will store and submit all your forecasts. When you have prepared a forecast in the  [given format](Forecast-format), please submit files via a pull request. This will also trigger our validation scripts to check the data format. We provide a [step-by-step explanation](Submission-via-website) on how to do this, using only the user interface of the GitHub website and a [shorter explanation](Submission-via-command-line) for more experienced GitHub users.
