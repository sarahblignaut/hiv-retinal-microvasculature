# Retinal microvasculature, HIV, ART and cardiovascular risk

Analysis code from my BSc Honours project in Bioinformatics and Computational
Biology at Stellenbosch University (2024; degree awarded cum laude). Thesis
title: *Exploring the association between retinal microvascular blood vessels
and human immunodeficiency virus, antiretroviral therapy and cardiovascular
disease risk factors.*

## Research question

Are retinal microvascular measurements associated with HIV infection,
antiretroviral therapy (ART) and cardiovascular disease (CVD) risk factors in
adults from the Western Cape, South Africa?

## Data

Cross-sectional data from 283 adults in the EndoAfrica study (Strijdom et al.,
2017), recruited at community health centres and HIV clinics in Worcester and
Cape Town. Participants were HIV-negative, or HIV-positive and either on ART or
ART-naive. Fundus images were taken with a Canon CR-2 non-mydriatic camera and
graded by a trained grader in IFLEXIS software (VITO, Belgium), which gives
retinal vessel measures such as vessel calibre (CRAE, CRVE), fractal
dimension, branching and tortuosity.

**The data are not included in this repository.** They are confidential
participant data collected under ethics approval, access is managed by the
EndoAfrica study team, and the study team has not yet published them.

## Methods

All analyses are in one Quarto document, `analysis.qmd`. The thesis analysis
was run in R 4.4.0.

- Descriptive statistics for the whole sample and by HIV and ART status
- Welch t-tests comparing clinical and retinal variables between groups
- Pearson correlations between clinical and retinal variables, shown as heatmaps
- Z-score standardisation of retinal measures, with hierarchical clustering
  heatmaps (ComplexHeatmap; Euclidean distance, complete linkage)
- Principal component analysis with base R `prcomp()`
- Multiple linear regression, one model per retinal measure, adjusted for age,
  sex, BMI, smoking and self-reported CVD risk factors
- Exploratory random forest and decision tree models, which were not part of
  the final report

Significance was set at p < 0.05, with no correction for multiple testing.

## Main findings

Some retinal measures differed between groups in unadjusted tests, but after
adjusting for age, sex, BMI, smoking and CVD risk factors, HIV and ART status
explained little of the variation in retinal measures (adjusted R² below 0.2).
PCA and hierarchical clustering showed no clear separation between the groups.
Preliminary analyses suggested possible links between retinal measures and ART
duration, viral load and CD4 count.

Limitations include the cross-sectional design, self-reported CVD risk
factors, a small ART-naive group and the lack of correction for multiple
testing.

## Running the code

The code runs only with access to the study data.

**Requirements:** R and [Quarto](https://quarto.org). Install the packages
with:

```r
install.packages(c(
  "broom", "caret", "circlize", "cowplot", "dplyr", "DT", "ggplot2",
  "janitor", "kableExtra", "lubridate", "purrr", "randomForest", "readr",
  "readxl", "rpart", "rpart.plot", "stringi", "stringr", "tibble", "tidyr"
))

install.packages("BiocManager")
BiocManager::install(c("ComplexHeatmap", "PCAtools"))
```

<!-- Package versions: paste the output of the version check here. -->

**Data files** (not included), placed in a `data/` folder:

- `data/endoafrica_retinal_data.xlsx`: the study spreadsheet
- `data/variable_names_edited.txt`: a tab-delimited mapping from raw to clean
  column names, edited by hand from `data/variable_names_raw.csv`, which the
  document writes

**Render** from the project folder:

```sh
quarto render analysis.qmd
```

Rendering also writes figure files (`.svg`, `.png`) to the project folder.
These are generated from participant data, so `.gitignore` keeps them out of
the repository.

## Repository contents

| File | Description |
|------|-------------|
| `analysis.qmd` | Quarto document with all analysis code (R) |
| `README.md` | This file |
| `LICENSE` | MIT License |
| `.gitignore` | Keeps data, rendered output and generated figures out of the repository |

## Acknowledgments

Supervised by Dr Elizna Maasdorp, Prof. Hans Strijdom and Dr Michelle Parker.

Data come from the EndoAfrica study, with ethics approval from the
Stellenbosch University Health Research Ethics Committee (N13/05/064 and
S16/07/114).

Strijdom H, De Boever P, Walzl G, et al. (2017). Cardiovascular risk and
endothelial function in people living with HIV/AIDS: design of the
multi-site, longitudinal EndoAfrica study in the Western Cape Province of
South Africa. *BMC Infectious Diseases*, 17(1), 41.

## License

The code is released under the MIT License (see `LICENSE`). No data are
included, and the license does not cover the study data.

## Contact

Sarah Blignaut, [github.com/sarahblignaut](https://github.com/sarahblignaut)
