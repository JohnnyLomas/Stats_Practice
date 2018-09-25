### ThinkStats2: Exploratory Data Analysis



#### Jump To



[Introduction](#introduction)

[iPython Notebook](#ipython-notebook)

[Importing the Data](#importing-the-data)

[Dataframes in Pandas](#dataframes-in-pandas)

[Data Cleaning](#transformations)

[Data Validation](#validation)

[End of Chapter Exercises](#end-of-chapter-exercises)



#### Introduction



The [NSFG](http://cdc.gov/nchs/nsfg.htm) is cross-sectional survey conducted by the federal government on U.S. citizens
between the ages of 15 and 44. The surveyors recruit a representative sample of people
from across the country and record answers to a list of questions. The purpose of the survey
is to build data for statistical analysis related to the population of the United States.
The following analysis uses data from the NSFG Cycle 6.



#### Working in the Ipython Notebook



Anaconda versions of python come with access to a coding workspace that allows you to run code 
while building a script; this is called the Ipython Notebook. To bring up the notebook, navigate
to the directory containing the files you need and type 'ipython notebook'. Much of the code
run while completeing the chapters of this book will be performed in the ipython notebook.



#### Importing the Data



Pregnancy data from the NSFG survey was imported using the provided function entitled 'ReadFemPreg()' 
which is defined in the script 'nsfg.py'. The
function creates a dataframe with pregnancy data necessary for using pandas from the NSFG
survey using another function called 'ReadFixedWidth()' which formats fixed with ASCII text files
in a proper form for dataframe construction. Code to view the pregnancy dataframe:

```
import nsfg
df = nsfg.ReadFemPreg()
df

```

#### Dataframes in Pandas



A dataframe contains a row for each entry and a column for each variable. It also contains the 
variable names, variable types, and methods for accessing data. It is a common form
for operations using statistical software.

Some operations with the nsfg dataframe in pandas: 

Obtain an 'index' of the column variables (An index is a data structure in pandas):

```
df.columns

```

Index into the column names to obtain a column name as a string:

```
df.columns[1]

```

Access a column from the data frame using the column's name. Accessing data in this way results
in a series, which is another pandas data structure:

```
col = df['pregordr']

```

A series is a data structure in Pandas that provides the data in the column along with the index
for each datum. The series name, number of entries, and data type is also stored.

Access elements of a series using an integer or a slice:

```
series[1]
series[2:5]

```


#### Transformations



Whenever raw data is imported it is typical that certain transformations constituting data 
cleaning must be performed in order to facilitate computation. ThinkStats has provided a function
called CleanFemPreg() that performs this in the nsfg data.

```
def CleanFemPreg(df):
	df.agepreg /= 100.0
	na_vals = [97, 98, 99]
	df.birthwgt_lb.replace(na_vals, np.nan, inplace=True)
	df.birthwgt_oz.replace(na_vals, np.nan, inplace=True)
	df[totalwgt_lb] = df.birthwgt_lb + df.birthwgt_oz / 16.0

```

Here, data age data encoded in centi-years is converted to years, the encoded values of 
97, 98, and 99 in the weight data are replaced with Nan values, and a new total weight column
is added which simply adds the birth weight columns together in pounds. The replace function 
is a valuable tool here.



#### Validation


One simple way to validate data and make sure you are understanding the data is to compute
basic statistical values and compare them to previously observed phenomena. The series data
structure in Pandas provides a useful tool for tallying data in coloums. The value_counts()
function provides values tallied up with their counts:

```
df.birthwgt_lb.value_counts(sort=False)

```

This gives a quick picture of the distribution of baby weights. Do they make sense? Nope... we
found a 51 pound baby. That data point will have to be removed.

0  8

1  40

2  53

3  98

4  229

5  697

6  2223

7  3049

8  1889

9  623

10 132

11 26

12 10

13 3

14 3

15 1

51 1



#### End of Chapter Exercises

##### Exercise 1.1

The following are useful tidbits of code that I found useful while completing the 
end of chapter exercises.

Obtain the value counts for column (ColumnName) from dataframe (df):

```
df.ColumnName.value_counts()
```

Count the number od Nan's in a column:

```
df.ColumnName.isnull().sum()
```

Obtain the mean value of a column:

```
df.ColumnName.mean()
```

Make a new column which is some transformation (recode) of another column:

```
df['NewColumn'] = df.OldColumn*5
```

Access rows with a specific value in a specified column:

```
df[df.ColumnName==value]
```





