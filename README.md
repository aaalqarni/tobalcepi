
<!-- README.md is generated from README.Rmd. Please edit that file -->

# tobalcepi <img src="tools/tobalcepi_hex.png" align="right" style="padding-left:10px;background-color:white;" width="100" height="100" />

[![Project Status: Active – The project has reached a stable, usable
state and is being actively
developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)

The package is usable but there are still bugs and further developments
that are being worked through i.e. some code and documentation is still
incomplete or in need of being refined. The code and documentation are
still undergoing internal review by the analyst team.

## Motivation

`tobalcepi` was created as part of a programme of work on the health
economics of tobacco and alcohol at the School of Health and Related
Research (ScHARR), The University of Sheffield. This programme is based
around the construction of the Sheffield Tobacco and Alcohol Policy
Model (STAPM), which aims to use comparable methodologies to evaluate
the impacts of tobacco and alcohol policies, and investigate the
consequences of clustering and interactions between tobacco and alcohol
consumption behaviours.

The motivation for `tobalcepi` was to organise the information on the
relative risks of diseases related to tobacco and alcohol consumption
and to provide functions to easily work with these data in modelling.
The suite of functions within `tobalcepi` processes the published data
on disease risks that stem from chronic and acute alcohol consumption,
from smoking, and on the decline in risk after ceasing or reducing
consumption. The package also includes functions to estimate population
attributable fractions, and to explore the interaction between the
disease risks that stem from tobacco and alcohol consumption.

> The risk functions in this package are all collated from published
> sources, which we have referenced.

## Usage

`tobalcepi` is a package for predicting individual risk of disease due
to tobacco and alcohol consumption based on published sources, and
summarising that risk.

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

We would like to ask that since the code and documentation is still
under development and is complex, that you consult with the authors
before you use it.

Please cite the latest version of the package using:  
“Duncan Gillespie, Laura Webster, Maddy Henney, Colin Angus and Alan
Brennan (2020). tobalcepi: Risk Functions and Attributable Fractions for
Tobacco and Alcohol. R package version x.x.x.
<https://STAPM.github.io/tobalcepi/>. DOI:”

-----

Since you will be downloading and installing a source package, you might
need to set your system up for building R packages:

It is a good idea to update R and all of your packages.

**Mac OS**: A convenient way to get the tools needed for compilation is
to install Xcode Command Line Tools. Note that this is much smaller than
full Xcode. In a shell, enter xcode-select –install. For installing
almost anything else, consider using [Homebrew](https://brew.sh/).

**Windows**: Install Rtools. This is not an R package\! It is “a
collection of resources for building packages for R under Microsoft
Windows, or for building R itself”. Go to
<https://cran.r-project.org/bin/windows/Rtools/> and install as
instructed.

-----

You can **install the development version of `hseclean`** from github
with:

``` r
#install.packages("devtools")
devtools::install_github("STAPM/tobalcepi")
```

-----

If there is an error with `install_github()`, one possible work-around
is

1.  Download the package “tarball” by copying this into your internet
    browser (making sure the numbers at the end indicate the latest
    version) `https://github.com/STAPM/tobalcepi/tarball/1.0.0`. When
    the window pops up, choose where to save the .tar.gz file.

2.  Go to the Terminal window in R Studio (or a console window in
    Windows by searching for “cmd”) and install the package from the
    downloaded file by typing `R CMD INSTALL file_path.tar.gz`.

-----

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

## Getting started

## Basic functionality
