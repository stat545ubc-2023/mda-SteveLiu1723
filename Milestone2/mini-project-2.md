*To complete this milestone, you can either edit [this `.rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are commented out with
`<!--- start your work here--->`. When you are done, make sure to knit
to an `.md` file by changing the output in the YAML header to
`github_document`, before submitting a tagged release on canvas.*

# Welcome to the rest of your mini data analysis project!

In Milestone 1, you explored your data. and came up with research
questions. This time, we will finish up our mini data analysis and
obtain results for your data by:

-   Making summary tables and graphs
-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

We will also explore more in depth the concept of *tidy data.*

**NOTE**: The main purpose of the mini data analysis is to integrate
what you learn in class in an analysis. Although each milestone provides
a framework for you to conduct your analysis, it’s possible that you
might find the instructions too rigid for your data set. If this is the
case, you may deviate from the instructions – just make sure you’re
demonstrating a wide range of tools and techniques taught in this class.

# Instructions

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work here--->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to your mini-analysis GitHub repository, and tag a
release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 50 points: 45 for your analysis, and
5 for overall reproducibility, cleanliness, and coherence of the Github
submission.

**Research Questions**: In Milestone 1, you chose two research questions
to focus on. Wherever realistic, your work in this milestone should
relate to these research questions whenever we ask for justification
behind your work. In the case that some tasks in this milestone don’t
align well with one of your research questions, feel free to discuss
your results in the context of a different research question.

# Learning Objectives

By the end of this milestone, you should:

-   Understand what *tidy* data is, and how to create it using `tidyr`.
-   Generate a reproducible and clear report using R Markdown.
-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

# Setup

Begin by loading your data and the tidyverse package below:

    library(datateachr) # <- might contain the data you picked!
    library(tidyverse)

# Task 1: Process and summarize your data

From milestone 1, you should have an idea of the basic structure of your
dataset (e.g. number of rows and columns, class types, etc.). Here, we
will start investigating your data more in-depth using various data
manipulation functions.

### 1.1 (1 point)

First, write out the 4 research questions you defined in milestone 1
were. This will guide your work through milestone 2:

<!-------------------------- Start your work below ---------------------------->

(I have to edit some of them since they are too advanced for this
course, like doing PCA and model selection procedures, which all types
of questions that specified here cannot help)

1.  How is area\_mean associated with the diagnostic result?

2.  Is there any difference between the distribution of mean measure and
    the distribution of the worst-case measure for these parameters?

3.  Is there any dependence structure between area\_mean and
    area\_worst?

4.  What is the proportion of observations which has both of their
    area\_mean and area\_worst larger the mean of two measures
    respectively? what’s the proportion of it in the subpopulations
    whose area\_mean &gt; mean(area\_mean) and whose area\_worst &gt;
    mean(area\_worst)?
    <!----------------------------------------------------------------------------->

Here, we will investigate your data using various data manipulation and
graphing functions.

### 1.2 (8 points)

Now, for each of your four research questions, choose one task from
options 1-4 (summarizing), and one other task from 4-8 (graphing). You
should have 2 tasks done for each research question (8 total). Make sure
it makes sense to do them! (e.g. don’t use a numerical variables for a
task that needs a categorical variable.). Comment on why each task helps
(or doesn’t!) answer the corresponding research question.

Ensure that the output of each operation is printed!

Also make sure that you’re using dplyr and ggplot2 rather than base R.
Outside of this project, you may find that you prefer using base R
functions for certain tasks, and that’s just fine! But part of this
project is for you to practice the tools we learned in class, which is
dplyr and ggplot2.

**Summarizing:**

1.  Compute the *range*, *mean*, and *two other summary statistics* of
    **one numerical variable** across the groups of **one categorical
    variable** from your data.
2.  Compute the number of observations for at least one of your
    categorical variables. Do not use the function `table()`!
3.  Create a categorical variable with 3 or more groups from an existing
    numerical variable. You can use this new variable in the other
    tasks! *An example: age in years into “child, teen, adult, senior”.*
4.  Compute the proportion and counts in each category of one
    categorical variable across the groups of another categorical
    variable from your data. Do not use the function `table()`!

**Graphing:**

1.  Create a graph of your choosing, make one of the axes logarithmic,
    and format the axes labels so that they are “pretty” or easier to
    read.
2.  Make a graph where it makes sense to customize the alpha
    transparency.

Using variables and/or tables you made in one of the “Summarizing”
tasks:

1.  Create a graph that has at least two geom layers.
2.  Create 3 histograms, with each histogram having different sized
    bins. Pick the “best” one and explain why it is the best.

Make sure it’s clear what research question you are doing each operation
for!

<!------------------------- Start your work below ----------------------------->

Research Question1:

    # task1 for research question 1
    cancer_M <- filter(cancer_sample, cancer_sample$diagnosis=="M")
    cancer_B <- filter(cancer_sample, cancer_sample$diagnosis=="B")
    cancer_M_aream_range <- range(cancer_M$area_mean)[2]- 
                            range(cancer_M$area_mean)[1]
    cancer_B_aream_range <- range(cancer_B$area_mean)[2]- 
                            range(cancer_B$area_mean)[1]
    cancer_M_aream_sd <- sd(cancer_M$area_mean)
    cancer_B_aream_sd <- sd(cancer_B$area_mean)
    cancer_M_aream_max <- max(cancer_M$area_mean)
    cancer_B_aream_max <- max(cancer_B$area_mean)
    cancer_M_aream_mean <- mean(cancer_M$area_mean)
    cancer_B_aream_mean <- mean(cancer_B$area_mean)
    Q1_11_tibble <- tibble(Diag_Result = c("M","B"),
                          Range = c(cancer_M_aream_range,cancer_B_aream_range),
                          Stand_Dev = c(cancer_M_aream_sd,cancer_B_aream_sd),
                          Maximum = c(cancer_M_aream_max,cancer_B_aream_max),
                          Mean = c(cancer_M_aream_mean,cancer_B_aream_mean))
    kableExtra::kable(Q1_11_tibble)

<table>
<thead>
<tr>
<th style="text-align:left;">
Diag\_Result
</th>
<th style="text-align:right;">
Range
</th>
<th style="text-align:right;">
Stand\_Dev
</th>
<th style="text-align:right;">
Maximum
</th>
<th style="text-align:right;">
Mean
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
M
</td>
<td style="text-align:right;">
2139.4
</td>
<td style="text-align:right;">
367.9380
</td>
<td style="text-align:right;">
2501.0
</td>
<td style="text-align:right;">
978.3764
</td>
</tr>
<tr>
<td style="text-align:left;">
B
</td>
<td style="text-align:right;">
848.6
</td>
<td style="text-align:right;">
134.2871
</td>
<td style="text-align:right;">
992.1
</td>
<td style="text-align:right;">
462.7902
</td>
</tr>
</tbody>
</table>

    # task6 for research question 1

    ggplot(data=cancer_sample, aes(diagnosis,area_mean,color=diagnosis))+
      geom_boxplot()+
      scale_y_continuous(trans='log10')+
      labs(x="Diagnostic Result", y="Mean of Area in log-scale")

![](mini-project-2_files/figure-markdown_strict/unnamed-chunk-3-1.png)
Both of them can help me because both of them provide me with the
information about the distribution of subpopulation. The task6 may be
more helpful since it reveals more information and is more
straightforward.

Research Question2:

    # task3 for research question 2
    Q1_21_cancer <- cancer_sample|>
                    mutate(mean_class = case_when(area_mean < 420 ~ "small",
                                     area_mean < 783 ~ "medium",
                                     TRUE ~ "large"),
                           worst_mean_class = case_when(area_worst < 515 ~ "small",
                                     area_worst < 1084 ~ "medium",
                                     TRUE ~ "large"))

    # task6 for research question 2
    Q1_22_cancer <- cancer_sample |>
                    pivot_longer(names_to="case",
                                 values_to="mean",
                                 cols=c(area_mean,area_worst))
    ggplot(data=Q1_22_cancer, aes(mean))+
      geom_histogram()+
      facet_wrap(~case)+
      scale_y_continuous(trans='log10')+
      labs(x="Mean", y="Frequency in log scale")

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Transformation introduced infinite values in continuous y-axis

    ## Warning: Removed 19 rows containing missing values (`geom_bar()`).

![](mini-project-2_files/figure-markdown_strict/unnamed-chunk-5-1.png) I
think task6 is better since it directly provides us a comparison between
two distributions. With task1, maybe we can check the corresponding
relationships between different levels for area\_mean and area\_worst,
but it is less intuitive than task6. From task6, it’s pretty clear to us
that both distributions are slightly right-skewed.

Research Question3:

    # task1 for research question 3
    # For the categorical variable, please refers to my task6 for RQ2
    cancer_aream_range <- range(cancer_sample$area_mean)[2]- 
                            range(cancer_sample$area_mean)[1]
    cancer_waream_range <- range(cancer_sample$area_worst)[2]- 
                            range(cancer_sample$area_worst)[1]
    cancer_aream_mean <- sd(cancer_sample$area_mean)
    cancer_waream_mean <- sd(cancer_sample$area_worst)
    cancer_cov <- cov(cancer_sample$area_mean,cancer_sample$area_worst)
    cancer_cor <- cor(cancer_sample$area_mean,cancer_sample$area_worst)
    Q1_31_tibble <- tibble(Diag_Result = c("General","Worst"),
                          Range = c(cancer_aream_range,cancer_waream_range),
                          Mean = c(cancer_aream_mean,cancer_waream_mean),
                          Covariance = c(cancer_cov,cancer_cov),
                          Correlation = c(cancer_cor,cancer_cor))
    kableExtra::kable(Q1_31_tibble)

<table>
<thead>
<tr>
<th style="text-align:left;">
Diag\_Result
</th>
<th style="text-align:right;">
Range
</th>
<th style="text-align:right;">
Mean
</th>
<th style="text-align:right;">
Covariance
</th>
<th style="text-align:right;">
Correlation
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
General
</td>
<td style="text-align:right;">
2357.5
</td>
<td style="text-align:right;">
351.9141
</td>
<td style="text-align:right;">
192192.6
</td>
<td style="text-align:right;">
0.9592133
</td>
</tr>
<tr>
<td style="text-align:left;">
Worst
</td>
<td style="text-align:right;">
4068.8
</td>
<td style="text-align:right;">
569.3570
</td>
<td style="text-align:right;">
192192.6
</td>
<td style="text-align:right;">
0.9592133
</td>
</tr>
</tbody>
</table>

    # task8 for research question 3
    ggplot(cancer_sample,aes(x=area_mean,y=area_worst))+
      geom_point()+
      geom_line()+
      labs(x="Area Mean in General", y="Area Mean in Worst Case")

![](mini-project-2_files/figure-markdown_strict/unnamed-chunk-7-1.png) I
think both tasks can reveal some information regarding the association
between two variables: Task1 gives me a direct measure on the strength
of linear relationshio between them, while task6 visually presents it.

Research Question4:

    # task4 for research question 4
    Q1_41_cancer <- cancer_sample |>
                    mutate(area_m_l = case_when(area_mean > mean(area_mean) 
                                                 ~ 1,
                                                area_mean <= mean(area_mean) 
                                                 ~ 0),
                           area_w_l = case_when(area_worst > mean(area_worst) 
                                                 ~ 1,
                                                area_worst <= mean(area_worst) 
                                                 ~ 0),
                           comb_l = case_when( area_m_l + area_w_l == 2
                                                 ~ 1,
                                                area_m_l + area_w_l != 2 
                                                 ~ 0))
    attach(Q1_41_cancer)
    # compute the proportion/count of observation whose area_mean and area_worst are 
    # both larger than the corresponding means in the all observations whose
    # area_mean is larger than the mean of area_mean.
    prop_ll_in_ml <- sum(comb_l)/sum(area_m_l)
    count_ll_in_ml <- sum(comb_l)
    # compute the proportion/count of observation whose area_mean and area_worst are 
    # both larger than the corresponding means in the all observations whose
    # area_worst is larger than the mean of area_worst.
    prop_ll_in_wl <- sum(comb_l)/sum(area_w_l)
    count_ll_in_wl <- sum(comb_l)
    detach(Q1_41_cancer)

    # task8 for research question 4
    ggplot(data=Q1_41_cancer)+
      geom_histogram(aes(x=area_mean,fill="area_mean",alpha=0.5))+
      geom_histogram(aes(x=area_worst,fill="area_worst",alpha=0.5))+
      geom_vline(xintercept = mean(Q1_41_cancer$area_mean),linetype="dashed")+
      geom_vline(xintercept = mean(Q1_41_cancer$area_worst),linetype="dashed")

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](mini-project-2_files/figure-markdown_strict/unnamed-chunk-9-1.png)
Task1 can help me to get a numerical result for my research question4
directly, while the task8 can visually let me know that the two
distributions are almost overlapped but cannot give me a result
directly. I personally prefer task1.
<!----------------------------------------------------------------------------->

### 1.3 (2 points)

Based on the operations that you’ve completed, how much closer are you
to answering your research questions? Think about what aspects of your
research questions remain unclear. Can your research questions be
refined, now that you’ve investigated your data a bit more? Which
research questions are yielding interesting results?

<!------------------------- Write your answer here ---------------------------->

About question1, actually we are interested in the comparison of both
distribution, and so histograms, box-plots and also comprehensive
summary statistics all work. This question has been solved.

About question2, we are still evaluating the comparison between two
distributions, but we are not using diagnosis results to distinguish two
distributions. The result is also pretty convincing here.

About question3, even though that we have a very high correlation
between the two variables (that’s kinda surprising to me since the value
is very close to 1 but the data is slightly diverse at the tail),
potentially the dependence structure can be non-linear, and so maybe
further exploration is needed. However, if we can refine our question as
the linear relationship between two variables, then the solution is
perfect.

About question4, the plot is pretty straightforward but it cannot give
us a precise result. In this case, task1 provided everything we need
after we created three new categorical variables. It’s not surprising
for me to see that the proportions with respect to subpopulations are
pretty high, since their high correlation has alreay been verified in
question3.

<!----------------------------------------------------------------------------->

# Task 2: Tidy your data

In this task, we will do several exercises to reshape our data. The goal
here is to understand how to do this reshaping with the `tidyr` package.

A reminder of the definition of *tidy* data:

-   Each row is an **observation**
-   Each column is a **variable**
-   Each cell is a **value**

### 2.1 (2 points)

Based on the definition above, can you identify if your data is tidy or
untidy? Go through all your columns, or if you have &gt;8 variables,
just pick 8, and explain whether the data is untidy or tidy.

<!--------------------------- Start your work below --------------------------->

Yes, the data is tidy! First of all, each row is one observation that is
indexed by an unique ID; except the diagnosis result, each column is a
numerical measure to an observation; each cell is a value.
<!----------------------------------------------------------------------------->

### 2.2 (4 points)

Now, if your data is tidy, untidy it! Then, tidy it back to it’s
original state.

If your data is untidy, then tidy it! Then, untidy it back to it’s
original state.

Be sure to explain your reasoning for this task. Show us the “before”
and “after”.

<!--------------------------- Start your work below --------------------------->

    # untidy the data by merging area_mean and area_worst
    cancer_untidy <- cancer_sample |>
                     pivot_longer(names_to="case",
                                 values_to="mean",
                                 cols=c(area_mean,area_worst))
    head(cancer_untidy)

    ## # A tibble: 6 × 32
    ##         ID diagnosis radius_mean texture_mean perimeter_mean smoothness_mean
    ##      <dbl> <chr>           <dbl>        <dbl>          <dbl>           <dbl>
    ## 1   842302 M                18.0         10.4           123.          0.118 
    ## 2   842302 M                18.0         10.4           123.          0.118 
    ## 3   842517 M                20.6         17.8           133.          0.0847
    ## 4   842517 M                20.6         17.8           133.          0.0847
    ## 5 84300903 M                19.7         21.2           130           0.110 
    ## 6 84300903 M                19.7         21.2           130           0.110 
    ## # ℹ 26 more variables: compactness_mean <dbl>, concavity_mean <dbl>,
    ## #   concave_points_mean <dbl>, symmetry_mean <dbl>,
    ## #   fractal_dimension_mean <dbl>, radius_se <dbl>, texture_se <dbl>,
    ## #   perimeter_se <dbl>, area_se <dbl>, smoothness_se <dbl>,
    ## #   compactness_se <dbl>, concavity_se <dbl>, concave_points_se <dbl>,
    ## #   symmetry_se <dbl>, fractal_dimension_se <dbl>, radius_worst <dbl>,
    ## #   texture_worst <dbl>, perimeter_worst <dbl>, smoothness_worst <dbl>, …

    # tidy it back by get it back to two columns
    cancer_tidyback <- cancer_untidy |>
                       pivot_wider(names_from = case,
                                   values_from = mean)
    head(cancer_tidyback)

    ## # A tibble: 6 × 32
    ##         ID diagnosis radius_mean texture_mean perimeter_mean smoothness_mean
    ##      <dbl> <chr>           <dbl>        <dbl>          <dbl>           <dbl>
    ## 1   842302 M                18.0         10.4          123.           0.118 
    ## 2   842517 M                20.6         17.8          133.           0.0847
    ## 3 84300903 M                19.7         21.2          130            0.110 
    ## 4 84348301 M                11.4         20.4           77.6          0.142 
    ## 5 84358402 M                20.3         14.3          135.           0.100 
    ## 6   843786 M                12.4         15.7           82.6          0.128 
    ## # ℹ 26 more variables: compactness_mean <dbl>, concavity_mean <dbl>,
    ## #   concave_points_mean <dbl>, symmetry_mean <dbl>,
    ## #   fractal_dimension_mean <dbl>, radius_se <dbl>, texture_se <dbl>,
    ## #   perimeter_se <dbl>, area_se <dbl>, smoothness_se <dbl>,
    ## #   compactness_se <dbl>, concavity_se <dbl>, concave_points_se <dbl>,
    ## #   symmetry_se <dbl>, fractal_dimension_se <dbl>, radius_worst <dbl>,
    ## #   texture_worst <dbl>, perimeter_worst <dbl>, smoothness_worst <dbl>, …

For this particular dataset, a lot of pair of measures are the measure
to the same thing but different in “in general” and “in worst case”.
Even though they are related, they are still separate features, and they
belong to the same observation. Therefore, here I used area\_mean and
area\_worst as an example to show that you cannot pivot\_longer the
data. Actually such an operation I did here can be applied to many pairs
of data.
<!----------------------------------------------------------------------------->

### 2.3 (4 points)

Now, you should be more familiar with your data, and also have made
progress in answering your research questions. Based on your interest,
and your analyses, pick 2 of the 4 research questions to continue your
analysis in the remaining tasks:

<!-------------------------- Start your work below ---------------------------->

1.  Is there any difference between the distribution of mean measure and
    the distribution of the worst-case measure for these parameters?

2.  Is there any dependence structure between area\_mean and
    area\_worst?

<!----------------------------------------------------------------------------->

Explain your decision for choosing the above two research questions.

<!--------------------------- Start your work below --------------------------->

First of all, the question regarding the dependence structure are the
only question is that I think has not been solved properly. However, a
measure to that may be sensitive to the properties of two distributions
respectively, like outliers, and so I also include the question that is
about the comparison between two distributions here.
<!----------------------------------------------------------------------------->

Now, try to choose a version of your data that you think will be
appropriate to answer these 2 questions. Use between 4 and 8 functions
that we’ve covered so far (i.e. by filtering, cleaning, tidy’ing,
dropping irrelevant columns, etc.).

(If it makes more sense, then you can make/pick two versions of your
data, one for each research question.)

<!--------------------------- Start your work below --------------------------->

    # For these two questions, all I need to do is drop other irrelevant columns.
    # The data is already tidy, and there is since the outliers are not errors, 
    # there is no reason for me to filter the data 
    cancer_new_version <- cancer_sample |>
                          select(ID, diagnosis, area_mean, area_worst)

# Task 3: Modelling

## 3.0 (no points)

Pick a research question from 1.2, and pick a variable of interest
(we’ll call it “Y”) that’s relevant to the research question. Indicate
these.

<!-------------------------- Start your work below ---------------------------->

**Research Question**: Is there any dependence structure between
area\_mean and area\_worst?

**Variable of interest**: area-worst

<!----------------------------------------------------------------------------->

## 3.1 (3 points)

Fit a model or run a hypothesis test that provides insight on this
variable with respect to the research question. Store the model object
as a variable, and print its output to screen. We’ll omit having to
justify your choice, because we don’t expect you to know about model
specifics in STAT 545.

-   **Note**: It’s OK if you don’t know how these models/tests work.
    Here are some examples of things you can do here, but the sky’s the
    limit.

    -   You could fit a model that makes predictions on Y using another
        variable, by using the `lm()` function.
    -   You could test whether the mean of Y equals 0 using `t.test()`,
        or maybe the mean across two groups are different using
        `t.test()`, or maybe the mean across multiple groups are
        different using `anova()` (you may have to pivot your data for
        the latter two).
    -   You could use `lm()` to test for significance of regression
        coefficients.

<!-------------------------- Start your work below ---------------------------->

    # I am going to fit a linear regression model to area_worst using area_mean
    pred_model <- lm(data=cancer_sample, area_worst~area_mean)
    summary(pred_model)

    ## 
    ## Call:
    ## lm(formula = area_worst ~ area_mean, data = cancer_sample)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1243.46   -67.21   -12.90    40.97  1365.59 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) -135.73793   14.27660  -9.508   <2e-16 ***
    ## area_mean      1.55190    0.01921  80.799   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 161.1 on 567 degrees of freedom
    ## Multiple R-squared:  0.9201, Adjusted R-squared:  0.9199 
    ## F-statistic:  6529 on 1 and 567 DF,  p-value: < 2.2e-16

<!----------------------------------------------------------------------------->

## 3.2 (3 points)

Produce something relevant from your fitted model: either predictions on
Y, or a single value like a regression coefficient or a p-value.

-   Be sure to indicate in writing what you chose to produce.
-   Your code should either output a tibble (in which case you should
    indicate the column that contains the thing you’re looking for), or
    the thing you’re looking for itself.
-   Obtain your results using the `broom` package if possible. If your
    model is not compatible with the broom function you’re needing, then
    you can obtain your results by some other means, but first indicate
    which broom function is not compatible.

<!-------------------------- Start your work below ---------------------------->

    # here I tried to produce the regression coefficient, its standard error
    # the test statistics and also the p-value
    library(broom)
    tidy(pred_model)

    ## # A tibble: 2 × 5
    ##   term        estimate std.error statistic   p.value
    ##   <chr>          <dbl>     <dbl>     <dbl>     <dbl>
    ## 1 (Intercept)  -136.     14.3        -9.51 5.47e- 20
    ## 2 area_mean       1.55    0.0192     80.8  2.69e-313

<!----------------------------------------------------------------------------->

# Task 4: Reading and writing data

Get set up for this exercise by making a folder called `output` in the
top level of your project folder / repository. You’ll be saving things
there.

## 4.1 (3 points)

Take a summary table that you made from Task 1, and write it as a csv
file in your `output` folder. Use the `here::here()` function.

-   **Robustness criteria**: You should be able to move your Mini
    Project repository / project folder to some other location on your
    computer, or move this very Rmd file to another location within your
    project repository / folder, and your code should still work.
-   **Reproducibility criteria**: You should be able to delete the csv
    file, and remake it simply by knitting this Rmd file.

<!-------------------------- Start your work below ---------------------------->

    write_csv(Q1_11_tibble,here::here("Output/Q1_11_tibble.csv"))

<!----------------------------------------------------------------------------->

## 4.2 (3 points)

Write your model object from Task 3 to an R binary file (an RDS), and
load it again. Be sure to save the binary file in your `output` folder.
Use the functions `saveRDS()` and `readRDS()`.

-   The same robustness and reproducibility criteria as in 4.1 apply
    here.

<!-------------------------- Start your work below ---------------------------->

    saveRDS(pred_model, file = here::here("Output/pred_model"))
    readRDS(here::here("Output/pred_model"))

    ## 
    ## Call:
    ## lm(formula = area_worst ~ area_mean, data = cancer_sample)
    ## 
    ## Coefficients:
    ## (Intercept)    area_mean  
    ##    -135.738        1.552

<!----------------------------------------------------------------------------->

# Overall Reproducibility/Cleanliness/Coherence Checklist

Here are the criteria we’re looking for.

## Coherence (0.5 points)

The document should read sensibly from top to bottom, with no major
continuity errors.

The README file should still satisfy the criteria from the last
milestone, i.e. it has been updated to match the changes to the
repository made in this milestone.

## File and folder structure (1 points)

You should have at least three folders in the top level of your
repository: one for each milestone, and one output folder. If there are
any other folders, these are explained in the main README.

Each milestone document is contained in its respective folder, and
nowhere else.

Every level-1 folder (that is, the ones stored in the top level, like
“Milestone1” and “output”) has a `README` file, explaining in a sentence
or two what is in the folder, in plain language (it’s enough to say
something like “This folder contains the source for Milestone 1”).

## Output (1 point)

All output is recent and relevant:

-   All Rmd files have been `knit`ted to their output md files.
-   All knitted md files are viewable without errors on Github. Examples
    of errors: Missing plots, “Sorry about that, but we can’t show files
    that are this big right now” messages, error messages from broken R
    code
-   All of these output files are up-to-date – that is, they haven’t
    fallen behind after the source (Rmd) files have been updated.
-   There should be no relic output files. For example, if you were
    knitting an Rmd to html, but then changed the output to be only a
    markdown file, then the html file is a relic and should be deleted.

Our recommendation: delete all output files, and re-knit each
milestone’s Rmd file, so that everything is up to date and relevant.

## Tagged release (0.5 point)

You’ve tagged a release for Milestone 2.

### Attribution

Thanks to Victor Yuan for mostly putting this together.
