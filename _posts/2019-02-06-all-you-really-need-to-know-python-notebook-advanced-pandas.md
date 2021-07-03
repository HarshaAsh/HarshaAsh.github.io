---
id: 728
title: 'All you ‘really’ need to know | Python Notebook | Advanced &#8211; Pandas'
date: 2019-02-06T14:26:52+05:30
author: Tamoghna Saha
layout: post
guid: https://www.harshaash.com/?p=728
permalink: /all-you-really-need-to-know-python-notebook-advanced-pandas/
image: /wp-content/uploads/2019/02/python-pandas.jpg
categories:
  - Uncategorized
tags:
  - data analytics
  - data cleaning
  - data science
  - dataframe
  - EDA
  - filtering
  - group by
  - merging
  - pandas
  - python
  - selection
  - sorting
---
<figure class="wp-block-image"><img loading="lazy" width="1024" height="172" src="https://www.harshaash.com/wp-content/uploads/2019/02/python-pandas-1024x172.jpg" alt="" class="wp-image-747" srcset="https://www.harshaash.com/wp-content/uploads/2019/02/python-pandas-1024x172.jpg 1024w, https://www.harshaash.com/wp-content/uploads/2019/02/python-pandas-300x50.jpg 300w, https://www.harshaash.com/wp-content/uploads/2019/02/python-pandas-768x129.jpg 768w, https://www.harshaash.com/wp-content/uploads/2019/02/python-pandas.jpg 1333w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure> 

It’s pretty obvious to summon the fact that you wouldn’t have clicked on this article if you have no understanding of the basics and intermediate level concepts of Python. You have? Then it is fair enough to go ahead with this article.

You are confused with some basic stuffs, or perhaps forgot about it? I got you covered with my previous articles. Check out the <a href="https://medium.com/@tamoghnasaha.22/a-quick-guide-to-python-notebook-beginners-6bbe3e2bb762" target="_blank" rel="noreferrer noopener"><em>notebook for beginners</em></a> to make your base strong and then climb up the ladder with intermediate level notebooks which I have divided it in 2 parts (<a href="https://medium.com/@tamoghnasaha.22/a-not-so-quick-but-conceptual-guide-to-python-notebook-intermediate-part-1-affd908a2a49" target="_blank" rel="noreferrer noopener"><em>1st part</em></a> and <a href="https://medium.com/@tamoghnasaha.22/a-not-so-quick-but-conceptual-guide-on-python-notebook-intermediate-part-2-b476d24765db" target="_blank" rel="noreferrer noopener"><em>2nd part</em></a>) so that you don’t find it lengthy and get exhausted in the midway.

**ATTENTION!!!**  
Pandas will _drop support_ for Python 2 from **1st January 2019**. This comes after Python’s core team announced they **will stop support for Python 2.7 from 2020 onward**. Hence, start working on Python 3.X.X.

As always, I have embedded the notebook at the end of the article. While writing this article, I faced issue in the code snippets — unable to print the Data Frames properly. So, it’s better if you go through the notebook rather than going through this article.

For explaining some of the functionalities with pandas, I have used a **Google Play Store** data-set from <a href="https://www.kaggle.com/lava18/google-play-store-apps" rel="noreferrer noopener" target="_blank">Kaggle</a>. _The data-set is a Web scraped data of 10,000 Play Store apps for analyzing the Android market._ I have performed some of the mentioned methods for each operation.

### Table of&nbsp;Content: {#9b38}

  * Pandas
  * Importing Data
  * Creating Test Object
  * Viewing Data
  * Data Cleaning
  * Selection
  * Filter, Sort & Group by
  * Iteration
  * Join, Merging
  * Statistics
  * Visualization
  * Exporting Data

### Pandas {#d04e}

Pandas is an open source data analysis library for providing easy-to-use data structures and data analysis tools.  
**DataFrame** is a m*n vector where  
* m is the number of rows  
* n is the number of columns

**Series** is a m*1 vector. Hence, each column in DataFrame is known as a pandas series.

**NOTE  
** * df — A pandas DataFrame object  
* s — A pandas Series object

### Importing Data {#de43}

<pre class="wp-block-preformatted">&gt;&gt;&gt; import pandas as pd<br />&gt;&gt;&gt; import numpy as np</pre>

<pre class="wp-block-preformatted">#read from csv<br />>>> df = pd.read_csv('google-play-store-apps/googleplaystore.csv')<br /><br /></pre>

