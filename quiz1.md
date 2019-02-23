---
title: "Data Science Capstone"
subtitle: "Quiz 1: Getting Started"
author: "Thomas Neitmann"
output:
  prettydoc::html_pretty:
    keep_md: yes
    theme: architect
---




```r
files = list.files("final/en_US", full.names = TRUE)
text = lapply(files, readr::read_lines, progress = FALSE)
files
```

```
## [1] "final/en_US/en_US.blogs.txt"   "final/en_US/en_US.news.txt"   
## [3] "final/en_US/en_US.twitter.txt"
```

## Question 1

The `en_US.blogs.txt` file is how many megabytes?


```r
fileSize = file.info(files[1L])$size
format(fileSize, big.mark = ",", scientific = F)
```

```
## [1] "210,160,014"
```


## Question 2

The `en_US.twitter.txt` has how many lines of text?


```r
nLines = length(text[[3L]])
format(nLines, big.mark = ",")
```

```
## [1] "2,360,148"
```


## Question 3

What is the length of the longest line seen in any of the three en_US data sets?


```r
numChar = lapply(text, function(t) max(nchar(t)))
names(numChar) = files
numChar
```

```
## $`final/en_US/en_US.blogs.txt`
## [1] 40833
## 
## $`final/en_US/en_US.news.txt`
## [1] 11384
## 
## $`final/en_US/en_US.twitter.txt`
## [1] 140
```


## Question 4

In the en_US twitter data set, if you divide the number of lines where the word "love" (all lowercase) occurs by the number of lines the word "hate" (all lowercase) occurs, about what do you get?


```r
loveFreq = sum(grepl("love", text[[3L]]))
hateFreq = sum(grepl("hate", text[[3L]]))
ratio = loveFreq / hateFreq
format(ratio, digits = 0)
```

```
## [1] "4"
```


## Question 5

The one tweet in the en_US twitter data set that matches the word "biostats" says what?


```r
biostatsIndex = which(grepl("biostats", text[[3L]]))
text[[3L]][biostatsIndex]
```

```
## [1] "i know how you feel.. i have biostats on tuesday and i have yet to study =/"
```


## Question 6

How many tweets have the exact characters "A computer once beat me at chess, but it was no match for me at kickboxing". (I.e. the line matches those characters exactly.)


```r
string = "^A computer once beat me at chess, but it was no match for me at kickboxing$"
sum(grepl(string, text[[3L]]))
```

```
## [1] 3
```
