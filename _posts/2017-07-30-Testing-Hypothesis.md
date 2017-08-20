---
layout: post
title: The effect of recession on housing prices in university towns
description: "Testing a hypothesis on the effect of recession on housing prices in university towns as compared to other towns"
headline:
modified:
category: Projects
tags: [testing-hypothesis]
imagefeature:
comments: true
share: true
mathjax:
---

The hypothesis that the university towns have their mean housing prices less effected by recessions is tested. To get a measure of the change in housing prices due to recession, a ratio of mean price of houses is used - for the quarter before the recession starts to that of the recession bottom. The price ratio for the university towns is compared with that of other towns by running a t-test using ```scipy.stats.ttest_ind```.

The data used here can be found at:
* The housing data from the
[Zillow research data site](http://www.zillow.com/research/data/) stored in the file ```City_Zhvi_AllHomes.csv```.
* The list of
[university towns in the United States](https://en.wikipedia.org/wiki/List_of_college_towns#College_towns_in_the_United_States)
from wikipedia has been copy and pasted into the file ```university_towns.txt```.
* The [GDP over time](http://www.bea.gov/national/index.htm#gdp) of the United States from the Bureau of Economic Analysis, US Department of Commerce, stored in the file ```gdplev.xls```

The data analysis is done in the following steps:
1. A dataframe of university towns is obtained with the names of state and town as multi-index.
2. A dataframe for GDP as well as differences in GDP is obtained and then quarters corresponding to the start of the recession as well as recession bottom are identified.
3. A dataframe for housing prices are obtained in desirable format which contains prices for both university and non-university towns.
4. The hypothesis is tested comparing the price ratio for university vs non-university towns.

Terminology:
* A _university town_ is a city which has a high percentage of university students compared to the total population of the city.
* A _quarter_ is a specific three month period, Q1 is January through March, Q2 is April through June, Q3 is July through September, Q4 is October through December.
* _Recession_ starts when GDP declines for two consecutive quarters and ends when GDP grows for two consecutive quarters.
* _Recession bottom_ is the quarter within a recession which had the lowest GDP.

Below is the code in python 3:
```python
import pandas as pd
from scipy.stats import ttest_ind
```

The following function reads the text file `university_towns.txt` and return a `pandas` dataframe consisting of the list of university towns along with their states.


```python
def get_list_of_university_towns():
    '''Returns a DataFrame with multi index consisting of the towns and
    the states from the university_towns.txt list.'''
    text_file = open("university_towns.txt")
    # Make a dictionary with key as the line number of the states that
    # have "[edit]" after them and value as state name itself without "[edit]"
    State = {idx: lines.strip().replace("[edit]", "")
             for idx,lines in enumerate(text_file) if "edit" in lines}
    # Convert the dictionary to a series
    State = pd.Series(State)
    # Create a data frame with one column as Region names
    university_towns = pd.read_csv("university_towns.txt", sep = "\n",
                                   header = None, names = ["RegionName"])
    # Add the above series as a column in dataframe
    university_towns["State"] = State
    # Forward fill for the "State" Column
    university_towns = university_towns.fillna(method = 'ffill')
    # Drop all rows that has state names in the column "RegionName"
    university_towns = university_towns.drop(State.index)
    # Edit the Region names to get rid of everything except the names of the towns
    university_towns["RegionName"] = list(map(lambda x: x.split("(")[0].rstrip(),
                                              university_towns["RegionName"]))
    # Set the two columns of State and Region names as multi-index
    university_towns = university_towns.set_index(["State", "RegionName"])
    return university_towns
print("First 20 entries from the list of university towns: \n")
get_list_of_university_towns().index.values[:10]
```

    First 20 entries from the list of university towns:

    array([('Alabama', 'Auburn'), ('Alabama', 'Florence'),
           ('Alabama', 'Jacksonville'), ('Alabama', 'Livingston'),
           ('Alabama', 'Montevallo'), ('Alabama', 'Troy'),
           ('Alabama', 'Tuscaloosa'), ('Alabama', 'Tuskegee'),
           ('Alaska', 'Fairbanks'), ('Arizona', 'Flagstaff')], dtype=object)




```python
GDP = pd.read_excel("gdplev.xls", skiprows = 5)

# Drop all the rows for the data that corresponds to quarters prior to the first
# quarter of 2000
GDP.drop(GDP.index[:214], inplace = True)

# Drop all the rows for which there is no data values
GDP.dropna(axis = 1, how = 'all', inplace = True)
print(GDP.columns)
# Keep only two columns: Quarter and GDP in billions of chained 2009 dollars
GDP = GDP.iloc[:,[0,2]]

# Rename columns
GDP.columns = ["Quarters", 'GDP in billions in current dollars']

# Set Quarters as the index to the dataframe
GDP.set_index("Quarters", inplace = True)
print("First 10 entries from the dataframe GDP: \n")
GDP.head(10)
```

    Index(['Unnamed: 4', 'GDP in billions of current dollars.1',
           'GDP in billions of chained 2009 dollars.1'],
          dtype='object')
    First 10 entries from the dataframe GDP:
<pre>
<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GDP in billions in current dollars</th>
    </tr>
    <tr>
      <th>Quarters</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000q1</th>
      <td>12359.1</td>
    </tr>
    <tr>
      <th>2000q2</th>
      <td>12592.5</td>
    </tr>
    <tr>
      <th>2000q3</th>
      <td>12607.7</td>
    </tr>
    <tr>
      <th>2000q4</th>
      <td>12679.3</td>
    </tr>
    <tr>
      <th>2001q1</th>
      <td>12643.3</td>
    </tr>
    <tr>
      <th>2001q2</th>
      <td>12710.3</td>
    </tr>
    <tr>
      <th>2001q3</th>
      <td>12670.1</td>
    </tr>
    <tr>
      <th>2001q4</th>
      <td>12705.3</td>
    </tr>
    <tr>
      <th>2002q1</th>
      <td>12822.3</td>
    </tr>
    <tr>
      <th>2002q2</th>
      <td>12893.0</td>
    </tr>
  </tbody>
</table>
</div>
</pre>

```python
# Create a dataframe out of GDP with two columns - Quarters and
# difference in GDP of consecutive quartes
GDP_diff = GDP.diff()
print("First 10 entries from the dataframe GDP_diff: \n")
GDP_diff.head(10)
```

    First 10 entries from the dataframe GDP_diff:  
<pre>
<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GDP in billions in current dollars</th>
    </tr>
    <tr>
      <th>Quarters</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000q1</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000q2</th>
      <td>233.4</td>
    </tr>
    <tr>
      <th>2000q3</th>
      <td>15.2</td>
    </tr>
    <tr>
      <th>2000q4</th>
      <td>71.6</td>
    </tr>
    <tr>
      <th>2001q1</th>
      <td>-36.0</td>
    </tr>
    <tr>
      <th>2001q2</th>
      <td>67.0</td>
    </tr>
    <tr>
      <th>2001q3</th>
      <td>-40.2</td>
    </tr>
    <tr>
      <th>2001q4</th>
      <td>35.2</td>
    </tr>
    <tr>
      <th>2002q1</th>
      <td>117.0</td>
    </tr>
    <tr>
      <th>2002q2</th>
      <td>70.7</td>
    </tr>
  </tbody>
</table>
</div>
</pre>



```python
def get_quarter_before_recession():
    '''Returns the year and quarter of the recession start time as a
    string value in a format such as 2005q3'''
    for i, quarter in enumerate(GDP_diff.index):
        if (GDP_diff.iloc[i+1] < 0).bool() and (GDP_diff.iloc[i+2] < 0).bool():
            return quarter
    return None  
print("Quarter before recession: ", get_quarter_before_recession())
```

    Quarter before recession:  2008q2



```python
def get_recession_bottom():
    flag = 0
    for i, quarter in enumerate(GDP_diff.index):
        if ((flag == 1) and (GDP_diff.iloc[i] > 0).bool() and
        (GDP_diff.iloc[i+1] > 0).bool()):
            end_idx = i+1
            break
        if ((flag == 0) and (GDP_diff.iloc[i] < 0).bool() and
        (GDP_diff.iloc[i+1] < 0).bool()):
            flag = 1
            start_idx = i
    GDP_recession = GDP.iloc[start_idx: end_idx + 1]
    idx = GDP_recession.idxmin()
    return idx[0]
print("Recession bottom: ", get_recession_bottom())
```

    Recession bottom:  2009q2



```python
def convert_housing_data_to_quarters():
    '''Converts the housing data given in monthly format to quarters
    from 2000q1 through 2016q3 and returns it as mean values in a
    dataframe. This dataframe have a multi-index in the shape of
    ["State","RegionName"].
    '''
    all_homes = pd.read_csv("City_Zhvi_AllHomes.csv")

    states = {'OH': 'Ohio', 'KY': 'Kentucky', 'AS': 'American Samoa',
              'NV': 'Nevada', 'WY': 'Wyoming', 'NA': 'National',
              'AL': 'Alabama', 'MD': 'Maryland', 'AK': 'Alaska',
              'UT': 'Utah', 'OR': 'Oregon', 'MT': 'Montana',
              'IL': 'Illinois', 'TN': 'Tennessee',
              'DC': 'District of Columbia', 'VT': 'Vermont',
              'ID': 'Idaho', 'AR': 'Arkansas', 'ME': 'Maine',
              'WA': 'Washington', 'HI': 'Hawaii', 'WI': 'Wisconsin',
              'MI': 'Michigan', 'IN': 'Indiana', 'NJ': 'New Jersey',
              'AZ': 'Arizona','GU': 'Guam', 'MS': 'Mississippi',
              'PR': 'Puerto Rico','NC': 'North Carolina', 'TX': 'Texas',
              'SD': 'South Dakota', 'MP': 'Northern Mariana Islands',
              'IA': 'Iowa', 'MO': 'Missouri', 'CT': 'Connecticut',
              'WV': 'West Virginia', 'SC': 'South Carolina',
              'LA': 'Louisiana', 'KS': 'Kansas', 'NY': 'New York',
              'NE': 'Nebraska', 'OK': 'Oklahoma', 'FL': 'Florida',
              'CA': 'California', 'CO': 'Colorado', 'PA': 'Pennsylvania',
              'DE': 'Delaware', 'NM': 'New Mexico', 'RI': 'Rhode Island',
              'MN': 'Minnesota', 'VI': 'Virgin Islands',
              'NH': 'New Hampshire', 'MA': 'Massachusetts', 'GA': 'Georgia',
              'ND': 'North Dakota', 'VA': 'Virginia'}
    # Replaces the abbreviations with the names of the states
    all_homes["State"].replace(states, inplace = True)
    all_homes = all_homes.set_index(["State","RegionName"])
    all_homes = all_homes.iloc[:, 49:250] # Discards irrelavant columns

    def quarters(col):
        if col.endswith(("01", "02", "03")):
            s = col[:4] + "q1"
        elif col.endswith(("04", "05", "06")):
            s = col[:4] + "q2"
        elif col.endswith(("07", "08", "09")):
            s = col[:4] + "q3"
        else:
            s = col[:4] + "q4"
        return s  
    # Groups the monthly columns into quarters using mean value of
    # the four monthly columns
    housing = all_homes.groupby(quarters, axis = 1).mean()
    housing = housing.sort_index()
    return housing

housing = convert_housing_data_to_quarters()
print("Columns: \n", housing.columns)
print("# Rows: ", len(housing))
```

    Columns:
     Index(['2000q1', '2000q2', '2000q3', '2000q4', '2001q1', '2001q2', '2001q3',
           '2001q4', '2002q1', '2002q2', '2002q3', '2002q4', '2003q1', '2003q2',
           '2003q3', '2003q4', '2004q1', '2004q2', '2004q3', '2004q4', '2005q1',
           '2005q2', '2005q3', '2005q4', '2006q1', '2006q2', '2006q3', '2006q4',
           '2007q1', '2007q2', '2007q3', '2007q4', '2008q1', '2008q2', '2008q3',
           '2008q4', '2009q1', '2009q2', '2009q3', '2009q4', '2010q1', '2010q2',
           '2010q3', '2010q4', '2011q1', '2011q2', '2011q3', '2011q4', '2012q1',
           '2012q2', '2012q3', '2012q4', '2013q1', '2013q2', '2013q3', '2013q4',
           '2014q1', '2014q2', '2014q3', '2014q4', '2015q1', '2015q2', '2015q3',
           '2015q4', '2016q1', '2016q2', '2016q3'],
          dtype='object')
    # Rows:  10730


**Hypothesis**: University towns have their mean housing prices less effected by recessions. Running a t-test to compare the ratio of the mean price of houses in university towns the quarter before the recession starts compared to the recession bottom. (`price_ratio=quarter_before_recession/recession_bottom`)



```python
def run_ttest():
    '''First creates new data showing the decline or growth of housing
    prices between the recession start and the recession bottom. Then
    runs a ttest comparing the university town values to the
    non-university towns values, return whether the alternative hypothesis
    (that the two groups are the same) is true or not as well as the
    p-value of the confidence.

    Returns the tuple (different, p, better) where different=True if
    the t-test is True at a p<0.01 (we reject the null hypothesis),
    or different=False if otherwise (we cannot reject the null hypothesis).
    The variable p is the exact p value returned from scipy.stats.ttest_ind().
    The value for better is either "university town" or "non-university town"
    depending on which has a lower mean price ratio (which is equivilent to
    a reduced market loss).'''
    housing = convert_housing_data_to_quarters()
    university_towns = get_list_of_university_towns()
    quarter_before_recession = get_quarter_before_recession()    
    recession_bottom = get_recession_bottom()

    # Keep columns corresponding to only two quarters:
    # quarter before recession and recession bottom
    housing = housing[[quarter_before_recession, recession_bottom]]
    housing["price_ratio"] = housing[quarter_before_recession].div(housing[recession_bottom])
    housing = housing.dropna()

    # Merge the housing dataframa with the one with the university towns taking
    # the intersection of both the dataframes. The new dataframe for housing in
    # university towns has the multi-index of States and Region names.
    university_housing = pd.merge(university_towns, housing, how = "inner",
                                  left_index = True, right_index = True)

    # Left over rows from housing gives the dataframe for housing
    # in non-university towns
    non_university_housing = housing[~housing.index.isin(university_housing.index)]

    # Testing the hypotheses
    t_stat, p_value = ttest_ind(university_housing["price_ratio"],
                                      non_university_housing["price_ratio"])

    if p_value < 0.01:
        different = True
    else:
        different = False
    if t_stat < 0:
        better = "university town"
    else:
        better = "non-university town"
    return (different, p_value, better)
run_ttest()
```




    (True, 0.002724063704761164, 'university town')



Conclusion: Since the p-value is less than 0.01, we reject the null hypotheses of equal expected price ratios for university and non-university towns. Moreover, t-statistic is negative implying the price ratio for the university towns is less than that for remaining towns. This in turn suggests that prices for houses in university towns were less affected during recession as compared to that of non-university towns.

Application of anaylsis: This suggests the real-estate investment in university towns might be a safer option as compared to non-university towns if there's a chance of impending recession in near future.
