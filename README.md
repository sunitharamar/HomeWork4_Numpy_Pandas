

```python
# This is Option 1: Heroes of Pymoli 
#analyzing the data for their most recent fantasy game Heroes of Pymoli.
```


```python
# Import the Pandas library
import pandas as pd
import os
import numpy as np
import json
```


```python
#======================================================================================================
```


```python
##################### This is the Starting section for "PLAYER COUNT" ################################## 
```


```python
#======================================================================================================
```


```python
# Reading my 2 input files from json format
my_data1_df = pd.read_json('purchase_data.json')
my_data2_df = pd.read_json('purchase_data2.json')

#Took screenshots from "my_data1_df" and uploaded to the HW github.
#Working Input file 
my_data_df = my_data2_df

```


```python
 
print(len(my_data_df))
my_data_df.head()

 
```

    78





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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Note that .describe() will only return summary statistics for your numeric columns(Age, Item ID, Price)
my_data_df.describe()
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
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>78.000000</td>
      <td>78.000000</td>
      <td>78.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>22.551282</td>
      <td>93.935897</td>
      <td>2.924359</td>
    </tr>
    <tr>
      <th>std</th>
      <td>7.339003</td>
      <td>56.352633</td>
      <td>1.134913</td>
    </tr>
    <tr>
      <th>min</th>
      <td>7.000000</td>
      <td>0.000000</td>
      <td>1.020000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>20.000000</td>
      <td>48.000000</td>
      <td>1.925000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>22.500000</td>
      <td>97.500000</td>
      <td>2.770000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>25.000000</td>
      <td>137.000000</td>
      <td>4.092500</td>
    </tr>
    <tr>
      <th>max</th>
      <td>40.000000</td>
      <td>181.000000</td>
      <td>4.810000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Remove the rows with missing data
clean_df = my_data_df.dropna(how="any")
clean_df.count() #just to make sure I ran this dropping the rows with missing data - still same number which is consistent
```




    Age          78
    Gender       78
    Item ID      78
    Item Name    78
    Price        78
    SN           78
    dtype: int64




```python
# How many times each unique Players participated with the value counts.
Player_count = clean_df["SN"].value_counts()
Player_count.head() 
```




    Sundaky74       2
    Aidaira26       2
    Chaniman66      2
    Hairith93       2
    Undirrasta74    1
    Name: SN, dtype: int64




```python
# Get the unique Player_count with length fucntion
total_columns = len(Player_count.axes[0]) # Total number of Players with axes[0] <- Rows , axes[1] <- Column
print(total_columns)
```

    74



```python
#Creating a new dataframe for results of "Total Players"
 
my_list = [{"Total Players": total_columns }] 
total_players_df = pd.DataFrame(my_list)
total_players_df
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>74</td>
    </tr>
  </tbody>
</table>
</div>




```python
#==================================================================================================================
```


```python
##################### This is the Starting section for " PURCHASING ANALYSIS (Total)" ############################## 
```


```python
#==================================================================================================================
```


```python
# List of unique item names from column
unique_item_names =  clean_df["Item Name"].unique()
#print(unique_item_names )
```


```python
#Total unique item names, using len function to get the list/array length.
Total_unique_item_names = len(unique_item_names)
#Total_unique_item_names
```


```python
# Average Purchase Price - in other words basically it is the mean value of the column "Price"
average_purchase_price =  clean_df["Price"].mean()
#print(average_purchase_price )
```


```python
# Total Number of Purchases
Total_number_of_purchases = clean_df["Item ID"].count()
#Total_number_of_purchases
```


```python
# Total Revenue
Total_revenue = clean_df["Price"].sum()
Total_revenue
```




    228.0999999999999




```python
# Gender Demographics

# Count of Male, Female, Non-Disclosed Players
Gender_count = clean_df["Gender"].value_counts() 

Gender_count.head()
```




    Male                     64
    Female                   13
    Other / Non-Disclosed     1
    Name: Gender, dtype: int64




```python
# Total Count of the Column "Gender"
total_count_gender = clean_df["Gender"].count()
#total_count_gender
```


