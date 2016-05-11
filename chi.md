# Chi
Kamila Kolpashnikova  

# Pearson's chi-squared test and Interpretation




The data here is derived from the [American Time Use Survey](http://www.bls.gov/tus/). For the coding procedures, contact me via email.

## Step 1. Downloading the dataset
You need to download the ATUS_full3.dta file from my github to your working directory.


```stata
use ATUS_full3.dta, clear
```



## Step 2. Choose nominal variables

In the datase, I will use two dummy variables. One which is sex of the respondent (Female; 1-'Female', 2-'Male'), and the other is whether the respondent has children under 5 years of age (Under5; 1-'has children under 5 y/o', 0 - otherwise).


```stata
tab Female
tab Under5
```

```


. use ATUS_full3.dta, clear

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

. tab Under5

     Under5 |      Freq.     Percent        Cum.
------------+-----------------------------------
          0 |    128,642       80.43       80.43
          1 |     31,295       19.57      100.00
------------+-----------------------------------
      Total |    159,937      100.00
```

## Step 3. Peform chi-squared test

You use an option `chi` with the `tabulate` command.


```stata
tab Female Under5, chi 
```

```


. use ATUS_full3.dta, clear

. tab Female Under5, chi 

 RECODE of |
     tesex |
  (Edited: |        Under5
      sex) |         0          1 |     Total
-----------+----------------------+----------
         0 |    56,965     12,924 |    69,889 
         1 |    71,677     18,371 |    90,048 
-----------+----------------------+----------
     Total |   128,642     31,295 |   159,937 

          Pearson chi2(1) =  91.1296   Pr = 0.000
```

## Step 4. Interpretation

Chi square is not a PRE measure (PRE - proportional reduction of error), so you cannot tell the strength of the association between the two variables just by looking at the chi. But by using chi-squared test and its significance we can say a bit about existence of the relation between the two variables.

Thus in the results above the chi square with 1 degree of freedom is 91.1296, and it's p-value is rounded to 0.000. If we choose the alpha-level 0.001 (you can also choose 0.05, 0.01, etc.), we can say that:

The p-value provides us with enough evidence to reject the null hypothesis of statistical independence.

We are 99.9% ($(1-\alpha-level)*100$) confident that we can reject the null hypothesis. 
OR 
There is only 0.1% ($\alpha-level*100$) chance that the relation between `dependent variable` and `independent variable` is due to chance.

Therefore, we conclude that:

The two variables are associated, i.e., they are not statistically independent.

## Alternative Step 3. Chi-squared test, non-significant results

Let's use the same test but comparing whether we have more Females oversampled on the weekends.


```stata
tab Weekday Female, chi
```

```


. use ATUS_full3.dta, clear

. tab Weekday Female, chi

 RECODE of |
tudiaryday |
   (Day of |
  the week |
  of diary |
  day (day |
    of the |    RECODE of tesex
week about |     (Edited: sex)
    which  |         0          1 |     Total
-----------+----------------------+----------
         0 |    35,062     45,306 |    80,368 
         1 |    34,827     44,742 |    79,569 
-----------+----------------------+----------
     Total |    69,889     90,048 |   159,937 

          Pearson chi2(1) =   0.3311   Pr = 0.565
```

## Step 4. Interpretation

In the output above, the chi square with 1 degree of freedom is 0.3311 and it's p-value is rounded to 0.565. If we choose the alpha-level 0.05 (or any other conventional level), we can say that:

The p-value does not provide us with enough evidence to reject the null hypothesis of statistical independence.

We don't have enough evidence to reject the null hypothesis at 0.05 level. 

Therefore, we conclude that:

We don't have enough evidence to suggest that these two variables are associated.
