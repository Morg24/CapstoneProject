\#\#Introduction In the world today, researchers have stated that
approximately 8-15% percent of the people that book a flight somewhere
in the world, misses their intended predicted flight. Approximately, 15%
are late to their flight and out of all the flights flown in one
complete year, 32% of the total flights are cancelled or delayed. The
dataset, shows that between the initiations of the airplane to the
landing of the airplane, there are numerous variables that take effect
to the timing of the flight. There are numerous variables are included
into the original dataset. The variables consist of weather, late
aircraft, and security delay. An incremental change in variables affect
the punctuality and take-off of aircrafts at airports. With the
abundance of airports in the world, the problem with passengers and
cancelled and delayed flights, is common. However, the variables in the
dataset show the variables factored into airports in the US. The
passenger that has more time between arrival and departure is usually
the person that experiences cancelled or delayed flights.

I would like to look at a model of an airplane’s arrival variable
dataset and analyze the variables and information in the dataset. This
will lead me to create a probability analysis that will show a decrease
in the probability of a flight being cancelled or delayed. I will use
probability and statistics in my experiment on the variables to create
graphs and models that displays the variation in probability change with
the manipulation of different delay variables. I predict that shortening
the time of the late aircraft delay will have the biggest impact on the
probability of a flight being cancelled. Even from the other factors,
weather may have the largest impact to create a delay in time for an
airliner. To know exactly how they affect the different variables, that
is where the models and statistics favor. Furthermore, the overall
experiment will use data analysis and eventually lead to a solution
being brought upon the problem of airline delay in society.

The goal of my project is to find major airport flight delay variations,
and manipulate the most significant variable to decrease the probability
of a delayed flight.

Origin- Two component variable that is measured over one month, LAX and
ATL Late Aircraft- Maintenance, baggage transportation, checking in
services and other daily processes of the airport Security- The delay
times caused by the security checkpoint inside the airports Weather-
Delay that was impactful due to hazardous storms or severe weather

The necessary libraries needed for the project has been installed and
are loaded here.

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 3.6.1

    ## -- Attaching packages ------------------------------------------------------------------------------------------ tidyverse 1.2.1 --

    ## v ggplot2 3.2.0     v purrr   0.3.2
    ## v tibble  2.1.3     v dplyr   0.8.3
    ## v tidyr   0.8.3     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.4.0

    ## Warning: package 'tibble' was built under R version 3.6.1

    ## Warning: package 'tidyr' was built under R version 3.6.1

    ## Warning: package 'readr' was built under R version 3.6.1

    ## Warning: package 'purrr' was built under R version 3.6.1

    ## Warning: package 'dplyr' was built under R version 3.6.1

    ## Warning: package 'forcats' was built under R version 3.6.1

    ## -- Conflicts --------------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(haven)