```python
#Creating a new dataframe for results of "Purchasing Analysis (Total)" with adding dollar sign to it. formating

def dollarsign(x):
    return '${:,.2f}'.format(x) 
 
    
my_dict = {"Number of unique Items": [Total_unique_item_names],
           "Average Price": [average_purchase_price],
           "Number of Purchases": [Total_number_of_purchases],
           "Total Revenue":  [Total_revenue]}  

my_df_2 = pd.DataFrame(my_dict)
my_df_2['Total Revenue'] =  my_df_2['Total Revenue'].apply(dollarsign)
my_df_2['Average Price'] =  my_df_2['Average Price'].apply(dollarsign)



my_df_2
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
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Number of unique Items</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$2.92</td>
      <td>78</td>
      <td>63</td>
      <td>$228.10</td>
    </tr>
  </tbody>
</table>
</div>




```python
#==================================================================================================================
```


```python
##################### This is the Starting section for " GENDER DEMOGRAPHICS " ############################## 
```


```python
#==================================================================================================================
```


```python
Percentage_Male = (((Gender_count.loc["Male"])/total_count_gender)*100)
#print(Percentage_Male)
 
```


```python
Percentage_Female = (((Gender_count.loc["Female"])/total_count_gender)*100)
#print(Percentage_Female)
```


```python

Percentage_Other_Nondisclosed = (((Gender_count.loc["Other / Non-Disclosed"])/total_count_gender)*100)
#print(Percentage_Other_Nondisclosed)
```


```python
# Creating a new dataframe for Gender Demographies
gender_dic = {"Gender": ["Male", "Female", "Other/Non-Disclosed"],
              "Percentage of Players": [Percentage_Male, Percentage_Female, Percentage_Other_Nondisclosed],
              "Total Count": [Gender_count.loc["Male"], Gender_count.loc["Female"], Gender_count.loc["Other / Non-Disclosed"]]}

gender_demography_df = pd.DataFrame(gender_dic) # set the row index to be "Gender"

#gender_demography_df
                            
```


```python
def percentsign(x):
    return '{:.2f}%'.format(x) 

gender_demography_df['Percentage of Players'] = gender_demography_df['Percentage of Players'].apply(percentsign)
#gender_demography_df
 
```


```python
gender_demography_df = gender_demography_df.set_index("Gender")

gender_demography_df
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
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>82.05%</td>
      <td>64</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>16.67%</td>
      <td>13</td>
    </tr>
    <tr>
      <th>Other/Non-Disclosed</th>
      <td>1.28%</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#==================================================================================================================
```


```python
##################### This is the Starting section for " PURCHASING ANALYSIS (Gender) " ############################## 
```


```python
#==================================================================================================================
```


```python
# Group my_data by the "Gender" column
grouped_Gender_df = my_data_df.groupby("Gender")

# Note that the "GroupBy" object by itself is not particularly useful
print(grouped_Gender_df)

```

    <pandas.core.groupby.DataFrameGroupBy object at 0x106618320>



```python
# Now the groupy object will be useful with the count/values
#grouped_Gender_df.count()
```


```python
# This is the data type float with series
Gender_purchase_count = grouped_Gender_df["Price"].sum()
#Gender_purchase_count

```


```python
type(grouped_Gender_df["Price"].sum())
```




    pandas.core.series.Series




```python
Gender_purchase_count.loc["Male"]
Gender_purchase_count.loc["Female"]
Gender_purchase_count.loc["Other / Non-Disclosed"]
```




    2.1200000000000001




```python
# This is the dataframe object which has all the sum of "Price" column grouped with the "Gender"
sum_Gender_df = grouped_Gender_df[["Price"]].sum()
#sum_Gender_df
```


```python
type(sum_Gender_df) # Now that we have converted the sum_Gender_df to a DataFrame we can access the locations
```




    pandas.core.frame.DataFrame




```python
# Values are accessed with the .loc() for individual "Gender" column

sum_Gender_df.loc["Male"]
#sum_Gender_df.loc["Female"]
#sum_Gender_df.loc["Other / Non-Disclosed"]
 
```




    Price    184.6
    Name: Male, dtype: float64




```python
# This is the data type float with series for Average/Mean purchase price
Gender_average_price = grouped_Gender_df["Price"].mean()
Gender_average_price

