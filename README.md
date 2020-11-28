
<!-- README.md is generated from README.Rmd. Please edit that file -->

# tobalcepi <img src="tools/tobalcepi_hex.png" align="right" style="padding-left:10px;background-color:white;" width="100" height="100" />

<!-- badges: start -->

[![Lifecycle:
maturing](https://img.shields.io/badge/lifecycle-maturing-blue.svg)](https://www.tidyverse.org/lifecycle/#maturing)
[![Project Status: Active – The project has reached a stable, usable
state and is being actively
developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)  
<!-- badges: end -->

## Motivation

The motivation for `tobalcepi` was to organise how we store, process and
use the information on the risks of disease that stem from tobacco
and/or alcohol consumption, including to provide functions to easily use
these risk estimates in modelling.

`tobalcepi` was created as part of a programme of work on the health
economics of tobacco and alcohol at the School of Health and Related
Research (ScHARR), The University of Sheffield. This programme is based
around the development of the Sheffield Tobacco and Alcohol Policy
Modelling (STAPM), which aims to use comparable methodologies to
evaluate the impacts of tobacco and alcohol policies, and investigate
the consequences of clustering and interactions between tobacco and
alcohol consumption behaviours.

## Relative risk data

The disease lists and risk functions in this package all have published
sources, which we have referenced. We store the master files for our
tobacco and alcohol disease lists and risk functions sources in the
University of Sheffield folder
`X:/ScHARR/PR_Disease_Risk_TA/Code/tables`. In order to obtain
mathematical descriptions of the risk functions for use in modelling, we
needed to contact some authors to ask for additional information.

### Alcohol

The high-level function for alcohol is `tobalcepi::RRalc()`, which
calculates individual risks of diseases as follows:

1.  **Alcohol - partially-attributable chronic conditions**:
    dose-response effects of current alcohol consumption on disease risk
    (Angus et al. [2018](#ref-Angus2018)) are hard-coded into the
    function `tobalcepi::RRalc()`. Updates to these risk functions must
    therefore be made by changing the function code.  
2.  **Alcohol - partially-attributable acute conditions**: dose-response
    effects of single-occasion alcohol consumption are hard coded into
    the function `tobalcepi::PArisk()`, which is called by
    `tobalcepi::RRalc()`. See
    [vignette(“alc\_pa\_risk”)](https://stapm.gitlab.io/r-packages/tobalcepi/articles/alc_partially_attrib_acute.html).  
3.  **Alcohol - wholly-attributable acute conditions**: these are not
    based on published risk functions but are based on thresholds, in UK
    standard units of alcohol drunk on a single occasion, over which
    individuals begin to experience an elevated risk for acute diseases
    that are wholly attributable to alcohol. This is applied by the
    function `tobalcepi::WArisk_acute()`, which is called by
    `tobalcepi::RRalc()`. See
    [vignette(“alc\_wa\_ac\_risk”)](https://stapm.gitlab.io/r-packages/tobalcepi/articles/alc_wholly_attrib_acute.html).  
4.  **Alcohol - wholly-attributable chronic conditions**: these are also
    based on thresholds in UK standard units of alcohol drunk on average
    in a week, over which individuals begin to experience an elevated
    risk for chronic diseases that are wholly attributable to alcohol.
    This is applied by code within the function `tobalcepi::RRalc()`.
    See
    [vignette(“alc\_wa\_ch\_risk”)](https://stapm.gitlab.io/r-packages/tobalcepi/articles/alc_wholly_attrib_chronic.html).

### Tobacco

See
[vignette(“smoke\_risks”)](https://stapm.gitlab.io/r-packages/tobalcepi/articles/smoking-disease-risks.html)

1.  `RRtob()` takes a lookup table of the risks associated with current
    vs. never smoking and assigns these to individuals based on their
    smoking state, age and sex (Webster et al.
    [2018](#ref-webster2018risk)).  
2.  We are in the process of developing the function `RRTobDR()` to
    stratify the risks of some cancers according to the amount smoked
    per day by current smokers. There is limited info on these
    dose-reponse effects, so we are gradually building up the
    epidemiological detail in this area as we review, critically
    appraise and integrate new risk data into our modelling.

### Lag times

Lag times are the information on the delay between a change to tobacco
or alcohol consumption and the decline in the risk of disease associated
with that consumption. The relevant functions are `tobalcepi::TobLags()`
(which uses lags stored in `tobalcepi::tobacco_lag_times`) and
`tobalcepi::AlcLags()` (which contains lags hard-coded into the
function).

### Tobacco - Alcohol risk interactions

We use estimates of potential tobacco - alcohol risk interactions for:

  - Oral cavity cancer  
  - Pharyngeal cancer  
  - Laryngeal cancer  
  - Oesophageal SCC cancer

These estimates are stored in `tobalcepi::tob_alc_risk_int`.

## Package data

Some useful, not risk-bearing, data is stored within the package and is
installed onto your computer when you download and load the package. We
use package data for data that is likely to be used across several
projects, that it is important to keep standardised across projects, and
is only likely to need updating after a long interval e.g. at least
annually.

The types of data included in tobalcepi are:

  - Lists of the names of the diseases that are related to tobacco
    and/or alcohol.  
  - Parameters used in the modelling of single occasion drinking.  
  - Tobacco relative risks of current vs. never smokers.
  - Tobacco lag times.  
  - Tobacco - alcohol risk interactions.

When these data need to be updated, the inputs and code in the package
folder `data-raw` will need to be changed, and the package rebuild with
a new version.

## Usage

`tobalcepi` is a package for predicting individual risk of disease due
to tobacco and alcohol consumption based on published sources, and
summarising that risk. The suite of functions within `tobalcepi`
processes the published data on the relative risks of disease that stem
from chronic and acute alcohol consumption, from smoking, and on the
decline in risk after ceasing or reducing consumption. The package also
includes functions to estimate population attributable fractions, and to
explore the interaction between the disease risks that stem from tobacco
and alcohol consumption.

The **inputs** are the published estimates of relative risk for each
disease (sometimes stratified by population subgroup).

The **processes** applied by the functions in `tobalcepi` give options
to estimate:

1.  The risk of injury or disease from acute alcohol consumption.  
2.  The risk of chronic disease based on the current amount of alcohol
    consumed.  
3.  The risk of chronic disease based on whether someone currently
    smokes, and how much they currently smoke.  
4.  The combined risk of disease in someone who smokes and drinks.  
5.  The change in risk of disease after someone ceases or reduces their
    consumption.  
6.  The population attributable fractions of disease to tobacco and/or
    alcohol (given suitable data on tobacco and alcohol consumption).

The **outputs** of these processes are datasets in which an individual’s
tobacco and/or alcohol consumption has been matched to their relative
risks of certain diseases, and aggregated datasets that summarise the
risks of disease within certain population subgroups.

## Installation

`tobalcepi` is currently available only to members of the project team
(but please contact Duncan Gillespie <duncan.gillespie@sheffield.ac.uk>
to discuss). To access you need to [**sign-up for a GitLab
account**](https://gitlab.com/). You will then need to be added to the
STAPM project team to gain access.

Once that is sorted, you can **install the development version** from
GitLab with:

``` r
#install.packages("devtools")
#install.packages("getPass")

devtools::install_git(
  "https://gitlab.com/stapm/r-packages/tobalcepi.git", 
  credentials = git2r::cred_user_pass("uname", getPass::getPass()),
  ref = "x.x.x",
  build_vignettes = TRUE
)

# Where uname is your Gitlab user name.
# ref = "x.x.x" is the version to install - remove this to install the latest version
# this should make a box pop up where you enter your GitLab password
```

Then load the package, and some other packages that are useful. Note
that the code within `tobalcepi` uses the `data.table::data.table()`
syntax.

``` r
# Load the package
library(tobalcepi)

# Other useful packages
library(dplyr) # for data manipulation and summary
library(magrittr) # for pipes
library(ggplot2) # for plotting
```

## Citation

Please cite the latest version of the package using:  
“Duncan Gillespie, Laura Webster, Maddy Henney, Colin Angus and Alan
Brennan (2020). tobalcepi: Risk Functions and Attributable Fractions for
Tobacco and Alcohol. R package version x.x.x.
<https://stapm.gitlab.io/r-packages/tobalcepi>”

## References

<div id="refs" class="references hanging-indent">

<div id="ref-Angus2018">

Angus, Colin, M Henney, L Webster, and Duncan Gillespie. 2018.
“Alcohol-Attributable Diseases and Dose-Response Curves for the
Sheffield Alcohol Policy Model Version 4.0.” The University of
Sheffield. <https://doi.org/10.15131/shef.data.6819689.v2>.

</div>

<div id="ref-webster2018risk">

Webster, Laura, Colin Angus, Alan Brennan, and Duncan Gillespie. 2018.
“Smoking and the Risks of Adult Diseases.” The University of
Sheffield. <https://doi.org/10.15131/shef.data.7411451.v1>.

</div>

</div>
