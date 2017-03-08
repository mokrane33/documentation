---
name: Static Image Export
permalink: r/static-image-export/
description: How to export plotly graphs as static images in R. Plotly supports png, svg, jpg, and pdf image export.
layout: user-guide
thumbnail: thumbnail/png-export.png
language: r
page_type: example_index
has_thumbnail: true
order: 3
display_as: file_settings
sitemap: false
output:
  html_document:
    keep_md: true
---



### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.


```r
library(plotly)
packageVersion('plotly')
```

```
## [1] '4.5.6.9000'
```

### Export Locally

Recent versions of the R package include an `export()` function, which does image export locally, but requires the webshot package:


```r
if (!require("webshot")) install.packages("webshot")
tmpFile <- tempfile(fileext = ".png")
export(plot_ly(), file = tmpFile)
browseURL(tmpFile)
```

### Export Using Your Plotly Account

Another option is to do image export through your plotly account.

First, you will require the development version of plotly, this can be installed using `devtools::install_github("ropensci/plotly")`. In addition, if you haven't already, let the R package know about your credentials.



```r
Sys.setenv("plotly_username" = "YOUR USER NAME")
Sys.setenv("plotly_api_key" = "YOUR API KEY")
```

This option will export the image on plotly's servers and write the content to a local file `"output.png"` in your working directory.


```r
library(plotly)
p <- plot_ly(x = c(1,2,3,4), y = c(2,4,1,3), type = 'scatter', mode = 'lines')
plotly_IMAGE(p, format = "png", out_file = "output.png")
```

![](https://images.plot.ly/plotly-documentation/images/output.png)

### Appending File Type to URL

You can also view the static version of any Plotly graph by appending `.png`,
`.pdf`, `.eps`, or `.svg` to the end of the URL. For example, view the static image of <https://plot.ly/~chris/1638> at <https://plot.ly/~chris/1638.png>. See [Using Plotly with rmarkdown/knitr](https://plot.ly/r/knitr/) for a way to embed these links in rmarkdown/knitr (Rmd) files.