Other ways of importing data depending on the file type.

  * **pd.read_table(filename)** — From a delimited text file (like TSV)
  * **pd.read_excel(filename)** — From an Excel file
  * **pd.read\_sql(query, connection\_object)** — Reads from a SQL table/database
  * **pd.read\_json(json\_string)** — Reads from a JSON file and extracts tables to a list of dataframes

### Create Test&nbsp;Objects {#b118}

  * **pd.DataFrame(dict)** — From a dict, keys for columns names, values for data as lists
  * **pd.DataFrame(np.random.rand(20,5))** — 5 columns and 20 rows of random floats
  * **pd.Series(my_list)** — Creates a series from an iterable my_list

<pre class="wp-block-preformatted">&gt;&gt;&gt; df_dict = pd.DataFrame(columns=['City','State'], data = [['Kolkata','West Bengal'], ['Bangalore','Karnataka']])<br />df_dict</pre>

<pre class="wp-block-preformatted">| |   City    | State       |<br />|0| Kolkata   | West Bengal |<br />|1| Bangalore | Karnataka   |</pre>

### Viewing Data {#7985}

  * **df.head(n)** — First n rows of the DataFrame [**replace head with tail**, you know what you will get]
  * **df.shape** — Number of rows and columns
  * **df.info()** — Index, Datatype and Memory
  * **df.describe()** — Summary statistics for numerical columns
  * **df.apply(pd.Series.value_counts)** — Unique values and counts for all columns

**s.value_counts(dropna=False)** — Views unique values and counts

<pre class="wp-block-preformatted">&gt;&gt;&gt; print("df shape\n")<br />&gt;&gt;&gt; print(df.shape)<br />&gt;&gt;&gt; print("\n================")<br />&gt;&gt;&gt; print("df info\n")<br />&gt;&gt;&gt; df.info()</pre>

<pre class="wp-block-preformatted">df shape<br /><br />(10841, 13)<br /><br />================<br />df info<br /><br />&lt;class 'pandas.core.frame.DataFrame'><br />RangeIndex: 10841 entries, 0 to 10840<br />Data columns (total 13 columns):<br />App               10841 non-null object<br />Category          10841 non-null object<br />Rating            9367 non-null float64<br />Reviews           10841 non-null object<br />Size              10841 non-null object<br />Installs          10841 non-null object<br />Type              10840 non-null object<br />Price             10841 non-null object<br />Content Rating    10840 non-null object<br />Genres            10841 non-null object<br />Last Updated      10841 non-null object<br />Current Ver       10833 non-null object<br />Android Ver       10838 non-null object<br />dtypes: float64(1), object(12)<br />memory usage: 1.1+ MB</pre>

### Selection {#3e0c}

  * **df[col]** or **df.col**&#8211; Returns column with label col as Series
  * **df[[col1, col2]]** — Returns Columns as a new DataFrame
  * **s.iloc[0]** — Selection by position
  * **s.loc[0]** — Selection by index
  * **df.loc[:,&nbsp;:]** and **df.iloc[:,&nbsp;:]** — First argument represents the number of rows and the second for columns
  * **df.ix[0:a, 0:b]** — Arguments notation is same as above but returns a rows and (b-1) columns **[deprecated in Python 3]**

<pre class="wp-block-preformatted"># row 0, all columns<br />&gt;&gt;&gt; df.loc[0, :]</pre>

<pre class="wp-block-preformatted">App               Photo Editor & Candy Camera & Grid & ScrapBook<br />Category                                          ART_AND_DESIGN<br />Rating                                                       4.1<br />Reviews                                                      159<br />Size                                                         19M<br />Installs                                                 10,000+<br />Type                                                        Free<br />Price                                                          0<br />Content Rating                                          Everyone<br />Genres                                              Art & Design<br />Last Updated                                     January 7, 2018<br />Current Ver                                                1.0.0<br />Android Ver                                         4.0.3 and up<br />Name: 0, dtype: object</pre>

<pre class="wp-block-preformatted"><br /># rows 0 to 4; all columns<br />&gt;&gt;&gt; df.loc[0:4,:] # : for columns is optional here since we are asking for all columns</pre>

<pre class="wp-block-preformatted"><br /># rows 0 to 4; selective columns<br />&gt;&gt;&gt; df.loc[0:4,['App','Category']]</pre>

<pre class="wp-block-preformatted">| | Apps | Category |<br />|0|Photo Editor & Candy Camera & Grid & ScrapBook |ART_AND_DESIGN|<br />|1|Coloring book moana |ART_AND_DESIGN|<br />|2|U Launcher Lite – FREE Live Cool Themes, Hide |ART_AND_DESIGN|<br />|3|Sketch - Draw & Paint |ART_AND_DESIGN|<br />|4|Pixel Draw - Number Art Coloring Book |ART_AND_DESIGN|</pre>

