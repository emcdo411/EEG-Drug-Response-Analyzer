# EEG-Drug-Response-Analyzer

A Shiny application for analyzing electroencephalography (EEG) data to predict drug response, leveraging advanced signal processing, machine learning, and interactive visualizations.

[![R](https://img.shields.io/badge/R-4.4.3-blue)](https://www.r-project.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](https://opensource.org/licenses/MIT)
[![Deployed](https://img.shields.io/badge/Deployed-Shinyapps.io-blue)](https://shinyapps.io/)

## Table of Contents

* [Summary](#summary)
* [Tech Stack](#tech-stack)
* [Installation](#installation)
* [Application Overview](#application-overview)
* [Why This Matters](#why-this-matters)
* [Conclusion](#conclusion)

## Summary

The `EEG-Drug-Response-Analyzer` is a robust, interactive Shiny application designed for data engineers and neuroscientists to analyze EEG data for drug response prediction. It supports both simulated and real EEG data in EDF format, integrating signal processing, feature extraction, clustering, and machine learning to deliver actionable insights. Key features include:

* **Data Input**: Upload EEG (`.edf`) and clinical (`.csv`) files or use simulated data.
* **Signal Processing**: Apply bandpass filtering (1–40 Hz), ICA cleaning, and extract power in alpha (8–12 Hz) and theta (4–8 Hz) bands.
* **Machine Learning**: Train `randomForest` models with 80/20 splits, achieving up to \~80% accuracy.
* **Clustering**: Use k-means clustering (2–5 clusters) on power features to find neural subgroups.
* **Visualization**: Interactive Plotly charts, spectrograms, and DT-powered tables.
* **Reporting**: Generate downloadable HTML reports via `rmarkdown`.
* **Debugging**: Built-in logs for EEG dimensions, power ranges, and clustering diagnostics.

## Tech Stack

### Core Language

* **R** 4.4.3

### Web Framework

* **[shiny](https://CRAN.R-project.org/package=shiny)**
* **[shinydashboard](https://CRAN.R-project.org/package=shinydashboard)**

### Visualization

* **[plotly](https://CRAN.R-project.org/package=plotly)**
* **[DT](https://CRAN.R-project.org/package=DT)**

### Signal Processing

* **[signal](https://CRAN.R-project.org/package=signal)**
* **[edfReader](https://CRAN.R-project.org/package=edfReader)**
* **[ica](https://CRAN.R-project.org/package=ica)**
* **[seewave](https://CRAN.R-project.org/package=seewave)**
* **[matrixStats](https://CRAN.R-project.org/package=matrixStats)**

### Machine Learning

* **[randomForest](https://CRAN.R-project.org/package=randomForest)**

### Reporting

* **[rmarkdown](https://CRAN.R-project.org/package=rmarkdown)**
* **[knitr](https://CRAN.R-project.org/package=knitr)**
* **[yaml](https://CRAN.R-project.org/package=yaml)**
* **[htmltools](https://CRAN.R-project.org/package=htmltools)**

### Deployment

* **Shinyapps.io**
* **[rsconnect](https://CRAN.R-project.org/package=rsconnect)** (for deployment)

## Installation

### Prerequisites

* R 4.4.3+
* RStudio (recommended)
* Pandoc (included with RStudio)

### Local Setup

```bash
# Clone the repo
git clone https://github.com/your-username/EEG-Drug-Response-Analyzer.git
cd EEG-Drug-Response-Analyzer

# Install dependencies
install.packages("renv")
renv::restore()

# Or manually:
install.packages(c("shinydashboard", "shiny", "plotly", "signal", "randomForest",
  "edfReader", "ica", "knitr", "rmarkdown", "seewave", "matrixStats",
  "DT", "yaml", "htmltools"))

# Launch the app
shiny::runApp()
```

Visit: [http://localhost](http://localhost):<port>

### Shinyapps.io Deployment

```r
install.packages("rsconnect")
library(rsconnect)
setAccountInfo(name = "your-name", token = "your-token", secret = "your-secret")
deployApp(appDir = ".", appName = "EEGDrugResponseAnalyzer", forceUpdate = TRUE)
```

Access the app: [https://your-name.shinyapps.io/EEGDrugResponseAnalyzer/](https://your-name.shinyapps.io/EEGDrugResponseAnalyzer/)

## Application Overview

### Data Ingestion

* Upload `.edf` EEG files and `.csv` clinical data.
* Simulates 64 channels × 4096 samples @ 256 Hz if no file is uploaded.

### Signal Processing

* Bandpass filter (1–40 Hz), ICA clean, mean-centering.
* Extract Alpha and Theta band power (0.0625 Hz resolution).

### Machine Learning

* Random forest binary classification.
* Accuracy displayed; model uses 100 trees, 80/20 data split.

### Clustering

* K-means (2–5 clusters) on power features.
* Cluster assignments visualized via scatterplots.

### Visualizations

* Plotly histograms, cluster plots, spectrogram heatmaps.
* Debug tab logs: channel count, unique power, freq resolution.

### Reporting

* HTML download with: summary stats, plots, power table, accuracy.

## Why This Matters

### Clinical Relevance

Predict EEG-based likelihood of drug response for depression, PTSD, and other CNS disorders.

### Engineering Value

Modular, reproducible codebase; `renv` ensures consistent environments.

### Reusability

Supports extensions for:

* Additional frequency bands (Delta, Beta)
* Deep learning pipelines
* Real-time EEG streaming

## Conclusion

`EEG-Drug-Response-Analyzer` is a production-grade application merging EEG biomarker discovery with predictive modeling and clean UX. Built for precision psychiatry, and adaptable to any team needing EEG-based analytics at scale.

To contribute, fork the repo and submit a PR. Built with R 4.4.3, licensed under MIT.
