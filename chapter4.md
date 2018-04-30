---
title       : jotain muuta
description : blaa blaa
---
## SRS

```yaml
type: NormalExercise

xp: 100

key: 0f16501f46
```

Next we'll calculate some figures from the population Province'91 data.

`@instructions`
Use codes

`@hint`



`@sample_code`
```{r}
# Task 1: Total of UE91
sum(province91$UE91) 


# Task 2
sum(province91$LAB91)
unemployment_rate <- sum(province91$UE91)/sum(province91$LAB91) 
unemployment_rate

# Task 3
median(province91$UE91)

# Task 4
var(province91$UE91)
sd(province91$UE91)


# Task 5

# Simple random sampling in R, package sampling
# srswor: Simple random sampling with replacement.
# srswor1: Simple random sampling without replacement (sequential method).
# srswr: Simple random sampling with replacement.
# srswor(n,N)
# n	= sample size
# N	= population size

install.packages("sampling")
library(sampling)
??sampling

# NOTE: Select your OWN seed number!
set.seed(123)
# select a sample
sampleprovince <- srswor(8,32)
# the sample is
(1:32)[sampleprovince==1]

# selected data
srs_sampledata <- getdata(province91, sampleprovince)
srs_sampledata

install.packages("survey")
library(survey)

# total=32:  fpc = finite population correction: fpc = (1-n/N)
# total=32 : Tarvitaan ??rellisyyskorjausta varten fpc = (1-n/N)
# This column (variable) fpc simply contains the number 32 for every record.
srs_sampledata$fpc <- 32
srs_sampledata$weights <- 4

# Construct a survey.srs.design object called province91.design specifying a simple random sampling design. 
# This province91.srs.design object will be used for all subsequent analysis commands:
province91.srs.design <-
  svydesign(
    ids = ~1 ,
    data = srs_sampledata,
    fpc = ~fpc ,
    weights = ~weights 
  )
# List design info
province91.srs.design

# View the weighted total population of this survey design, by referring to the weights 
# column from the original data.frame:
sum(province91$weights)
sum(srs_sampledata$weights)

# Count the number of unweighted observations where the variable ue91 is not missing:
unwtd.count(~UE91, province91.srs.design)

# Print the mean and standard error of the ue91 variable:
svymean(~UE91, province91.srs.design)

# Print the weighted total and standard error of the ue91 variable:
svytotal(~UE91, province91.srs.design)

# confint() Computes confidence intervals
confint(svytotal(~UE91, province91.srs.design))

# Task 6
# print unemployment rate for population
svyratio(~UE91,~LAB91, province91.srs.design)

# median
svyquantile(~UE91, province91.srs.design, quantiles = 0.5, ci = TRUE)

```





