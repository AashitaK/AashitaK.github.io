
# Extracting dates from medical records
### - Aashita Kesarwani

The aim of the project is first to identify dates given in different formats from the messy medical data and convert them in the same format and then sort them. The project was a weekly assignment from the course [Applied Text Mining in Python](https://www.coursera.org/learn/python-text-mining/) offered by the University of Michigan on Coursera. 

First, we start with loading data and importing pandas module for working with the data:


```python
import pandas as pd
doc = []
with open('dates.txt') as file:
    for line in file:
        doc.append(line)
df = pd.Series(doc)
```

Our data consists of medical notes where each note has a date that needs to be extracted. There are 500 records in total as shown below:


```python
df
```




    0           03/25/93 Total time of visit (in minutes):\n
    1                         6/18/85 Primary Care Doctor:\n
    2      sshe plans to move as of 7/8/71 In-Home Servic...
    3                  7 on 9/27/75 Audit C Score Current:\n
    4      2/6/96 sleep studyPain Treatment Pain Level (N...
    5                      .Per 7/06/79 Movement D/O note:\n
    6      4, 5/18/78 Patient's thoughts about current su...
    7      10/24/89 CPT Code: 90801 - Psychiatric Diagnos...
    8                           3/7/86 SOS-10 Total Score:\n
    9               (4/10/71)Score-1Audit C Score Current:\n
    10     (5/11/85) Crt-1.96, BUN-26; AST/ALT-16/22; WBC...
    11                         4/09/75 SOS-10 Total Score:\n
    12     8/01/98 Communication with referring physician...
    13     1/26/72 Communication with referring physician...
    14     5/24/1990 CPT Code: 90792: With medical servic...
    15     1/25/2011 CPT Code: 90792: With medical servic...
    16           4/12/82 Total time of visit (in minutes):\n
    17          1; 10/13/1976 Audit C Score, Highest/Date:\n
    18                   4, 4/24/98 Relevant Drug History:\n
    19     ) 59 yo unemployed w referred by Urgent Care f...
    20           7/21/98 Total time of visit (in minutes):\n
    21                        10/21/79 SOS-10 Total Score:\n
    22      3/03/90 CPT Code: 90792: With medical services\n
    23      2/11/76 CPT Code: 90792: With medical services\n
    24     07/25/1984 CPT Code: 90791: No medical services\n
    25     4-13-82 Other Child Mental Health Outcomes Sca...
    26      9/22/89 CPT Code: 90792: With medical services\n
    27        9/02/76 CPT Code: 90791: No medical services\n
    28                                9/12/71 [report_end]\n
    29     10/24/86 Communication with referring physicia...
                                 ...                        
    470    y1983 Clinic Hospital, first hospitalization, ...
    471    tProblems Urinary incontinence : mild urge inc...
    472    .2010 - wife; nightmares and angry outbursts; ...
    473         shx of TBI (1975) ISO MVA.Medical History:\n
    474    sPatient reported losing three friends that pa...
    475                        TSH okay in 2015 Prior EKG:\n
    476    1989 Family Psych History: Family History of S...
    477    oEnjoys animals, had a dog x 14 yrs who died i...
    478    eHistory of small right parietal subgaleal hem...
    479    sIn KEP Psychiatryfor therapy and medications ...
    480    1. Esophageal cancer, dx: 2013, on FOLFOX with...
    481                                        y1974 (all)\n
    482    h/o restraining order by sister/mother in 1990...
    483    sTexas Medical Center; Oklahoma for 2 weeks; 1...
    484    Death of former partner in 2004 by overdose as...
    485    Was "average" student.  "I didn't have too man...
    486    Contemplating jumping off building - 1973 - di...
    487    appendectomy s/p delivery 1992 Prior relevant ...
    488    tProblems renal cell cancer : s/p nephrectomy ...
    489        ran own business for 35 years, sold in 1985\n
    490                                  Lab: B12 969 2007\n
    491                                   )and 8mo in 2009\n
    492    .Moved to USA in 1986. Suffered from malnutrit...
    493                                              r1978\n
    494    . Went to Emerson, in Newfane Alaska. Started ...
    495    1979 Family Psych History: Family History of S...
    496    therapist and friend died in ~2006 Parental/Ca...
    497                         2008 partial thyroidectomy\n
    498    sPt describes a history of sexual abuse as a c...
    499    . In 1980, patient was living in Naples and de...
    Length: 500, dtype: object



