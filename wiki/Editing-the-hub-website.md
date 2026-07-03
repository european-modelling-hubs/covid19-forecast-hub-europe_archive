The hub website is an [rmarkdown website](https://bookdown.org/yihui/rmarkdown/rmarkdown-site.html) hosted at <https://www.github.com/covid19-forecast-hub-europe/covid19-forecast-hub-europe-website>.

In rmarkdown websites, each page is a Rmarkdown (`.Rmd`) document and the website navigation bar and global parameters are specified in `_site.yml`.

Once you commit and push a change in a `.Rmd` document or `_site.yml`, the changes will be automatically deployed after a couple of minutes.

# Editing a page

To edit a specific page, simply edit the related `.Rmd` file. For example, if you want to modify the ["Background" page](https://covid19forecasthub.eu/background.html), edit [`background.Rmd`](https://github.com/covid19-forecast-hub-europe/covid19-forecast-hub-europe-website/blob/f6615e50c32878babc129aaffb85e74945072553/background.Rmd).

Similarly, if you want to edit the disclaimer on the ["Visualisation" page](https://covid19forecasthub.eu/visualisation.html), edit [`visualisation.Rmd`](https://github.com/covid19-forecast-hub-europe/covid19-forecast-hub-europe-website/blob/f6615e50c32878babc129aaffb85e74945072553/visualisation.Rmd), and more specifically, [the text contained in between `<p id="limitation">...</p>`](
https://github.com/covid19-forecast-hub-europe/covid19-forecast-hub-europe-website/blob/f6615e50c32878babc129aaffb85e74945072553/visualisation.Rmd#L71-L73). 

# Removing a page

To unlist a page from the navigation bar, remove it from the `navbar` field in `_site.yml`, as demonstrated below (example to remove the ["Visualisation" page](https://covid19forecasthub.eu/visualisation.html)):

![image](https://user-images.githubusercontent.com/10783929/185575908-9d113504-c83e-499b-86ae-4d4373b49c50.png)

When unlisted, the page will typically not be visited because it's not linked from anywhere. However, users with direct links (and in some cases, search engines) can still access it directly. To remove the page entirely, remove the related `.Rmd` file (e.g., [`visualisation.Rmd`](https://github.com/covid19-forecast-hub-europe/covid19-forecast-hub-europe-website/blob/f6615e50c32878babc129aaffb85e74945072553/visualisation.Rmd) in the case of the ["Visualisation" page](https://covid19forecasthub.eu/visualisation.html).)

# Editing the reports

The forecast hub framework has an additional unusual complication: reports are generated from `.Rmd` location in the current GitHub repository, within the [`code/reports/` folder](https://github.com/covid19-forecast-hub-europe/covid19-forecast-hub-europe/tree/main/code/reports).
Reports are automatically rendered:
- [At 16:00 UTC on Sunday for country reports](https://github.com/covid19-forecast-hub-europe/covid19-forecast-hub-europe/blob/main/.github/workflows/reports-country.yml#L4-L5)
- [At 11:45 on Tuesday and Wednesday for model reports](https://github.com/covid19-forecast-hub-europe/covid19-forecast-hub-europe/blob/main/.github/workflows/reports-country.yml#L4-L5)

# Git flow

Whenever you try to edit the website, whether to modify or remove a page, or modify the reports, please do so by submitting a Pull Request and wait until all checks have passed (green check mark) to merge it. We have built in safeguards to ensure that you don't push changes in one place which break things in another place. 

![](https://user-images.githubusercontent.com/10783929/179529195-da881937-ba6c-422c-96a9-85b7d2366e10.png)