---
title: Tidyverse Basics II

date: 2018-09-09T00:00:00.000Z
lastmod: 2018-09-09T00:00:00.000Z

draft: false
toc: true
type: docs


linktitle: Tidyverse Basics II
menu:
  tutorial:
    parent: Presidental Elections
    weight: 3
---




# Data exploration
There will be many instances in which you want to get an idea of what the people in your dataset look like. For instance, let's take a look at the gender and levels of education in the CCES dataset. There are two variables that we will work with:

- `gender` = Gender
- `educ` = Educational Attainment 


## Count of gender

```r
cces_data %>% # I want to look at the cces_data
  count(gender) # Show me a count of gender
```

```
## # A tibble: 2 x 2
##   gender     n
##   <ord>  <int>
## 1 Male   29531
## 2 Female 35069
```

## Another way
Here's another way to do it:


```r
cces_data %>% # I want to look at the cces_data
  group_by(gender) %>% # Group the data by gender 
  summarise(n = n()) # Give me a count
```

```
## # A tibble: 2 x 2
##   gender     n
##   <ord>  <int>
## 1 Male   29531
## 2 Female 35069
```



## Education?

```r
cces_data %>% # I want to look at the cces_data
  count(educ) # Show me a count of education
```

```
## # A tibble: 6 x 2
##   educ                     n
##   <ord>                <int>
## 1 No HS                 1971
## 2 High school graduate 16381
## 3 Some college         15685
## 4 2-year                7169
## 5 4-year               14884
## 6 Post-grad             8510
```

## Education another way
Here's another way:

```r
cces_data %>% # I want to look at the cces_data
  group_by(educ) %>% # Group the data by education 
  summarise(n = n()) # Give me a count
```

```
## # A tibble: 6 x 2
##   educ                     n
##   <ord>                <int>
## 1 No HS                 1971
## 2 High school graduate 16381
## 3 Some college         15685
## 4 2-year                7169
## 5 4-year               14884
## 6 Post-grad             8510
```


# What about both?

What if I want to see gender by education level? This will help us get an idea of the levels of education are consistent, or similar accross gender.

## Gender by Education


```r
cces_data %>% # I want to look at the cces_data
  count(gender, educ) # Show me a count of gender BY educational level
```

```
## # A tibble: 12 x 3
##    gender educ                     n
##    <ord>  <ord>                <int>
##  1 Male   No HS                  756
##  2 Male   High school graduate  6642
##  3 Male   Some college          7050
##  4 Male   2-year                2995
##  5 Male   4-year                7431
##  6 Male   Post-grad             4657
##  7 Female No HS                 1215
##  8 Female High school graduate  9739
##  9 Female Some college          8635
## 10 Female 2-year                4174
## 11 Female 4-year                7453
## 12 Female Post-grad             3853
```

## Gender by Education another way


```r
cces_data %>% # I want to look at the cces_data
  group_by(gender, educ) %>% # Group the data by gender then education
  summarise(n = n()) # Show me a count of gender BY educational level
```

```
## # A tibble: 12 x 3
## # Groups:   gender [2]
##    gender educ                     n
##    <ord>  <ord>                <int>
##  1 Male   No HS                  756
##  2 Male   High school graduate  6642
##  3 Male   Some college          7050
##  4 Male   2-year                2995
##  5 Male   4-year                7431
##  6 Male   Post-grad             4657
##  7 Female No HS                 1215
##  8 Female High school graduate  9739
##  9 Female Some college          8635
## 10 Female 2-year                4174
## 11 Female 4-year                7453
## 12 Female Post-grad             3853
```



# Proportions and Percents

This information is ok, but limited. Knowing that there are 756 males in the sample that have *No HS diploma*, is not that useful. What would be better is to know what **proportion** or **percentage** of males in the sample have no HS diploma. This is useful because the sample is nationally representative, meaning it is like a snapshot of the US population. So by using a proportion, we can get an idea of what the real US population looks like on this particular measure.

## Gender by Education Proportions

Look we can see that .22 or 22% of males in the CCES dataset have a HS diploma


```r
cces_data %>% # I want to look at the cces_data
  count(gender, educ) %>% # Show me a count of gender by educational level
  group_by(gender) %>% # I want to group by Gender, since I'm interested in the Proportion (percentage) of MALES
  mutate(proportion = n /sum(n)) # Create a variable that takes the raw count then divides it by the total for each gender.
```