```




    Gender
    Female                   3.183077
    Male                     2.884375
    Other / Non-Disclosed    2.120000
    Name: Price, dtype: float64




```python
Gender_average_price.loc["Male"]
Gender_average_price.loc["Female"]
Gender_average_price.loc["Other / Non-Disclosed"]
```




    2.1200000000000001




```python
#grouped_players_df = clean_df.groupby(["SN", "Gender"])
#print(grouped_players_df) 


 
#create a new FILTERABLE object that has the count of each group (Male, Female, Other count) 
df = clean_df[['SN','Gender']].groupby(['SN','Gender']).size().reset_index(name='count')


Male_count_df = df[df.Gender == 'Male']
len(Male_count_df)
#Male_count_df

Female_count_df = df[df.Gender == 'Female']
#len(Female_count_df)
#Female_count_df
 
Other_count_df = df[df.Gender == 'Other / Non-Disclosed']
#len(Other_count_df)
#Other_count_df
```


```python
# Normalization Totals in mathematical world
#Standardize = (X, mean, STDEV)
#mean = average
#X = starting number (move to each number at a time)
#STDEV = range (A1:A7) # column
```


```python
# Normalized Totals for Male 
# Total Purchase Value/Number of players(each group)
male_normalized_total = (Gender_purchase_count.loc["Male"])/(len(Male_count_df) )

male_normalized_total
Gender_purchase_count.loc["Male"]
```




    184.59999999999999




```python
# Normalized Totals for Female 
# Total Purchase Value/Number of players(each group)
female_normalized_total = (Gender_purchase_count.loc["Female"])/(len(Female_count_df))
female_normalized_total
```




    3.1830769230769231




```python
# Normalized Totals for Other/Non-Disclosed
# Total Purchase Value/Number of players(each group)
other_normalized_total = (Gender_purchase_count.loc["Other / Non-Disclosed"])/(len(Other_count_df))
other_normalized_total
```




    2.1200000000000001




```python
 # Creating a new dataframe for Purchasing Analysis (Gender)
purchasing_analysis_gender_dic = {"Gender": ["Male", "Female", "Other/Non-Disclosed"],
                                  "Purchase Count": [Gender_count.loc["Male"], Gender_count.loc["Female"], Gender_count.loc["Other / Non-Disclosed"]],
                                  "Average Purchase Price": [Gender_average_price.loc["Male"],Gender_average_price.loc["Female"],Gender_average_price.loc["Other / Non-Disclosed"]],
                                  "Total Purchase Value": [Gender_purchase_count.loc["Male"],Gender_purchase_count.loc["Female"],Gender_purchase_count.loc["Other / Non-Disclosed"]],
                                  "Normalized Totals": [ male_normalized_total, female_normalized_total, other_normalized_total],
                                  "# players(each group)":[(len(Male_count_df)), (len(Female_count_df)),(len(Other_count_df))]}
            

purchasing_analysis_gender_df = pd.DataFrame(purchasing_analysis_gender_dic) # Set the row index to be "Gender"

purchasing_analysis_gender_df['Average Purchase Price'] = purchasing_analysis_gender_df['Average Purchase Price'].apply(dollarsign)
purchasing_analysis_gender_df['Normalized Totals'] = purchasing_analysis_gender_df['Normalized Totals'].apply(dollarsign)
purchasing_analysis_gender_df['Total Purchase Value'] = purchasing_analysis_gender_df['Total Purchase Value'].apply(dollarsign)


#purchasing_analysis_gender_df
```


```python
purchasing_analysis_gender_df = purchasing_analysis_gender_df.set_index("Gender")
purchasing_analysis_gender_df
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
      <th># players(each group)</th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>60</td>
      <td>$2.88</td>
      <td>$3.08</td>
      <td>64</td>
      <td>$184.60</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>13</td>
      <td>$3.18</td>
      <td>$3.18</td>
      <td>13</td>
      <td>$41.38</td>
    </tr>
    <tr>
      <th>Other/Non-Disclosed</th>
      <td>1</td>
      <td>$2.12</td>
      <td>$2.12</td>
      <td>1</td>
      <td>$2.12</td>
    </tr>
  </tbody>
</table>
</div>




```python
#==================================================================================================================
```


```python
##################### This is the Starting section for " PURCHASING ANALYSIS (Age) " ############################## 
```


```python
#==================================================================================================================
```


```python
# First call my_data to examine it 
clean_df.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>




```python
#clean_df["SN"].count()
# This is the dataframe object which has all the sum of "Price" column grouped with the "Gender"
sum_Age_df = grouped_Gender_df[["Price"]].sum()
#sum_Age_df
```


```python
#Create bins and bin labels for the Age Column

