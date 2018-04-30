---
title: Data
description: >-
  This is a template chapter.


---
## Ex 1.1

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: b9c7132246
```

Introduction

`@instructions`
Download the Province'91 data. The dataset is available from [http://vliss.helsinki.fi/chapter2/province91-population.html ](url)

`@hint`
Use package haven.


`@sample_code`
```{r}
# install package tidyverse
install.packages("tidyverse")
# load package tidyverse
library(tidyverse)
# read Province91 text dataset
province91 <- read.table("province91.txt",header = TRUE)

# print head of dataset
head(province91)

# more info
str(province91)


```





