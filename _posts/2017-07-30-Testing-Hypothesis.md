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
 
The data files used here can be found at:
* The housing data from the 
[Zillow research data site](http://www.zillow.com/research/data/) stored in the file ```City_Zhvi_AllHomes.csv```.
* The list of
[university towns in the United States](https://en.wikipedia.org/wiki/List_of_college_towns#College_towns_in_the_United_States)
from wikipedia has been copy and pasted into the file ```university_towns.txt```. 
* The [GDP over time](http://www.bea.gov/national/index.htm#gdp) of the United States from the Bureau of Economic Analysis, US Department of Commerce, stored in the file ```gdplev.xls```
Below is the code for Python 3:

```python
import pandas as pd
from scipy.stats import ttest_ind
```

A _university town_ is a city which has a high percentage of university students compared to the total population of the city.


```python
def get_list_of_university_towns():
    '''Returns a DataFrame with multi index consisting of the towns and the states from the 
    university_towns.txt list.'''
    text_file = open("university_towns.txt")
    # Make a dictionary with key as the line number of the states that have "[edit]" after them 
    # and value as state name itself without "[edit]" 
    State = {idx: lines.strip().replace("[edit]", "") 
             for idx,lines in enumerate(text_file) if "edit" in lines} 
    # Convert the dictionary to a series
    State = pd.Series(State) 
    # Create a data frame with one column as Region names
    university_towns = pd.read_csv("university_towns.txt", sep = "\n", header = None, 
                                   names = ["RegionName"])
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
print("List of university towns: \n")
get_list_of_university_towns()
```

    List of university towns: 
    
    
<pre>
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
    </tr>
    <tr>
      <th>State</th>
      <th>RegionName</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">Alabama</th>
      <th>Auburn</th>
    </tr>
    <tr>
      <th>Florence</th>
    </tr>
    <tr>
      <th>Jacksonville</th>
    </tr>
    <tr>
      <th>Livingston</th>
    </tr>
    <tr>
      <th>Montevallo</th>
    </tr>
    <tr>
      <th>Troy</th>
    </tr>
    <tr>
      <th>Tuscaloosa</th>
    </tr>
    <tr>
      <th>Tuskegee</th>
    </tr>
    <tr>
      <th>Alaska</th>
      <th>Fairbanks</th>
    </tr>
    <tr>
      <th rowspan="3" valign="top">Arizona</th>
      <th>Flagstaff</th>
    </tr>
    <tr>
      <th>Tempe</th>
    </tr>
    <tr>
      <th>Tucson</th>
    </tr>
    <tr>
      <th rowspan="8" valign="top">Arkansas</th>
      <th>Arkadelphia</th>
    </tr>
    <tr>
      <th>Conway</th>
    </tr>
    <tr>
      <th>Fayetteville</th>
    </tr>
    <tr>
      <th>Jonesboro</th>
    </tr>
    <tr>
      <th>Magnolia</th>
    </tr>
    <tr>
      <th>Monticello</th>
    </tr>
    <tr>
      <th>Russellville</th>
    </tr>
    <tr>
      <th>Searcy</th>
    </tr>
    <tr>
      <th rowspan="10" valign="top">California</th>
      <th>Angwin</th>
    </tr>
    <tr>
      <th>Arcata</th>
    </tr>
    <tr>
      <th>Berkeley</th>
    </tr>
    <tr>
      <th>Chico</th>
    </tr>
    <tr>
      <th>Claremont</th>
    </tr>
    <tr>
      <th>Cotati</th>
    </tr>
    <tr>
      <th>Davis</th>
    </tr>
    <tr>
      <th>Irvine</th>
    </tr>
    <tr>
      <th>Isla Vista</th>
    </tr>
    <tr>
      <th>University Park, Los Angeles</th>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Virginia</th>
      <th>Wise</th>
    </tr>
    <tr>
      <th>Chesapeake</th>
    </tr>
    <tr>
      <th rowspan="5" valign="top">Washington</th>
      <th>Bellingham</th>
    </tr>
    <tr>
      <th>Cheney</th>
    </tr>
    <tr>
      <th>Ellensburg</th>
    </tr>
    <tr>
      <th>Pullman</th>
    </tr>
    <tr>
      <th>University District, Seattle</th>
    </tr>
    <tr>
      <th rowspan="9" valign="top">West Virginia</th>
      <th>Athens</th>
    </tr>
    <tr>
      <th>Buckhannon</th>
    </tr>
    <tr>
      <th>Fairmont</th>
    </tr>
    <tr>
      <th>Glenville</th>
    </tr>
    <tr>
      <th>Huntington</th>
    </tr>
    <tr>
      <th>Montgomery</th>
    </tr>
    <tr>
      <th>Morgantown</th>
    </tr>
    <tr>
      <th>Shepherdstown</th>
    </tr>
    <tr>
      <th>West Liberty</th>
    </tr>
    <tr>
      <th rowspan="13" valign="top">Wisconsin</th>
      <th>Appleton</th>
    </tr>
    <tr>
      <th>Eau Claire</th>
    </tr>
    <tr>
      <th>Green Bay</th>
    </tr>
    <tr>
      <th>La Crosse</th>
    </tr>
    <tr>
      <th>Madison</th>
    </tr>
    <tr>
      <th>Menomonie</th>
    </tr>
    <tr>
      <th>Milwaukee</th>
    </tr>
    <tr>
      <th>Oshkosh</th>
    </tr>
    <tr>
      <th>Platteville</th>
    </tr>
    <tr>
      <th>River Falls</th>
    </tr>
    <tr>
      <th>Stevens Point</th>
    </tr>
    <tr>
      <th>Waukesha</th>
    </tr>
    <tr>
      <th>Whitewater</th>
    </tr>
    <tr>
      <th>Wyoming</th>
      <th>Laramie</th>
    </tr>
  </tbody>
</table>
<p>517 rows × 0 columns</p>
</div>
</pre>


A _quarter_ is a specific three month period, Q1 is January through March, Q2 is April through June, Q3 is July through September, Q4 is October through December.


```python
GDP = pd.read_excel("gdplev.xls", skiprows = 5)

# Drop all the rows for the data that corresponds to quarters prior to the first quarter of 2000
GDP.drop(GDP.index[:214], inplace = True)

# Drop all the rows for which there is no data values
GDP.dropna(axis = 1, how = 'all', inplace = True)

# Keep only two relevant columns: Quarter and GDP in billions of chained 2009 dollars
GDP = GDP[[0,2]]

# Rename columns
GDP.columns = ["Quarters", 'GDP in billions in current dollars']

# Set Quarters as the index to the dataframe
GDP.set_index("Quarters", inplace = True)
GDP
```

<pre>
<div>
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
    <tr>
      <th>2002q3</th>
      <td>12955.8</td>
    </tr>
    <tr>
      <th>2002q4</th>
      <td>12964.0</td>
    </tr>
    <tr>
      <th>2003q1</th>
      <td>13031.2</td>
    </tr>
    <tr>
      <th>2003q2</th>
      <td>13152.1</td>
    </tr>
    <tr>
      <th>2003q3</th>
      <td>13372.4</td>
    </tr>
    <tr>
      <th>2003q4</th>
      <td>13528.7</td>
    </tr>
    <tr>
      <th>2004q1</th>
      <td>13606.5</td>
    </tr>
    <tr>
      <th>2004q2</th>
      <td>13706.2</td>
    </tr>
    <tr>
      <th>2004q3</th>
      <td>13830.8</td>
    </tr>
    <tr>
      <th>2004q4</th>
      <td>13950.4</td>
    </tr>
    <tr>
      <th>2005q1</th>
      <td>14099.1</td>
    </tr>
    <tr>
      <th>2005q2</th>
      <td>14172.7</td>
    </tr>
    <tr>
      <th>2005q3</th>
      <td>14291.8</td>
    </tr>
    <tr>
      <th>2005q4</th>
      <td>14373.4</td>
    </tr>
    <tr>
      <th>2006q1</th>
      <td>14546.1</td>
    </tr>
    <tr>
      <th>2006q2</th>
      <td>14589.6</td>
    </tr>
    <tr>
      <th>2006q3</th>
      <td>14602.6</td>
    </tr>
    <tr>
      <th>2006q4</th>
      <td>14716.9</td>
    </tr>
    <tr>
      <th>2007q1</th>
      <td>14726.0</td>
    </tr>
    <tr>
      <th>2007q2</th>
      <td>14838.7</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>2009q1</th>
      <td>14375.0</td>
    </tr>
    <tr>
      <th>2009q2</th>
      <td>14355.6</td>
    </tr>
    <tr>
      <th>2009q3</th>
      <td>14402.5</td>
    </tr>
    <tr>
      <th>2009q4</th>
      <td>14541.9</td>
    </tr>
    <tr>
      <th>2010q1</th>
      <td>14604.8</td>
    </tr>
    <tr>
      <th>2010q2</th>
      <td>14745.9</td>
    </tr>
    <tr>
      <th>2010q3</th>
      <td>14845.5</td>
    </tr>
    <tr>
      <th>2010q4</th>
      <td>14939.0</td>
    </tr>
    <tr>
      <th>2011q1</th>
      <td>14881.3</td>
    </tr>
    <tr>
      <th>2011q2</th>
      <td>14989.6</td>
    </tr>
    <tr>
      <th>2011q3</th>
      <td>15021.1</td>
    </tr>
    <tr>
      <th>2011q4</th>
      <td>15190.3</td>
    </tr>
    <tr>
      <th>2012q1</th>
      <td>15291.0</td>
    </tr>
    <tr>
      <th>2012q2</th>
      <td>15362.4</td>
    </tr>
    <tr>
      <th>2012q3</th>
      <td>15380.8</td>
    </tr>
    <tr>
      <th>2012q4</th>
      <td>15384.3</td>
    </tr>
    <tr>
      <th>2013q1</th>
      <td>15491.9</td>
    </tr>
    <tr>
      <th>2013q2</th>
      <td>15521.6</td>
    </tr>
    <tr>
      <th>2013q3</th>
      <td>15641.3</td>
    </tr>
    <tr>
      <th>2013q4</th>
      <td>15793.9</td>
    </tr>
    <tr>
      <th>2014q1</th>
      <td>15747.0</td>
    </tr>
    <tr>
      <th>2014q2</th>
      <td>15900.8</td>
    </tr>
    <tr>
      <th>2014q3</th>
      <td>16094.5</td>
    </tr>
    <tr>
      <th>2014q4</th>
      <td>16186.7</td>
    </tr>
    <tr>
      <th>2015q1</th>
      <td>16269.0</td>
    </tr>
    <tr>
      <th>2015q2</th>
      <td>16374.2</td>
    </tr>
    <tr>
      <th>2015q3</th>
      <td>16454.9</td>
    </tr>
    <tr>
      <th>2015q4</th>
      <td>16490.7</td>
    </tr>
    <tr>
      <th>2016q1</th>
      <td>16525.0</td>
    </tr>
    <tr>
      <th>2016q2</th>
      <td>16583.1</td>
    </tr>
  </tbody>
</table>
<p>66 rows × 1 columns</p>
</div>
</pre>



```python
# Create a dataframe out of GDP with two columns - Quarters and difference in GDP of consecutive quartes
GDP_diff = GDP.diff()
GDP_diff
```

<pre>
<div>
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
    <tr>
      <th>2002q3</th>
      <td>62.8</td>
    </tr>
    <tr>
      <th>2002q4</th>
      <td>8.2</td>
    </tr>
    <tr>
      <th>2003q1</th>
      <td>67.2</td>
    </tr>
    <tr>
      <th>2003q2</th>
      <td>120.9</td>
    </tr>
    <tr>
      <th>2003q3</th>
      <td>220.3</td>
    </tr>
    <tr>
      <th>2003q4</th>
      <td>156.3</td>
    </tr>
    <tr>
      <th>2004q1</th>
      <td>77.8</td>
    </tr>
    <tr>
      <th>2004q2</th>
      <td>99.7</td>
    </tr>
    <tr>
      <th>2004q3</th>
      <td>124.6</td>
    </tr>
    <tr>
      <th>2004q4</th>
      <td>119.6</td>
    </tr>
    <tr>
      <th>2005q1</th>
      <td>148.7</td>
    </tr>
    <tr>
      <th>2005q2</th>
      <td>73.6</td>
    </tr>
    <tr>
      <th>2005q3</th>
      <td>119.1</td>
    </tr>
    <tr>
      <th>2005q4</th>
      <td>81.6</td>
    </tr>
    <tr>
      <th>2006q1</th>
      <td>172.7</td>
    </tr>
    <tr>
      <th>2006q2</th>
      <td>43.5</td>
    </tr>
    <tr>
      <th>2006q3</th>
      <td>13.0</td>
    </tr>
    <tr>
      <th>2006q4</th>
      <td>114.3</td>
    </tr>
    <tr>
      <th>2007q1</th>
      <td>9.1</td>
    </tr>
    <tr>
      <th>2007q2</th>
      <td>112.7</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>2009q1</th>
      <td>-202.0</td>
    </tr>
    <tr>
      <th>2009q2</th>
      <td>-19.4</td>
    </tr>
    <tr>
      <th>2009q3</th>
      <td>46.9</td>
    </tr>
    <tr>
      <th>2009q4</th>
      <td>139.4</td>
    </tr>
    <tr>
      <th>2010q1</th>
      <td>62.9</td>
    </tr>
    <tr>
      <th>2010q2</th>
      <td>141.1</td>
    </tr>
    <tr>
      <th>2010q3</th>
      <td>99.6</td>
    </tr>
    <tr>
      <th>2010q4</th>
      <td>93.5</td>
    </tr>
    <tr>
      <th>2011q1</th>
      <td>-57.7</td>
    </tr>
    <tr>
      <th>2011q2</th>
      <td>108.3</td>
    </tr>
    <tr>
      <th>2011q3</th>
      <td>31.5</td>
    </tr>
    <tr>
      <th>2011q4</th>
      <td>169.2</td>
    </tr>
    <tr>
      <th>2012q1</th>
      <td>100.7</td>
    </tr>
    <tr>
      <th>2012q2</th>
      <td>71.4</td>
    </tr>
    <tr>
      <th>2012q3</th>
      <td>18.4</td>
    </tr>
    <tr>
      <th>2012q4</th>
      <td>3.5</td>
    </tr>
    <tr>
      <th>2013q1</th>
      <td>107.6</td>
    </tr>
    <tr>
      <th>2013q2</th>
      <td>29.7</td>
    </tr>
    <tr>
      <th>2013q3</th>
      <td>119.7</td>
    </tr>
    <tr>
      <th>2013q4</th>
      <td>152.6</td>
    </tr>
    <tr>
      <th>2014q1</th>
      <td>-46.9</td>
    </tr>
    <tr>
      <th>2014q2</th>
      <td>153.8</td>
    </tr>
    <tr>
      <th>2014q3</th>
      <td>193.7</td>
    </tr>
    <tr>
      <th>2014q4</th>
      <td>92.2</td>
    </tr>
    <tr>
      <th>2015q1</th>
      <td>82.3</td>
    </tr>
    <tr>
      <th>2015q2</th>
      <td>105.2</td>
    </tr>
    <tr>
      <th>2015q3</th>
      <td>80.7</td>
    </tr>
    <tr>
      <th>2015q4</th>
      <td>35.8</td>
    </tr>
    <tr>
      <th>2016q1</th>
      <td>34.3</td>
    </tr>
    <tr>
      <th>2016q2</th>
      <td>58.1</td>
    </tr>
  </tbody>
</table>
<p>66 rows × 1 columns</p>
</div>
</pre>


A _recession_ starts when GDP declines for two consecutive quarters and ends when GDP grows for two consecutive quarters.


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
    

A _recession bottom_ is the quarter within a recession which had the lowest GDP.


```python
def get_recession_bottom():
    flag = 0
    for i, quarter in enumerate(GDP_diff.index):
        if (flag == 1) and (GDP_diff.iloc[i] > 0).bool() and (GDP_diff.iloc[i+1] > 0).bool():
            end_idx = i+1
            break
        if (flag == 0) and (GDP_diff.iloc[i] < 0).bool() and (GDP_diff.iloc[i+1] < 0).bool():
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
    '''Converts the housing data given in monthly format to quarters from 2000q1 through 2016q3 
    and returns it as mean values in a dataframe. This dataframe have a multi-index in the shape 
    of ["State","RegionName"].
    '''
    all_homes = pd.read_csv("City_Zhvi_AllHomes.csv")
    
    states = {'OH': 'Ohio', 'KY': 'Kentucky', 'AS': 'American Samoa', 'NV': 'Nevada', 
              'WY': 'Wyoming', 'NA': 'National', 'AL': 'Alabama', 'MD': 'Maryland', 
              'AK': 'Alaska', 'UT': 'Utah', 'OR': 'Oregon', 'MT': 'Montana', 'IL': 'Illinois', 
              'TN': 'Tennessee', 'DC': 'District of Columbia', 'VT': 'Vermont', 'ID': 'Idaho', 
              'AR': 'Arkansas', 'ME': 'Maine', 'WA': 'Washington', 'HI': 'Hawaii', 'WI': 'Wisconsin', 
              'MI': 'Michigan', 'IN': 'Indiana', 'NJ': 'New Jersey', 'AZ': 'Arizona', 'GU': 'Guam', 
              'MS': 'Mississippi', 'PR': 'Puerto Rico', 'NC': 'North Carolina', 'TX': 'Texas', 
              'SD': 'South Dakota', 'MP': 'Northern Mariana Islands', 'IA': 'Iowa', 'MO': 'Missouri', 
              'CT': 'Connecticut', 'WV': 'West Virginia', 'SC': 'South Carolina', 'LA': 'Louisiana', 
              'KS': 'Kansas', 'NY': 'New York', 'NE': 'Nebraska', 'OK': 'Oklahoma', 'FL': 'Florida', 
              'CA': 'California', 'CO': 'Colorado', 'PA': 'Pennsylvania', 'DE': 'Delaware', 
              'NM': 'New Mexico', 'RI': 'Rhode Island', 'MN': 'Minnesota', 'VI': 'Virgin Islands', 
              'NH': 'New Hampshire', 'MA': 'Massachusetts', 'GA': 'Georgia', 'ND': 'North Dakota', 
              'VA': 'Virginia'}
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
    # Groups the monthly columns into quarters using mean value of the four monthly columns
    housing = all_homes.groupby(quarters, axis = 1).mean() 
    housing = housing.sort_index()
    return housing

housing = convert_housing_data_to_quarters()
print("Columns: \n", housing.columns)
print("# Rows: ", len(housing))
housing.head()
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
    



<pre>
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>2000q1</th>
      <th>2000q2</th>
      <th>2000q3</th>
      <th>2000q4</th>
      <th>2001q1</th>
      <th>2001q2</th>
      <th>2001q3</th>
      <th>2001q4</th>
      <th>2002q1</th>
      <th>2002q2</th>
      <th>...</th>
      <th>2014q2</th>
      <th>2014q3</th>
      <th>2014q4</th>
      <th>2015q1</th>
      <th>2015q2</th>
      <th>2015q3</th>
      <th>2015q4</th>
      <th>2016q1</th>
      <th>2016q2</th>
      <th>2016q3</th>
    </tr>
    <tr>
      <th>State</th>
      <th>RegionName</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Alabama</th>
      <th>Adamsville</th>
      <td>69033.333333</td>
      <td>69166.666667</td>
      <td>69800.000000</td>
      <td>71966.666667</td>
      <td>73466.666667</td>
      <td>74000.000000</td>
      <td>73333.333333</td>
      <td>73100.000000</td>
      <td>73333.333333</td>
      <td>73133.333333</td>
      <td>...</td>
      <td>77066.666667</td>
      <td>75966.666667</td>
      <td>71900.0</td>
      <td>71666.666667</td>
      <td>73033.333333</td>
      <td>73933.333333</td>
      <td>73866.666667</td>
      <td>74166.666667</td>
      <td>74933.333333</td>
      <td>74700.0</td>
    </tr>
    <tr>
      <th>Alabaster</th>
      <td>122133.333333</td>
      <td>123066.666667</td>
      <td>123166.666667</td>
      <td>123700.000000</td>
      <td>123233.333333</td>
      <td>125133.333333</td>
      <td>127766.666667</td>
      <td>127200.000000</td>
      <td>127300.000000</td>
      <td>128000.000000</td>
      <td>...</td>
      <td>147133.333333</td>
      <td>147633.333333</td>
      <td>148700.0</td>
      <td>148900.000000</td>
      <td>149566.666667</td>
      <td>150366.666667</td>
      <td>151733.333333</td>
      <td>153466.666667</td>
      <td>155100.000000</td>
      <td>155850.0</td>
    </tr>
    <tr>
      <th>Albertville</th>
      <td>73966.666667</td>
      <td>72600.000000</td>
      <td>72833.333333</td>
      <td>74200.000000</td>
      <td>75900.000000</td>
      <td>76000.000000</td>
      <td>72066.666667</td>
      <td>73566.666667</td>
      <td>76533.333333</td>
      <td>76366.666667</td>
      <td>...</td>
      <td>84033.333333</td>
      <td>84766.666667</td>
      <td>86800.0</td>
      <td>88466.666667</td>
      <td>89500.000000</td>
      <td>90233.333333</td>
      <td>91366.666667</td>
      <td>92000.000000</td>
      <td>92466.666667</td>
      <td>92200.0</td>
    </tr>
    <tr>
      <th>Arab</th>
      <td>83766.666667</td>
      <td>81566.666667</td>
      <td>81333.333333</td>
      <td>82966.666667</td>
      <td>84200.000000</td>
      <td>84533.333333</td>
      <td>81666.666667</td>
      <td>83900.000000</td>
      <td>87266.666667</td>
      <td>87700.000000</td>
      <td>...</td>
      <td>113366.666667</td>
      <td>111700.000000</td>
      <td>111600.0</td>
      <td>110166.666667</td>
      <td>109433.333333</td>
      <td>110900.000000</td>
      <td>112233.333333</td>
      <td>110033.333333</td>
      <td>110100.000000</td>
      <td>112000.0</td>
    </tr>
    <tr>
      <th>Ardmore</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>140533.333333</td>
      <td>139566.666667</td>
      <td>140900.0</td>
      <td>143233.333333</td>
      <td>143000.000000</td>
      <td>144600.000000</td>
      <td>143966.666667</td>
      <td>142566.666667</td>
      <td>143233.333333</td>
      <td>141950.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 67 columns</p>
</div>
</pre>


**Hypothesis**: University towns have their mean housing prices less effected by recessions. Running a t-test to compare the ratio of the mean price of houses in university towns the quarter before the recession starts compared to the recession bottom. (`price_ratio=quarter_before_recession/recession_bottom`)



```python
def run_ttest():
    '''First creates new data showing the decline or growth of housing prices
    between the recession start and the recession bottom. Then runs a ttest
    comparing the university town values to the non-university towns values, 
    return whether the alternative hypothesis (that the two groups are the same)
    is true or not as well as the p-value of the confidence. 
    
    Returns the tuple (different, p, better) where different=True if the t-test is
    True at a p<0.01 (we reject the null hypothesis), or different=False if 
    otherwise (we cannot reject the null hypothesis). The variable p is the 
    exact p value returned from scipy.stats.ttest_ind(). The value for better is 
    either "university town" or "non-university town" depending on which has a 
    lower mean price ratio (which is equivilent to a reduced market loss).'''
    
    
    housing = convert_housing_data_to_quarters()
    university_towns = get_list_of_university_towns()
    quarter_before_recession = get_quarter_before_recession()    
    recession_bottom = get_recession_bottom()
    
    # Keep columns corresponding to only two quarters - quarter before recession and recession bottom
    housing = housing[[quarter_before_recession, recession_bottom]]
    housing["price_ratio"] = housing[quarter_before_recession].div(housing[recession_bottom])
    housing = housing.dropna()
    
    # Merge the housing dataframa with the one with the university towns taking the intersection of 
    # both the dataframes. The new dataframe for housing in university towns has the multi-index of 
    # States and Region names.
    university_housing = pd.merge(university_towns, housing, how = "inner", 
                                  left_index = True, right_index = True)
    
    # Left over rows from housing gives the dataframe for housing in non-university towns
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



Since the p-value is less than 0.01, we reject the null hypotheses of equal expected price ratios for university and non-university towns. Moreover, t-statistic is negative implying the price ratio for the university towns is less than that for remaining towns. This in turn suggests that prices for houses in university towns were less affected during recession as compared to that of non-university towns. 

