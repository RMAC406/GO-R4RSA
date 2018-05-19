---
title: "Data Structures"
teaching: 40
exercises: 15
questions:
- "How can I read data in R?"
- "What are the basic data types in R?"
- "How do I represent categorical information in R?"
objectives:
- "To be aware of the different types of data."
- "To begin exploring data frames, and understand how they are related to vectors, factors and lists."
- "To be able to ask questions from R about the type, class, and structure of an object."
keypoints:
- "Use `read.csv` to read tabular data in R."
- "The basic data types in R are double, integer, complex, logical, and character."
- "Use factors to represent categories in R."
source: Rmd
---

```{r, include=FALSE}
source("../bin/chunk-options.R")
knitr_fig_path("04-")

# Introduction to the Gapminder Data Set

For this Software Carpentry Workshop we will be working with the Gapminder data set. This data  set contains population size, life expectancy and GDP per capita for many countries over time. This data set will allow us to explore data handling and manipulation techniques in R.

### Save the data in the data directory

Now we have a good directory structure we will now place/save the data file in the `data/` directory.


Download the gapminder data from [here](https://raw.githubusercontent.com/resbaz/r-novice-gapminder-files/master/data/gapminder-FiveYearData.csv).

1. Download the file (CTRL + S, right mouse click -> "Save as", or File -> "Save page as")
2. Make sure it's saved under the name `gapminder-FiveYearData.csv`
3. Save the file in the `data/` folder within your project.



It is useful to get some general idea about the dataset, directly from the
command line (i.e. UNIX shell), before loading it into R. Understanding the dataset better
will come in handy when making decisions on how to load it in R. Use the command-line
shell to answer the following questions:
1. What is the size of the file?
```
ls -lh data/gapminder-FiveYearData.csv
```
2. How many rows of data does it contain?
```
wc -l data/gapminder-FiveYearData.csv
```
3. What kinds of values are stored in this file?
```
 head data/gapminder-FiveYearData.csv
```


 ## Load the data into R studio
 One of R's most powerful features is its ability to deal with tabular data -
 such as you may already have in a spreadsheet or a CSV file. The `read.table` function is used for reading in tabular data stored in a text file where the columns of data are separated by punctuation characters such as CSV files (csv = comma-separated values). Tabs and commas are the most common punctuation characters used to separate or delimit data points in csv files.
 For convenience R provides 2 other versions of `read.table`. These are: `read.csv`
 for files where the data are separated with commas and `read.delim` for files
 where the data are separated with tabs. Let's start by loading the gapminder data set:

 ```
 gapminder <- read.csv(file = "gapminder.csv")
 gapminder
 ```
 Here the first 166 lines are shown, and 1538 additional lines are not shown. To view the entire dataset in tabular form use View().
 ```
 View(gapminder) #note uppercase 'V'
 ```
The tabular view makes it a little easier to see that this data set is organized in "wide" format, meaning that each row contains a data point, and each column contains various information pertaining to that sample.
## Introduction to Data Types and Structures
 We can begin exploring our dataset right away, lets look first at the structure of our data set:
```{r}
str(gapminder)
```
This output gives us a lot of useful information:
First, the "gapminder" data set is a Data Frame, which is on of the data structures that R can handle.
Next, there appear to be 1704 rows (observations) and 6 columns (each containing a variable)
Each variable is then listed after the `$` sign, following the variable name we get some information about each column.
 - Data type
 - Some idea of what the values are

In R there are 5 main data types:

 - integer: contains integers (i.e. whole numbers as you would expect)
 - numeric: floating point numbers (also called 'double')
 - complex: numeric including imaginary numbers (i)
 - logical: `TRUE` or `FALSE`
 - character: letter(s), numbers(s), word(s)
To determine which data type a value or vector is, use class()
```{r}
x<-(2)
class(x)
```

 > ## Tip: Data Types
 >
 > The definition of data types listed above seem straight forward, but confusion (and error messages) can arise when unintended data types are assigned.
 > the value `2` could be stored as an integer, numeric, complex, or a character.
 > To convert a value to an integer:
 > ```
 > as.integer(value)
 > ```
 > To convert a value to numeric:
 > ```
 > as.numeric(value)
 > ```
 > To convert a value to a character:
 > ```
 > as.character(value)
 > ```
 > There is an order of 'strictness' by definition: any entry can be a 'character' but only specific values can be integers.
 > ```{r}
 > as.integer("test")
 > ```
 >
 {: .callout}

## Vectors

Vectors in R can take on any *one* of the above data types (one variable-- one data type). A data frame (like gapminder) is a collection of variables (in a certain order), each variable can hold a different data type.

## Other Data Structures

The simplest data structure in R is a **list**, which is essentially a vector, or collection of values in a specific order. Every value in a list must be of the same type (i.e. all integers, or all characters, not a combination)

A **Data Frame** is a collection of lists, these lists are in a certain order and are useful for storing tabular data. Think of each list as a column in a spreadsheet, because each one is ordered, each row can contain different information about each data point. Although each column/list must contain a single data type, differnet columns can contain different data types (e.g. Column 1: integers, Column 2: characters, Column 3: logical...).

Data in R can also be stored as a **matrix**, which is similar to a data frame, except that all variables must be of the same data type (i.e. every value is an integer, or numeric or which ever), and not a combination of data types. Additionally R can define an **array** which is similar to a matrix in that all values must be of the same type, but allows higher dimensions (matrices are limited to 2 dimensions).

Additionally, data types can be **factored**, which groups the values within a variable into a finite number of *factors*. For example, think about a variable full of integers, this could contain data such as test scores (i.e. values range 0-100) or group the observations (i.e.students) in to belonging to 'classroom 1' or 'classroom 2.'

> ## Tip: Factors
>
> A variety of unexpected things (though mostly error messages and goofy plots) can occur when variables are not treated as factors when they should be (or vice versa).
> To convert a variable to a factor:
> ```
> as.factor(variable-name)
> ```
> To convert a factored variable to character:
> ```
> as.character(factored-variable-name)
> ```
> ```
> as.numeric(factored-variable-name)
> ```
{: .callout}

## Data set descriptions

So if we look here at the output from `str(gapminder)`` it looks like 5 continents are represented. Which continents are listed here? To pull the values from one column (i.e. the continent column) we will use <kbd>$</kbd> operator
```
gapminder$continent
```
```{r echo=false}
tail(gapminder$continent)
```
This displays many of the entries, then gets cut-off. We can see that each of these values get repeated numerous times in the data set so they appear in this printout several times. To view the unique instances for this factored variable use  `unique()`

```
unique(gapminder$continent)
```
Another very useful function for examining data sets is `length()`

```{r}
length(gapminder$continent)
```
