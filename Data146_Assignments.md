# Exercises for Monday, 02.08.2021

#### Initialization
```
import pandas as pd

data_path = 'gapminder.tsv'
data = pd.read_csv(data_path, sep='\t')
```

## Exercise 1
### How many unique years are included in the data set and what are they?

#### Code for Ex. 1
```
ex1_list = list(data['year'].unique())
ex1_count = len(ex1_list)
```
There are 12 years. The years are:  [1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, 2002, 2007]

## Exercise 2
### What is the maximum population value, when was it recorded and where was it found?

#### Code for Ex. 2
```
max_pop = data['pop'].max()
idx_pop = data['pop']==max_pop
ex2_ans = data[idx_pop]
```

The maximum population was in China in 2007, recorded at 1318683096.

## Exercise 3
### Extract all data from Europe: In 1952, which European country had the smallest population and what was its population in 2007?

#### Code for Ex. 3
```
idx_eu = data['continent']=='Europe'
eu_data = data[idx_eu] # extraction of all Europe data

idx_52 = eu_data['year']==1952
eu_52 = eu_data[idx_52]
min_52 = eu_52['pop'].min()
idx_min = eu_data['pop']==min_52
ex3 = eu_data[idx_min] # The country with the smallest population

idx_later = eu_sub['country']=='Iceland'
later_pop = eu_sub[idx_later]
idx_later_pop = later_pop['year']==2007
fin = later_pop[idx_later_pop] # This country's data in 2007.
```

The country with the smallest population in 1952 was Iceland, and in 2007 Iceland's population was 301931. 
