
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Datamation pacakge

## Installation

datamation is not yet available on CRAN, but you can install it from
GitHub with

``` r
remotes::install_github("seankross/datamations")
```

## Examples for Plot-based Datamations

With the zip file you downloaded, run the code below (`README.Rmd`) to
reproduce the datamation gifs. (`eval=FALSE` in chunk options might
prevent you from automatically running the chunks. Remove if necessary.)

``` r
library(datamation)
library(animation)
library(tidyverse)
```

``` r
degree_title_step1 <- "Step 1: Each dot shows one person\n            and each group shows degree type"
degree_title_step2 <- "Step 2: Next you plot the salary of each person\n            within each group"
degree_title_step3 <- "Step 3: Lastly you plot the average salary \n            of each group and zoom in"
work_degree_title_step1 <- "Step 1: Each dot shows one person and each group\n            shows degree type AND work setting"
```

``` r
plot_pipe <- "small_salary %>% group_by(Degree) %>% summarize(mean = mean(Salary))"

# The command below takes 70 seconds to execute on my machine
datamation_sanddance(plot_pipe, output = "mean_salary_group_by_degree.gif",
                     titles = c(degree_title_step1, degree_title_step2, degree_title_step3), 
                     nframes = 30)

plot_pipe2 <- "small_salary %>% group_by(Degree, Work) %>% summarize(mean = mean(Salary))"

# The command below takes 15 seconds to execute on my machine
datamation_sanddance(plot_pipe2, output = "mean_salary_group_by_degree_work.gif",
                     titles = c(work_degree_title_step1, degree_title_step2, degree_title_step3))
```

## Examples for Table-based Datamations

``` r
# The command below takes 20 seconds to execute on my machine
pipeline <- "small_salary_data %>% group_by(Degree)"
dmpkg::datamation_tibble(pipeline, output = "salary_group_degree.gif")

# The command below takes 40 seconds to execute on my machine
pipeline <- "mtcars %>% group_by(cyl)"
dmpkg::datamation_tibble(pipeline, output = "mtcars_group_cyl.gif")

# The command below takes 50 seconds to execute on my machine
pipeline <- "small_salary_data %>% group_by(Degree, Work) %>% summarize(Avg_Salary = mean(Salary))"
dmpkg::datamation_tibble(pipeline, output = "salary_group2_summarize_mean.gif")

# The command below takes 50 seconds to execute on my machine
pipeline <- "small_salary_data %>% group_by(Degree, Work) %>% summarize(Avg_Salary = mean(Salary))"
dmpkg::datamation_tibble(pipeline, output = "salary_group2_summarize_mean.gif",
                         titles = c("Grouping by Degree and Work", 
                                    "Calculating the Mean of Each Group"))
```