age_bins = [0, 9, 14, 19, 24, 29, 34, 39, 100]
age_labels = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+" ]

#Bin the Age column
# cut() returns a Pandas Series containing each of the binned column's values translated into their corresponding bins

pd.cut(clean_df["Age"], age_bins, labels=age_labels)
```




    0     20-24
    1     20-24
    2     15-19
    3     15-19
    4     20-24
    5       <10
    6       40+
    7     25-29
    8     15-19
    9     35-39
    10    20-24
    11    35-39
    12    20-24
    13    30-34
    14      <10
    15    20-24
    16    20-24
    17      <10
    18    10-14
    19    20-24
    20    35-39
    21    10-14
    22    15-19
    23    20-24
    24    20-24
    25    15-19
    26      <10
    27    25-29
    28    20-24
    29    20-24
          ...  
    48    25-29
    49    20-24
    50    20-24
    51    25-29
    52    20-24
    53    15-19
    54    25-29
    55    20-24
    56    15-19
    57    20-24
    58    30-34
    59    35-39
    60    20-24
    61    20-24
    62    15-19
    63    10-14
    64    20-24
    65    20-24
    66    20-24
    67    20-24
    68    20-24
    69    30-34
    70    25-29
    71    25-29
    72    20-24
    73    35-39
    74    35-39
    75    15-19
    76    20-24
    77    20-24
    Name: Age, Length: 78, dtype: category
    Categories (8, object): [<10 < 10-14 < 15-19 < 20-24 < 25-29 < 30-34 < 35-39 < 40+]




```python
type(age_bins)
```




    list




```python
# We can append our new bins to clean_df

clean_df["Age_Category"] = pd.cut(clean_df["Age"], age_bins, labels=age_labels)
#clean_df.head()
```


```python
# Binning allowing for more vigorous analysis
# we can now group by our bins for mean/Average value

grouped_age_purchase_df = clean_df.groupby("Age_Category")

 
#avg_purchase_price = grouped_age_purchase_df["Price"].mean()
#grouped_age_purchase_df
```


```python
# Binning allowing for more vigorous analysis
# we can now group by our bins for sum value

grouped_age_purchase_df = clean_df.groupby("Age_Category")
 
#This is to create in variables to assign the values of sum later
tot_purchase_value = grouped_age_purchase_df["Price" ].sum() 
tot_purchase_value
```




    Age_Category
    <10       13.82
    10-14      8.96
    15-19     30.41
    20-24    108.89
    25-29     26.11
    30-34     13.89
    35-39     21.37
    40+        4.65
    Name: Price, dtype: float64




```python
# This gives us the count of all the bins in categorized
#grouped_age_purchase_df.count()
 
```


```python
purchase_count = grouped_age_purchase_df["Gender"].value_counts() # saving in variables
p1 = purchase_count.loc['<10'].sum()
p2 = purchase_count.loc['10-14'].sum()
p3 = purchase_count.loc['15-19'].sum()
p4 = purchase_count.loc['20-24'].sum()
p5 = purchase_count.loc['25-29'].sum()
p6 = purchase_count.loc['30-34'].sum()
p7 = purchase_count.loc['35-39'].sum()
p8 = purchase_count.loc['40+'].sum()

#purchase_count 
#purchase_count.loc['<10'].sum()

```


```python
# Normalized Totals for Age demographics
# Total Purchase Value/# of people each group
normalized1 = tot_purchase_value.iloc[0]/p1
normalized2 = tot_purchase_value.iloc[1]/p2
normalized3 = tot_purchase_value.iloc[2]/p3
normalized4 = tot_purchase_value.iloc[3]/p4
normalized5 = tot_purchase_value.iloc[4]/p5
normalized6 = tot_purchase_value.iloc[5]/p6
normalized7 = tot_purchase_value.iloc[6]/p7
normalized8 = tot_purchase_value.iloc[7]/p8
 
