# Python_Restaurant-tips-analysis
![Uploading Restaurant Tip.jpg…]()

## Data import
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