An example of medical record is shown below. 


```python
df[19]
```




    ') 59 yo unemployed w referred by Urgent Care for psychiatric evaluation and follow up. The patient reports she has been dx w BAD. Her main complaint today is anergy. Ms. Hartman was evaluated on one occasion 5/21/77. She was a cooperative but somewhat vague historian.History of Present Illness and Precipitating Events\n'



The dates in the records are encoded in different formats. Here is a list of some of the variants present in this dataset:  
1. 04/20/2009; 04/20/09; 4/20/09; 4/3/09  
2. Mar-20-2009; Mar 20, 2009; March 20, 2009;  Mar. 20, 2009; Mar 20 2009  
3. 20 Mar 2009; 20 March 2009; 20 Mar. 2009; 20 March, 2009  
4. Mar 20th, 2009; Mar 21st, 2009; Mar 22nd, 2009  
5. Feb 2009; Sep 2009; Oct 2010  
6. 6/2008; 12/2009  
7. 2009; 2010    
 
I encountered a couple typos in the dates as this is a raw, real-life derived dataset. Below is the code to extract all the dates while ignoring other numerals that might seem similar to dates.


```python
Text = df.copy()
Text = Text.str.replace("Janaury", "January")
Text = Text.str.replace("Decemeber", "December")
def re_1(text):
    return text.str.extract("(?P<Date>(?P<Month>[01]?\d)[/-](?P<Day>[0123]?\d)[/-](?P<Year>\d{4}))")
def re_2(text):
    return text.str.extract("(?P<Date>(?P<Month>[01]?\d)[/-](?P<Day>[0123]?\d)[/-](?P<Year>\d{2}))")
def re_3(text):
    return text.str.extract("(?P<Date>(?P<Month>[01]?\d)[/-](?P<Year>[12][90]\d{2}))")
def re_4(text):
    return text.str.extract("(?P<Date>(?P<Day>[0123]?\d)\s(?P<Month>January|February|March|April|June|July|August|September|October|November|December|Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec)\s(?P<Year>\d{4}))")
def re_5(text):
    return text.str.extract("(?P<Date>(?P<Month>January|February|March|April|June|July|August|September|October|November|December|Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec)\.?\s(?P<Day>[0123]?\d),?\s(?P<Year>\d{4}))")
def re_6(text):
    return text.str.extract("(?P<Date>(?P<Month>January|February|March|April|June|July|August|September|October|November|December|Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),?\s(?P<Year>\d{4}))")
def re_7(text):
    return text.str.extract("(?P<Date>(?P<Year>\d{4}))")
df1 = re_1(Text).dropna(how="all")
Text = Text.drop(list(df1.index))
df2 = re_2(Text).dropna(how="all")
Text = Text.drop(list(df2.index))
df2.Year = df2.Year.apply(lambda x: '19' + x)
df3 = re_3(Text).dropna(how="all")
df3["Day"] = 1
Text = Text.drop(list(df3.index))
df4 = re_4(Text).dropna(how="all")
df4.Month = df4.Month.apply(lambda x: x[:3])
Text = Text.drop(list(df4.index))
df5 = re_5(Text).dropna(how="all")
df5.Month = df5.Month.apply(lambda x: x[:3])
Text = Text.drop(list(df5.index))
df6 = re_6(Text).dropna(how="all")
df6.Month = df6.Month.apply(lambda x: x[:3])
df6["Day"] = 1
Text = Text.drop(list(df6.index))
df7 = re_7(Text).dropna(how="all")
df7["Day"] = 1
df7["Month"] = 1
Text = Text.drop(list(df7.index))

Date = pd.concat([df1, df2, df3, df4, df5, df6, df7])
Date.sample(30)
```




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
      <th>Date</th>
      <th>Day</th>
      <th>Month</th>
      <th>Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>69</th>
      <td>11/3/1985</td>
      <td>3</td>
      <td>11</td>
      <td>1985</td>
    </tr>
    <tr>
      <th>22</th>
      <td>3/03/90</td>
      <td>03</td>
      <td>3</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>103</th>
      <td>9/22/82</td>
      <td>22</td>
      <td>9</td>
      <td>1982</td>
    </tr>
    <tr>
      <th>480</th>
      <td>2013</td>
      <td>1</td>
      <td>1</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>229</th>
      <td>June 2011</td>
      <td>1</td>
      <td>Jun</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>259</th>
      <td>Nov 1979</td>
      <td>1</td>
      <td>Nov</td>
      <td>1979</td>
    </tr>
    <tr>
      <th>320</th>
      <td>November 2012</td>
      <td>1</td>
      <td>Nov</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>155</th>
      <td>10 Oct 1974</td>
      <td>10</td>
      <td>Oct</td>
      <td>1974</td>
    </tr>
    <tr>
      <th>310</th>
      <td>Oct 1992</td>
      <td>1</td>
      <td>Oct</td>
      <td>1992</td>
    </tr>
    <tr>
      <th>331</th>
      <td>December 1993</td>
      <td>1</td>
      <td>Dec</td>
      <td>1993</td>
    </tr>
    <tr>
      <th>207</th>
      <td>August 12 2004</td>
      <td>12</td>
      <td>Aug</td>
      <td>2004</td>
    </tr>
    <tr>
      <th>135</th>
      <td>10 Oct 1985</td>
      <td>10</td>
      <td>Oct</td>
      <td>1985</td>
    </tr>
    <tr>
      <th>201</th>
      <td>December 23, 1999</td>
      <td>23</td>
      <td>Dec</td>
      <td>1999</td>
    </tr>
    <tr>
      <th>400</th>
      <td>11/2008</td>
      <td>1</td>
      <td>11</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>322</th>
      <td>October 1991</td>
      <td>1</td>
      <td>Oct</td>
      <td>1991</td>
    </tr>
    <tr>
      <th>64</th>
      <td>07/29/1994</td>
      <td>29</td>
      <td>07</td>
      <td>1994</td>
    </tr>
    <tr>
      <th>65</th>
      <td>08/11/78</td>
      <td>11</td>
      <td>08</td>
      <td>1978</td>
    </tr>
    <tr>
      <th>142</th>
      <td>22 Jan 1996</td>
      <td>22</td>
      <td>Jan</td>
      <td>1996</td>
    </tr>
    <tr>
      <th>350</th>
      <td>5/2004</td>
      <td>1</td>
      <td>5</td>
      <td>2004</td>
    </tr>
    <tr>
      <th>424</th>
      <td>4/1979</td>
      <td>1</td>
      <td>4</td>
      <td>1979</td>
    </tr>
    <tr>
      <th>407</th>
      <td>8/1999</td>
      <td>1</td>
      <td>8</td>
      <td>1999</td>
    </tr>
    <tr>
      <th>165</th>
      <td>18 August 1975</td>
      <td>18</td>
      <td>Aug</td>
      <td>1975</td>
    </tr>
    <tr>
      <th>396</th>
      <td>8/2008</td>
      <td>1</td>
      <td>8</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>311</th>
      <td>February, 1995</td>
      <td>1</td>
      <td>Feb</td>
      <td>1995</td>
    </tr>
    <tr>
      <th>221</th>
      <td>Oct 18, 1980</td>
      <td>18</td>
      <td>Oct</td>
      <td>1980</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5/11/85</td>
      <td>11</td>
      <td>5</td>
      <td>1985</td>
    </tr>
    <tr>
      <th>262</th>
      <td>Jun 2002</td>
      <td>1</td>
      <td>Jun</td>
      <td>2002</td>
    </tr>
    <tr>
      <th>38</th>
      <td>7/27/1986</td>
      <td>27</td>
      <td>7</td>
      <td>1986</td>
    </tr>
    <tr>
      <th>230</th>
      <td>May 1986</td>
      <td>1</td>
      <td>May</td>
      <td>1986</td>
    </tr>
    <tr>
      <th>249</th>
      <td>April 1993</td>
      <td>1</td>
      <td>Apr</td>
      <td>1993</td>
    </tr>
  </tbody>
