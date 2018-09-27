### ThinkStats2: Distributions



#### Jump To


[Histograms](#histograms)
[Outliers](#outliers)
[Summarizing Distributions](#summarizing-distributions)

#### Histograms

Histograms are a useful way to display a distribution of data. They represent the frequency,
or number of times the value appears in the data. Histograms are not a good method for comparing
two distributions because the sample sizes may be different. With different sample sizes, frequencies
while appear different when two distributions are plotted side-by-side.In python, frequencies are often computed
with the help of **dictionaries**.The following code builds a dictionary that maps the values 
in a sequence to their frequencies.

```
Given a sequence of values (t):

hist = {}
for x in t:
	hist[x] = hist.get(x,0) + 1
```

The get() method ensures that if the key indexed in the dictionary does not exist, the 
second argument (0) will be returned instead of an error.


Plotting data in python can be easily accomplished using **pyplot** which is part of the 
**matplotlib** package. Below is some example code for plotting with pyplot:

```
Plot a sequence of y values against a sequence of x values:

import matplotlib.pyplot as plt
plt.plot([1,2,3,4,5], [5, 4, 3, 2, 1])
plt.ylabel("Y_values")
plt.xlabel("X_values")
plt.show()
```
```
Plot multiple sequences with different colored lines given sequences (x1, y1, x2, y2):

import matplotlib.pyplot as plt
plt.plot(x1, y1, "b-", x2, y2, "g-")
plt.ylabel("Y_values")
plt.xlabel("X_values")
plt.show()
```
```
Plot a histogram form a sequence of values (x):

import matplotlib.pyplot as plt
plt.hist(x)
plt.title("Title")
plt.xlabel("values")
plt.ylabel("Frequency")
plt.grid(True)
plt.show()
```


#### Outliers


Histograms do not always reveal the presence of outliers so it is a good idea to check the 
data for extreme values. Outliers may represent errors in measurement, recording, etc. and
may not accurately reflect the phenomena. One way to look for outliers would be to sort the 
data from largest to smallest and look at the top few values. This can then be repeated while
sorting from smallest to largest. Outliers can be handled with contextual knowledge of the 
phenomena or using statistical tests related to the underlying distributions.


#### Summarizing Distributions


A histogram gives a good general overview of the shape of a distribution, but it gives a 
limited summary of the data. Summary statistics have been developed in order to explore the 
following important aspects of a data set:

- Central Tendency. Does the data cluster around some central point?
- Modes. Is there more than one cluster?
- Spread. How variable is the data?
- Tails. What is the behavoir of the set near the largest and smallest values?
- Outliers. Are there extreme values?

Pandas provides methods through which mean, variance, and standard deviation can be computed:

```
mean = df.ColumnName.mean()
variance = df.ColumnName.var()
standard_deviation = df.ColumnName.std()
```

Effect size is a statistic that attempts to determine whether or not the means from two
distributions are different. One method of doing this is Cohen's Effect Size (d). This 
statistic uses the means from two groups and their pooled variance to compute a difference
given as the number of standard deviations. Below is the code for a Cohen's d method provided
by thinkstats2:

```
def CohenEffectSize(group1, group2):
	diff = group1.mean() - group2.mean()
	var1 = group1.var()
	var2 = group2.var()
	n1, n2 = len(group1), len(group2)
	28 Chapter 2. Distributions
	pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
	d = diff / math.sqrt(pooled_var)
	return d
```


#### End of Chapter Exercises

Useful code from the exercises:

