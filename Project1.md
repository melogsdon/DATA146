# Project 1
#### **Question 1**: 

A Python package is a collection of executable modules and functions under a common namespace, indicated by the `.` used to call it. A library, on the other hand, is a collection of packages that may be imported into a file-- however, there may also be a library of functions inside a package that indicates a collection of functions rather than a collection of packages. 

Using a package and its library of functions requires that the user first install the package by importing it:
~~~~
   import pandas as pd
   
   import numpy
~~~~
   
Later, the user can call a function from the package's function library as though the function were created by the user, as long as the user specifies which package the function comes from.

~~~~
   example = pd.head()
~~~~
   
The `pd.` tells the computer to look for the function `head()` in the pandas package, which was imported under the alias `pd` above. 
If no alias had been given, the user would call it by its full name.

~~~~
   example = numpy.array(some_argument)
~~~~
   
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

- & : Bitwise "and" operator: if both of two bits are 1, set each bit to 1. In essence, "True" if both of two conditionals are True. (*Note: parentheses must be used about each conditional, as shown below.)
   ~~~~
         a = 6
         b = 8
         c = ((a==6) & (b==8)) # c is True because (a==6) and (b==8) are both True.
   ~~~~

- == : indicates equivalence: returns True if two objects are equivalent, and False if they are not. 
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
        
- &#124; : Bitwise "inclusive or": Each bit is set to 1 if one of the two bits is 1. A pair of conditionals is considered True *either* if one value is True *or* if both are True.

   ~~~~
         a = 6
         b = 8
         c = ((a==6) | (b==9)) # c is True because (a==6) is True.        
         d = ((a==4) | (b==8)) # d is True because (b==8) is True.        
         e = ((a==6) | (b==8)) # e is True because both (a==6) and (b==8) are True.
         f = ((a==4) | (b==9)) $ f is False because neither (a==4) nor (b==9) is True.
   ~~~~

- ^ : Bitwise "exclusive or": Each bite is set to 1 if and only if one bit is equal to 1. A pair of conditionals is considered True if and only if one of the two values is True.

   ~~~~
         a = 6
         b = 8
         c = ((a==6) ^ (b==9)) # c is True because (a==6) and (b==9) is False.
         d = ((a==4) ^ (b==9)) # d is False because neither conditional is True.        
         e = ((a==6) ^ (b==8)) # e is False because neither conditional is False.

   ~~~~

#### **Question 7**: 

- `.loc`  : allows dataframe subsetting by the *label* of a row or column
- `.iloc` : allows dataframe subsetting by the *index* of a row or column

Consider our GDP table from above (with an additional index column) to be a dataframe called `df`:

   | Index | Country | GDP (Nearest billion) |
   |--- | ------- | --- |
   | 0 | Germany | 265B |
   | 1 | France | 186B |
   | 2 | Italy | 166B |
   | 3 | Spain | 117B |

Since they're already sorted from greatest to least GDP, subset this by the three lowest GDPs we can use `.iloc` to subset the last three, from index 1 (Spain) until the first index which we do not want to include (in this case, index 4; alternatively, we could have left the last index blank to indicate stopping at the end).

~~~~
         df.iloc[1:4]
~~~~

The resulting table will then read:

   | Index | Country | GDP (Nearest billion) |
   |--- | ------- | --- |
   | 1 | France | 186B |
   | 2 | Italy | 166B |
   | 3 | Spain | 117B |

#### **Question 8**: 
An Application Programming Interface (API) acts as an intermediate between a data source (such as a web source) and a the local file in which a user analyzes or processes the data-- it allows the user to access, copy, and alter the data locally when the code is run later. 

We will need to import `requests`, `os`, and `pandas`, in order to construct a request to a remote server, pull the data and write to a local file, and import the data into a local work session, respectively. 

~~~~
         import requests
         import os
         import pandas
~~~~

Next, we need to specify a data source by its url and a folder name in which the data should go when it is pulled from the web. Here, I've called this folder "Data" and provided an `if` conditional that uses `os` to check if there is such a folder in the directory in which I'm working-- if there is no such folder, it will create it for me. Then I specify a filename into which I will write the copied data.

~~~~        
         url = 'https://onlinedata.com/download_data'
         
         folder_name = 'Data'
         if not os.path.exists(data_folder):
            os.makedirs(data_folder)
            
         file_name = 'os.path.join(folder_name, 'File')        
~~~~

Finally, the last steps are to access the web_source using `requests`, and open (`open()`) and `write()` a copy of the data into the file I created. 

Once this is done, I can use `pandas` to simply read the file and create a dataframe!

~~~~       
         web_source = requests.get(url)
         
         with open(file_name, 'wb') as i:
            i.write(web_source.content)
            
         my_dataframe = pandas.read_csv(filename)
~~~~

#### **Question 9**: 

The pandas `apply()` function allows a particular function to be applied repeatedly throughough a dataframe. It allows users to specify which axis to apply the function using the `axis` argument (`axis=0` for rows and `axis=1` for columns). Instead of applying it to each individual "cell" within the dataframe, it allows operations to be performed in bulk. 

Alternatively, a user may execute a `for` loop to visit each cell in a series, though this is less preferable as it requires more lines of code. The `apply()` function essentially allows us to execute a `for` loop across the contents of a series, applying an operation to each item in the series as the function iterates through.  


#### **Question 10**: 
Instead of using `iloc` to subset a number of variables to a new data frame, a user may prefer to use logical operators to group together and select for desired conditions, then use `[]` brackets to subset a a dataframe by filtering out columns or rows that don't meet the required criteria. 

First, we would set a conditional (or series of conditionals, if needed), such as `dataframe['Column']=='Contains_This'`. Then, we could select each row in this column for which this conditional is True by setting this equal to the original dataframe (or a copy!):

~~~~
         filtered_dataframe = dataframe[dataframe['Column']=='Contains_This']
~~~~

The resulting dataframe `filtered_dataframe` will filter through the rows in column `Column` that contain the variable `Contains_This`. 