<pre class="wp-block-preformatted"><br /># rows 0 to 4; selective columns using iloc<br />&gt;&gt;&gt; df.iloc[0:4,[0,1]]</pre>

<pre class="wp-block-preformatted">| | Apps | Category |<br />|0|Photo Editor & Candy Camera & Grid & ScrapBook |ART_AND_DESIGN|<br />|1|Coloring book moana |ART_AND_DESIGN|<br />|2|U Launcher Lite – FREE Live Cool Themes, Hide |ART_AND_DESIGN|<br />|3|Sketch - Draw & Paint |ART_AND_DESIGN|</pre>

**NOTE**:

  * In **loc**, we are mentioning the column names for selection, while in **iloc** we are specifying the column number
  * In **loc**, rows are getting printed including the upper bound, while in **iloc**, it is excluding it

<g class="gr_ gr\_7 gr-alert gr\_gramm gr\_inline\_cards gr\_run\_anim Punctuation only-ins replaceWithoutSep" id="7" data-gr-id="7">Also</g> **NOTE** the following:

  * For creating a new DataFrame using column names

`df[[col1, col2]]`

is same as

`df.loc[:,[col1, col2]]`

  * For printing the first 5 rows of the DataFrame

`df[0:n]`

is same as

`df.iloc[0:n,&nbsp;:]`

### Data Cleaning {#ddfe}

  * **df.drop([col1, col2, col3], inplace = True, axis=1)** — Remove set of column(s)
  * **df.columns = [‘a’,’b’,’c’]** — Renames columns
  * **df.isnull()** — Checks for null Values, Returns Boolean DataFrame
  * **df.isnull().any()** — Returns boolean value for each column, gives True if any null value detected corresponding to that column
  * **df.dropna()** — Drops all rows that contain null values
  * **df.dropna(axis=1)** — Drops all columns that contain null values
  * **df.fillna(x)** — Replaces all null values with x
  * **s.replace(1,’one’)** — Replaces all values equal to 1 with ‘one’
  * **s.replace([1,3], [‘one’,’three’])** — Replaces all 1 with ‘one’ and 3 with ‘three’
  * **df.rename(columns = lambda x: x + ‘_1’)** — Mass renaming of columns
  * **df.rename(columns = {‘old\_name’: ‘new\_name’})** — Selective renaming
  * **df.rename(index = lambda x: x + 1)** — Mass renaming of index
  * **df[new_col] = df.col1 + ‘, ‘ + df.col2** — Add two columns to create a new column in the same DataFrame

<pre class="wp-block-preformatted">&gt;&gt;&gt; df.drop(['Category'], inplace=True, axis = 1)</pre>

<pre class="wp-block-preformatted">&gt;&gt;&gt; df_any_null = df.isnull().any()<br />&gt;&gt;&gt; df_any_null</pre>

<pre class="wp-block-preformatted">App               False<br />Rating             True<br />Reviews           False<br />Size              False<br />Installs          False<br />Type               True<br />Price             False<br />Content Rating     True<br />Genres            False<br />Last Updated      False<br />Current Ver        True<br />Android Ver        True<br />dtype: bool</pre>

<pre class="wp-block-preformatted">&gt;&gt;&gt; df.dropna(axis=0, inplace=True)<br />&gt;&gt;&gt; df_check_null = df.isnull().any()<br />&gt;&gt;&gt; print(df.shape)<br />&gt;&gt;&gt; df_check_null</pre>

<pre class="wp-block-preformatted">(9360, 12)</pre>

<pre class="wp-block-preformatted">App               False<br />Rating            False<br />Reviews           False<br />Size              False<br />Installs          False<br />Type              False<br />Price             False<br />Content Rating    False<br />Genres            False<br />Last Updated      False<br />Current Ver       False<br />Android Ver       False<br />dtype: bool</pre>

<pre class="wp-block-preformatted"># mass renaming of column where column names are made lower case and any blank spaces is replaced with _</pre>

<pre class="wp-block-preformatted">&gt;&gt;&gt; df_new_cols_name = df.rename(columns = lambda x: (x.lower()).replace(' ','_'))</pre>

