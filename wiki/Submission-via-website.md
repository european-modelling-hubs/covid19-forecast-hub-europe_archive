*The following is an adapted version of [materials](https://github.com/KITmetricslab/covid19-forecast-hub-de/wiki) provided by the Germany/Poland Forecast Hub under the MIT license*

As an external contributor you cannot upload files directly. Instead, you need to create a fork and submit your files via a pull request. This will also trigger our validation scripts to check the data format.

Here we guide you through the process of submitting forecasts using the GitHub website (if you are familiar with GitHub you may prefer to submit by using git in the command line, see [here](./Submission-via-command-line)). We assume that you already have your forecasts in the required [submission format](Forecast-format).

If you've already commited your submission folder and want to add a new forecast, see [Subsequent Submissions](#Subsequent-Submissions).

##### Fork the repository
1. Go to https://github.com/epiforecasts/covid19-forecast-hub-europe and click on `Fork` in the top right corner:

![fork](https://github.com/kathsherratt/covid19-forecast-hub-europe/raw/pull-request-demo/pull-request-demo/fork.png)

This will create your personal copy of the repository. You can always come back to your fork by clicking on the `Fork` button.

##### Commit first submission to your fork

2. In your fork navigate to the folder `data-processed/`. This is where all forecasts are stored.
3. Click on "Upload files"
![upload-files](https://github.com/kathsherratt/covid19-forecast-hub-europe/raw/pull-request-demo/pull-request-demo/upload-files.png)

4. Drag and drop your submission folder:

![drag-and-drop](https://github.com/kathsherratt/covid19-forecast-hub-europe/raw/pull-request-demo/pull-request-demo/drag-and-drop.png)

_This may look like the files are uploaded seperately, but it will actually create the folder._

5. Give the commit a meaningful name, select `commit directly to the master branch` and click on `Commit changes` (Note: this will commit to your fork).

[[images/pull-request-demo/commit.png]]

#### Create pull request
6. Now that your submission is uploaded to your fork, the next step is to open a pull request to _pull_ your submission to the main repository. In your fork click on `New pull request`:
![pr1](https://github.com/kathsherratt/covid19-forecast-hub-europe/raw/pull-request-demo/pull-request-demo/pull-request-1.png)

7. Make sure the `base repository` is the main repository (Epiforecasts) and the `head repository` is your fork (_instead of kathsherratt it should be your username_) and then click on `Create pull request`.
![pr2](https://github.com/kathsherratt/covid19-forecast-hub-europe/blob/pull-request-demo/pull-request-demo/pull-request-2.png)

8. Enter a title as your model name and forecast date, and click on `Create pull request`.
![pr3](https://github.com/kathsherratt/covid19-forecast-hub-europe/blob/pull-request-demo/pull-request-demo/pull-request-3.png)

#### Wait for validation and merge (by admins)
That's it - now our validation scripts will check the data format, this may take a while.
[[images/pull-request-demo/pr_check.png]]

When it has completed successfully, your submission will be merged to the main repository by one of our admins, with the additional manual check that the `forecast_date` is either the date the pull request was submitted or the previous date. Any exceptions to this rule should be justified and documented with a comment on the pull request.

You can also find your pull request [here](https://github.com/epiforecasts/covid19-forecast-hub-europe/pulls). If you run into any problems, please refer to our [troubleshooting](./Troubleshooting-Pull-Requests) or [get in touch](epiforecasts/covid19-forecast-hub-europe/issues)!


# Subsequent Submissions
If you've already created your submission folder and want to add a new forecast, do the following:

2b. In your fork navigate to your submission folder, for example `data-processed/Template-ExampleModel`.

3b. Click on "Upload files".

4b. Drag and drop your newest forecast file.

Afterwards continue from step 5 until the end.
