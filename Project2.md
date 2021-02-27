#### Continuous, Ordinal, and Nominal Data
**Describe continuous, ordinal and nominal data. Provide examples of each. Describe a model of your own construction that incorporates variables of each type of data. You are perfectly welcome to describe your model using english rather than mathematical notation if you prefer. Include hypothetical variables that represent your features and target.**

**Continuous data** spans some range along a continuum, is typically not countable, and is able to be segmented into increasingly smaller increments.
  e.g. length of time, volume of liquid, mass of an object
  
**Ordinal data** has a chronology or order that must be preserved.
  e.g. order in which runners finish a race, school grade level 
  
**Nominal data** is often qualitative with no obvious ordering, and describes categories into which data fall.
  e.g. college majors/minors, a senator's political stances

**Example**: In a fourth grade English class, a teacher may consider a student's average weekly spelling test score (continuous) as well as their position in a school spelling bee (ordinal) to determine whether students fall into "Excellent", "Acceptable", or "Needs Improvement" categories (nominal) for fourth-grade spelling. 
 
 ~~~~
 (Avg. score)*0.8 + (1/(Spelling Bee Position))*0.2 = Student spelling score
 ~~~~
  
  | Category | Spelling Score |
  | ------ | -------- |
  | Excellent | 1.0 - 0.7 |
  | Acceptable | 0.699 - 0.4  |
  | Needs Improvement | 0.399 or below |

#### Question 2
**Comment out the seed from your randomly generated data set of 1000 observations and use the beta distribution to produce a plot that has a mean that approximates the 50th percentile. Also produce both a right skewed and left skewed plot by modifying the alpha and beta parameters from the distribution. Be sure to modify the widths of your columns in order to improve legibility of the bins (intervals). Include the mean and median for all three plots.**


#### Question 3
**Using the gapminder data set, produce two overlapping histograms within the same plot describing life expectancy in 1952 and 2007. Plot the overlapping histograms using both the raw data and then after applying a logarithmic transformation (np.log10() is fine). Which of the two resulting plots best communicates the change in life expectancy amongst all of these countries from 1952 to 2007?**


#### Question 4
**Using the seaborn library of functions, produce a box and whiskers plot of population for all countries at the given 5-year intervals. Also apply a logarithmic transformation to this data and produce a second plot. Which of the two resulting box and whiskers plots best communicates the change in population amongst all of these countries from 1952 to 2007?**