### Filter, Sort & Group&nbsp;By {#0b32}

  * **df[df[col] > 0.5]** — Rows where the values in col > 0.5
  * **df[(df[col] > 0.5) & (df[col] < 0.7)]** — Rows where 0.7 > col > 0.5
  * **df.sort_values(col1)** — Sorts values by col1 in ascending order
  * **df.sort_values(col2,ascending=False)** — Sorts values by col2 in descending order
  * **df.sort_values([col1,col2],ascending=[True,False])** — Sorts values by col1 in ascending order then col2 in descending order
  * **df.groupby(col)** — Returns a groupby object for values from one column
  * **df.groupby([col1,col2])** — Returns a groupby object values from multiple columns
  * **df.groupby(col1)[col2].mean()** — (Aggregation) Returns the mean of the values in col2, grouped by the values in col1
  * **df.pivot_table(index=col1,values=[col2,col3],aggfunc=mean)** — Creates a pivot table that groups by col1 and calculates the mean of col2 and col3
  * **df.apply(np.mean)** — Applies a function across each column
  * **df.apply(np.max, axis=1)** — Applies a function across each row
  * **df.applymap(lambda arg(s): expression)** — Apply the expression on each value of the DataFrame
  * **df[col].map(lambda arg(s): expression)** — Apply the expression on each value of the column col

<pre class="wp-block-preformatted">&gt;&gt;&gt; df_high_rating = df[(df['Rating'] &gt; 4) & (df['Rating'] &lt; 5)]<br />&gt;&gt;&gt; print(df_high_rating.shape)</pre>

<pre class="wp-block-preformatted">(6522, 12)</pre>

<pre class="wp-block-preformatted">&gt;&gt;&gt; print(df.groupby('Genres').size())</pre>

<pre class="wp-block-preformatted">Genres<br />Action                                   358<br />Action;Action & Adventure                 17<br />Adventure                                 73<br />Adventure;Action & Adventure              13<br />Adventure;Brain Games                      1<br />Adventure;Education                        2<br />Arcade                                   207<br />Arcade;Action & Adventure                 15<br />Arcade;Pretend Play                        1<br />Art & Design                              55<br />Art & Design;Creativity                    7<br />Art & Design;Pretend Play                  2<br />Auto & Vehicles                           73<br />Beauty                                    42<br />Board                                     41<br />Board;Action & Adventure                   3<br />Board;Brain Games                         15<br />Board;Pretend Play                         1<br />Books & Reference                        178<br />Books & Reference;Education                2<br />Business                                 303<br />Card                                      45<br />Card;Action & Adventure                    2<br />Card;Brain Games                           1<br />Casino                                    37<br />Casual                                   185<br />Casual;Action & Adventure                 21<br />Casual;Brain Games                        13<br />Casual;Creativity                          7<br />Casual;Education                           3<br />                                        ... <br />Puzzle;Education                           1<br />Racing                                    93<br />Racing;Action & Adventure                 20<br />Racing;Pretend Play                        1<br />Role Playing                             106<br />Role Playing;Action & Adventure            7<br />Role Playing;Brain Games                   1<br />Role Playing;Pretend Play                  5<br />Shopping                                 238<br />Simulation                               194<br />Simulation;Action & Adventure             11<br />Simulation;Education                       3<br />Simulation;Pretend Play                    4<br />Social                                   259<br />Sports                                   333<br />Sports;Action & Adventure                  4<br />Strategy                                 103<br />Strategy;Action & Adventure                2<br />Strategy;Creativity                        1<br />Strategy;Education                         1<br />Tools                                    732<br />Tools;Education                            1<br />Travel & Local                           225<br />Travel & Local;Action & Adventure          1<br />Trivia                                    28<br />Video Players & Editors                  158<br />Video Players & Editors;Creativity         2<br />Video Players & Editors;Music & Video      3<br />Weather                                   75<br />Word                                      28<br />Length: 115, dtype: int64</pre>

<pre class="wp-block-preformatted">>>> print(df_high_rating.groupby(['Rating','Type']).size())</pre>

<pre class="wp-block-preformatted">Rating  Type<br />4.1     Free     675<br />        Paid      32<br />4.2     Free     889<br />        Paid      62<br />4.3     Free    1025<br />        Paid      51<br />4.4     Free    1031<br />        Paid      77<br />4.5     Free     964<br />        Paid      73<br />4.6     Free     741<br />        Paid      82<br />4.7     Free     446<br />        Paid      53<br />4.8     Free     195<br />        Paid      39<br />4.9     Free      81<br />        Paid       6<br />dtype: int64</pre>

<pre class="wp-block-preformatted"># store the grouped by table in a dataframe<br />>>> df_group_by = pd.DataFrame({'count': df_high_rating.groupby(['Rating','Type']).size()}).reset_index()</pre>

<pre class="wp-block-preformatted"># iterating through groupby<br />>>> grouped = df_high_rating.groupby('Rating')<br />>>> for name,group in grouped:<br />        if name >= 4.8: #only printing for rating 4.8 and 4.9<br />            print(name)<br />            print(group)<br />            print("="*50)</pre>