```

    ## Warning: package 'haven' was built under R version 3.6.1

``` r
library(sjmisc)
```

    ## Warning: package 'sjmisc' was built under R version 3.6.1

    ## 
    ## Attaching package: 'sjmisc'

    ## The following object is masked from 'package:purrr':
    ## 
    ##     is_empty

    ## The following object is masked from 'package:tidyr':
    ## 
    ##     replace_na

    ## The following object is masked from 'package:tibble':
    ## 
    ##     add_case

``` r
library(plyr)
```

    ## Warning: package 'plyr' was built under R version 3.6.1

    ## -------------------------------------------------------------------------

    ## You have loaded plyr after dplyr - this is likely to cause problems.
    ## If you need functions from both plyr and dplyr, please load plyr first, then dplyr:
    ## library(plyr); library(dplyr)

    ## -------------------------------------------------------------------------

    ## 
    ## Attaching package: 'plyr'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     arrange, count, desc, failwith, id, mutate, rename, summarise,
    ##     summarize

    ## The following object is masked from 'package:purrr':
    ## 
    ##     compact

``` r
library(ggplot2)
library(rmarkdown)
library(caret)
```

    ## Warning: package 'caret' was built under R version 3.6.1

    ## Loading required package: lattice

    ## 
    ## Attaching package: 'caret'

    ## The following object is masked from 'package:purrr':
    ## 
    ##     lift

All of the packages are loaded. Therefore, we load the data into R and
call the data frame dta.

``` r
getwd()
```

    ## [1] "C:/Users/kenneth.morgan/Documents/DATA-WR"

``` r
OrigFlight1 <- read.csv("OrigFlight1.csv")
glimpse(OrigFlight1)
```

    ## Observations: 60,744
    ## Variables: 7
    ## $ X            <int> 233, 234, 237, 238, 240, 241, 242, 243, 244, 245,...
    ## $ ArrDelay     <int> 15, 32, 42, 22, 96, 15, 66, 34, 24, 33, 62, 51, 3...
    ## $ DepDelay     <int> 25, 40, 52, 32, 110, 20, 77, 45, 36, 30, 27, 55, ...
    ## $ Origin       <fct> LAX, LAX, LAX, LAX, LAX, LAX, LAX, LAX, LAX, LAX,...
    ## $ Weather      <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0...
    ## $ Security     <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0...
    ## $ LateAircraft <int> 11, 21, 24, 12, 91, 8, 55, 28, 6, 14, 14, 47, 1, ...

\#\#Data Wrangling Remove Insignificant Variables-  
As one scans through the dataset, you will see that there was an
abundance of variables that were not going to give you an accurate
approach to my research question. Therefore, I had to use a simple logic
approach to each variable. That approach was to simply ask myself do I
see this variable impacting airlines. Going down the list, I saw that
the delay times for Late Aircraft, Security, and Weather Delay were
going to impact enough to provide a statistical analysis. I went into
RStudio to use a code to remove 26 variables of the starting 30, which
leaves me with the 4 variables in the final dataset. Rename Variables-
The variables in the dataset were given a name that came with the
dataset. However, for my preference I would like for the variables to be
named to where I understand them fully. Therefore, I used a code that
renames all the variables in the dataset. I renamed the variables to
Weather, Security, and Late Aircraft. Remove N/A- With respect to having
a dataset with more than a million observations. Some of the
observations in the dataset were filled with N/A values. This is
information that I do not need in the dataset. From this point, the N/A
removal code was very beneficial because the actual values in the
dataset will be the values being analyzed. The code deleted the N/A
observations, which results me with my final dataset. Create a Subset of
Data- The final subset of data comes from the final product of removing
the redundant data in the dataset. The information that was not needed
such as the N/A and extra observations were removed by the code. I found
that to actually analyze my data to the standard was that I had to mine
the data down to two major airports on different sides of the US. Those
two airports are places where I was going to analyze data from, so that
there will be more of an accurate approach to the delay rate from major
airports.

\#\#Exploratory Data Analysis Now that the data have been ingested it is
time to begin the exploration. The first thing to do is to have a quick
look at our data. For that, the `str()` function and the more
human-readable (and intuitive), `glimpse()` function. is used.

``` r
glimpse(OrigFlight1)
```

    ## Observations: 60,744
    ## Variables: 7
    ## $ X            <int> 233, 234, 237, 238, 240, 241, 242, 243, 244, 245,...
    ## $ ArrDelay     <int> 15, 32, 42, 22, 96, 15, 66, 34, 24, 33, 62, 51, 3...
    ## $ DepDelay     <int> 25, 40, 52, 32, 110, 20, 77, 45, 36, 30, 27, 55, ...
    ## $ Origin       <fct> LAX, LAX, LAX, LAX, LAX, LAX, LAX, LAX, LAX, LAX,...
    ## $ Weather      <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0...
    ## $ Security     <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0...
    ## $ LateAircraft <int> 11, 21, 24, 12, 91, 8, 55, 28, 6, 14, 14, 47, 1, ...

As expected, there are 60744 rows with 4 variables inside of the data
set. The variables are Weather, Origin, Security, and Late Aircraft.
Variations in the delay times are shown throughout the dataset. The
range for the delay times, range from 0-875.

``` r
str(OrigFlight1)
```

    ## 'data.frame':    60744 obs. of  7 variables:
    ##  $ X           : int  233 234 237 238 240 241 242 243 244 245 ...
    ##  $ ArrDelay    : int  15 32 42 22 96 15 66 34 24 33 ...
    ##  $ DepDelay    : int  25 40 52 32 110 20 77 45 36 30 ...
    ##  $ Origin      : Factor w/ 2 levels "ATL","LAX": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ Weather     : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ Security    : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ LateAircraft: int  11 21 24 12 91 8 55 28 6 14 ...

``` r
ggplot(OrigFlight1, aes(x = Origin, y = LateAircraft, color = Origin)) + geom_jitter() + ggtitle("Origin vs Late Aircraft")
```

![](Capstone_files/figure-markdown_github/unnamed-chunk-4-1.png)

``` r
ggplot(OrigFlight1, aes(x = Origin, y = Weather, color = Origin)) + geom_jitter() +ggtitle("Origin vs Weather")
```

![](Capstone_files/figure-markdown_github/unnamed-chunk-4-2.png)

``` r
ggplot(OrigFlight1, aes(x = Origin, y = Security, color = Origin)) + geom_jitter() +ggtitle("Origin vs Security")
```

![](Capstone_files/figure-markdown_github/unnamed-chunk-4-3.png)

\#\#Statistical Analysis Determine if there is a difference in means
between the treatment and the control groups for the variables “Score
and Std\_Score.” These two values are equivalent, but there may be value
in examining both.

Throughtout the experiment there were variables that were found to be
less significant. Therefore, the change in variables led to differences
in scatter plots of the delay ratio. The delay times were plotted as the
independent variables changed along the y-axis. The x-variable being the
dependent variable was “Origin.” The different variables resulted in
different variations from one sctter plot to the next.

Above are the first couple of scatter plots I received once I ran the
graphs through R. The scatter plots above show no correlation between
the variables. Here, I noticed that the variables I were measuring in
the graphs were not continuous values. Indicating a non-linear
relationship between the variables. This led me to taking a deeper dive
into the dataset and seeking variables that will create a better
relationship. Hence, the variables were not giving me the results I
hoped for, there were changes made to the variables.

\#\#The Results Results that came from the components of the experiment
were interesting. The first model, “model2”, was ran and showed a
R-squared value of .0117. This indicated the model was not best fit for
the regression model. Therefore, I had to change a dependent variable in
the model. From here, I changed “Origin” to “Arrival Delay”. This
variable however, was ran with the independent variables and resulted in
a model that displayed a R-squared of .8829. I knew that this model was
more significant due to the value being close to 1. This model also
showed a standard deviation that was lower than the first model. Then,
the p-value for the model was low also. All validating the best fit
model for the dataset. In conclusion, this showed me that the variable
of Late Aircraft was not significant to the model. My hypothesis was
wrong and the machine learning assisted me in finding the best fit
model.

``` r
 ggplot(OrigFlight1, aes(x = DepDelay, y = ArrDelay, color = Origin)) + geom_jitter() +ggtitle("Departure Delay vs Arrival Delay")
