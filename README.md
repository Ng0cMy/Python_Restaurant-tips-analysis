# Python_Restaurant-tips-analysis

![image](https://github.com/Ng0cMy/Python_Restaurant-tips-analysis/assets/162866097/8d995ac6-f7ba-41b6-932a-be89dcc2bcb0)


## 📥 Data import and 🔍 exploration

### First, let's import the needed libraries: Pandas & Matplotlib.

##### Code here:

      import pandas as pd

      import matplotlib.pyplot as plt
  
### Then load data and take a look at the first 5 rows to be sure, that data is loaded properly.

##### Code here:

      df = pd.read_csv('link')
  
      df.head()
  
##### Result:
  
|  |id  |total_bill  | tip|sex  |smoker  |day  |time  |size  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  0| 0 |  16.99|  1.01|Female  |No  |Sun |Dinner  | 2 |
|  1|  1|  10.34|  1.66|  Male| No |Sun  | Dinner |3  |
|  2|  2| 21.01 |  3.50|  Male|  No| Sun | Dinner | 3 |
|  3|3  |  23.68| 3.31 |  Male|  No| Sun | Dinner |  2|
|4|4   |24.59|3.61|Female|No|Sun|Dinner|4|

### The columns of the dataframe and their types:

##### Code here:
 
      df.info()

#### According to the types, we have string columns considered as objects:

##### Result:

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

##### Code here:

      df = df.convert_dtypes()
  
      df.info()

##### Result:
  
<class 'pandas.core.frame.DataFrame'>

RangeIndex: 244 entries, 0 to 243

Data columns (total 8 columns):

|#|Column|Non-Null|Count|Dtype|
|--- | ------   |   ------|--------|  -----  |
| 0|   id|          244 |non-null|    int64  |
| 1 |  total_bill|  244| non-null |   float64|
| 2 | tip  |       244| non-null  |  float64|
| 3 |  sex |        244| non-null |   **string** |
| 4 |  smoker|     244 |non-null  |  **string** |
| 5 |  day |        244| non-null |   **string** |
| 6 |  time  |      244 |non-null |   **string** |
| 7 |  size  |      244| non-null |   int64  |

dtypes: float64(2), int64(2), string(4)

memory usage: 16.3 KB

## Basic descriptive statistics

### Show a descriptive statistics on the numeric columns:

##### Code here:

      df.describe()

##### Result:

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

## 💸 Tip value influencers

### 🚬 Do smoker people give more tips?

Let's figure out the difference between smokers and non-smokers in terms of their behavior and purchasing habits in public catering establishments.

### Separate smokers and non-smokers

#### Create a new dataframe smokers_df

##### Code here:

      smokers_df = df.query('smoker == "Yes"')
  
      smokers_df.sample(5)

##### Result:

|id|	total_bill|	tip|	sex|	smoker|	day|	time|	size|
|---|---|---|---|---|---|---|---|
|218|	218|	7.74|	1.44|	Male|	Yes|	Sat|	Dinner|	2|
|90|	90|	28.97|	3.0|	Male|	Yes|	Fri|	Dinner|	2|
|56|	56|	38.01|	3.0|	Male|	Yes|	Sat|	Dinner|	4|
|231|	231|	15.69|	3.0|	Male|	Yes|	Sat|	Dinner|	3|
|230|	230|	24.01|	2.0|	Male|	Yes|	Sat|	Dinner|	4|

#### Create a new dataframe non_smokers_df

##### Code here:

      non_smokers_df = df.query('smoker == "No"')
  
      non_smokers_df.sample(5)

##### Result:

| |	id|	total_bill|	tip|	sex|	smoker|	day|	time|	size|
|---|---|---|---|---|---|---|---|---
|75|	75|	10.51	|1.25|	Male|	No|	Sat|	Dinner|	2|
|3|	3|	23.68|	3.31|	Male|	No|	Sun|	Dinner|	2|
|104|	104|	20.92	|4.08|	Female|	No|	Sat|	Dinner|	2|
|16|	16|	10.33|	1.67|	Female|	No|	Sun|	Dinner|	3|
|33|	33|	20.69	|2.45|	Female|	No|	Sat|	Dinner|	4|

### Compare their measures of central tendency

#### 🌏 Calculate measures of central tendency for the whole dataset first

##### Code here:

###### *The 'tip' column through the whole dataset*

      common_tip_min = df['tip'].min()
  
      common_tip_max = df['tip'].max()
  
      common_tip_median = df['tip'].median()
  
###### *Make a list of values*

      common_values = [common_tip_min, common_tip_max, common_tip_mean, common_tip_median]
  
 ###### *Round all the values to 4 decimal places*

      common_values = map(lambda x: round(x, 4), common_values)
  
 ###### *Make a dataframe from the list*

      common_mct = pd.DataFrame(common_values, index=['min', 'max', 'mean', 'median'])

###### *Output the dataframe*

      common_mct

##### Result:

||0|
|---|---|
|min|	1.0000|
|max|	10.0000|
|mean|	2.9983|
|median|	2.9000|

#### 🚬 Calculate measures of central tendency for only smokers

##### Code here:

###### *The 'tip' column through smoke*

      smokers_tip_min = smokers_df['tip'].min()

      smokers_tip_max = smokers_df['tip'].max()

      smokers_tip_mean = smokers_df['tip'].mean()

      smokers_tip_median = smokers_df['tip'].median()

###### *Make a list of values*

      smokers_values = [smokers_tip_min, smokers_tip_max, smokers_tip_mean, smokers_tip_median]

###### *Round all the values to 4 decimal places*

      smokers_values = map(lambda x: round(x, 4), smokers_values)

###### *Make a dataframe from the list*

      smokers_mct = pd.DataFrame(smokers_values, index=['smokers_min', 'smokers_max', 'smokers_mean', 'smokers_median'])

###### *Output the dataframe*

      smokers_mct

##### Result:

||0|
|--|--|
|smokers_min|	1.0000|
|smokers_max|	10.0000|
|smokers_mean|	3.0087|
|smokers_median	|3.0000|

#### 🚭 Calculate measures of central tendency for non-smokers

##### Code here:

###### *The 'tip' column through non-smokes*

      non_smokers_tip_min = non_smokers_df['tip'].min()
  
      non_smokers_tip_max = non_smokers_df['tip'].max()

      non_smokers_tip_mean = non_smokers_df['tip'].mean()

      non_smokers_tip_median = non_smokers_df['tip'].median()

###### *Make a list of values*

      non_smokers_values = [non_smokers_tip_min, non_smokers_tip_max, non_smokers_tip_mean, non_smokers_tip_median]

###### *Round all the values to 4 decimal places*

      non_smokers_values = map(lambda x: round(x, 4), non_smokers_values)

###### *Make a dataframe from the list*

      non_smokers_mct = pd.DataFrame(non_smokers_values, index=['non_smokers_min', 'non_smokers_max', 'non_smokers_mean', 'non_smokers_median'])

###### *Output the dataframe*

      non_smokers_mct

##### Result:

||0|
|---|---|
|non_smokers_min	|1.0000|
|non_smokers_max|	9.0000|
|non_smokers_mean|	2.9919|
|non_smokers_median|	2.7400|

#### Retrieve results together

##### Code here:

      all_vals_dict = {
           'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
           'Smokers': {'min': smokers_tip_min, 'max': smokers_tip_max, 'mean': smokers_tip_mean, 'median': smokers_tip_median},
           'Non-smokers': {'min': non_smokers_tip_min, 'max': non_smokers_tip_max, 'mean': non_smokers_tip_mean, 'median': non_smokers_tip_median}
      }

###### *Make a dataframe*

      all_mct = pd.DataFrame(all_vals_dict)

###### *Output the dataframe*

      all_mct

##### Result:

|Common|	Smokers|	Non-smokers|
|---|---|---|
|min|	1.000000|	1.00000|	1.000000|
|max|	10.000000|	10.00000|	9.000000|
|mean|	2.998279|	3.00871|	2.991854|
|median|	2.900000|	3.00000|	2.740000|

## 📝 Conclusion

### Based on the data analyzed above, it seems that smokers tend to TIP more than non-smokers, however, this difference is not significant.
### However, comparing measures of central tendency is not enough; we need to consider the distribution of the data to gain further insights.

##  Look at histograms

###  🌏 Whole dataset tips histogram

#### Plot the histogram for the whole dataset tips distribution.

##### Code here:

      plt.figure(figsize=(15, 5))
      plt.hist(df.tip, bins = 20, color = '#74b9ff')
      plt.xlabel = 'Tip value'
      plt.ylabel = 'Frequency'
      plt.title = 'Whole dataset tip values'
      plt.grid(True)
      plt.show()

##### Result:

![image](https://github.com/Ng0cMy/Python_Restaurant-tips-analysis/assets/162866097/c6527854-6f15-4071-8b29-9ddf3ac13f71)

### 🚬 Smokers tips histogram

#### Plot the histogram for smokers tips distribution.

###### Code here:

      plt.figure(figsize=(15, 5))
      plt.hist(smokers_df.tip, bins = 20, color = '#ff7675')
      plt.xlabel = 'Tip value'
      plt.ylabel = 'Frequency'
      plt.title = 'Smokers tip values'
      plt.grid(True)
      plt.show()

##### Result:

![image](https://github.com/Ng0cMy/Python_Restaurant-tips-analysis/assets/162866097/77d11181-fd0f-4254-91e5-7293b4181060)


### 🚭 Non-smokers tips histogram

#### Plot the histogram for non-smokers tips distribution.

      plt.figure(figsize=(15, 5))
      plt.hist(non_smokers_df.tip, bins = 20, color = '#55efc4')
      plt.xlabel = 'Tip value'
      plt.ylabel = 'Frequency'
      plt.title = 'Non-smokers tip values'
      plt.grid(True)
      plt.show()

##### Result:

![image](https://github.com/Ng0cMy/Python_Restaurant-tips-analysis/assets/162866097/e3d88ee0-4e0a-4943-8bdc-f51c6bfb7df5)

### ⭐ Plot all 3 charts in a row in the same cell:

###### Code here:

      fig, axes = plt.subplots(1, 3, figsize=(12, 4))
      axes[0].hist(df.tip, bins=20, color='#74b9ff')
      axes[0].set_title('Whole dataset tip values')
      axes[0].grid(True)
      axes[1].hist(smokers_df.tip, bins=20, color='#ff7675')
      axes[1].set_title('Smokers tip values')
      axes[1].grid(True)
      axes[2].hist(non_smokers_df.tip, bins=20, color='#55efc4')
      axes[2].set_title('Non-smokers tip values')
      axes[2].grid(True)
      plt.show()

##### Result:

![image](https://github.com/Ng0cMy/Python_Restaurant-tips-analysis/assets/162866097/f9830f4c-daf3-4006-8bcd-0a9fcf7c60dc)

## 📝 Conclusion

### According to the chart, non-smokers are less likely to tip amounts of $7 or more. However, the overall frequency of tipping among non-smokers is higher than that of smokers.
### Overall, most people tend to tip between $2 and $4 at restaurants.