#normalized2
```


```python
# Average purchase price (Total Purchase value/purchase count) 
avg_purchase1 = tot_purchase_value.iloc[0]/purchase_count.iloc[0]
avg_purchase2 = tot_purchase_value.iloc[1]/purchase_count.iloc[1]
avg_purchase3 = tot_purchase_value.iloc[2]/purchase_count.iloc[2]
avg_purchase4 = tot_purchase_value.iloc[3]/purchase_count.iloc[3]
avg_purchase5 = tot_purchase_value.iloc[4]/purchase_count.iloc[4]
avg_purchase6 = tot_purchase_value.iloc[5]/purchase_count.iloc[5]
avg_purchase7 = tot_purchase_value.iloc[6]/purchase_count.iloc[6]
avg_purchase8 = tot_purchase_value.iloc[7]/purchase_count.iloc[7]

```


```python
# Creating a new dataframe for Purchasing Analysis (Age)
purchasing_analysis_Age_dic = {"Age": ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"],
                                  "Average Purchase Price": [avg_purchase1,
                                                             avg_purchase2,
                                                             avg_purchase3,
                                                             avg_purchase4,
                                                             avg_purchase5,
                                                             avg_purchase6,
                                                             avg_purchase7,
                                                             avg_purchase8],
                                  "Total Purchase Value": [tot_purchase_value.iloc[0],
                                                           tot_purchase_value.iloc[1],
                                                           tot_purchase_value.iloc[2],
                                                           tot_purchase_value.iloc[3],
                                                           tot_purchase_value.iloc[4],
                                                           tot_purchase_value.iloc[5],
                                                           tot_purchase_value.iloc[6],
                                                           tot_purchase_value.iloc[7]],
                                  "Normalized Totals": [normalized1,
                                                        normalized2,
                                                        normalized3,
                                                        normalized4,
                                                        normalized5,
                                                        normalized6,
                                                        normalized7,
                                                        normalized8],
                                  "Purchase Count": [purchase_count.iloc[0],
                                                     purchase_count.iloc[1],
                                                     purchase_count.iloc[2],
                                                     purchase_count.iloc[3],
                                                     purchase_count.iloc[4],
                                                     purchase_count.iloc[5],
                                                     purchase_count.iloc[6],
                                                     purchase_count.iloc[7]],
                                    "# people each group": [p1,
                                                               p2,
                                                               p3,
                                                               p4,
                                                               p5,
                                                               p6,
                                                               p7,
                                                               p8]}

purchasing_analysis_Age_df = pd.DataFrame(purchasing_analysis_Age_dic) # Set the row index to be "Age"

purchasing_analysis_Age_df['Average Purchase Price'] = purchasing_analysis_Age_df['Average Purchase Price'].apply(dollarsign)
purchasing_analysis_Age_df['Total Purchase Value'] = purchasing_analysis_Age_df['Total Purchase Value'].apply(dollarsign)
purchasing_analysis_Age_df['Normalized Totals'] = purchasing_analysis_Age_df['Normalized Totals'].apply(dollarsign)

purchasing_analysis_Age_df = purchasing_analysis_Age_df.set_index("Age")
purchasing_analysis_Age_df

purchasing_analysis_Age_df

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
      <th># people each group</th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>5</td>
      <td>$2.76</td>
      <td>$2.76</td>
      <td>5</td>
      <td>$13.82</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>3</td>
      <td>$8.96</td>
      <td>$2.99</td>
      <td>1</td>
      <td>$8.96</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>11</td>
      <td>$30.41</td>
      <td>$2.76</td>
      <td>1</td>
      <td>$30.41</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>36</td>
      <td>$108.89</td>
      <td>$3.02</td>
      <td>1</td>
      <td>$108.89</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>9</td>
      <td>$2.90</td>
      <td>$2.90</td>
      <td>9</td>
      <td>$26.11</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>7</td>
      <td>$6.94</td>
      <td>$1.98</td>
      <td>2</td>
      <td>$13.89</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>6</td>
      <td>$0.74</td>
      <td>$3.56</td>
      <td>29</td>
      <td>$21.37</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>1</td>
      <td>$0.66</td>
      <td>$4.65</td>
      <td>7</td>
      <td>$4.65</td>
    </tr>
  </tbody>
</table>
</div>




```python
#==================================================================================================================
```


```python
##################### This is the Starting section for " TOP SPENDERS " ############################## 
```


```python
#==================================================================================================================
```


```python
# First call my_data to examine it 
clean_df.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age_Category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
#create a new FILTERABLE object that has the count of each group (Male, Female, Other count) 

grouped_df = clean_df.groupby(["SN"])['Price'].sum()
#grouped_df

#Saving in a DataFrame format. Building the tables one by one
#grouped_SN = clean_df.groupby(["SN"]).agg({'Price': 'sum'})
top_spenders_df = pd.DataFrame(grouped_df)
#top_spenders_df.head()
 
```