<pre class="wp-block-preformatted"># aggregation<br />>>> grouped = df.groupby('Genres')<br />>>> print(grouped['Rating'].agg(np.mean))</pre>

<pre class="wp-block-preformatted">Genres<br />Action                                   4.285475<br />Action;Action & Adventure                4.311765<br />Adventure                                4.180822<br />Adventure;Action & Adventure             4.423077<br />Adventure;Brain Games                    4.600000<br />Adventure;Education                      4.100000<br />Arcade                                   4.304348<br />Arcade;Action & Adventure                4.346667<br />Arcade;Pretend Play                      4.500000<br />Art & Design                             4.380000<br />Art & Design;Creativity                  4.400000<br />Art & Design;Pretend Play                3.900000<br />Auto & Vehicles                          4.190411<br />Beauty                                   4.278571<br />Board                                    4.292683<br />Board;Action & Adventure                 4.033333<br />Board;Brain Games                        4.340000<br />Board;Pretend Play                       4.800000<br />Books & Reference                        4.346067<br />Books & Reference;Education              4.200000<br />Business                                 4.121452<br />Card                                     4.086667<br />Card;Action & Adventure                  4.300000<br />Card;Brain Games                         4.400000<br />Casino                                   4.286486<br />Casual                                   4.150811<br />Casual;Action & Adventure                4.266667<br />Casual;Brain Games                       4.469231<br />Casual;Creativity                        4.314286<br />Casual;Education                         4.266667<br />                                           ...   <br />Puzzle;Education                         4.600000<br />Racing                                   4.173118<br />Racing;Action & Adventure                4.300000<br />Racing;Pretend Play                      4.500000<br />Role Playing                             4.275472<br />Role Playing;Action & Adventure          4.342857<br />Role Playing;Brain Games                 4.300000<br />Role Playing;Pretend Play                4.020000<br />Shopping                                 4.259664<br />Simulation                               4.151546<br />Simulation;Action & Adventure            4.418182<br />Simulation;Education                     4.366667<br />Simulation;Pretend Play                  4.350000<br />Social                                   4.255598<br />Sports                                   4.236637<br />Sports;Action & Adventure                4.350000<br />Strategy                                 4.245631<br />Strategy;Action & Adventure              4.600000<br />Strategy;Creativity                      4.400000<br />Strategy;Education                       4.500000<br />Tools                                    4.046585<br />Tools;Education                          4.500000<br />Travel & Local                           4.109333<br />Travel & Local;Action & Adventure        4.100000<br />Trivia                                   4.039286<br />Video Players & Editors                  4.063924<br />Video Players & Editors;Creativity       4.100000<br />Video Players & Editors;Music & Video    4.000000<br />Weather                                  4.244000<br />Word                                     4.410714<br />Name: Rating, Length: 115, dtype: float64</pre>

<pre class="wp-block-preformatted"><br /># applying multiple aggregation functions at once<br />&gt;&gt;&gt; print(grouped['Rating'].agg([np.sum, np.mean, np.std]))</pre>

