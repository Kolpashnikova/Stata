# ttest
Kamila Kolpashnikova  

# T-test




The data here is derived from the [American Time Use Survey](http://www.bls.gov/tus/). For the coding procedures, contact me via email.

## Step 1. Downloading the dataset
You need to download the ATUS_full3.dta file from my github to your working directory.


```stata
use ATUS_full3.dta, clear
```



## Step 2. Choose a Continuous Variable and Two Groups to Continuous

In the datase, I will use two ordinal variables. One which is time spent on cooking (DVCOOK) and the two groups are represented by the `Female` variable.


```stata
sum DVCOOK
tab Female
```

```


. use ATUS_full3.dta, clear

. sum DVCOOK



    Variable |       Obs        Mean    Std. Dev.       Min        Max
-------------+--------------------------------------------------------
      DVCOOK |    159937    35.49352    55.49618          0        995

. 


. tab Female

  RECODE of |
      tesex |
   (Edited: |
       sex) |      Freq.     Percent        Cum.
------------+-----------------------------------
          0 |     69,889       43.70       43.70
          1 |     90,048       56.30      100.00
------------+-----------------------------------
      Total |    159,937      100.00
```

## Step 3. Peform t-test

You use the `ttest` command.


```stata
ttest DVCOOK, by(Female)
```

```


. use ATUS_full3.dta, clear


. ttest DVCOOK, by(Female)

Two-sample t test with equal variances
------------------------------------------------------------------------------
   Group |     Obs        Mean    Std. Err.   Std. Dev.   [95% Conf. Interval]
---------+--------------------------------------------------------------------
       0 |   69889    19.97658    .1501022     39.6818    19.68238    20.27078
       1 |   90048    47.53669    .2085418    62.57921    47.12795    47.94543
---------+--------------------------------------------------------------------
combined |  159937    35.49352    .1387678    55.49618    35.22154     35.7655
---------+--------------------------------------------------------------------
    diff |           -27.56011    .2711471               -28.09156   -27.02867
------------------------------------------------------------------------------
    diff = mean(0) - mean(1)                                      t = -1.0e+02
Ho: diff = 0                                     degrees of freedom =   159935

    Ha: diff < 0                 Ha: diff != 0                 Ha: diff > 0
 Pr(T < t) = 0.0000         Pr(|T| > |t|) = 0.0000          Pr(T > t) = 1.0000

```

In the output above, the difference of -27.56011 has a t of -100(-1.0e+02) and it is statistically significant.

## Step 4. Interpretation
The mean time spent on cooking for men is 19.98.The mean time spent on cooking for women is 47.54. This difference is statistically significant, t(159935) = -100, p < .001. In other words, there is a significant difference in time spent on cooking between women and men.