```python
#Rename the column Price to "Total Purchase Value"
top_spenders_df.rename(columns={'Price': 'Total_Purchase_Value'}, inplace=True)
```


```python
# To get the count of the players for each category
grouped_count = clean_df.groupby(["SN"])['Age'].count()
#grouped_count
```


```python
# Pass in drop=True to prevent appending a new column with the old indexes to the dataframe
#top_spenders_df.reset_index(drop=True)
#top_spenders_df.head()

top_spenders_df['Purchase_Count'] = pd.DataFrame(clean_df.groupby(["SN"])['Age'].count())
top_spenders_df['Average_Purchase_Price'] = top_spenders_df['Total_Purchase_Value'].div(top_spenders_df['Purchase_Count'])

 
#top_spenders_df.head()
 


```


```python
# Sorting in the highest values of top 5 player purchases
sorted_df =top_spenders_df.sort_values("Total_Purchase_Value", ascending=False) 
#sorted_df = sorted_df.reset_index(drop=True)
#sorted_df.head()
```


```python
# After the sorting, then formating the sorted values, because the sort does not work with formats '$'
format_top_spenders_df = sorted_df
format_top_spenders_df['Average_Purchase_Price'] = format_top_spenders_df['Average_Purchase_Price'].apply(dollarsign)
format_top_spenders_df['Total_Purchase_Value'] = format_top_spenders_df['Total_Purchase_Value'].apply(dollarsign)
format_top_spenders_df.head()
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
      <th>Total_Purchase_Value</th>
      <th>Purchase_Count</th>
      <th>Average_Purchase_Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Sundaky74</th>
      <td>$7.41</td>
      <td>2</td>
      <td>$3.71</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <td>$5.13</td>
      <td>2</td>
      <td>$2.56</td>
    </tr>
    <tr>
      <th>Eusty71</th>
      <td>$4.81</td>
      <td>1</td>
      <td>$4.81</td>
    </tr>
    <tr>
      <th>Chanirra64</th>
      <td>$4.78</td>
      <td>1</td>
      <td>$4.78</td>
    </tr>
    <tr>
      <th>Alarap40</th>
      <td>$4.71</td>
      <td>1</td>
      <td>$4.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
#==================================================================================================================#
```


```python
##################### This is the Starting section for " MOST POPULAR ITEMS " ############################## 
```


```python
#==================================================================================================================#
```


```python
# First call my_data to examine it 
clean_df.head() 
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age_Category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Set Item ID as our index
clean_df_indexed_on_id = clean_df.set_index('Item Name')
clean_df_indexed_on_id.head()

 
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age_Category</th>
    </tr>
    <tr>
      <th>Item Name</th>
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
      <th>Apocalyptic Battlescythe</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>Dawne</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>Putrid Fan</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>Twilight's Carver</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>Feral Katana</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
#clean_df_indexed_on_id.index 
```


```python
# Grouped Dataframe by Item ID and Item Name and created new dataframe
grouped_ItemID_Name_df = clean_df.groupby(["Item ID", "Item Name"])

grouped_ItemID_Name_df.sum()

most_popular_df = pd.DataFrame(grouped_ItemID_Name_df.sum())
#most_popular_df.head() 
 
```


```python
# adding new column  to existing dataframe
most_popular_df['Purchase_Count'] = clean_df.groupby(["Item ID", "Item Name"])["Item Name"].count()
#most_popular_df.head()
 
```


```python
#  Rename column 'Item Price'of Price dataframe 
most_popular_df = most_popular_df.rename(columns={'Price': 'Item_Price' })
#most_popular_df.head()
```


```python
# Total Purchase Value calculations
most_popular_df['Total_Purchase_Value'] = most_popular_df['Purchase_Count'].mul(most_popular_df['Item_Price'])

most_popular_df['Item_Price'] = most_popular_df['Item_Price'].apply(dollarsign)
most_popular_df['Total_Purchase_Value'] = most_popular_df['Total_Purchase_Value'].apply(dollarsign)
 
#most_popular_df.head()
```