<pre class="wp-block-preformatted">sum      mean       std<br />Genres                                                           <br />Action                                 1534.2  4.285475  0.291353<br />Action;Action & Adventure                73.3  4.311765  0.172780<br />Adventure                               305.2  4.180822  0.312542<br />Adventure;Action & Adventure             57.5  4.423077  0.148064<br />Adventure;Brain Games                     4.6  4.600000       NaN<br />Adventure;Education                       8.2  4.100000  0.000000<br />Arcade                                  891.0  4.304348  0.351323<br />Arcade;Action & Adventure                65.2  4.346667  0.306749<br />Arcade;Pretend Play                       4.5  4.500000       NaN<br />Art & Design                            240.9  4.380000  0.321685<br />Art & Design;Creativity                  30.8  4.400000  0.404145<br />Art & Design;Pretend Play                 7.8  3.900000  0.000000<br />Auto & Vehicles                         305.9  4.190411  0.543692<br />Beauty                                  179.7  4.278571  0.362603<br />Board                                   176.0  4.292683  0.417367<br />Board;Action & Adventure                 12.1  4.033333  0.057735<br />Board;Brain Games                        65.1  4.340000  0.297129<br />Board;Pretend Play                        4.8  4.800000       NaN<br />Books & Reference                       773.6  4.346067  0.429046<br />Books & Reference;Education               8.4  4.200000  0.707107<br />Business                               1248.8  4.121452  0.624422<br />Card                                    183.9  4.086667  0.708263<br />Card;Action & Adventure                   8.6  4.300000  0.000000<br />Card;Brain Games                          4.4  4.400000       NaN<br />Casino                                  158.6  4.286486  0.310163<br />Casual                                  767.9  4.150811  0.442218<br />Casual;Action & Adventure                89.6  4.266667  0.367877<br />Casual;Brain Games                       58.1  4.469231  0.209701<br />Casual;Creativity                        30.2  4.314286  0.291139<br />Casual;Education                         12.8  4.266667  0.152753<br />...                                       ...       ...       ...<br />Puzzle;Education                          4.6  4.600000       NaN<br />Racing                                  388.1  4.173118  0.327089<br />Racing;Action & Adventure                86.0  4.300000  0.194666<br />Racing;Pretend Play                       4.5  4.500000       NaN<br />Role Playing                            453.2  4.275472  0.340815<br />Role Playing;Action & Adventure          30.4  4.342857  0.229907<br />Role Playing;Brain Games                  4.3  4.300000       NaN<br />Role Playing;Pretend Play                20.1  4.020000  0.426615<br />Shopping                               1013.8  4.259664  0.404577<br />Simulation                              805.4  4.151546  0.401710<br />Simulation;Action & Adventure            48.6  4.418182  0.252262<br />Simulation;Education                     13.1  4.366667  0.152753<br />Simulation;Pretend Play                  17.4  4.350000  0.331662<br />Social                                 1102.2  4.255598  0.413809<br />Sports                                 1410.8  4.236637  0.423600<br />Sports;Action & Adventure                17.4  4.350000  0.191485<br />Strategy                                437.3  4.245631  0.373583<br />Strategy;Action & Adventure               9.2  4.600000  0.000000<br />Strategy;Creativity                       4.4  4.400000       NaN<br />Strategy;Education                        4.5  4.500000       NaN<br />Tools                                  2962.1  4.046585  0.616731<br />Tools;Education                           4.5  4.500000       NaN<br />Travel & Local                          924.6  4.109333  0.505816<br />Travel & Local;Action & Adventure         4.1  4.100000       NaN<br />Trivia                                  113.1  4.039286  0.808904<br />Video Players & Editors                 642.1  4.063924  0.554566<br />Video Players & Editors;Creativity        8.2  4.100000  0.000000<br />Video Players & Editors;Music & Video    12.0  4.000000  0.000000<br />Weather                                 318.3  4.244000  0.331353<br />Word                                    123.5  4.410714  0.325849<br /><br />[115 rows x 3 columns]</pre>

### Iteration {#6045}

To iterate over the rows of the DataFrame, we can use the following functions:

  * **df.iteritems()** − to iterate over the (key,value) pairs
  * **df.iterrows()** − iterate over the rows as (index,series) pairs
  * **df.itertuples()** − this method will return an iterator yielding a named tuple for each row in the DataFrame. The **first element** of the tuple will be the **row’s corresponding index value**, while the remaining values are the row values.

<pre class="wp-block-preformatted">&gt;&gt;&gt; iterated_df = pd.DataFrame(np.random.randn(4,3),columns=['col1','col2','col3'])<br />&gt;&gt;&gt; for key,value in iterated_df.iteritems():<br />        print(key)<br />        print(value)</pre>

<pre class="wp-block-preformatted">col1<br />0   -0.031657<br />1   -2.031456<br />2    2.820815<br />3   -0.153405<br />Name: col1, dtype: float64<br />col2<br />0    0.152370<br />1   -1.157595<br />2    2.817094<br />3   -0.227610<br />Name: col2, dtype: float64<br />col3<br />0    1.047588<br />1   -0.461455<br />2   -0.177125<br />3   -0.698067<br />Name: col3, dtype: float64</pre>

### Operations with text&nbsp;data {#cdaf}

String operations can be performed on Series in the format **s.str.op** where **op** can be:

  1. **swapcase** — Swaps the case lower/upper.
  2. **lower() / upper()** — Converts strings in the Series/Index to lower / upper case.
  3. **len()** — Computes String length.
  4. **strip()** — Helps strip whitespace(including newline) from each string in the Series/index from both the sides.
  5. **split(‘ ‘)** — Splits each string with the given pattern.
  6. **cat(sep=’ ‘)** — Concatenates the series/index elements with given separator.
  7. **get_dummies()** — Returns the DataFrame with One-Hot Encoded values.
  8. **contains(pattern)** — Returns Boolean True for each element if the substring contains in the element, else False.
  9. **replace(a,b)** — Replaces the value a with the value b.
 10. **repeat(value)** — Repeats each element with specified number of times.
 11. **count(pattern)** — Returns count of appearance of pattern in each element.
 12. **startswith(pattern) / endswith(pattern)** — Returns true if the element in the Series/Index starts / ends with the pattern.
 13. **find(pattern)** — Returns the first position of the first occurrence of the pattern. Returns -1 if not found.
 14. **findall(pattern)** — Returns a list of all occurrence of the pattern.
 15. **islower() / isupper() / isnumeric()** — Checks whether all characters in each string in the Series/Index in lower / upper case / numeric or not. Returns Boolean.

