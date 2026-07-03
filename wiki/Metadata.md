Each model is required to have metadata stored in a text file. Please read the instructions here carefully before preparing the first submission, as this will fail if the Metadata is not supplied, or not supplied in the right format.

The text file should be named `team-model.yml` and saved in the [`model-metadata/` directory](https://github.com/covid19-forecast-hub-europe/covid19-forecast-hub-europe/tree/main/model-metadata).

This should be written in [yaml format](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html) (i.e. `key: value`), copying the below structure. This file describes each of the variables (keys) in the yaml document. Please order the variables in this order. You can consult an [example metadata file](https://github.com/epiforecasts/covid19-forecast-hub-europe/blob/main/data-processed/EuroCOVIDhub-ensemble/metadata-EuroCOVIDhub-ensemble.txt) for further guidance. Each line should contain one `key: value` pair.

Upon first submission, a series of checks will be run on the Metadata file, and an error thrown if any of the checks fails - a common problem, for example, is that the text contains a colon (`:`) - if that is the case, best to put quotation marks (`"`) around the entry. If you are having trouble getting the metadata to pass the checks, please do not hesitate to get in touch with us. For future submission, the file only needs to be change if there is a change to the model (e.g., additional input data is being used).

## Required variables

### team_name
The name of your team that is less than 50 characters.

### model_name
The name of your model that is less than 50 characters.

### model_abbr
This is for uniquely identifying your team and model in our system, and should be the name of your sub-directory in `data-processed`.

This should be a short name for your team and model that is less than 30 alphanumeric characters. This must be in the format of `[team]-[model]`, where each of `[team]` and `[model]` are text strings that are less than 15 alphanumeric characters that do not include a hyphen or whitespace. An example of a valid team-model name is `UMass-MechBayes` or `UCLA-SuEIR`.

### model_contributors

A list of all individuals involved in the forecasting effort and their affiliations. At least one contributor needs to have a valid email address. All email addresses provided will be added to an email distribution list for model contributors.

The syntax of this field should be

```
model_contributors:
  - name: Contributor 1
    affiliation: Affiliation 1
    email: user1@example.com
  - name: Contributor 2
    affiliation: Affiliation 2
    email: user2@example.com
```

For each contributor, you can also add the optional `twitter` and `orcid` fields.

### website_url

A url to a website that has additional data about your model.
We encourage teams to submit the most user-friendly version of your
model, e.g. a dashboard, or similar, that displays your model forecasts.

If you only have a more technical site, e.g. github repo, please include that link here.


### license

One of [licenses]([https://github.com/epiforecasts/covid19-forecast-hub-europe/wiki/Licensing). If the value is "other", then a LICENSE.txt file must exist within the `data-processed/team-model` folder and provide a license.

We encourage teams to submit as a "cc-by-4.0" to allow the broadest possible uses including private vaccine production (which would be excluded by the "cc-by-nc-4.0" license).

### team_model_designation

Upon initial submission this field should be one of “primary”, “proposed” or “other”. For teams submitting only one model, this should be “primary”. For each team, only one model can be designated as “primary”.

* *Primary* means the model will be scored in evaluations, eligible for inclusion in the ensemble, and visualized.

* *Proposed* means the team would like the model to be considered as a "secondary" model rather than an "other" model.
  * The Hub team will determine whether the model's methodology is distinct enough that the model should be included in the ensemble, in which case the model will get the "secondary" designation.
  * If the methodology is not distinct enough, e.g. it differs from the primary model by setting certain parameters to specific values, then the model will be designated as "other".

* *Secondary* means the forecasts will be visualized and eligible for inclusion in the ensemble and scoring in evaluations.

* *Other* means the forecasts will not be visualized or included in the ensemble, but still scored in evaluations.


### methods

A brief description of your forecasting methodology that is less than 200
characters.


## Optional

### team_funding

Like an acknowledgement in a manuscript, you can acknowledge funding here.

### repo_url

A github (or similar) repository url.

### data_inputs

A description of the data sources used to inform the model and the truth data targeted by model forecasts. For example, sources might include hospitalisation data, behavioural data such as [Google mobility](https://www.google.com/covid19/mobility/) etc., and we usually expect target data to include [JHU data](https://github.com/epiforecasts/covid19-forecast-hub-europe/wiki/Targets-and-horizons#truth-data).

An example description could be:

> cases forecasts use hospitalisation data provided by the Ministry of Health at the national level, Google mobility data and target JHU data

### citation

A url (doi link preferred) to an extended description of your model,
e.g. blog post, website, preprint, or peer-reviewed manuscript.

### methods_long

An extended description of the methods used in the model.

If the model is modified, this field can be used to provide:
* date of modification
* description of the change

***

**Note**: When you upload the model meta-data file, ECDC will collect the personal data that you provide (your name and email) and include this data in an email distributor and a Discussion forum, as a mean of communication between ECDC and you. You can unsubscribe at any time, and ECDC will then delete your personal data.
