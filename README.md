# Python_Restaurant-tips-analysis
![Uploading Restaurant Tip.jpg…]()

## Data exploration

### First, let's import the needed libraries: Pandas & Matplotlib.

Code here:
  import pandas as pd
  import matplotlib.pyplot as plt
  
### Then load data and take a look at the first 5 rows to be sure, that data is loaded properly.

Code here:

  df = pd.read_csv('link')
  
  df.head()
  
#### Result:
  
|  |id  |total_bill  | tip|sex  |smoker  |day  |time  |size  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  0| 0 |  16.99|  1.01|Female  |No  |Sun |Dinner  | 2 |
|  1|  1|  10.34|  1.66|  Male| No |Sun  | Dinner |3  |
|  2|  2| 21.01 |  3.50|  Male|  No| Sun | Dinner | 3 |
|  3|3  |  23.68| 3.31 |  Male|  No| Sun | Dinner |  2|
|4|4   |24.59|3.61|Female|No|Sun|Dinner|4|

### the columns of the dataframe and their types:

Code here:
 
  df.info()

#### According to the types, we have string columns considered as objects:

<class 'pandas.core.frame.DataFrame'>

RangeIndex: 244 entries, 0 to 243

Data columns (total 8 columns):

|#|Column|Non-Null|Count|Dtype|
|--- | ------   |   ------|--------|  -----  |
| 0|   id|          244 |non-null|    int64  |
| 1 |  total_bill|  244| non-null |   float64|
| 2 | tip  |       244| non-null  |  float64|
| 3 |  sex |        244| non-null |   **object** |
| 4 |  smoker|     244 |non-null  |  **object** |
| 5 |  day |        244| non-null |   **object** |
| 6 |  time  |      244 |non-null |   **object** |
| 7 |  size  |      244| non-null |   int64  |

dtypes: float64(2), int64(2), object(4)

memory usage: 15.4+ KB

#### Let's fix their types, make them string and checked the result:

Code here:
  df = df.convert_dtypes()
  
  df.info()
  
<class 'pandas.core.frame.DataFrame'>

RangeIndex: 244 entries, 0 to 243

Data columns (total 8 columns):

|#|Column|Non-Null|Count|Dtype|
|--- | ------   |   ------|--------|  -----  |
| 0|   id|          244 |non-null|    int64  |
| 1 |  total_bill|  244| non-null |   float64|
| 2 | tip  |       244| non-null  |  float64|
| 3 |  sex |        244| non-null |   **object** |
| 4 |  smoker|     244 |non-null  |  **object** |
| 5 |  day |        244| non-null |   **object** |
| 6 |  time  |      244 |non-null |   **object** |
| 7 |  size  |      244| non-null |   int64  |

dtypes: float64(2), int64(2), string(4)

memory usage: 16.3 KB

## Basic descriptive statistics

### Show a descriptive statistics on the numeric columns:

||	id|	total_bill|	tip|	size|
|----|---|---|---|---|
|count	244.0	244.0	244.0	244.0
|  |  |  |  |  |
|mean|	121.5|	19.785943|	2.998279|	2.569672|
|std|	70.580923|	8.902412|	1.383638|	0.9511|
|min|	0.0|	3.07|	1.0|	1.0|
|25%|	60.75|	13.3475|	2.0|	2.0|
|50%|	121.5|	17.795	|2.9	|2.0|
|75%|	182.25|	24.1275|	3.5625|	3.0|
|max|	243.0	|50.81|	10.0|	6.0|

## Tip value influencers

### Do smoker people give more tips?

Let's figure out the difference between smokers and non-smokers in terms of their behavior and purchasing habits in public catering establishments.

### Separate smokers and non-smokers

#### Create a new dataframe smokers_df
Code here:

  smokers_df = df.query('smoker == "Yes"')
  
  smokers_df.sample(5)

|id|	total_bill|	tip|	sex|	smoker|	day|	time|	size|
|---|---|---|---|---|---|---|---|
|218|	218|	7.74|	1.44|	Male|	Yes|	Sat|	Dinner|	2|
|90|	90|	28.97|	3.0|	Male|	Yes|	Fri|	Dinner|	2|
|56|	56|	38.01|	3.0|	Male|	Yes|	Sat|	Dinner|	4|
|231|	231|	15.69|	3.0|	Male|	Yes|	Sat|	Dinner|	3|
|230|	230|	24.01|	2.0|	Male|	Yes|	Sat|	Dinner|	4|

#### Create a new dataframe non_smokers_df

Code here:

  non_smokers_df = df.query('smoker == "No"')
  
  non_smokers_df.sample(5)



| |	id|	total_bill|	tip|	sex|	smoker|	day|	time|	size|
|---|---|---|---|---|---|---|---|---
|75|	75|	10.51	|1.25|	Male|	No|	Sat|	Dinner|	2|
|3|	3|	23.68|	3.31|	Male|	No|	Sun|	Dinner|	2|
|104|	104|	20.92	|4.08|	Female|	No|	Sat|	Dinner|	2|
|16|	16|	10.33|	1.67|	Female|	No|	Sun|	Dinner|	3|
|33|	33|	20.69	|2.45|	Female|	No|	Sat|	Dinner|	4|

### Compare their measures of central tendency

#### Calculate measures of central tendency for the whole dataset first

Code here:

*The 'tip' column through the whole dataset*

  common_tip_min = df['tip'].min()
  
  common_tip_max = df['tip'].max()
  
  common_tip_mean = df['tip'].mean()
  
  common_tip_median = df['tip'].median()
  
*Make a list of values*

  common_values = [common_tip_min, common_tip_max, common_tip_mean, common_tip_median]
  
*Round all the values to 4 decimal places*

  common_values = map(lambda x: round(x, 4), common_values)
  
*Make a dataframe from the list*

  common_mct = pd.DataFrame(common_values, index=['min', 'max', 'mean', 'median'])

*Output the dataframe*

  common_mct