```

![](Capstone_files/figure-markdown_github/unnamed-chunk-5-1.png)

``` r
ggplot(OrigFlight1, aes(x = LateAircraft, y = ArrDelay, color = Origin)) + geom_jitter() + ggtitle("Arrival Delay vs Late Aircraft")
```

![](Capstone_files/figure-markdown_github/unnamed-chunk-5-2.png)

``` r
ggplot(OrigFlight1, aes(x = Security, y = ArrDelay, color = Origin)) + geom_jitter() +ggtitle("Security vs Arrival Delay")
```

![](Capstone_files/figure-markdown_github/unnamed-chunk-5-3.png) The
scatter plots that I have now, are the graphs I received once I changed
my dependent variable. I then ran the graphs with more significant
variables because Origin is not a continuous variable. Therefore, Origin
could not be ran as the dependent variable. However, the new variable
Arrival Deay was more significant. This variable was immediately
affected by the variable.

Looking into the new graphs, one can see the tremendous difference from
the first set of graphs to the new. There is a positive correlation
between each variable. The best graph was the Departure Delay vs Arrival
Delay graph. This graph shows a linear correlation for the delay values
under each variable. The arrival delay is the variable that will impact
the delay rate the most.

\#\#Machine Learning - Linear Regression

From analyzing the data, one can see that the research question needs
significant variables. To make this research question be changeable by
machine learning, there will have to be two or more independent
variables being ran upon a dependent variable. Since the dependent
variable is a numerical value, my machine learning technique will use a
linear regression model. The different variables will be modeled to test
for significance. The Origin variable is set to be the dependent
variable due to, this variable containing the two components (ATL and
LAX) that will be analyzed over a month’s span. Then the 3 independent
variables will be measured under 3 different models.

Now I will simplify my clean dataset. The new dataset will be divided
into two sets. An outcome from this step was a training set and testing
set. The model will be fitted onto the training set to help predict
observations on the validation set.

``` r
validation_index <- createDataPartition(OrigFlight1$ArrDelay, p=0.80, list=FALSE)
# select 20% of the data for validation
validation <- OrigFlight1[-validation_index,]
# use the remaining 80% of data to training and testing the models
OrigFlight1<- OrigFlight1[validation_index,]
```

Before the linear model was created, we had to create a validation data
set to run the model on 80 percent and 20 percent to get the best
outcome. The training data set is the 80% and the test data set is the
20 %.

``` r
fit <- train(ArrDelay~LateAircraft + DepDelay, data=OrigFlight1, method="lm", metric="RMSE")
print(fit)
```

    ## Linear Regression 
    ## 
    ## 48597 samples
    ##     2 predictor
    ## 
    ## No pre-processing
    ## Resampling: Bootstrapped (25 reps) 
    ## Summary of sample sizes: 48597, 48597, 48597, 48597, 48597, 48597, ... 
    ## Resampling results:
    ## 
    ##   RMSE      Rsquared   MAE     
    ##   17.20269  0.8806001  10.88194
    ## 
    ## Tuning parameter 'intercept' was held constant at a value of TRUE

``` r
model4 =lm(ArrDelay ~ LateAircraft + DepDelay, data=OrigFlight1)
summary(model4)
```

    ## 
    ## Call:
    ## lm(formula = ArrDelay ~ LateAircraft + DepDelay, data = OrigFlight1)
    ## 
    ## Residuals:
    ##    Min     1Q Median     3Q    Max 
    ## -78.02  -9.31  -2.39   5.58 355.85 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  5.4684489  0.1147915  47.638   <2e-16 ***
    ## LateAircraft 0.0004228  0.0025050   0.169    0.866    
    ## DepDelay     0.9419830  0.0017925 525.510   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 17.21 on 48594 degrees of freedom
    ## Multiple R-squared:  0.8812, Adjusted R-squared:  0.8812 
    ## F-statistic: 1.803e+05 on 2 and 48594 DF,  p-value: < 2.2e-16

Due to varibales in the dataset not having a positive impact towards the
R-squared value, the changing in variables had to be made. The Weather
and Security delay variables were values that did not raise the
R-squared value closer to one. Therefore, the actual arrival and
departure delay variables had to be brought into the equation. These two
variables changed the standard deviation value and R-squared value
instantly.

From the model, I observed that the variables in the model gave me a
R-squared value of .1175. This value was to low, which led to some
manipulation of variables. There had to be a variable change therefore,
the experiment would have been ran with a bad model. The significance of
the P-value was to find a best fit model that will help eliminate a bad
model. The RMSE, began to decrease once the dependent variable was
changed. The variable changed initiated a better model.

Machine Learning Model
*y* = 5.3487508*x*<sub>1</sub> − .0004022*x*<sub>2</sub> + .9441706*x*<sub>3</sub>

\#\#Recommendations 1. Try to use another intervention 2. Collect
additional data from datasets to perform future data analysis 3. Higher
me fulltime

\#\#Future Work From the first dataset, there were more than 50
different airports. The cleaned dataset and dataset that was analyzed
had two major US airports. I would like to expand my research to more
airports around the US. The variables that I would like to work with in
the future will have a higher level of significance in a model.
Therefore, the probability of delayed flights will be lowered in the US,
once the variables are manipulated. From this, I would like to analyze
data from large datasets and create models that will analyze numerical
values distinctively.
