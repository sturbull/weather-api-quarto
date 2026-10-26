# weather-api-quarto

A Quarto (R) weather report for eight New Zealand centres. Each render pulls current conditions and a 7-day forecast from the [Open-Meteo forecast API](https://open-meteo.com/en/docs), which needs no API key. Charts use [echarts4r](https://echarts4r.john-coene.com/) and tables use [gt](https://gt.rstudio.com/).

## Render locally

```r
quarto::quarto_render("report.qmd")
```

Or from a terminal: `quarto render report.qmd`.

## Update the manifest

Posit Connect Cloud installs R packages from `manifest.json`. Regenerate it after adding or removing packages in `report.qmd`:

```r
rsconnect::writeManifest(appPrimaryDoc = "report.qmd", appFiles = c("report.qmd", "styles.scss", "logo.png"), quarto = TRUE)
```

## Publish on a schedule

1. Push this repo to GitHub.
2. In [Posit Connect Cloud](https://connect.posit.cloud/), choose **Publish**, pick Quarto, select this repo and branch, and set `report.qmd` as the primary file.
3. Once it has published, open the content's settings and add a schedule. Each scheduled run re-renders the report on Connect Cloud, so the page shows the forecast as of that run.

Scheduled republishing is only available on paid Connect Cloud plans. See the [announcement](https://docs.posit.co/connect-cloud/whats-new/posts/2025-10-02-schedule-content-republishing.html) for the schedule options.
