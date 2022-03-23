---
title: Introduction to Pandas
layout: post
date: 2019-01-11 11:20
image: /assets/images/IntroductionToPandas/pandas.png
headerImage: true
tag:
- pandas
- tutorial
- Explained

star: false
category: blog
author: Rohit Midha
---
This is the first tutorial of the Explained! series.

I will be cataloging all the work I do with regards to PyLibraries and will share it here or on [my Github](http://bit.ly/RohitMidha23GitHub).

I will also be updating this post as and when I work on Pandas.

That being said, Dive in!

## Series


```python
import pandas as pd
import numpy as np
import random
```


```python
first_series = pd.Series([1,2,3, np.nan ,"hello"])
first_series
```




    0        1
    1        2
    2        3
    3      NaN
    4    hello
    dtype: object




```python
series = pd.Series([1,2,3, np.nan ,"hello"], index = ['A','B','C','Unknown','String'])
series
#indexing the Series with custom values
```




    A              1
    B              2
    C              3
    Unknown      NaN
    String     hello
    dtype: object




```python
dict = {"Python": "Fun", "C++": "Outdated","Coding":"Hmm.."}
series = pd.Series(dict)
series
# Dict to pandas Series
```




    Python         Fun
    C++       Outdated
    Coding       Hmm..
    dtype: object




```python
series[['Coding','Python']]
```




    Coding    Hmm..
    Python      Fun
    dtype: object




```python
series.index
```




    Index(['Python', 'C++', 'Coding'], dtype='object')




```python
series.values
```




    array(['Fun', 'Outdated', 'Hmm..'], dtype=object)




```python
series.describe()
```




    count            3
    unique           3
    top       Outdated
    freq             1
    dtype: object




```python
#Series is a mutable data structures and you can easily change any item’s value:
series['Coding'] = 'Awesome'
series
```




    Python         Fun
    C++       Outdated
    Coding     Awesome
    dtype: object




```python
# add new values:
series['Java'] = 'Okay'
series
```




    Python         Fun
    C++       Outdated
    Coding     Awesome
    Java          Okay
    dtype: object




```python
# If it is necessary to apply any mathematical operation to Series items, you may done it like below:
num_series = pd.Series([1,2,3,4,5,6,None])
num_series_changed = num_series/2
num_series_changed
```




    0    0.5
    1    1.0
    2    1.5
    3    2.0
    4    2.5
    5    3.0
    6    NaN
    dtype: float64




```python
# NULL/NaN checking can be performed with isnull() and notnull().
print(series.isnull())
print(num_series.notnull())
print(num_series_changed.notnull())
```

    Python    False
    C++       False
    Coding    False
    Java      False
    dtype: bool
    0     True
    1     True
    2     True
    3     True
    4     True
    5     True
    6    False
    dtype: bool
    0     True
    1     True
    2     True
    3     True
    4     True
    5     True
    6    False
    dtype: bool

---
## DataFrames


```python
data = {'year': [1990, 1994, 1998, 2002, 2006, 2010, 2014],
        'winner': ['Germany', 'Brazil', 'France', 'Brazil','Italy', 'Spain', 'Germany'],
        'runner-up': ['Argentina', 'Italy', 'Brazil','Germany', 'France', 'Netherlands', 'Argentina'],
        'final score': ['1-0', '0-0 (pen)', '3-0', '2-0', '1-1 (pen)', '1-0', '1-0'] }
world_cup = pd.DataFrame(data, columns=['year', 'winner', 'runner-up', 'final score'])
world_cup
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>winner</th>
      <th>runner-up</th>
      <th>final score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1990</td>
      <td>Germany</td>
      <td>Argentina</td>
      <td>1-0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1994</td>
      <td>Brazil</td>
      <td>Italy</td>
      <td>0-0 (pen)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1998</td>
      <td>France</td>
      <td>Brazil</td>
      <td>3-0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2002</td>
      <td>Brazil</td>
      <td>Germany</td>
      <td>2-0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2006</td>
      <td>Italy</td>
      <td>France</td>
      <td>1-1 (pen)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2010</td>
      <td>Spain</td>
      <td>Netherlands</td>
      <td>1-0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2014</td>
      <td>Germany</td>
      <td>Argentina</td>
      <td>1-0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Another way to set a DataFrame is the using of Python list of dictionaries:

data_2 = [{'year': 1990, 'winner': 'Germany', 'runner-up': 'Argentina', 'final score': '1-0'},
          {'year': 1994, 'winner': 'Brazil', 'runner-up': 'Italy', 'final score': '0-0 (pen)'},
          {'year': 1998, 'winner': 'France', 'runner-up': 'Brazil', 'final score': '3-0'},
          {'year': 2002, 'winner': 'Brazil', 'runner-up': 'Germany', 'final score': '2-0'},
          {'year': 2006, 'winner': 'Italy','runner-up': 'France', 'final score': '1-1 (pen)'},
          {'year': 2010, 'winner': 'Spain', 'runner-up': 'Netherlands', 'final score': '1-0'},
          {'year': 2014, 'winner': 'Germany', 'runner-up': 'Argentina', 'final score': '1-0'}
         ]
world_cup = pd.DataFrame(data_2)
world_cup
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>final score</th>
      <th>runner-up</th>
      <th>winner</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1-0</td>
      <td>Argentina</td>
      <td>Germany</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0-0 (pen)</td>
      <td>Italy</td>
      <td>Brazil</td>
      <td>1994</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3-0</td>
      <td>Brazil</td>
      <td>France</td>
      <td>1998</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2-0</td>
      <td>Germany</td>
      <td>Brazil</td>
      <td>2002</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1-1 (pen)</td>
      <td>France</td>
      <td>Italy</td>
      <td>2006</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1-0</td>
      <td>Netherlands</td>
      <td>Spain</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1-0</td>
      <td>Argentina</td>
      <td>Germany</td>
      <td>2014</td>
    </tr>
  </tbody>
</table>
</div>




```python
print("First 2 Rows: ",end="\n\n")
print (world_cup.head(2),end="\n\n")
print ("Last 2 Rows : ",end="\n\n")
print (world_cup.tail(2),end="\n\n")
print("Using slicing : ",end="\n\n")
print (world_cup[2:4])
```

    First 2 Rows:

      final score  runner-up   winner  year
    0         1-0  Argentina  Germany  1990
    1   0-0 (pen)      Italy   Brazil  1994

    Last 2 Rows :

      final score    runner-up   winner  year
    5         1-0  Netherlands    Spain  2010
    6         1-0    Argentina  Germany  2014

    Using slicing :

      final score runner-up  winner  year
    2         3-0    Brazil  France  1998
    3         2-0   Germany  Brazil  2002

---
### CSV
#### Reading:

`df = pd.read_csv("path\to\the\csv\file\for\reading")`
#### Writing:

`df.to_csv("path\to\the\folder\where\you\want\save\csv\file")`


### TXT file(s)
(txt file can be read as a CSV file with other separator (delimiter); we suppose below that columns are separated by tabulation):

#### Reading:

`df = pd.read_csv("path\to\the\txt\file\for\reading", sep='\t')`
#### Writing:

`df.to_csv("path\to\the\folder\where\you\want\save\txt\file", sep='\t')`
### JSON files
(an open-standard format that uses human-readable text to transmit data objects consisting of attribute–value pairs. It is the most common data format used for asynchronous browser/server communication. By its view it is very similar to Python dictionary)

#### Reading:

`df = pd.read_json("path\to\the\json\file\for\reading", sep='\t')`
#### Writing:

`df.to_json("path\to\the\folder\where\you\want\save\json\file", sep='\t')`


```python
# To write world_cup Dataframe to a CSV File
world_cup.to_csv("worldcup.csv")
# To save CSV file without index use index=False attribute

print("File Written!",end="\n\n")

#To check if it was written
import os
print(os.path.exists('worldcup.csv'))

# reading from it in a new dataframe df
df = pd.read_csv('worldcup.csv')
print(df.head())


```

    File Written!

    True
       Unnamed: 0 final score  runner-up   winner  year
    0           0         1-0  Argentina  Germany  1990
    1           1   0-0 (pen)      Italy   Brazil  1994
    2           2         3-0     Brazil   France  1998
    3           3         2-0    Germany   Brazil  2002
    4           4   1-1 (pen)     France    Italy  2006



```python
# We can also load the data without index as :
df = pd.read_csv('worldcup.csv',index_col=0)
print(df)
```

      final score    runner-up   winner  year
    0         1-0    Argentina  Germany  1990
    1   0-0 (pen)        Italy   Brazil  1994
    2         3-0       Brazil   France  1998
    3         2-0      Germany   Brazil  2002
    4   1-1 (pen)       France    Italy  2006
    5         1-0  Netherlands    Spain  2010
    6         1-0    Argentina  Germany  2014


---
You can find the dataset used in the following code [here](http://bit.ly/MoviesDatasetExplained).
```python
movies=pd.read_csv("data/movies.csv",encoding = "ISO-8859-1")
# encoding is added only for this specific dataset because it gave error with utf-8
```


```python
movies['release_date'] = movies['release_date'].map(pd.to_datetime)
print(movies.head(20))

#print(movies.describe())
```

        user_id  movie_id  rating  timestamp   age gender     occupation zip_code  \
    0       196       242       3  881250949  49.0      M         writer    55105   
    1       305       242       5  886307828  23.0      M     programmer    94086   
    2         6       242       4  883268170  42.0      M      executive    98101   
    3       234       242       4  891033261  60.0      M        retired    94702   
    4        63       242       3  875747190  31.0      M      marketing    75240   
    5       181       242       1  878961814  26.0      M      executive    21218   
    6       201       242       4  884110598  27.0      M         writer    E2A4H   
    7       249       242       5  879571438  25.0      M        student    84103   
    8        13       242       2  881515193  47.0      M       educator    29206   
    9       279       242       3  877756647  33.0      M     programmer    85251   
    10      145       242       5  875269755  31.0      M  entertainment    V3N4P   
    11       90       242       4  891382267  60.0      M       educator    78155   
    12      271       242       4  885844495  51.0      M       engineer    22932   
    13       18       242       5  880129305  35.0      F          other    37212   
    14        1       242       5  889751633   NaN      M            NaN    85711   
    15      207       242       4  890793823  39.0      M      marketing    92037   
    16       14       242       4  876964570  45.0      M      scientist    55106   
    17      113       242       2  875075887  47.0      M      executive    95032   
    18      123       242       5  879809053   NaN      F         artist    20008   
    19      296       242       4  884196057  43.0      F  administrator    16803   

         movie_title release_date   ...    Fantasy  Film-Noir  Horror  Musical  \
    0   Kolya (1996)   1997-01-24   ...          0          0       0        0   
    1   Kolya (1996)   1997-01-24   ...          0          0       0        0   
    2   Kolya (1996)   1997-01-24   ...          0          0       0        0   
    3   Kolya (1996)   1997-01-24   ...          0          0       0        0   
    4   Kolya (1996)   1997-01-24   ...          0          0       0        0   
    5   Kolya (1996)   1997-01-24   ...          0          0       0        0   
    6   Kolya (1996)   1997-01-24   ...          0          0       0        0   
    7   Kolya (1996)   1997-01-24   ...          0          0       0        0   
    8   Kolya (1996)   1997-01-24   ...          0          0       0        0   
    9   Kolya (1996)   1997-01-24   ...          0          0       0        0   
    10  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    11  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    12  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    13  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    14  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    15  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    16  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    17  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    18  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    19  Kolya (1996)   1997-01-24   ...          0          0       0        0   

        Mystery  Romance  Sci-Fi  Thriller  War  Western  
    0         0        0       0         0    0        0  
    1         0        0       0         0    0        0  
    2         0        0       0         0    0        0  
    3         0        0       0         0    0        0  
    4         0        0       0         0    0        0  
    5         0        0       0         0    0        0  
    6         0        0       0         0    0        0  
    7         0        0       0         0    0        0  
    8         0        0       0         0    0        0  
    9         0        0       0         0    0        0  
    10        0        0       0         0    0        0  
    11        0        0       0         0    0        0  
    12        0        0       0         0    0        0  
    13        0        0       0         0    0        0  
    14        0        0       0         0    0        0  
    15        0        0       0         0    0        0  
    16        0        0       0         0    0        0  
    17        0        0       0         0    0        0  
    18        0        0       0         0    0        0  
    19        0        0       0         0    0        0  

    [20 rows x 30 columns]



```python
movies_rating = movies['rating']
# Here we are showing only one column, i.e. a Series
print ('type:', type(movies_rating))
movies_rating.head()
```

    type: <class 'pandas.core.series.Series'>





    0    3
    1    5
    2    4
    3    4
    4    3
    Name: rating, dtype: int64




```python
# Filtering data
# Let's display only women
movies_user_female = movies[movies['gender']=='F']
print(movies_user_female.head())
```

        user_id  movie_id  rating  timestamp   age gender     occupation zip_code  \
    13       18       242       5  880129305  35.0      F          other    37212   
    18      123       242       5  879809053   NaN      F         artist    20008   
    19      296       242       4  884196057  43.0      F  administrator    16803   
    21      270       242       5  876953744  18.0      F        student    63119   
    22      240       242       5  885775683  23.0      F       educator    20784   

         movie_title release_date   ...    Fantasy  Film-Noir  Horror  Musical  \
    13  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    18  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    19  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    21  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    22  Kolya (1996)   1997-01-24   ...          0          0       0        0   

        Mystery  Romance  Sci-Fi  Thriller  War  Western  
    13        0        0       0         0    0        0  
    18        0        0       0         0    0        0  
    19        0        0       0         0    0        0  
    21        0        0       0         0    0        0  
    22        0        0       0         0    0        0  

    [5 rows x 30 columns]



```python
#to see all the different values possible for a given column
occupation_list = movies['occupation']
print(occupation_list)
```

    0               writer
    1           programmer
    2            executive
    3              retired
    4            marketing
    5            executive
    6               writer
    7              student
    8             educator
    9           programmer
    10       entertainment
    11            educator
    12            engineer
    13               other
    14                 NaN
    15           marketing
    16           scientist
    17           executive
    18              artist
    19       administrator
    20             student
    21             student
    22            educator
    23                 NaN
    24              writer
    25                 NaN
    26                 NaN
    27           marketing
    28       administrator
    29             student
                 ...      
    99970         educator
    99971            other
    99972            other
    99973            other
    99974    administrator
    99975           artist
    99976           artist
    99977           artist
    99978           artist
    99979           artist
    99980           artist
    99981    entertainment
    99982          student
    99983          student
    99984           artist
    99985           artist
    99986           artist
    99987          student
    99988        librarian
    99989           writer
    99990              NaN
    99991           artist
    99992            other
    99993            other
    99994          student
    99995          student
    99996          student
    99997          student
    99998           writer
    99999         engineer
    Name: occupation, Length: 100000, dtype: object

---
### Work with indexes and MultiIndex option


```python
import random
indexes = [random.randrange(0,100) for i in range(5)]
data = [{i:random.randint(0,10) for i in 'ABCDE'} for i in range(5)]
df = pd.DataFrame(data, index=[1,2,3,4,5])
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>8</td>
      <td>6</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>9</td>
      <td>8</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>7</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>8</td>
      <td>1</td>
      <td>3</td>
      <td>8</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>7</td>
      <td>4</td>
      <td>4</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
movies_user_gender_male = movies[movies['gender']=='M']
movies_user_gender_male_dup = movies_user_gender_male.drop_duplicates(keep=False)
print(movies_user_gender_male.head())
# From this we can clearly see age has missing value and that from 100,000 the data reduced to 74260,
# due to filtering and removing duplicates

```

       user_id  movie_id  rating  timestamp   age gender  occupation zip_code  \
    0      196       242       3  881250949  49.0      M      writer    55105   
    1      305       242       5  886307828  23.0      M  programmer    94086   
    2        6       242       4  883268170  42.0      M   executive    98101   
    3      234       242       4  891033261  60.0      M     retired    94702   
    4       63       242       3  875747190  31.0      M   marketing    75240   

        movie_title release_date   ...    Fantasy  Film-Noir  Horror  Musical  \
    0  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    1  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    2  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    3  Kolya (1996)   1997-01-24   ...          0          0       0        0   
    4  Kolya (1996)   1997-01-24   ...          0          0       0        0   

       Mystery  Romance  Sci-Fi  Thriller  War  Western  
    0        0        0       0         0    0        0  
    1        0        0       0         0    0        0  
    2        0        0       0         0    0        0  
    3        0        0       0         0    0        0  
    4        0        0       0         0    0        0  

    [5 rows x 30 columns]



```python
#gender = female and age between 30 and 40
gender_required = ['F']
filtered_df = movies[((movies['gender'] == 'F') & (movies['age'] > 30) & (movies['age'] <40))]
filtered_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>age</th>
      <th>gender</th>
      <th>occupation</th>
      <th>zip_code</th>
      <th>movie_title</th>
      <th>release_date</th>
      <th>...</th>
      <th>Fantasy</th>
      <th>Film-Noir</th>
      <th>Horror</th>
      <th>Musical</th>
      <th>Mystery</th>
      <th>Romance</th>
      <th>Sci-Fi</th>
      <th>Thriller</th>
      <th>War</th>
      <th>Western</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>13</th>
      <td>18</td>
      <td>242</td>
      <td>5</td>
      <td>880129305</td>
      <td>35.0</td>
      <td>F</td>
      <td>other</td>
      <td>37212</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>129</td>
      <td>242</td>
      <td>4</td>
      <td>883243972</td>
      <td>36.0</td>
      <td>F</td>
      <td>marketing</td>
      <td>07039</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>39</th>
      <td>34</td>
      <td>242</td>
      <td>5</td>
      <td>888601628</td>
      <td>38.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>42141</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>42</th>
      <td>209</td>
      <td>242</td>
      <td>4</td>
      <td>883589606</td>
      <td>33.0</td>
      <td>F</td>
      <td>educator</td>
      <td>85710</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>110</th>
      <td>861</td>
      <td>242</td>
      <td>5</td>
      <td>881274504</td>
      <td>38.0</td>
      <td>F</td>
      <td>NaN</td>
      <td>14085</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>147</th>
      <td>11</td>
      <td>393</td>
      <td>4</td>
      <td>891905222</td>
      <td>39.0</td>
      <td>F</td>
      <td>other</td>
      <td>30329</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>157</th>
      <td>269</td>
      <td>393</td>
      <td>1</td>
      <td>891451036</td>
      <td>31.0</td>
      <td>F</td>
      <td>librarian</td>
      <td>43201</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>160</th>
      <td>5</td>
      <td>393</td>
      <td>2</td>
      <td>875636265</td>
      <td>33.0</td>
      <td>F</td>
      <td>other</td>
      <td>15213</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>161</th>
      <td>18</td>
      <td>393</td>
      <td>3</td>
      <td>880130930</td>
      <td>35.0</td>
      <td>F</td>
      <td>NaN</td>
      <td>37212</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>167</th>
      <td>151</td>
      <td>393</td>
      <td>2</td>
      <td>879528692</td>
      <td>38.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>48103</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>178</th>
      <td>152</td>
      <td>393</td>
      <td>5</td>
      <td>884018430</td>
      <td>33.0</td>
      <td>F</td>
      <td>educator</td>
      <td>68767</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>187</th>
      <td>330</td>
      <td>393</td>
      <td>4</td>
      <td>876547004</td>
      <td>35.0</td>
      <td>F</td>
      <td>educator</td>
      <td>33884</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>210</th>
      <td>450</td>
      <td>393</td>
      <td>4</td>
      <td>882812349</td>
      <td>35.0</td>
      <td>F</td>
      <td>educator</td>
      <td>11758</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>213</th>
      <td>457</td>
      <td>393</td>
      <td>3</td>
      <td>882548583</td>
      <td>33.0</td>
      <td>F</td>
      <td>salesman</td>
      <td>30011</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>241</th>
      <td>577</td>
      <td>393</td>
      <td>4</td>
      <td>880475363</td>
      <td>36.0</td>
      <td>F</td>
      <td>student</td>
      <td>77845</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>246</th>
      <td>593</td>
      <td>393</td>
      <td>4</td>
      <td>886194041</td>
      <td>31.0</td>
      <td>F</td>
      <td>educator</td>
      <td>68767</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>267</th>
      <td>716</td>
      <td>393</td>
      <td>3</td>
      <td>879796596</td>
      <td>36.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>44265</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>280</th>
      <td>796</td>
      <td>393</td>
      <td>4</td>
      <td>893218933</td>
      <td>32.0</td>
      <td>F</td>
      <td>writer</td>
      <td>33755</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>325</th>
      <td>264</td>
      <td>381</td>
      <td>4</td>
      <td>886123596</td>
      <td>36.0</td>
      <td>F</td>
      <td>writer</td>
      <td>90064</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>328</th>
      <td>5</td>
      <td>381</td>
      <td>1</td>
      <td>875636540</td>
      <td>33.0</td>
      <td>F</td>
      <td>other</td>
      <td>15213</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>329</th>
      <td>18</td>
      <td>381</td>
      <td>4</td>
      <td>880131474</td>
      <td>35.0</td>
      <td>F</td>
      <td>other</td>
      <td>37212</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>330</th>
      <td>256</td>
      <td>381</td>
      <td>5</td>
      <td>882165135</td>
      <td>35.0</td>
      <td>F</td>
      <td>none</td>
      <td>39042</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>331</th>
      <td>151</td>
      <td>381</td>
      <td>5</td>
      <td>879528754</td>
      <td>38.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>48103</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>358</th>
      <td>450</td>
      <td>381</td>
      <td>2</td>
      <td>882374497</td>
      <td>35.0</td>
      <td>F</td>
      <td>educator</td>
      <td>11758</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>384</th>
      <td>716</td>
      <td>381</td>
      <td>4</td>
      <td>879795644</td>
      <td>36.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>44265</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>387</th>
      <td>786</td>
      <td>381</td>
      <td>3</td>
      <td>882843397</td>
      <td>36.0</td>
      <td>F</td>
      <td>engineer</td>
      <td>01754</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>388</th>
      <td>796</td>
      <td>381</td>
      <td>3</td>
      <td>893047208</td>
      <td>32.0</td>
      <td>F</td>
      <td>writer</td>
      <td>33755</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>397</th>
      <td>861</td>
      <td>381</td>
      <td>4</td>
      <td>881274780</td>
      <td>38.0</td>
      <td>F</td>
      <td>student</td>
      <td>14085</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>406</th>
      <td>911</td>
      <td>381</td>
      <td>5</td>
      <td>892839846</td>
      <td>37.0</td>
      <td>F</td>
      <td>writer</td>
      <td>53210</td>
      <td>Muriel's Wedding (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>423</th>
      <td>79</td>
      <td>251</td>
      <td>5</td>
      <td>891271545</td>
      <td>39.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>03755</td>
      <td>Shall We Dance? (1996)</td>
      <td>1997-07-11</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99139</th>
      <td>5</td>
      <td>374</td>
      <td>3</td>
      <td>875636905</td>
      <td>33.0</td>
      <td>F</td>
      <td>other</td>
      <td>15213</td>
      <td>Mighty Morphin Power Rangers: The Movie (1995)</td>
      <td>1995-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99146</th>
      <td>911</td>
      <td>374</td>
      <td>1</td>
      <td>892841118</td>
      <td>37.0</td>
      <td>F</td>
      <td>writer</td>
      <td>53210</td>
      <td>Mighty Morphin Power Rangers: The Movie (1995)</td>
      <td>1995-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99189</th>
      <td>18</td>
      <td>958</td>
      <td>5</td>
      <td>880129731</td>
      <td>35.0</td>
      <td>F</td>
      <td>other</td>
      <td>37212</td>
      <td>To Live (Huozhe) (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99235</th>
      <td>450</td>
      <td>1249</td>
      <td>3</td>
      <td>882812821</td>
      <td>35.0</td>
      <td>F</td>
      <td>educator</td>
      <td>11758</td>
      <td>For Love or Money (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99249</th>
      <td>796</td>
      <td>1055</td>
      <td>3</td>
      <td>893188577</td>
      <td>32.0</td>
      <td>F</td>
      <td>writer</td>
      <td>33755</td>
      <td>Simple Twist of Fate, A (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99255</th>
      <td>264</td>
      <td>1474</td>
      <td>2</td>
      <td>886123728</td>
      <td>36.0</td>
      <td>F</td>
      <td>writer</td>
      <td>90064</td>
      <td>Nina Takes a Lover (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99261</th>
      <td>264</td>
      <td>1475</td>
      <td>2</td>
      <td>886123596</td>
      <td>36.0</td>
      <td>F</td>
      <td>writer</td>
      <td>90064</td>
      <td>Bhaji on the Beach (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99279</th>
      <td>938</td>
      <td>1254</td>
      <td>1</td>
      <td>891357019</td>
      <td>38.0</td>
      <td>F</td>
      <td>technician</td>
      <td>55038</td>
      <td>Gone Fishin' (1997)</td>
      <td>1997-05-30</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99294</th>
      <td>269</td>
      <td>1479</td>
      <td>2</td>
      <td>891451111</td>
      <td>31.0</td>
      <td>F</td>
      <td>librarian</td>
      <td>43201</td>
      <td>Reckless (1995)</td>
      <td>1995-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99298</th>
      <td>450</td>
      <td>1479</td>
      <td>3</td>
      <td>882377479</td>
      <td>35.0</td>
      <td>F</td>
      <td>educator</td>
      <td>11758</td>
      <td>Reckless (1995)</td>
      <td>1995-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99313</th>
      <td>5</td>
      <td>267</td>
      <td>4</td>
      <td>875635064</td>
      <td>33.0</td>
      <td>F</td>
      <td>other</td>
      <td>15213</td>
      <td>unknown</td>
      <td>NaT</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99324</th>
      <td>18</td>
      <td>113</td>
      <td>5</td>
      <td>880129628</td>
      <td>35.0</td>
      <td>F</td>
      <td>other</td>
      <td>37212</td>
      <td>Horseman on the Roof, The (Hussard sur le toit...</td>
      <td>1996-04-19</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99333</th>
      <td>18</td>
      <td>973</td>
      <td>3</td>
      <td>880129595</td>
      <td>35.0</td>
      <td>F</td>
      <td>other</td>
      <td>37212</td>
      <td>Grateful Dead (1995)</td>
      <td>1996-10-18</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99352</th>
      <td>151</td>
      <td>1297</td>
      <td>1</td>
      <td>879542847</td>
      <td>38.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>48103</td>
      <td>Love Affair (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99359</th>
      <td>450</td>
      <td>1297</td>
      <td>4</td>
      <td>882812635</td>
      <td>35.0</td>
      <td>F</td>
      <td>educator</td>
      <td>11758</td>
      <td>Love Affair (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99361</th>
      <td>796</td>
      <td>1297</td>
      <td>2</td>
      <td>893047504</td>
      <td>32.0</td>
      <td>F</td>
      <td>writer</td>
      <td>33755</td>
      <td>Love Affair (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99364</th>
      <td>151</td>
      <td>1299</td>
      <td>4</td>
      <td>879543423</td>
      <td>38.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>48103</td>
      <td>Penny Serenade (1941)</td>
      <td>1941-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99370</th>
      <td>796</td>
      <td>1299</td>
      <td>2</td>
      <td>892676043</td>
      <td>32.0</td>
      <td>F</td>
      <td>writer</td>
      <td>33755</td>
      <td>Penny Serenade (1941)</td>
      <td>1941-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99452</th>
      <td>688</td>
      <td>1127</td>
      <td>5</td>
      <td>884153606</td>
      <td>37.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>60476</td>
      <td>Truman Show, The (1998)</td>
      <td>1998-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99477</th>
      <td>34</td>
      <td>1024</td>
      <td>5</td>
      <td>888602618</td>
      <td>38.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>42141</td>
      <td>Mrs. Dalloway (1997)</td>
      <td>1997-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99501</th>
      <td>129</td>
      <td>1176</td>
      <td>4</td>
      <td>883244059</td>
      <td>36.0</td>
      <td>F</td>
      <td>marketing</td>
      <td>07039</td>
      <td>Welcome To Sarajevo (1997)</td>
      <td>1997-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99541</th>
      <td>356</td>
      <td>1294</td>
      <td>4</td>
      <td>891405721</td>
      <td>32.0</td>
      <td>F</td>
      <td>homemaker</td>
      <td>92688</td>
      <td>Ayn Rand: A Sense of Life (1997)</td>
      <td>1998-02-13</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99561</th>
      <td>796</td>
      <td>1415</td>
      <td>3</td>
      <td>893219254</td>
      <td>32.0</td>
      <td>F</td>
      <td>writer</td>
      <td>33755</td>
      <td>Next Karate Kid, The (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99630</th>
      <td>450</td>
      <td>1518</td>
      <td>4</td>
      <td>887138957</td>
      <td>35.0</td>
      <td>F</td>
      <td>educator</td>
      <td>11758</td>
      <td>Losing Isaiah (1995)</td>
      <td>1995-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99642</th>
      <td>577</td>
      <td>1517</td>
      <td>3</td>
      <td>880475644</td>
      <td>36.0</td>
      <td>F</td>
      <td>student</td>
      <td>77845</td>
      <td>Race the Sun (1996)</td>
      <td>1996-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99648</th>
      <td>450</td>
      <td>1521</td>
      <td>3</td>
      <td>882812350</td>
      <td>35.0</td>
      <td>F</td>
      <td>educator</td>
      <td>11758</td>
      <td>Mr. Wonderful (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99660</th>
      <td>796</td>
      <td>1522</td>
      <td>3</td>
      <td>893194740</td>
      <td>32.0</td>
      <td>F</td>
      <td>writer</td>
      <td>33755</td>
      <td>Trial by Jury (1994)</td>
      <td>1994-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99695</th>
      <td>577</td>
      <td>1531</td>
      <td>4</td>
      <td>880475408</td>
      <td>36.0</td>
      <td>F</td>
      <td>student</td>
      <td>77845</td>
      <td>Far From Home: The Adventures of Yellow Dog (1...</td>
      <td>1995-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99852</th>
      <td>450</td>
      <td>1603</td>
      <td>3</td>
      <td>887139728</td>
      <td>35.0</td>
      <td>F</td>
      <td>educator</td>
      <td>11758</td>
      <td>Angela (1995)</td>
      <td>1996-02-16</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>99981</th>
      <td>839</td>
      <td>1664</td>
      <td>1</td>
      <td>875752902</td>
      <td>38.0</td>
      <td>F</td>
      <td>entertainment</td>
      <td>90814</td>
      <td>8 Heads in a Duffel Bag (1997)</td>
      <td>1997-04-18</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5183 rows × 30 columns</p>
</div>



#### Note
In the above fragment you HAVE TO ADD parantheses to each and every argument that is being compared else you will get an error.

As you can see after filtering result tables (i.e. DataFrames) have non-ordered indexes. To fix this trouble you may write the following:


```python
filtered_df = filtered_df.reset_index()
filtered_df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>age</th>
      <th>gender</th>
      <th>occupation</th>
      <th>zip_code</th>
      <th>movie_title</th>
      <th>...</th>
      <th>Fantasy</th>
      <th>Film-Noir</th>
      <th>Horror</th>
      <th>Musical</th>
      <th>Mystery</th>
      <th>Romance</th>
      <th>Sci-Fi</th>
      <th>Thriller</th>
      <th>War</th>
      <th>Western</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>13</td>
      <td>18</td>
      <td>242</td>
      <td>5</td>
      <td>880129305</td>
      <td>35.0</td>
      <td>F</td>
      <td>other</td>
      <td>37212</td>
      <td>Kolya (1996)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>27</td>
      <td>129</td>
      <td>242</td>
      <td>4</td>
      <td>883243972</td>
      <td>36.0</td>
      <td>F</td>
      <td>marketing</td>
      <td>07039</td>
      <td>Kolya (1996)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>39</td>
      <td>34</td>
      <td>242</td>
      <td>5</td>
      <td>888601628</td>
      <td>38.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>42141</td>
      <td>Kolya (1996)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>42</td>
      <td>209</td>
      <td>242</td>
      <td>4</td>
      <td>883589606</td>
      <td>33.0</td>
      <td>F</td>
      <td>educator</td>
      <td>85710</td>
      <td>Kolya (1996)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>110</td>
      <td>861</td>
      <td>242</td>
      <td>5</td>
      <td>881274504</td>
      <td>38.0</td>
      <td>F</td>
      <td>NaN</td>
      <td>14085</td>
      <td>Kolya (1996)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>147</td>
      <td>11</td>
      <td>393</td>
      <td>4</td>
      <td>891905222</td>
      <td>39.0</td>
      <td>F</td>
      <td>other</td>
      <td>30329</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>157</td>
      <td>269</td>
      <td>393</td>
      <td>1</td>
      <td>891451036</td>
      <td>31.0</td>
      <td>F</td>
      <td>librarian</td>
      <td>43201</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>160</td>
      <td>5</td>
      <td>393</td>
      <td>2</td>
      <td>875636265</td>
      <td>33.0</td>
      <td>F</td>
      <td>other</td>
      <td>15213</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>161</td>
      <td>18</td>
      <td>393</td>
      <td>3</td>
      <td>880130930</td>
      <td>35.0</td>
      <td>F</td>
      <td>NaN</td>
      <td>37212</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>167</td>
      <td>151</td>
      <td>393</td>
      <td>2</td>
      <td>879528692</td>
      <td>38.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>48103</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 31 columns</p>
</div>




```python
# set 'user_id' 'movie_id' as index
filtered_df_new = filtered_df.set_index(['user_id','movie_id'])
filtered_df_new.head(10)

# Note that set_index takes only a list as an argument to it.
# if you remove the [] then only the first argument is set as the index.
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>index</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>age</th>
      <th>gender</th>
      <th>occupation</th>
      <th>zip_code</th>
      <th>movie_title</th>
      <th>release_date</th>
      <th>IMDb_URL</th>
      <th>...</th>
      <th>Fantasy</th>
      <th>Film-Noir</th>
      <th>Horror</th>
      <th>Musical</th>
      <th>Mystery</th>
      <th>Romance</th>
      <th>Sci-Fi</th>
      <th>Thriller</th>
      <th>War</th>
      <th>Western</th>
    </tr>
    <tr>
      <th>user_id</th>
      <th>movie_id</th>
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
      <th>18</th>
      <th>242</th>
      <td>13</td>
      <td>5</td>
      <td>880129305</td>
      <td>35.0</td>
      <td>F</td>
      <td>other</td>
      <td>37212</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>http://us.imdb.com/M/title-exact?Kolya%20(1996)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>129</th>
      <th>242</th>
      <td>27</td>
      <td>4</td>
      <td>883243972</td>
      <td>36.0</td>
      <td>F</td>
      <td>marketing</td>
      <td>07039</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>http://us.imdb.com/M/title-exact?Kolya%20(1996)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>34</th>
      <th>242</th>
      <td>39</td>
      <td>5</td>
      <td>888601628</td>
      <td>38.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>42141</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>http://us.imdb.com/M/title-exact?Kolya%20(1996)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>209</th>
      <th>242</th>
      <td>42</td>
      <td>4</td>
      <td>883589606</td>
      <td>33.0</td>
      <td>F</td>
      <td>educator</td>
      <td>85710</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>http://us.imdb.com/M/title-exact?Kolya%20(1996)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>861</th>
      <th>242</th>
      <td>110</td>
      <td>5</td>
      <td>881274504</td>
      <td>38.0</td>
      <td>F</td>
      <td>NaN</td>
      <td>14085</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>http://us.imdb.com/M/title-exact?Kolya%20(1996)</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>11</th>
      <th>393</th>
      <td>147</td>
      <td>4</td>
      <td>891905222</td>
      <td>39.0</td>
      <td>F</td>
      <td>other</td>
      <td>30329</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>http://us.imdb.com/M/title-exact?Mrs.%20Doubtf...</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>269</th>
      <th>393</th>
      <td>157</td>
      <td>1</td>
      <td>891451036</td>
      <td>31.0</td>
      <td>F</td>
      <td>librarian</td>
      <td>43201</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>http://us.imdb.com/M/title-exact?Mrs.%20Doubtf...</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <th>393</th>
      <td>160</td>
      <td>2</td>
      <td>875636265</td>
      <td>33.0</td>
      <td>F</td>
      <td>other</td>
      <td>15213</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>http://us.imdb.com/M/title-exact?Mrs.%20Doubtf...</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>18</th>
      <th>393</th>
      <td>161</td>
      <td>3</td>
      <td>880130930</td>
      <td>35.0</td>
      <td>F</td>
      <td>NaN</td>
      <td>37212</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>http://us.imdb.com/M/title-exact?Mrs.%20Doubtf...</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>151</th>
      <th>393</th>
      <td>167</td>
      <td>2</td>
      <td>879528692</td>
      <td>38.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>48103</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>http://us.imdb.com/M/title-exact?Mrs.%20Doubtf...</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 29 columns</p>
</div>




```python
# By default, `set_index()` returns a new DataFrame.
# so you’ll have to specify if you’d like the changes to occur in place.
# Here we used filtered_df_new to get the new dataframe and now see the type of filtererd_df_new

print(type(filtered_df_new.index))
```

    <class 'pandas.core.indexes.multi.MultiIndex'>


Notice here that we now have a new sort of 'index' which is `MultiIndex`, which contains information about indexing of DataFrame and allows manipulating with this data.


```python
filtered_df_new.index.names
# Gives you the names of the two index values we set as a FrozenList
```




    FrozenList(['user_id', 'movie_id'])



Method `get_level_values()` allows to get all values for the corresponding index level.
`get_level_values(0)` corresponds to 'user_id' and `get_level_values(1)` corresponds to 'movie_id'


```python
print(filtered_df_new.index.get_level_values(0))
print(filtered_df_new.index.get_level_values(1))
```

    Int64Index([ 18, 129,  34, 209, 861,  11, 269,   5,  18, 151,
                ...
                129, 356, 796, 450, 577, 450, 796, 577, 450, 839],
               dtype='int64', name='user_id', length=5183)
    Int64Index([ 242,  242,  242,  242,  242,  393,  393,  393,  393,  393,
                ...
                1176, 1294, 1415, 1518, 1517, 1521, 1522, 1531, 1603, 1664],
               dtype='int64', name='movie_id', length=5183)

---
### Selection by label and position
Object selection in pandas is now supported by three types of multi-axis indexing.

* `.loc` works on labels in the index;
* `.iloc` works on the positions in the index (so it only takes integers);

The sequence of the following examples demonstrates how we can manipulate with DataFrame’s rows.
At first let’s get the first row of movies:


```python
movies.loc[0]
```




    user_id                                                     196
    movie_id                                                    242
    rating                                                        3
    timestamp                                             881250949
    age                                                          49
    gender                                                        M
    occupation                                               writer
    zip_code                                                  55105
    movie_title                                        Kolya (1996)
    release_date                                1997-01-24 00:00:00
    IMDb_URL        http://us.imdb.com/M/title-exact?Kolya%20(1996)
    unknown                                                       0
    Action                                                        0
    Adventure                                                     0
    Animation                                                     0
    Childrens                                                     0
    Comedy                                                        1
    Crime                                                         0
    Documentary                                                   0
    Drama                                                         0
    Fantasy                                                       0
    Film-Noir                                                     0
    Horror                                                        0
    Musical                                                       0
    Mystery                                                       0
    Romance                                                       0
    Sci-Fi                                                        0
    Thriller                                                      0
    War                                                           0
    Western                                                       0
    Name: 0, dtype: object




```python
movies.loc[1:3]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>age</th>
      <th>gender</th>
      <th>occupation</th>
      <th>zip_code</th>
      <th>movie_title</th>
      <th>release_date</th>
      <th>...</th>
      <th>Fantasy</th>
      <th>Film-Noir</th>
      <th>Horror</th>
      <th>Musical</th>
      <th>Mystery</th>
      <th>Romance</th>
      <th>Sci-Fi</th>
      <th>Thriller</th>
      <th>War</th>
      <th>Western</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>305</td>
      <td>242</td>
      <td>5</td>
      <td>886307828</td>
      <td>23.0</td>
      <td>M</td>
      <td>programmer</td>
      <td>94086</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>242</td>
      <td>4</td>
      <td>883268170</td>
      <td>42.0</td>
      <td>M</td>
      <td>executive</td>
      <td>98101</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>234</td>
      <td>242</td>
      <td>4</td>
      <td>891033261</td>
      <td>60.0</td>
      <td>M</td>
      <td>retired</td>
      <td>94702</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 30 columns</p>
</div>



If you want to return specific columns then you have to specify them as a separate argument of .loc


```python
movies.loc[1:3 , 'movie_title']
```




    1    Kolya (1996)
    2    Kolya (1996)
    3    Kolya (1996)
    Name: movie_title, dtype: object




```python
movies.loc[1:5 , ['movie_title','age','gender']]
# If more than one column is to be selected then you have to give the second argument of .loc as a list
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>movie_title</th>
      <th>age</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Kolya (1996)</td>
      <td>23.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kolya (1996)</td>
      <td>42.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kolya (1996)</td>
      <td>60.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kolya (1996)</td>
      <td>31.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Kolya (1996)</td>
      <td>26.0</td>
      <td>M</td>
    </tr>
  </tbody>
</table>
</div>




```python
# movies.iloc[1:5 , ['movie_title','age','gender']]
# Gives error as iloc only uses integer values
```


```python
movies.iloc[0]
```




    user_id                                                     196
    movie_id                                                    242
    rating                                                        3
    timestamp                                             881250949
    age                                                          49
    gender                                                        M
    occupation                                               writer
    zip_code                                                  55105
    movie_title                                        Kolya (1996)
    release_date                                1997-01-24 00:00:00
    IMDb_URL        http://us.imdb.com/M/title-exact?Kolya%20(1996)
    unknown                                                       0
    Action                                                        0
    Adventure                                                     0
    Animation                                                     0
    Childrens                                                     0
    Comedy                                                        1
    Crime                                                         0
    Documentary                                                   0
    Drama                                                         0
    Fantasy                                                       0
    Film-Noir                                                     0
    Horror                                                        0
    Musical                                                       0
    Mystery                                                       0
    Romance                                                       0
    Sci-Fi                                                        0
    Thriller                                                      0
    War                                                           0
    Western                                                       0
    Name: 0, dtype: object




```python
movies.iloc[1:5]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>age</th>
      <th>gender</th>
      <th>occupation</th>
      <th>zip_code</th>
      <th>movie_title</th>
      <th>release_date</th>
      <th>...</th>
      <th>Fantasy</th>
      <th>Film-Noir</th>
      <th>Horror</th>
      <th>Musical</th>
      <th>Mystery</th>
      <th>Romance</th>
      <th>Sci-Fi</th>
      <th>Thriller</th>
      <th>War</th>
      <th>Western</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>305</td>
      <td>242</td>
      <td>5</td>
      <td>886307828</td>
      <td>23.0</td>
      <td>M</td>
      <td>programmer</td>
      <td>94086</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>242</td>
      <td>4</td>
      <td>883268170</td>
      <td>42.0</td>
      <td>M</td>
      <td>executive</td>
      <td>98101</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>234</td>
      <td>242</td>
      <td>4</td>
      <td>891033261</td>
      <td>60.0</td>
      <td>M</td>
      <td>retired</td>
      <td>94702</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>63</td>
      <td>242</td>
      <td>3</td>
      <td>875747190</td>
      <td>31.0</td>
      <td>M</td>
      <td>marketing</td>
      <td>75240</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>4 rows × 30 columns</p>
</div>




```python
# movies.select(lambda x: x%2==0).head() is the same as :
movies.loc[movies.index.map(lambda x: x%2==0)].head()

# .select() has been deprecated for now and will be completely removed in future updates so use .loc
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>age</th>
      <th>gender</th>
      <th>occupation</th>
      <th>zip_code</th>
      <th>movie_title</th>
      <th>release_date</th>
      <th>...</th>
      <th>Fantasy</th>
      <th>Film-Noir</th>
      <th>Horror</th>
      <th>Musical</th>
      <th>Mystery</th>
      <th>Romance</th>
      <th>Sci-Fi</th>
      <th>Thriller</th>
      <th>War</th>
      <th>Western</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>196</td>
      <td>242</td>
      <td>3</td>
      <td>881250949</td>
      <td>49.0</td>
      <td>M</td>
      <td>writer</td>
      <td>55105</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>242</td>
      <td>4</td>
      <td>883268170</td>
      <td>42.0</td>
      <td>M</td>
      <td>executive</td>
      <td>98101</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>63</td>
      <td>242</td>
      <td>3</td>
      <td>875747190</td>
      <td>31.0</td>
      <td>M</td>
      <td>marketing</td>
      <td>75240</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>201</td>
      <td>242</td>
      <td>4</td>
      <td>884110598</td>
      <td>27.0</td>
      <td>M</td>
      <td>writer</td>
      <td>E2A4H</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>13</td>
      <td>242</td>
      <td>2</td>
      <td>881515193</td>
      <td>47.0</td>
      <td>M</td>
      <td>educator</td>
      <td>29206</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 30 columns</p>
</div>

---

## Working with Missing Data
Pandas primarily uses the value np.nan to represent missing data (in table missed/empty value are marked by NaN). It is by default not included in computations. Missing data creates many issues at mathematical or computational tasks with DataFrames and Series and it’s important to know how fight with these values.


```python
ages = movies['age']
sum(ages)
```




    nan



This is because there are so many cases where Age isn't given and hence takes on the value of np.nan.
We can use `fillna()`a very effecient pandas method for filling missing values


```python
ages = movies['age'].fillna(0)
sum(ages)
```




    3089983.0



This fills all the values with 0 and calculates the sum.
To remain only rows with non-null values you can use method `dropna()`


```python
ages = movies['age'].dropna()
sum(ages)
```




    3089983.0




```python
movies_nonnull = movies.dropna()
movies_nonnull.head(20)
#14th value was dropped because it had a missing value in a column
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>age</th>
      <th>gender</th>
      <th>occupation</th>
      <th>zip_code</th>
      <th>movie_title</th>
      <th>release_date</th>
      <th>...</th>
      <th>Fantasy</th>
      <th>Film-Noir</th>
      <th>Horror</th>
      <th>Musical</th>
      <th>Mystery</th>
      <th>Romance</th>
      <th>Sci-Fi</th>
      <th>Thriller</th>
      <th>War</th>
      <th>Western</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>196</td>
      <td>242</td>
      <td>3</td>
      <td>881250949</td>
      <td>49.0</td>
      <td>M</td>
      <td>writer</td>
      <td>55105</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>305</td>
      <td>242</td>
      <td>5</td>
      <td>886307828</td>
      <td>23.0</td>
      <td>M</td>
      <td>programmer</td>
      <td>94086</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>242</td>
      <td>4</td>
      <td>883268170</td>
      <td>42.0</td>
      <td>M</td>
      <td>executive</td>
      <td>98101</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>234</td>
      <td>242</td>
      <td>4</td>
      <td>891033261</td>
      <td>60.0</td>
      <td>M</td>
      <td>retired</td>
      <td>94702</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>63</td>
      <td>242</td>
      <td>3</td>
      <td>875747190</td>
      <td>31.0</td>
      <td>M</td>
      <td>marketing</td>
      <td>75240</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>181</td>
      <td>242</td>
      <td>1</td>
      <td>878961814</td>
      <td>26.0</td>
      <td>M</td>
      <td>executive</td>
      <td>21218</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>201</td>
      <td>242</td>
      <td>4</td>
      <td>884110598</td>
      <td>27.0</td>
      <td>M</td>
      <td>writer</td>
      <td>E2A4H</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>249</td>
      <td>242</td>
      <td>5</td>
      <td>879571438</td>
      <td>25.0</td>
      <td>M</td>
      <td>student</td>
      <td>84103</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>13</td>
      <td>242</td>
      <td>2</td>
      <td>881515193</td>
      <td>47.0</td>
      <td>M</td>
      <td>educator</td>
      <td>29206</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>279</td>
      <td>242</td>
      <td>3</td>
      <td>877756647</td>
      <td>33.0</td>
      <td>M</td>
      <td>programmer</td>
      <td>85251</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>145</td>
      <td>242</td>
      <td>5</td>
      <td>875269755</td>
      <td>31.0</td>
      <td>M</td>
      <td>entertainment</td>
      <td>V3N4P</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>90</td>
      <td>242</td>
      <td>4</td>
      <td>891382267</td>
      <td>60.0</td>
      <td>M</td>
      <td>educator</td>
      <td>78155</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>271</td>
      <td>242</td>
      <td>4</td>
      <td>885844495</td>
      <td>51.0</td>
      <td>M</td>
      <td>engineer</td>
      <td>22932</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>18</td>
      <td>242</td>
      <td>5</td>
      <td>880129305</td>
      <td>35.0</td>
      <td>F</td>
      <td>other</td>
      <td>37212</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>207</td>
      <td>242</td>
      <td>4</td>
      <td>890793823</td>
      <td>39.0</td>
      <td>M</td>
      <td>marketing</td>
      <td>92037</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>14</td>
      <td>242</td>
      <td>4</td>
      <td>876964570</td>
      <td>45.0</td>
      <td>M</td>
      <td>scientist</td>
      <td>55106</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>113</td>
      <td>242</td>
      <td>2</td>
      <td>875075887</td>
      <td>47.0</td>
      <td>M</td>
      <td>executive</td>
      <td>95032</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>296</td>
      <td>242</td>
      <td>4</td>
      <td>884196057</td>
      <td>43.0</td>
      <td>F</td>
      <td>administrator</td>
      <td>16803</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>154</td>
      <td>242</td>
      <td>3</td>
      <td>879138235</td>
      <td>25.0</td>
      <td>M</td>
      <td>student</td>
      <td>53703</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>270</td>
      <td>242</td>
      <td>5</td>
      <td>876953744</td>
      <td>18.0</td>
      <td>F</td>
      <td>student</td>
      <td>63119</td>
      <td>Kolya (1996)</td>
      <td>1997-01-24</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>20 rows × 30 columns</p>
</div>




```python
movies_notnull = movies.dropna(how='all',subset=['age','occupation'])
#Drops all nan values from movies belonging to age and occupation
movies_notnull.info()
#Notice how age and occupation now have nearly 6000 lesser values
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 99616 entries, 0 to 99999
    Data columns (total 30 columns):
    user_id         99616 non-null int64
    movie_id        99616 non-null int64
    rating          99616 non-null int64
    timestamp       99616 non-null int64
    age             93731 non-null float64
    gender          99616 non-null object
    occupation      93806 non-null object
    zip_code        99616 non-null object
    movie_title     99616 non-null object
    release_date    99607 non-null datetime64[ns]
    IMDb_URL        99603 non-null object
    unknown         99616 non-null int64
    Action          99616 non-null int64
    Adventure       99616 non-null int64
    Animation       99616 non-null int64
    Childrens       99616 non-null int64
    Comedy          99616 non-null int64
    Crime           99616 non-null int64
    Documentary     99616 non-null int64
    Drama           99616 non-null int64
    Fantasy         99616 non-null int64
    Film-Noir       99616 non-null int64
    Horror          99616 non-null int64
    Musical         99616 non-null int64
    Mystery         99616 non-null int64
    Romance         99616 non-null int64
    Sci-Fi          99616 non-null int64
    Thriller        99616 non-null int64
    War             99616 non-null int64
    Western         99616 non-null int64
    dtypes: datetime64[ns](1), float64(1), int64(23), object(5)
    memory usage: 23.6+ MB


Thus, if `how='all'`, we get DataFrame, where all values in both columns from subset are NaN.

If `how='any'`, we get DataFrame, where at least one contains NaN.


```python
movies.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>age</th>
      <th>unknown</th>
      <th>Action</th>
      <th>Adventure</th>
      <th>Animation</th>
      <th>Childrens</th>
      <th>...</th>
      <th>Fantasy</th>
      <th>Film-Noir</th>
      <th>Horror</th>
      <th>Musical</th>
      <th>Mystery</th>
      <th>Romance</th>
      <th>Sci-Fi</th>
      <th>Thriller</th>
      <th>War</th>
      <th>Western</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>100000.00000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>1.000000e+05</td>
      <td>93731.000000</td>
      <td>100000.0000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>...</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.00000</td>
      <td>100000.00000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>462.48475</td>
      <td>425.530130</td>
      <td>3.529860</td>
      <td>8.835289e+08</td>
      <td>32.966500</td>
      <td>0.0001</td>
      <td>0.255890</td>
      <td>0.137530</td>
      <td>0.036050</td>
      <td>0.071820</td>
      <td>...</td>
      <td>0.013520</td>
      <td>0.017330</td>
      <td>0.053170</td>
      <td>0.049540</td>
      <td>0.052450</td>
      <td>0.194610</td>
      <td>0.12730</td>
      <td>0.21872</td>
      <td>0.093980</td>
      <td>0.018540</td>
    </tr>
    <tr>
      <th>std</th>
      <td>266.61442</td>
      <td>330.798356</td>
      <td>1.125674</td>
      <td>5.343856e+06</td>
      <td>11.561809</td>
      <td>0.0100</td>
      <td>0.436362</td>
      <td>0.344408</td>
      <td>0.186416</td>
      <td>0.258191</td>
      <td>...</td>
      <td>0.115487</td>
      <td>0.130498</td>
      <td>0.224373</td>
      <td>0.216994</td>
      <td>0.222934</td>
      <td>0.395902</td>
      <td>0.33331</td>
      <td>0.41338</td>
      <td>0.291802</td>
      <td>0.134894</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.00000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>8.747247e+08</td>
      <td>7.000000</td>
      <td>0.0000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>254.00000</td>
      <td>175.000000</td>
      <td>3.000000</td>
      <td>8.794487e+08</td>
      <td>24.000000</td>
      <td>0.0000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>447.00000</td>
      <td>322.000000</td>
      <td>4.000000</td>
      <td>8.828269e+08</td>
      <td>30.000000</td>
      <td>0.0000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>682.00000</td>
      <td>631.000000</td>
      <td>4.000000</td>
      <td>8.882600e+08</td>
      <td>40.000000</td>
      <td>0.0000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>943.00000</td>
      <td>1682.000000</td>
      <td>5.000000</td>
      <td>8.932866e+08</td>
      <td>73.000000</td>
      <td>1.0000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>...</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.00000</td>
      <td>1.00000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 24 columns</p>
</div>



At first, let’s find all unique dates in `‘release_date’` column of `movies` and then select only dates in range lower than 1995.


```python
movies['release_date'] = movies['release_date'].map(pd.to_datetime)
# We map it to_datetime as pandas has a set way to deal with dates and then we can effectively work with dates.
unique_dates = movies['release_date'].drop_duplicates().dropna()
# Drops duplicates and nan values
unique_dates
```




    0       1997-01-24
    117     1993-01-01
    309     1994-01-01
    409     1997-07-11
    455     1986-01-01
    785     1997-01-01
    881     1987-01-01
    1137    1979-01-01
    1253    1996-04-26
    1525    1995-01-01
    1557    1996-03-08
    1850    1996-11-15
    2331    1990-01-01
    2851    1971-01-01
    2972    1978-01-01
    3432    1997-07-04
    3735    1996-04-12
    4269    1996-12-18
    4347    1996-04-23
    4583    1996-10-04
    4745    1997-06-27
    4751    1997-01-31
    4798    1996-06-28
    4961    1988-01-01
    5208    1995-10-30
    5392    1996-02-09
    5863    1996-09-28
    6861    1997-05-09
    7058    1996-10-11
    7186    1997-08-15
               ...    
    96679   1996-09-24
    96855   1997-01-29
    96948   1996-09-04
    97195   1996-09-16
    97434   1997-12-18
    97639   1998-03-17
    97816   1996-06-05
    98068   1996-12-15
    98546   1998-04-03
    98574   1996-05-17
    98590   1998-03-10
    98739   1996-10-26
    98748   1998-01-23
    98786   1998-03-14
    98856   1932-01-01
    98969   1996-01-15
    99205   1996-04-02
    99280   1998-02-20
    99321   1997-04-22
    99598   1998-10-09
    99650   1998-02-01
    99702   1996-07-22
    99737   1926-01-01
    99813   1998-01-21
    99885   1998-02-11
    99938   1986-04-26
    99940   1998-03-06
    99958   1996-09-18
    99967   1996-02-28
    99977   1997-04-30
    Name: release_date, Length: 240, dtype: datetime64[ns]




```python
# find dates with year lower/equal than 1995
unique_dates_1 = filter(lambda x: x.year <= 1995, unique_dates)
# filter() takes two arguments. First one should return only boolean values and the second one is the variable over which ititerates over.
# This basically takes unique_dates and uses the lambda function (here, it returns bool values) and filters True cases.

unique_dates_1
```




    <filter at 0x1187af6a0>



Here we have used `drop_duplicates()` method to select only `unique` Series values. Then we can filter `movies` with respect to `release_date` condition. Each `datetime` Python object possesses with attributes `year`, `month`, `day`, etc. allowing to extract values of year, month, day, etc. from the date. We call the new DataFrame as `old_movies`.


```python
old_movies = movies[movies['release_date'].isin(unique_dates_1)]
old_movies.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>age</th>
      <th>gender</th>
      <th>occupation</th>
      <th>zip_code</th>
      <th>movie_title</th>
      <th>release_date</th>
      <th>...</th>
      <th>Fantasy</th>
      <th>Film-Noir</th>
      <th>Horror</th>
      <th>Musical</th>
      <th>Mystery</th>
      <th>Romance</th>
      <th>Sci-Fi</th>
      <th>Thriller</th>
      <th>War</th>
      <th>Western</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>117</th>
      <td>196</td>
      <td>393</td>
      <td>4</td>
      <td>881251863</td>
      <td>49.0</td>
      <td>M</td>
      <td>writer</td>
      <td>55105</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>22</td>
      <td>393</td>
      <td>4</td>
      <td>878886989</td>
      <td>25.0</td>
      <td>M</td>
      <td>writer</td>
      <td>40206</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>244</td>
      <td>393</td>
      <td>3</td>
      <td>880607365</td>
      <td>28.0</td>
      <td>M</td>
      <td>technician</td>
      <td>80525</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>120</th>
      <td>298</td>
      <td>393</td>
      <td>4</td>
      <td>884183099</td>
      <td>44.0</td>
      <td>M</td>
      <td>executive</td>
      <td>01581</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>121</th>
      <td>286</td>
      <td>393</td>
      <td>4</td>
      <td>877534481</td>
      <td>27.0</td>
      <td>M</td>
      <td>student</td>
      <td>15217</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 30 columns</p>
</div>



Now we may filter DataFrame `old_movies` by `age` and `rating`. Lets’ drop `timestamp`, `zip_code`


```python
# get all users with age less than 25 that rated old movies higher than 3
old_movies_watch = old_movies[(old_movies['age']<25) & (old_movies['rating']>3)]
# Drop timestamp and zip_code
old_movies_watch = old_movies_watch.drop(['timestamp', 'zip_code'],axis=1)

old_movies_watch.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>age</th>
      <th>gender</th>
      <th>occupation</th>
      <th>movie_title</th>
      <th>release_date</th>
      <th>IMDb_URL</th>
      <th>unknown</th>
      <th>...</th>
      <th>Fantasy</th>
      <th>Film-Noir</th>
      <th>Horror</th>
      <th>Musical</th>
      <th>Mystery</th>
      <th>Romance</th>
      <th>Sci-Fi</th>
      <th>Thriller</th>
      <th>War</th>
      <th>Western</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>124</th>
      <td>303</td>
      <td>393</td>
      <td>4</td>
      <td>19.0</td>
      <td>M</td>
      <td>student</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>http://us.imdb.com/M/title-exact?Mrs.%20Doubtf...</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>135</th>
      <td>276</td>
      <td>393</td>
      <td>4</td>
      <td>21.0</td>
      <td>M</td>
      <td>student</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>http://us.imdb.com/M/title-exact?Mrs.%20Doubtf...</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>153</th>
      <td>128</td>
      <td>393</td>
      <td>4</td>
      <td>24.0</td>
      <td>F</td>
      <td>marketing</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>http://us.imdb.com/M/title-exact?Mrs.%20Doubtf...</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>162</th>
      <td>130</td>
      <td>393</td>
      <td>5</td>
      <td>20.0</td>
      <td>M</td>
      <td>none</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>http://us.imdb.com/M/title-exact?Mrs.%20Doubtf...</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>183</th>
      <td>314</td>
      <td>393</td>
      <td>4</td>
      <td>20.0</td>
      <td>F</td>
      <td>student</td>
      <td>Mrs. Doubtfire (1993)</td>
      <td>1993-01-01</td>
      <td>http://us.imdb.com/M/title-exact?Mrs.%20Doubtf...</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>

---

`Pandas` has support for accelerating certain types of binary numerical and boolean operations using the `numexpr `library (it uses smart chunking, caching, and multiple cores) and the `bottleneck` libraries (is a set of specialized cython routines that are especially fast when dealing with arrays that have NaNs). It allows one to increase pandas functionality a lot. This advantage is shown for some boolean and calculation operations. To count the time elapsed on operation performing we will use the decorator


```python
# this function counts the time for a particular operation

def timer(func):
    from datetime import datetime
    def wrapper(*args):
        start = datetime.now()
        func(*args)
        end = datetime.now()
        return 'elapsed time = {' + str(end - start)+'}'
    return wrapper

```


```python
import random
n = 100
# generate rangon datasets
df_1 = pd.DataFrame({'col :'+str(i):[random.randint(-100,100) for j in range(n)]for i in range(n)})
# here we pass a dictionary to the DataFrame() constructor.
# The key is "col : i" where i can take random values and the value for those keys is i.

df_2 = pd.DataFrame({'col :'+str(i):[random.randint(-100,100) for j in range(n)] for i in range(n)})

@timer
def direct_comparison(df_1, df_2):
    bool_df = pd.DataFrame({'col_{}'.format(i): [True for j in range(n)] for i in range(n)})
    for i in range(len(df_1.index)):
        for j in range(len(df_1.loc[i])):
            if df_1.loc[i, df_1.columns[j]] >= df_2.loc[i, df_2.columns[j]]:
                bool_df.loc[i,bool_df.columns[j]] = False
    return bool_df

@timer
def pandas_comparison(df_1, df_2):
    return df_1 < df_2

print ('direct_comparison:', (direct_comparison(df_1, df_2)))
print ('pandas_comparison:', (pandas_comparison(df_1, df_2)))
```

    direct_comparison: elapsed time = {0:00:03.362719}
    pandas_comparison: elapsed time = {0:00:00.029600}


As you can see, the difference in speed is too noticeable.

Besides, pandas possesses methods `eq` (equal), `ne` (not equal), `lt` (less then), `gt` (greater than), `le` (less or equal) and `ge` (greater or equal) for simplifying boolean comparison

---

## Matrix Addition


```python
df = pd.DataFrame({'A':[1,2,3],'B':[-2,-3,-4],"C":[7,8,9]})
dfa = pd.DataFrame({'A':[1,2,3],'D':[6,7,8],"C":[12,12,12]})
dfc = df + dfa
dfc
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>NaN</td>
      <td>19</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>NaN</td>
      <td>20</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>NaN</td>
      <td>21</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.le(dfa)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



You can also apply the reductions: `empty`, `any()`, `all()`, and `bool()` to provide a way to summarize a boolean result:


```python
(df<0).all()
```




    A    False
    B     True
    C    False
    dtype: bool




```python
# here horyzontal direction for comparison is taking into account and we check all row’s items
(df < 0).all(axis=1)
```




    0    False
    1    False
    2    False
    dtype: bool




```python
# here vertical direction for comparison is taking into
# account and we check if just one column’s item satisfies the condition
(df < 0).any()
```




    A    False
    B     True
    C    False
    dtype: bool




```python
# here we check if all DataFrame's items satisfy the condition
(df < 0).any().any()
```




    True




```python
# here we check if DataFrame no one element
df.empty
```




    False


---
### Descriptive Statistics


|Function|Description|
|--|-------------------------------|
|abs|absolute value|
|count|number of non-null observations|
|cumsum|cumulative sum (a sequence of partial sums of a given sequence)|
|sum|sum of values|
|mean|mean of values|
|mad|mean absolute deviation|
|median|arithmetic median of values|
|min|minimum value|
|max|maximum value|
|mode|mode|
|prod|product of values|
|std|unbiased standard deviation|
|var|unbiased variance|



```python
print("Sum : ", movies['age'].sum())
```

    Sum :  3089983.0



```python
print(df)
```

       A  B  C
    0  1 -2  7
    1  2 -3  8
    2  3 -4  9



```python
print("Mean : ")
print(df.mean())

print("\nMean of all Mean Values: ")
print(df.mean().mean())

print("\nMedian: ")
print(df.median())

print("\nStandard Deviation: ")
print(df.std())

print("\nVariance: ")
print(df.var())

print("\nMax: ")
print(df.max())
```

    Mean :
    A    2.0
    B   -3.0
    C    8.0
    dtype: float64

    Mean of all Mean Values:
    2.3333333333333335

    Median:
    A    2.0
    B   -3.0
    C    8.0
    dtype: float64

    Standard Deviation:
    A    1.0
    B    1.0
    C    1.0
    dtype: float64

    Variance:
    A    1.0
    B    1.0
    C    1.0
    dtype: float64

    Max:
    A    3
    B   -2
    C    9
    dtype: int64

---
## Function Applications
When you need to make some transformations with some column’s or row’s elements, then method `map` will be helpful (it works like pure Python function `map()` ). But there is also possibility to apply some function to each DataFrame element (not to a column or a row) – method `apply(map)` aids in this case.



```python
movies.loc[:, (movies.dtypes == np.int64) | (movies.dtypes == np.float64)].apply(np.mean)
# This calculates the mean of all the columns present in movies
```




    user_id        4.624848e+02
    movie_id       4.255301e+02
    rating         3.529860e+00
    timestamp      8.835289e+08
    age            3.296650e+01
    unknown        1.000000e-04
    Action         2.558900e-01
    Adventure      1.375300e-01
    Animation      3.605000e-02
    Childrens      7.182000e-02
    Comedy         2.983200e-01
    Crime          8.055000e-02
    Documentary    7.580000e-03
    Drama          3.989500e-01
    Fantasy        1.352000e-02
    Film-Noir      1.733000e-02
    Horror         5.317000e-02
    Musical        4.954000e-02
    Mystery        5.245000e-02
    Romance        1.946100e-01
    Sci-Fi         1.273000e-01
    Thriller       2.187200e-01
    War            9.398000e-02
    Western        1.854000e-02
    dtype: float64




```python
# to print mean of all row values in movies :
movies.loc[:,(movies.dtypes==np.int64) | (movies.dtypes==np.float64)].apply(np.mean, axis = 1)
```




    0        3.671881e+07
    1        3.692952e+07
    2        3.680285e+07
    3        3.712641e+07
    4        3.648948e+07
    5        3.662343e+07
    6        3.683796e+07
    7        3.664883e+07
    8        3.672981e+07
    9        3.657322e+07
    10       3.646959e+07
    11       3.714094e+07
    12       3.691021e+07
    13       3.667207e+07
    14       3.868486e+07
    15       3.711643e+07
    16       3.654020e+07
    17       3.646151e+07
    18       3.825258e+07
    19       3.684153e+07
    20       3.663078e+07
    21       3.653976e+07
    22       3.690734e+07
    23       3.700433e+07
    24       3.804139e+07
    25       3.704913e+07
    26       3.715335e+07
    27       3.680185e+07
    28       3.682009e+07
    29       3.682872e+07
                 ...     
    99970    3.836551e+07
    99971    3.702680e+07
    99972    3.703066e+07
    99973    3.705424e+07
    99974    3.661341e+07
    99975    3.714594e+07
    99976    3.714594e+07
    99977    3.714592e+07
    99978    3.714594e+07
    99979    3.714594e+07
    99980    3.714592e+07
    99981    3.648981e+07
    99982    3.869825e+07
    99983    3.720672e+07
    99984    3.714594e+07
    99985    3.714584e+07
    99986    3.876098e+07
    99987    3.704094e+07
    99988    3.712668e+07
    99989    3.696509e+07
    99990    3.712652e+07
    99991    3.713393e+07
    99992    3.807540e+07
    99993    3.684269e+07
    99994    3.678404e+07
    99995    3.705384e+07
    99996    3.866487e+07
    99997    3.705384e+07
    99998    3.696514e+07
    99999    3.670202e+07
    Length: 100000, dtype: float64



### Remember

The attribute axis define the horizontal `(axis=1)` or vertical direction for calculations `(axis=0)`

---
## Groupby with Dictionary

Find more about this at my GeeksForGeeks [Publication](https://www.geeksforgeeks.org/combining-multiple-columns-in-pandas-groupby-with-dictionary/).

---
## Breaking up a String into columns using regex

Find more about this at my GeeksForGeeks [Publication](https://www.geeksforgeeks.org/split-a-string-into-columns-using-regex-in-pandas-dataframe/).

---
## Ranking Rows in Pandas

Find more about this at my GeeksForGeeks [Publication](https://www.geeksforgeeks.org/ranking-rows-of-pandas-dataframe/).


---

<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/RohitMidha23" data-size="large" data-show-count="true" aria-label="Follow @RohitMidha23 on GitHub">Follow @RohitMidha23</a>
<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>

Find more at my Github repository [Explained](http://bit.ly/ExplainedRepo).

Show some :heart: by :star:ing it.

<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/RohitMidha23/Explained" data-size="large" data-show-count="true" aria-label="Star RohitMidha23/Explained on GitHub">Star</a>
<a href="https://github.com/RohitMidha23/Explained" class="github-corner" aria-label="View source on GitHub"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#fff; color:#151513; position: absolute; top: 0; border: 0; left: 0; transform: scale(-1, 1);" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a><style>.github-corner:hover .octo-arm{animation:octocat-wave 560ms ease-in-out}@keyframes octocat-wave{0%,100%{transform:rotate(0)}20%,60%{transform:rotate(-25deg)}40%,80%{transform:rotate(10deg)}}@media (max-width:500px){.github-corner:hover .octo-arm{animation:none}.github-corner .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>
