---
title: "R Notebook - Data Wrangling - dplyr"
output: github_document
  
---

##dplyr agenda

--Basics   
--select()   
--filter()    
--arrange()    
--mutate()    
--summarize()    
--group_by()    

-----     

###Prerequisites
```{r, message=FALSE}
library(dplyr)
library(ggplot2)
```


-----    

###Basics
```{r}
tibble <- tbl_df(diamonds) #Convert diamonds dataset into tbl_df
head(tibble) #View first 6 rows
```

```{r}
dim(tibble) #Check the dimensions of the dataset
```

-----     

###select()

#####select a subset of columns, and in a specified order
```{r}
select(tibble, color, cut)
```

#####select a subset of columns, and by specifying a sequence of columns by name
```{r}
select(tibble, clarity:price)
```

#####select a subset of columns, and by specifying columns to omit from the full dataset
```{r}
select(tibble, -carat) #Select all columns except the carat column
```
```{r}
select(tibble, -(carat:clarity)) #Select all columns except the named sequence of columns carat:clarity
```

-----     

###filter()

#####filter dataset to return a subset of rows
```{r}
filter(tibble, cut == "Premium") #Select rows representing only Premium cut diamonds
```

#####filter dataset to return subset of rows based on multiple conditions
```{r}
filter(tibble, cut == "Premium", color == "D") #Select rows representing only diamonds of Premium cut AND D color classification 
```

```{r}
filter(tibble, carat > 1.0000, price < 5000) #Select rows representing only diamonds of carat over 1.0000 AND price less than 5000
```

```{r}
filter(tibble, carat > 1.0000 | price < 5000) #Select rows representing only diamonds of carat over 1.0000 OR price less than 50000
```

#####filter dataset to return rows which with/out NA values
```{r}
filter(tibble, is.na(cut)) #Select rows representing diamonds which have NA values for cut
```

```{r}
filter(tibble, !is.na(cut)) #Select rows representing diamonds which do NOT have NA values for cut
```

-----     

###arrange()

#####arrange rows based on particular values of a variable
```{r}
arrange(tibble, color) #Arrange rows based on their color classification, default order is  ascending 
```

```{r}
arrange(tibble, desc(color)) #Arrange rows based on their color classification, specifying in descending order
```

```{r}
arrange(tibble, desc(color), desc(carat)) #Arrange rows based first on their color classification, specifying in descending order, and then within the same color classification, ordered by their carat value, specifying in descending order
```

-----     

###mutate()

#####creates & adds new variables 
```{r}
mutate(tibble, euro_price = price*0.9) #Create new variable euro_price based on existing price variable
```

-----     

###summarize()

######collapse the dataset into a single row
```{r}
summarize(tibble, mean(carat)) #Summarizes mean statistic for carat variable
```

-----     

###group_by()

#####group dataset by some ^attribute, and then summarize
```{r}
grouped <- group_by(tibble, cut) #Group dataset by cut classification and assign to object
summarize(grouped, count = n(), average_price = mean(price)) #Compute a count and average_price value for each cut classification, using the grouped data
```

```{r}
summarize(grouped, no_unique_prices = n_distinct(price)) #Compute the no. of unique prices for each cut classification, using the grouped data
```
