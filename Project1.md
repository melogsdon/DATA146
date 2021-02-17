# Project 1
#### **Question 1**: 

A Python package is a collection of executable modules and functions under a common namespace, indicated by the `.` used to call it. A library, on the other hand, is a collection of packages that may be imported into a file-- however, there may also be a library of functions inside a package that indicates a collection of functions rather than a collection of packages. 

Using a package and its library of functions requires that the user first install the package by importing it:

   `import pandas as pd`
   
   `import numpy`
   
Later, the user can call a function from the package's function library as though the function were created by the user, as long as the user specifies which package the function comes from.

   `example = pd.head()`
   
The `pd.` tells the computer to look for the function `head()` in the pandas package, which was imported under the alias `pd` above. 
If no alias had been given, the user would call it by its full name.

   `example = numpy.array(some_argument)`
   
As you can see, importing the package under an alias allows the user to access the functions inside it moore quickly and cleanly (as long as the alias is easy to remember!). 
Alii are especially helpful when using the package repeatedly!

#### **Question 2**: 

A dataframe is a (typically two-dimensional) data structure that organizes and allows clear presentation of a data set. In Python, the pandas package offers tools to process and analyze data by creating dataframes from data sets that may be either imported or created. 

pandas has a useful function `read_csv()` that allows a user to import the contents of an external file. It takes as an argument the path of the file to be imported, and may take an additional argument specifying the type of file if it is not a `.csv` extension. 

So, to import the file `my_data.csv` into the file in which I'm working, I would call the `read_csv()` function in pandas and pass the file path as an argument. Here, I will assume that `my_data.csv` is in the same directory as my current file and so I don't need to supply the full path.

~~~~
   import pandas as pd
   
   imported_data = pd.read_csv('my_data.csv')
~~~~

If the file `my_data.csv` had instead been `my_data.tsv`, indicating values separated by tabs instead of commas, I would need to pass in the argument `sep=` to tell the function 
to look for tabs. 

~~~~
   import pandas as pd
   
   imported_data = pd.read_csv('my_data.tsv', sep=`\t`)
~~~~

"my_data.tsv" contains data for the favorite colors of people in my family and the number of shirts they own in that color. If I want to get details about the average and mean of the number of favorite-colored shirts per person, I can use the `describe()` function that will return a chart containing calculations such as standard deviation, mean (average), maxima and minima, and more.

The `.shape` command (notice it has no parentheses!) returns the number of rows and columns in the dataframe, which may also be called features and targets. 

#### **Question 3**: 

The year variable contains the years for which data (population, life expectancy, GDP, etc) was recorded. A brief analysis of the years reveals that data was recorded every five years from 1952 and until 2007. In order to update the data to 2021, we would add two more entries after 2007, one in 2012 and one in 2017. 

#### **Question 4**: 

The lowest recorded life expetancy is from Rwanda in 1992, when it was just over 23 years old. This was possibly due to civil unrest and widespread violence-- in 1992, Rwanda was in the middle of a civil war that ended in the Rwandan genocide of 1994. 

#### **Question 5**: 

| Country | GDP (Nearest billion) |
| ------- | --- |
| Germany | 265B |
| France | 186B |
| Italy | 166B |
| Spain | 117B |


#### **Question 6**: 
You have been introduced to four logical operators thus far: &, ==, | and ^. Describe each one including its purpose and function. Provide an example of how each might be used in the context of programming.

- **&** 'and' operator:
- **==** indicates equivalence: returns True if two objects are equivalent, and False if they are not. 
   For ints, the '==' operator compares values. 
   
   ~~~~     
           a = 6
           b = (a==6) 
   ~~~~
       
    `b` is now True. If `a` were set equal to any other number, `b` would be False.
    For strings, this logical operator would compare character-by-character.
    
    ~~~~
           string = 'Morgan'
           a = string=='Morgan' # a is True.
           b = string=='morgan' # b is False.
           c = string=='bubble' # c is also False.
    ~~~~
        
- **|** inclusive or: 
- **^** exclusive or:

#### **Question 7**: 
**Describe the difference between .loc and .iloc. Provide an example of how to extract a series of consecutive observations from a data frame. Stretch goal: provide an example of how to extract all observations from a series of consecutive columns.**

#### **Question 8**: 
**Describe how an api works. Provide an example of how to construct a request to a remote server in order to pull data, write it to a local file and then import it to your current work session.**

#### **Question 9**: 

The pandas `apply()` function allows a particular function to be applied repeatedly throughough a dataframe. It allows users to specify which axis to apply the function (`axis=0` for rows and `axis=1` for columns). Instead of applying it to each individual "cell" within the dataframe, it allows operations to be performed in bulk. 

Alternatively, a user may execute a `for` loop to visit each cell in a series, though this is less preferable as it requires more lines of code. The `apply()` function essentially allows us to execute a `for` loop across the contents of a series, applying an operation to each item in the series as the function iterates through.  


#### **Question 10**: 
**Also describe an alternative approach to filtering the number of columns in a data frame. Instead of using .iloc, what other approach might be used to select, filter and assign a subset number of variables to a new data frame?**

Instead of using `iloc` to subset a number of variables to a new data frame, a user may prefer to use logical operators to group together and select for desired conditions.  