</table>
</div>



Once these date patterns are extracted from the text, they are encoded in the same format of  the next step is to sort them in ascending chronological order according to the following rules:  
1. Assumed all dates in xx/xx/xx format are mm/dd/yy.    
2. Assumed all dates where year is encoded in only two digits are years from the 1900's (e.g. 1/5/89 is January 5th, 1989).  
3. If the day is missing (e.g. 9/2009), assumed it is the first day of the month (e.g. September 1, 2009).    
4. If the month is missing (e.g. 2010), assumed it is the first of January of that year (e.g. January 1, 2010).

Below is the code to sort the dates in ascending chronological order:


```python
months_dict = {'Jan': 1, 'Feb': 2, 'Mar': 3, 'Apr': 4, 'May': 5, 'Jun': 6, 
               'Jul': 7, 'Aug': 8, 'Sep': 9, 'Oct': 10, 'Nov': 9, 'Dec': 12}
Date.Month = Date.Month.replace(months_dict)
Date.Month = Date.Month.astype('int')
Date.Day = Date.Day.astype('int')
Date.Year = Date.Year.astype('int')
Date = Date.sort_values(by=["Year", "Month", "Day"])
Date
```




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
      <th>Date</th>
      <th>Day</th>
      <th>Month</th>
      <th>Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>4/10/71</td>
      <td>10</td>
      <td>4</td>
      <td>1971</td>
    </tr>
    <tr>
      <th>84</th>
      <td>5/18/71</td>
      <td>18</td>
      <td>5</td>
      <td>1971</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/8/71</td>
      <td>8</td>
      <td>7</td>
      <td>1971</td>
    </tr>
    <tr>
      <th>53</th>
      <td>7/11/71</td>
      <td>11</td>
      <td>7</td>
      <td>1971</td>
    </tr>
    <tr>
      <th>28</th>
      <td>9/12/71</td>
      <td>12</td>
      <td>9</td>
      <td>1971</td>
    </tr>
    <tr>
      <th>474</th>
      <td>1972</td>
      <td>1</td>
      <td>1</td>
      <td>1972</td>
    </tr>
    <tr>
      <th>153</th>
      <td>13 Jan 1972</td>
      <td>13</td>
      <td>1</td>
      <td>1972</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1/26/72</td>
      <td>26</td>
      <td>1</td>
      <td>1972</td>
    </tr>
    <tr>
      <th>129</th>
      <td>06 May 1972</td>
      <td>6</td>
      <td>5</td>
      <td>1972</td>
    </tr>
    <tr>
      <th>98</th>
      <td>5/13/72</td>
      <td>13</td>
      <td>5</td>
      <td>1972</td>
    </tr>
    <tr>
      <th>111</th>
      <td>6/10/72</td>
      <td>10</td>
      <td>6</td>
      <td>1972</td>
    </tr>
    <tr>
      <th>225</th>
      <td>June 15, 1972</td>
      <td>15</td>
      <td>6</td>
      <td>1972</td>
    </tr>
    <tr>
      <th>31</th>
      <td>7/20/72</td>
      <td>20</td>
      <td>7</td>
      <td>1972</td>
    </tr>
    <tr>
      <th>191</th>
      <td>30 Nov 1972</td>
      <td>30</td>
      <td>9</td>
      <td>1972</td>
    </tr>
    <tr>
      <th>171</th>
      <td>04 Oct 1972</td>
      <td>4</td>
      <td>10</td>
      <td>1972</td>
    </tr>
    <tr>
      <th>486</th>
      <td>1973</td>
      <td>1</td>
      <td>1</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>415</th>
      <td>2/1973</td>
      <td>1</td>
      <td>2</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>335</th>
      <td>February 1973</td>
      <td>1</td>
      <td>2</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2/14/73</td>
      <td>14</td>
      <td>2</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>405</th>
      <td>03/1973</td>
      <td>1</td>
      <td>3</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>323</th>
      <td>March 1973</td>
      <td>1</td>
      <td>3</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>422</th>
      <td>4/1973</td>
      <td>1</td>
      <td>4</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>375</th>
      <td>06/1973</td>
      <td>1</td>
      <td>6</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>380</th>
      <td>7/1973</td>
      <td>1</td>
      <td>7</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>345</th>
      <td>10/1973</td>
      <td>1</td>
      <td>10</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>57</th>
      <td>12/01/73</td>
      <td>1</td>
      <td>12</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>481</th>
      <td>1974</td>
      <td>1</td>
      <td>1</td>
      <td>1974</td>
    </tr>
    <tr>
      <th>436</th>
      <td>2/1974</td>
      <td>1</td>
      <td>2</td>
      <td>1974</td>
    </tr>
    <tr>
      <th>104</th>
      <td>2/24/74</td>
      <td>24</td>
      <td>2</td>
      <td>1974</td>
    </tr>
    <tr>
      <th>299</th>
      <td>March 1974</td>
      <td>1</td>
      <td>3</td>
      <td>1974</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>220</th>
      <td>June 25, 2012</td>
      <td>25</td>
      <td>6</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>208</th>
      <td>September 01, 2012</td>
      <td>1</td>
      <td>9</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>243</th>
      <td>Sep 2012</td>
      <td>1</td>
      <td>9</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>320</th>
      <td>November 2012</td>
      <td>1</td>
      <td>9</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>139</th>
      <td>21 Oct 2012</td>
      <td>21</td>
      <td>10</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>383</th>
      <td>12/2012</td>
      <td>1</td>
      <td>12</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>244</th>
      <td>January, 2013</td>
      <td>1</td>
      <td>1</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>286</th>
      <td>January 2013</td>
      <td>1</td>
      <td>1</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>480</th>
      <td>2013</td>
      <td>1</td>
      <td>1</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>431</th>
      <td>4/2013</td>
      <td>1</td>
      <td>4</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>279</th>
      <td>Sep 2013</td>
      <td>1</td>
      <td>9</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>198</th>
      <td>October. 11, 2013</td>
      <td>11</td>
      <td>10</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>381</th>
      <td>1/2014</td>
      <td>1</td>
      <td>1</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>463</th>
      <td>2014</td>
      <td>1</td>
      <td>1</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>366</th>
      <td>7/2014</td>
      <td>1</td>
      <td>7</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>439</th>
      <td>10/2014</td>
      <td>1</td>
      <td>10</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>255</th>
      <td>Oct 2014</td>
      <td>1</td>
      <td>10</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>401</th>
      <td>12/2014</td>
      <td>1</td>
      <td>12</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>475</th>
      <td>2015</td>
      <td>1</td>
      <td>1</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>257</th>
      <td>Sep 2015</td>
      <td>1</td>
      <td>9</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>152</th>
      <td>28 Sep 2015</td>
      <td>28</td>
      <td>9</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>235</th>
      <td>Oct 2015</td>
      <td>1</td>
      <td>10</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>464</th>
      <td>2016</td>
      <td>1</td>
      <td>1</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>253</th>
      <td>Feb 2016</td>
      <td>1</td>
      <td>2</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>427</th>
      <td>5/2016</td>
      <td>1</td>
      <td>5</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>231</th>
      <td>May 2016</td>
      <td>1</td>
      <td>5</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>141</th>
      <td>30 May 2016</td>
      <td>30</td>
      <td>5</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>186</th>
      <td>13 Oct 2016</td>
      <td>13</td>
      <td>10</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>161</th>
      <td>19 Oct 2016</td>
      <td>19</td>
      <td>10</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>413</th>
      <td>11/2016</td>
      <td>1</td>
      <td>11</td>
      <td>2016</td>
    </tr>
  </tbody>
</table>
<p>500 rows × 4 columns</p>
</div>



The first column above is the index which is unique to each medical record, so now we have medical records sorted in ascending chronological order of the dates mentioned in them. The indices of the earliest 10 medical records are given below:


```python
print("\n".join(map(str,Date.index[:10])))
```

    9
    84
    2
    53
    28
    474
    153
    13
    129
    98