```python
# Drop the Age column to create new dataframe of Most popular Items

 
#new_size_df = Heroes_popular_df.sum()
most_popular_df.drop('Age', axis = 1, inplace=True )
 
  
```


```python
# Sorting in the highest values of top 5  purchase count
sorted_most_popular_df = most_popular_df.sort_values("Purchase_Count", ascending=False) 
sorted_most_popular_df.head()
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
      <th></th>
      <th>Item_Price</th>
      <th>Purchase_Count</th>
      <th>Total_Purchase_Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <th>Mourning Blade</th>
      <td>$10.92</td>
      <td>3</td>
      <td>$32.76</td>
    </tr>
    <tr>
      <th>90</th>
      <th>Betrayer</th>
      <td>$8.24</td>
      <td>2</td>
      <td>$16.48</td>
    </tr>
    <tr>
      <th>111</th>
      <th>Misery's End</th>
      <td>$3.58</td>
      <td>2</td>
      <td>$7.16</td>
    </tr>
    <tr>
      <th>64</th>
      <th>Fusion Pummel</th>
      <td>$4.84</td>
      <td>2</td>
      <td>$9.68</td>
    </tr>
    <tr>
      <th>154</th>
      <th>Feral Katana</th>
      <td>$8.22</td>
      <td>2</td>
      <td>$16.44</td>
    </tr>
  </tbody>
</table>
</div>




```python
#==================================================================================================================#
```


```python
##################### This is the Starting section for " MOST PROFITABLE(Purchase Value) ITEMS " ############################## 
```


```python
#==================================================================================================================#
```


```python
# First call my_data to examine it 
print(len(clean_df))
clean_df.head()

# Grouped Dataframe by Item ID and Item Name and created new dataframe
grouped_ItemID_Name_df = clean_df.groupby(["Item ID", "Item Name"])

grouped_ItemID_Name_df.sum()

most_profitable_df = pd.DataFrame(grouped_ItemID_Name_df.sum())
#most_profitable_df.head() 

# adding new column  to existing dataframe
most_profitable_df['Purchase_Count'] = clean_df.groupby(["Item ID", "Item Name"])["Item Name"].count()
 

#  Rename column 'Item Price'of Price dataframe 
most_profitable_df = most_profitable_df.rename(columns={'Price': 'Item_Price' })
 
# Total Purchase Value calculations
most_profitable_df['Total_Purchase_Value'] = most_profitable_df['Purchase_Count'].mul(most_profitable_df['Item_Price'])

#new_size_df = Heroes_popular_df.sum()
most_profitable_df.drop('Age', axis = 1, inplace=True )
 
```

    78



```python
# Sorting in the highest values of top 5 Most Profitable Items without a dollarsign '$'
sorted_top_profitable_df = most_profitable_df.sort_values("Total_Purchase_Value", ascending=False) 
#sorted_top_profitable_df.head() 
 
```


```python
#  After sorting, I am formating with dollar sign. Because my sort does not work with %, $...
format_sorted_top_profitable_df = sorted_top_profitable_df
format_sorted_top_profitable_df['Item_Price'] = format_sorted_top_profitable_df['Item_Price'].apply(dollarsign)
format_sorted_top_profitable_df['Total_Purchase_Value'] = format_sorted_top_profitable_df['Total_Purchase_Value'].apply(dollarsign)
```


```python
format_sorted_top_profitable_df.head()
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
      <th></th>
      <th>Item_Price</th>
      <th>Purchase_Count</th>
      <th>Total_Purchase_Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <th>Mourning Blade</th>
      <td>$10.92</td>
      <td>3</td>
      <td>$32.76</td>
    </tr>
    <tr>
      <th>117</th>
      <th>Heartstriker, Legacy of the Light</th>
      <td>$9.42</td>
      <td>2</td>
      <td>$18.84</td>
    </tr>
    <tr>
      <th>93</th>
      <th>Apocalyptic Battlescythe</th>
      <td>$8.98</td>
      <td>2</td>
      <td>$17.96</td>
    </tr>
    <tr>
      <th>90</th>
      <th>Betrayer</th>
      <td>$8.24</td>
      <td>2</td>
      <td>$16.48</td>
    </tr>
    <tr>
      <th>154</th>
      <th>Feral Katana</th>
      <td>$8.22</td>
      <td>2</td>
      <td>$16.44</td>
    </tr>
  </tbody>
</table>
</div>