<pre class="wp-block-preformatted">&gt;&gt;&gt; s = pd.Series(['Tom ', ' William Rick', 'John', 'Alber@t'])<br />&gt;&gt;&gt; print(s.str.contains(' '))</pre>

<pre class="wp-block-preformatted">0     True<br />1     True<br />2    False<br />3    False<br />dtype: bool</pre>

### Joining, Merging {#94aa}

  1. **df1.append(df2)** — Adds the rows in df1 to the end of df2 (columns should be identical)
  2. **pd.concat([df1, df2], axis=1)** — Adds the columns in df1 to the end of df2 (rows should be identical)
  3. **pd.merge(left, right, how=’inner’, on=None, left\_on=None, right\_on=None, left\_index=False, right\_index=False, sort=True)** — where

  * left − A DataFrame object.
  * right − Another DataFrame object.
  * how − One of ‘left’, ‘right’, ‘outer’, ‘inner’. Defaults to inner. Each method has been described below.
  * on − Columns (names) to join on. **Must be found in both** the left and right DataFrame objects.
  * left_on − Columns from the left DataFrame to use as keys.
  * right_on − Columns from the right DataFrame to use as keys.
  * left_index − If True, use the index (row labels) from the left DataFrame as its join key(s). In case of a DataFrame with a MultiIndex (hierarchical), the number of levels must match the number of join keys from the right DataFrame.
  * right\_index − Same usage as left\_index for the right DataFrame.
  * sort − Sort the result DataFrame by the join keys in _lexicographical order_. Defaults to True, setting to False will improve the performance substantially in many cases.

<pre class="wp-block-preformatted">&gt;&gt;&gt; left = pd.DataFrame({<br />         'id':[1,2,3,4,5],<br />         'Name': ['Alex', 'Amy', 'Allen', 'Alice', 'Ayan'],<br />         'subject_id':['sub1','sub2','sub4','sub6','sub5']})</pre>

<pre class="wp-block-preformatted">&gt;&gt;&gt; right = pd.DataFrame(<br />         {'id':[1,2,3,4,5],<br />         'Name': ['Billy', 'Brian', 'Brock', 'Bryce', 'Betty'],<br />         'subject_id':['sub2','sub4','sub3','sub6','sub5']})</pre>

<pre class="wp-block-preformatted">&gt;&gt;&gt; print(pd.concat([left,right],ignore_index=True)) # merging by rows<br />&gt;&gt;&gt; print('='*50)<br />&gt;&gt;&gt; print(left.append(right)) # also merging by rows<br />&gt;&gt;&gt; print('='*50)<br />&gt;&gt;&gt; print(pd.concat([left,right],axis=1)) # merging by columns</pre>

<pre class="wp-block-preformatted">id   Name subject_id<br />0   1   Alex       sub1<br />1   2    Amy       sub2<br />2   3  Allen       sub4<br />3   4  Alice       sub6<br />4   5   Ayan       sub5<br />5   1  Billy       sub2<br />6   2  Brian       sub4<br />7   3  Brock       sub3<br />8   4  Bryce       sub6<br />9   5  Betty       sub5<br />==================================================<br />   id   Name subject_id<br />0   1   Alex       sub1<br />1   2    Amy       sub2<br />2   3  Allen       sub4<br />3   4  Alice       sub6<br />4   5   Ayan       sub5<br />0   1  Billy       sub2<br />1   2  Brian       sub4<br />2   3  Brock       sub3<br />3   4  Bryce       sub6<br />4   5  Betty       sub5<br />==================================================<br />   id   Name subject_id  id   Name subject_id<br />0   1   Alex       sub1   1  Billy       sub2<br />1   2    Amy       sub2   2  Brian       sub4<br />2   3  Allen       sub4   3  Brock       sub3<br />3   4  Alice       sub6   4  Bryce       sub6<br />4   5   Ayan       sub5   5  Betty       sub5</pre>

<pre class="wp-block-preformatted"><br /># merge two dataframes on a key<br />&gt;&gt;&gt; print(pd.merge(left,right,on='id'))<br />&gt;&gt;&gt; print('='*50)<br /># merge two dataframes on multiple keys<br />&gt;&gt;&gt; print(pd.merge(left,right,on=['id','subject_id']))</pre>

