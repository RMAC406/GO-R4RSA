---
title: "Introduction to R and RStudio"
teaching: 60
exercises: ?
questions:
- "How to find your way around RStudio?"
- "How to interact with R?"
- "How to manage your environment?"
- "How to install packages?"
- "How can we use R studio to help stay organized?"
objectives:
- "Describe the purpose and use of each pane in the RStudio IDE"
- "Locate buttons and options in the RStudio IDE"
- "Define a variable"
- "Assign data to a variable"
- "Manage a workspace in an interactive R session"
- "Use mathematical and comparison operators"
- "Call functions"
- "Manage packages"
- "Create a self-contained project in R Studio for analyzing the data in the SWC session"
keypoints:
- "Use RStudio to write and run R programs."
- "R has the usual arithmetic operators and mathematical functions."
- "Use `<-` to assign values to variables."
- "Use `ls()` to list the variables in a program."
- "Use `rm()` to delete objects in a program."
- "Use `install.packages()` to install packages (libraries)."
- "Use RStudio to create and manage projects with consistent layout."
- "Treat raw data as read-only."
- "Treat generated output as disposable."


```{r, include=FALSE}
source("../bin/chunk-options.R")
knitr_fig_path("02-")
```

## Motivation

Science is a multi-step process: once you've designed an experiment and collected
data, the real fun begins! This lesson will teach you how to start this process using
R and RStudio. We will begin with raw data, perform exploratory analyses, and learn
how to plot results graphically. This example starts with a dataset from
[gapminder.org](https://www.gapminder.org) containing population, life expectancy and
GDP per capita information for many countries through time. We will use this example data
set to illustrate the power and basic functionality of the R programing language
using R studio. R studio is an integrated development environment (IDE) that provides
many helpful tools, some of which we will be using. R studio is not necessary, in fact
all of what we will be doing could be done straight from the command line similar to how we
interacted with BASH in the UNIX lesson.
In this lesson, we will:
* Open Rstudio and have a quick look around
* Load the gapminder data set
* Examine the structure and contents of the data set
* Make a plot to look at the relationship between life expectancy and GDP per capita
* Customize the appearance of plots
* Save plots as .pdf files
* Create reports to save code, comments, R output and plots.


## Before Starting The Workshop

Please ensure you have the latest version of R and RStudio installed on your machine.
This is important, as some packages used in the workshop may not install correctly
(or at all) if R is not up to date.

[Download and install the latest version of R here](https://www.r-project.org/)
[Download and install RStudio here](https://www.rstudio.com/)

## Introduction to RStudio

Welcome to the R portion of the Software Carpentry workshop.

Throughout this lesson, we're going to teach you some of the fundamentals of
the R language as well as some best practices for organizing code for
scientific projects that will make your life easier.

We'll be using RStudio: a free, open source R integrated development
environment. It provides a built in editor, works on all platforms (including
on servers) and provides many advantages such as integration with version
control and project management.


**Basic layout**

When you first open RStudio, you will be greeted by three panels:

  1. The interactive R console (entire left)
  2. Environment/History (tabbed in upper right)
  3. Files/Plots/Packages/Help/Viewer (tabbed in lower right)

![RStudio layout](../figure1)

Once you open files, such as R scripts (file > new file > script), an editor panel
will also open in the top left, giving us four panels, the R console is now on the
bottom left.

1. The Rscript: this is basically a text file that you can type into and save on
your computer.
The scripts you write here will be available to run again in the future.
 interactive R console (entire left)
2. Environment/History (tabbed in upper right)
3. The interactive R console (bottom left)
4. Files/Plots/Packages/Help/Viewer (tabbed in lower right)

![RStudio layout with .R file open](../fig/01-rstudio-script.png)


## Work flow within RStudio
There are two main ways you can work within RStudio.

1. Test and play within the interactive R console then copy code into
a .R file to run later.
   *  This works well when doing small tests and initially starting off.
   *  It quickly becomes laborious
2. Start writing in an .R file and use RStudio's short cut keys for the Run command
to push the current line, selected lines or modified lines to the
interactive R console.
   * This is a great way to start; all your code is saved for later
   * You will be able to run the file you create from within RStudio
   or using R's `source()`  function.
   * The line of code that the cursor is on can be run with the shortcut: `Control` + `Enter`
   * To run multiple lines of code, highlight the selection and press `Control` + `Enter`
   * On OS X use `&#8984`+`Enter`

> ## Tip: Running segments of your code
>
> RStudio offers you great flexibility in running code from within the editor
> window. There are buttons, menu choices, and keyboard shortcuts. To run the
> current line, you can
> 1. click on the `Run` button above the editor panel, or
> 2. select "Run Lines" from the "Code" menu, or
> 3. hit <kbd>Ctrl</kbd>+<kbd>Return</kbd> in Windows or Linux
> or <kbd>&#8984;</kbd>+<kbd>Return</kbd> on OS X.
> (This shortcut can also be seen by hovering
> the mouse over the button). To run a block of code, select it and then `Run`.
> If you have modified a line of code within a block of code you have just run,
> there is no need to reselct the section and `Run`, you can use the next button
> along, `Re-run the previous region`. This will run the previous code block
> including the modifications you have made.
{: .callout}

## Introduction to R

Much of your time in R will be spent in the R interactive
console. This is where you will run all of your code, and can be a
useful environment to try out ideas before adding them to an R script
file. This console in RStudio is the same as the one you would get if
you typed in `R` in your command-line environment.

The first thing you will see in the R interactive session is a bunch
of information, followed by a ">" and a blinking cursor. In many ways
this is similar to the shell environment you learned about during the
shell lessons: it operates on the same idea of a "Read, evaluate,
print loop": you type in commands, R tries to execute them, and then
returns a result.

## Using R as a calculator

The simplest thing you could do with R is do arithmetic:

```{r}
1 + 100
```

And R will print out the answer, with a preceding "[1]". Don't worry about this.
For now think of it as indicating output.

Like bash, if you type in an incomplete command, R will wait for you to
complete it:

~~~
> 1 +
~~~
{: .r}

~~~
+
~~~
{: .output}

Any time you hit return and the R session shows a "+" instead of a ">", it
means it's waiting for you to complete the command. If you want to cancel
a command you can simply hit "Esc" and RStudio will give you back the ">"
prompt.

> ## Tip: Cancelling commands
>
> If you're using R from the commandline instead of from within RStudio,
> you need to use <kbd>Ctrl</kbd>+<kbd>C</kbd> instead of <kbd>Esc</kbd>
> to cancel the command. This applies to Mac users as well!
>
> Cancelling a command isn't only useful for killing incomplete commands:
> you can also use it to tell R to stop running code (for example if it's
> taking much longer than you expect), or to get rid of the code you're
> currently writing.
>
{: .callout}

When using R as a calculator, the order of operations is the same as you might
expect: from highest to lowest precedence:

 - Parentheses: `(`, `)`
 - Exponents: `^` or `**`
 - Divide: `/`
 - Multiply: `*`
 - Add: `+`
 - Subtract: `-`

```{r}
3 + 5 * 2
```

Use parentheses to group operations in order to force the order of
evaluation if it differs from the default, or to make clear what you
intend.

```{r}
(3 + 5) * 2
```


> ## Tip: Comments
>
> Text can be added after a line of code to "comment" on the code, without being
> executed. Anything that follows after the hash (or pound or octothorpe) symbol
> `#` is ignored by R when it executes code.
>
{: .callout}



## Mathematical functions

R has many built in mathematical functions. To call a function,
we simply type its name, followed by  open and closing parentheses.
Anything we type inside the parentheses is called the function's
arguments:

```{r}
sin(1)  # trigonometry functions
```

```{r}
log(10)  # natural logarithm
```


Don't worry about trying to remember every function in R. You
can look them up on online, or if you can remember the
start of the function's name, use the tab completion in RStudio.

One advantage that RStudio has over R on its own, it
has auto-completion abilities that allow you to more easily
look up functions, their arguments, and the values that they
take.

Typing a `?` before the name of a command will open the help page
for that command. As well as providing a detailed description of
the command and how it works, scrolling to the bottom of the
help page will usually show a collection of code examples which
illustrate command usage. We'll go through an example later.

> ## Getting help
>
> There are many ways to get help:
>
> - Typing a `?` before the name of a command will open the help page
for that command.
> - Tab complete can be useful if you know how the command starts
> - Internet search
>
{: .callout}

## Comparing things (logical operators)

We can also do comparison in R:

```{r}
1 == 1  # equality (note two equals signs, read as "is equal to")
```

```{r}
1 != 2  # inequality (read as "is not equal to")
```

```{r}
1 < 2  # less than
```

```{r}
1 <= 1  # less than or equal to
```

```{r}
1 > 0  # greater than
```

```{r}
1 >= -9 # greater than or equal to
```
The output for each of these functions will be either TRUE or FALSE
> ## Tip: Comparing Numbers
>
> A word of warning about comparing numbers: you should
> not use `==` to compare two numbers unless they are
> integers (a data type which can specifically represent
> only whole numbers).
>
> Computers may only represent decimal numbers with a
> certain degree of precision, so two numbers which look
> the same when printed out by R, may actually have
> different underlying representations and therefore be
> different by a small margin of error (called Machine
> numeric tolerance).
>
> Instead you should use the `all.equal` function.
> ```{r}
> all.equal(1.2, 1.2)
> ```
> Further reading: [http://floating-point-gui.de/](http://floating-point-gui.de/)
>
{: .callout}

## Variables and assignment

We can store values in variables using the assignment operator `<-`, like this:

```{r}
x <- 1/40
```

Notice that assignment does not print a value. Instead, we stored it for later
in something called a **variable**. `x` now contains the **value** `0.025`:

```{r}
x
```

More precisely, the stored value is a *decimal approximation* of
this fraction called a [floating point number](http://en.wikipedia.org/wiki/Floating_point).

Look for the `Environment` tab in the upper right panel of RStudio, and you will see that `x` and its value
have appeared. Our variable `x` can be used in place of a number in any calculation that expects a number:

```{r}
log(x)
```

Notice also that variables can be reassigned:

```{r}
x <- 100
```

`x` used to contain the value 0.025 and and now it has the value 100.

Assignment values can contain the variable being assigned to:

```{r}
x <- x + 1
y <- x * 2
```

The right hand side of the assignment can be any valid R expression.
The right hand side is *fully evaluated* before the assignment occurs.

Variable names can contain letters, numbers, underscores and periods. They
cannot start with a number nor contain spaces at all. Different people use
different conventions for long variable names, these include

  * periods.between.words
  * underscores\_between_words
  * camelCaseToSeparateWords

What you use is up to you, but **be consistent**.

It is also possible to use the `=` operator for assignment:

```{r}
x = 1/40
```

But this is much less common among R users.  The most important thing is to
**be consistent** with the operator you use. There are occasionally places
where it is less confusing to use `<-` than `=`, and it is the most common
symbol used in the community. So the recommendation is to use `<-`.

> ## Challenge 1
>
> Which of the following are valid R variable names?
> ```{r}
> min_height
> max.height
> _age
> .mass
> MaxLength
> min-length
> 2widths
> celsius2kelvin
> ```
>
> > ## Solution to challenge 1
> >
> > The following can be used as R variables:
> >
> > ```{r ch1pt1-sol, eval=FALSE}
> > min_height
> > max.height
> > MaxLength
> > celsius2kelvin
> > ```
> >
> > The following creates a hidden variable:

> > ```{r}
> > .mass
> > ```
> >
> > The following will not be able to be used to create a variable
> > ```{r ch1pt3-sol, eval=FALSE}
> > _age
> > min-length
> > 2widths
> > ```
> {: .solution}
{: .challenge}

> ## Challenge 2
>
> What will be the value of each  variable  after each
> statement in the following program?
>
> ```{r, eval=FALSE}
> mass <- 47.5
> age <- 122
> mass <- mass * 2.3
> age <- age - 20
> ```
>
> > ## Solution to challenge 2
> >
> > ```{r ch2pt1-sol}
> > mass <- 47.5
> > ```
> > This will give a value of `r mass` for the variable mass
> >
> > ```{r ch2pt2-sol}
> > age <- 122
> > ```
> > This will give a value of `r age` for the variable age
> >
> > ```{r ch2pt3-sol}
> > mass <- mass * 2.3
> > ```
> > This will multiply the existing value of `r mass/2.3` by 2.3 to give a new value of
> > `r mass` to the variable mass.
> >
> > ```{r ch2pt4-sol}
> > age <- age - 20
> > ```
> > This will subtract 20 from the existing value of `r age + 20 ` to give a new value
> > of `r age` to the variable age.
> {: .solution}
{: .challenge}

> ## Challenge 3
>
> Run the code from the previous challenge, and write a command to
> compare mass to age. Is mass larger than age?
>
> > ## Solution to challenge 3
> >
> > One way of answering this question in R is to use the `>` to set up the following:
> > ```{r ch3-sol}
> > mass > age
> >```
> > This should yield a boolean value of TRUE since `r mass` is greater than `r age`.
> {: .solution}
{: .challenge}

## Vectorization

One final thing to be aware of is that R is *vectorized*, meaning that
variables and functions can have vectors as values. In R, a vector is a set of values of
the same data type, that are placed in a specific order. Functions can be performed on
every value in the vector.

```{r}
1:5 # colon notation indicates successive numbers
2^(1:5) # operations can be performed on every value in the vector
x <- 1:5
2^x
c(1,3,5,7) #vectors can be defined specifically using c()
```

In R a function can be called on every component of a list without a 'for loop'


## Managing your environment

There are a few useful commands you can use to interact with the R session.

`ls` will list all of the variables and functions stored in the global environment
(your working R session):

```{r}
ls()
```

Note here that we didn't give any arguments to `ls`, but we still
needed to give the parentheses to tell R to call the function.


You can use `rm` to delete objects you no longer need:

```{r}
rm(x)
```

## R Packages

It is possible to add functions to R by writing a package, or by
obtaining a package written by someone else. As of this writing, there
are over 10,000 packages available on CRAN (the comprehensive R archive
network). R and RStudio have functionality for managing packages:

* You can see what packages are installed by typing
  `installed.packages()`
* You can install packages by typing `install.packages("packagename")`,
  where `packagename` is the package name, in quotes.
* You can update installed packages by typing `update.packages()`
* You can remove a package with `remove.packages("packagename")`
* You can make a package available for use with `library(packagename)`



> ## Challenge 4
>
> Install the following packages: `ggplot2`, `plyr`, `gridExtra`
>
> > ## Solution to challenge 4
> >
> > We can use the `install.packages()` command to install the required packages.
> > ```{r ch5-sol, eval=FALSE}
> > install.packages("ggplot2")
> > library("ggplot2")
> > install.packages("plyr")
> > library("plyr")
> > install.packages("gridExtra")
> > library("gridExtra")
> >```
> {: .solution}
{: .challenge}





## Introduction

The scientific process is naturally incremental, and many projects
start life as random notes, some code, then a manuscript, and
eventually everything is a bit mixed together.

<blockquote class="twitter-tweet"><p>Managing your projects in a reproducible fashion
doesn't just make your science reproducible, it makes your life easier.</p>— Vince Buffalo
(@vsbuffalo) <a href="https://twitter.com/vsbuffalo/status/323638476153167872">April 15, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Most people tend to organize their projects like this:

![](../fig/bad_layout.png)

There are many reasons why we should *ALWAYS* avoid this:

1. It is really hard to tell which version of your data is
the original and which is the modified;
2. It gets really messy because it mixes files with various
extensions together;
3. It probably takes you a lot of time to actually find
things, and relate the correct figures to the exact code
that has been used to generate it;

A good project layout will ultimately make your life easier:

* It will help ensure the integrity of your data;
* It makes it simpler to share your code with someone else
(a lab-mate, collaborator, or supervisor);
* It allows you to easily upload your code with your manuscript submission;
* It makes it easier to pick the project back up after a break.

## A possible solution

Fortunately, there are tools and packages which can help you manage your work effectively.

One of the most powerful and useful aspects of RStudio is its project management
functionality. We'll be using this today to create a self-contained, reproducible
project.

> ## Tip: R studio (and other programs) can not replace diligent organization!
>
> There are numerous programs (including R Studio) that can help to organize and
manage projects. However there is no replacement for good data habits. Some good practices include:
> - Consistent directory organization
> - Consistent and descriptive file names
> - Version  Control
>
> In both cases, the message that R prints out usually give you clues
> how to fix a problem.
>
{: .callout}

> ## Challenge: Creating a self-contained project
>
> We're going to create a new project in RStudio:
>
> 1. Click the "File" menu button, then "New Project".
> 2. Click "New Directory".
> 3. Click "Empty Project".
> 4. Type in the name of the directory to store your project, e.g. "SWC-2018-May_GapminderAnalysis"
> 5. Click the "Create Project" button.
{: .challenge}

Now when we start R in this project directory, or open this project with RStudio,
all of our work on this project will be entirely self-contained in this directory.

## Best practices for project organization

Although there is no "best" way to lay out a project, there are some general
principles to adhere to that will make project management easier:

### Treat data as read only

This is probably the most important goal of setting up a project. Data is
typically time consuming and/or expensive to collect. Working with them
interactively (e.g., in Excel) where they can be modified means you are never
sure of where the data came from, or how it has been modified since collection.
It is therefore a good idea to treat your data as "read-only".

### Data Cleaning

In many cases your data will be "dirty": it will need significant preprocessing
to get into a format R (or any other programming language) will find useful. This
task is sometimes called "data munging". I find it useful to store these scripts
in a separate folder, and create a second "read-only" data folder to hold the
"cleaned" data sets.

### Treat generated output as disposable

Anything generated by your scripts should be treated as disposable: it should
all be able to be regenerated from your scripts.

There are lots of different ways to manage this output. I find it useful to
have an output folder with different sub-directories for each separate
analysis. This makes it easier later, as many of my analyses are exploratory
and don't end up being used in the final project, and some of the analyses
get shared between projects.

> ## Tip: Good Enough Practices for Scientific Computing
>
> [Good Enough Practices for Scientific Computing](https://github.com/swcarpentry/
> good-enough-practices-in-scientific-computing/blob/gh-pages/good-enough-practices-
> for-scientific-computing.pdf) gives the following recommendations for project organization:
>
> 1. Put each project in its own directory, which is named after the project.
> 2. Put text documents associated with the project in the `doc` directory.
> 3. Put raw data and metadata in the `data` directory, and files generated during
> cleanup and analysis in a `results` directory.
> 4. Put source for the project's scripts and programs in the `src` directory,
> and programs brought in from elsewhere or compiled locally in the `bin` directory.
> 5. Name all files to reflect their content or function.
>
{: .callout}



> ## Tip: Avoiding Duplication
> You may find yourself using data or analysis scripts across several projects.
> Reusable chunks of code can be get pulled into their own functions. These functions
> that you'll reuse across analyses and projects should be stored separately.
> Typically you want to avoid duplication to save space and avoid having to make
> updates to code in multiple places.
> In this case I find it useful to make "symbolic links", which are essentially
> shortcuts to files somewhere else on a filesystem. On Linux and OS X you can
> use the `ln -s` command, and on Windows you can either create a shortcut or
> use the `mklink` command from the windows terminal.
{: .callout}
