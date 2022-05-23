+++
title =  "Filtering Julia Dataframes with Other Julia DataFrames."
date = "2022-05-22T16:30:32.169Z"
description = "How to filter the columns of Dataframes just like in Python."
author = "Justin Napolitano"
image = "post-image.png"
featuredimage = "post-image.png"
categories = ['Julia','Tutorials']
tags = ['julia', 'dataframes' 'set operations']
images = ['featured-julia.jpeg']
series = ['Julia Tutorials']
+++

# Transitioning from Python to Julia

I've begun to transition some of my worflow from Python to Julia.  Apprehending a new language is somewhat difficult.  Python conventions and syntactical sugar do not always translate to Julia.  

## Filtering a dataframe in Python.  

There are a number of ways to do this in Python.  Review [this article](https://towardsdatascience.com/8-ways-to-filter-pandas-dataframes-d34ba585c1b8) for a quick summary.  

I typically filter with logical operators and the iloc method.  



### Filtering with Logical Operators and LOC


Below is taken from an excerpt of my work published at [energy.jnapolitano.io](https://energy.jnapolitano.io/parts/nuclear-plants.html).  You can review the entire document there for more information. 



```Python

isfilepath = "<File Path Here>

# Reading Power plants data into a geopands df.  
powerplants_df = gpd.read_file(gisfilepath)
#Selecting only Operational Plants with loc
# Copying the result as i will be modifying the contents later.
powerplants_df=powerplants_df.loc[powerplants_df['STATUS'] == 'OP'].copy()
#the data i worked with reported na's as -999  or -772 for some legacy institutional reason the correlated with something I wasn't privy to. As a heuristic convention I took the minimum to replace with nan.  I replaced them with 0 instead of just dropping them.  
na = powerplants_df.COAL_USED.min()
powerplants_df.replace(na, 0 , inplace=True)
```

## Doing this in Julia

### The Filter Function

The built in Filter function in julia permitted me to iterate of each row of the File column in the loc_dataframe.  I then checked if that item was within the oyez_dataframe File column.  There may be a way to accomplish this by passing a Truth table, but I have yet to figure it out.  

```julia

filtered_df = filter(row -> (row.File in oyez_dataframe.File), loc_dataframe)

```