<pre class="wp-block-preformatted">id Name_x subject_id_x Name_y subject_id_y<br />0   1   Alex         sub1  Billy         sub2<br />1   2    Amy         sub2  Brian         sub4<br />2   3  Allen         sub4  Brock         sub3<br />3   4  Alice         sub6  Bryce         sub6<br />4   5   Ayan         sub5  Betty         sub5<br />==================================================<br />   id Name_x subject_id Name_y<br />0   4  Alice       sub6  Bryce<br />1   5   Ayan       sub5  Betty<br /><br /></pre>

<pre class="wp-block-preformatted">| Merge Method | SQL Equivalent | Description |<br />| left  | LEFT OUTER JOIN  | Use keys from left object |<br />| right | RIGHT OUTER JOIN | Use keys from right object |<br />| outer | FULL OUTER JOIN  | Use union of keys |<br />| inner | INNER JOIN       | Use intersection of keys |</pre>

<pre class="wp-block-preformatted"><br />&gt;&gt;&gt; print(pd.merge(left, right, on='subject_id', how='inner'))</pre>

<pre class="wp-block-preformatted">id_x Name_x subject_id  id_y Name_y<br />0     2    Amy       sub2     1  Billy<br />1     3  Allen       sub4     2  Brian<br />2     4  Alice       sub6     4  Bryce<br />3     5   Ayan       sub5     5  Betty</pre>

### Statistics {#6544}

  * **df.mean()** — Returns the mean of all columns
  * **df.corr()** — Returns the correlation between columns in a DataFrame
  * **df.count()** — Returns the number of non-null values in each DataFrame column
  * **df.max()** — Returns the highest value in each column
  * **df.min()** — Returns the lowest value in each column
  * **df.median()** — Returns the median of each column
  * **df.std()** — Returns the standard deviation of each column

<pre class="wp-block-preformatted">&gt;&gt;&gt; df['Rating'].mean()</pre>

<pre class="wp-block-preformatted">4.191837606837606</pre>

### Visualization {#f426}

The following charts we can generate straight from pandas:

  * **bar** or **barh** for bar plots
  * **hist** for histogram
  * **area** for area plots
  * **scatter** for scatter plots

<pre class="wp-block-preformatted">&gt;&gt;&gt; df_group_by[df_group_by['Type']=='Free']['count'].plot()</pre>

<pre class="wp-block-preformatted">&lt;matplotlib.axes._subplots.AxesSubplot at 0x7f0dd22b64e0&gt;</pre><figure class="wp-block-image">

![](https://cdn-images-1.medium.com/max/1600/1*NJ2ExZppRpdqO5ETfvxlsw.png) </figure> 

<pre class="wp-block-preformatted">&gt;&gt;&gt; df_bar = df_high_rating[['Rating','Reviews']][:10]<br />&gt;&gt;&gt; df_bar['Reviews'] = df_bar['Reviews'].astype(int)</pre>

<pre class="wp-block-preformatted">&gt;&gt;&gt; df_bar.plot.bar(stacked = True)</pre>

<pre class="wp-block-preformatted">&lt;matplotlib.axes._subplots.AxesSubplot at 0x7f0dd221cdd8&gt;</pre><figure class="wp-block-image">

![](https://cdn-images-1.medium.com/max/1600/1*rQPKgfxJvB5ewRqPtiA5_g.png) </figure> 

<pre class="wp-block-preformatted">&gt;&gt;&gt; df_bar.plot.scatter(x='Rating', y='Reviews')</pre>

<pre class="wp-block-preformatted">&lt;matplotlib.axes._subplots.AxesSubplot at 0x7f0dd21487b8&gt;</pre><figure class="wp-block-image">

![](https://cdn-images-1.medium.com/max/1600/1*hwpFgGXsoi3eY6wP9M8C4w.png) </figure> 

### Exporting the&nbsp;Data {#8b8f}

  * **df.to_csv(filename)** — Writes to a CSV file
  * **df.to_excel(filename)** — Writes to an Excel file
  * **df.to\_sql(table\_name, connection_object)** — Writes to a SQL table
  * **df.to_json(filename)** — Writes to a file in JSON format
  * **df.to_html(filename)** — Saves as an HTML table

<pre class="wp-block-preformatted">>>> df_new_cols_name.to_csv('./google-play-store-apps/cleaned_googleplay_data.csv')</pre>

<hr class="wp-block-separator" />

I hope you have liked this article. If yes, then do share it with your friends or colleagues who you think will be benefited.