```
## # A tibble: 12 x 4
## # Groups:   gender [2]
##    gender educ                     n proportion
##    <ord>  <ord>                <int>      <dbl>
##  1 Male   No HS                  756     0.0256
##  2 Male   High school graduate  6642     0.225 
##  3 Male   Some college          7050     0.239 
##  4 Male   2-year                2995     0.101 
##  5 Male   4-year                7431     0.252 
##  6 Male   Post-grad             4657     0.158 
##  7 Female No HS                 1215     0.0346
##  8 Female High school graduate  9739     0.278 
##  9 Female Some college          8635     0.246 
## 10 Female 2-year                4174     0.119 
## 11 Female 4-year                7453     0.213 
## 12 Female Post-grad             3853     0.110
```

## Gender by Education Proportions another way


```r
cces_data %>% # I want to look at the cces_data 
  group_by(gender,educ) %>% # I want to group by Gender, since I'm interested in the Proportion (percentage) of MALES
  summarise( n = n()) %>% # Give me a count
  mutate(proportion = n /sum(n)) # Create a variable that takes the raw count then divides it by the total for each gender.
```

```
## # A tibble: 12 x 4
## # Groups:   gender [2]
##    gender educ                     n proportion
##    <ord>  <ord>                <int>      <dbl>
##  1 Male   No HS                  756     0.0256
##  2 Male   High school graduate  6642     0.225 
##  3 Male   Some college          7050     0.239 
##  4 Male   2-year                2995     0.101 
##  5 Male   4-year                7431     0.252 
##  6 Male   Post-grad             4657     0.158 
##  7 Female No HS                 1215     0.0346
##  8 Female High school graduate  9739     0.278 
##  9 Female Some college          8635     0.246 
## 10 Female 2-year                4174     0.119 
## 11 Female 4-year                7453     0.213 
## 12 Female Post-grad             3853     0.110
```






# What about the proportions/percentages?

Somtimes you don't need to know the full breakdown of education and you really just want to know for each gender, what level of education do **most** people in your data have? All we need to to get the level of education for each gender that has the largest proportion.

## Largest Proportion

Sweet! This tells you that most of the males in the dataset have a 4-year degree, while most of the females in the dataset are high school graduates.


```r
cces_data %>% # I want to look at the CCES dataset 
  group_by(gender, educ) %>% # Group by gender and education level
  summarise(n = n()) %>% # give me a count
  mutate(proportion = n /sum(n)) %>% # give me the proportion
  top_n(1) # give me the top proportion for each gender
```

```
## Selecting by proportion
```

```
## # A tibble: 2 x 4
## # Groups:   gender [2]
##   gender educ                     n proportion
##   <ord>  <ord>                <int>      <dbl>
## 1 Male   4-year                7431      0.252
## 2 Female High school graduate  9739      0.278
```

## Largest Proportion another way

```r
cces_data %>% # I want to look at the CCES dataset 
  count(gender, educ) %>% # Group by gender and education level
  group_by(gender) %>% # give me a count
  mutate(proportion = n /sum(n)) %>% # give me the proportion
  top_n(1) # give me the top proportion for each gender
```

```
## Selecting by proportion
```

```
## # A tibble: 2 x 4
## # Groups:   gender [2]
##   gender educ                     n proportion
##   <ord>  <ord>                <int>      <dbl>
## 1 Male   4-year                7431      0.252
## 2 Female High school graduate  9739      0.278
```

## Smallest Proportion

We can also do the smallest proportion too! Looks like for both males and females, those with NO HS diploma make up the smallest proportion of each group.


```r
cces_data %>% # I want to look at the CCES dataset 
  count(gender, educ) %>% # Group by gender and education level
  group_by(gender) %>% # give me a count
  mutate(proportion = n /sum(n)) %>% # give me the proportion
  top_n(-1) # give me the smallest proportion for each gender
```

```
## Selecting by proportion
```

```
## # A tibble: 2 x 4
## # Groups:   gender [2]
##   gender educ      n proportion
##   <ord>  <ord> <int>      <dbl>
## 1 Male   No HS   756     0.0256
## 2 Female No HS  1215     0.0346
```


