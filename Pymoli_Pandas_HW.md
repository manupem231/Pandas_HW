

```python
import pandas as pd # importing pandas, numpy, os and json dependencies
import numpy as np
import os
import json

file_path = os.path.join('purchase_data.json') # Defining file path
#file_path = os.path.join('purchase_data2.json')
pymoli_df = pd.read_json(file_path, orient = 'records') # Reading json file
pymoli_df.head()
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
Total_Players_df = len(pymoli_df['SN'].value_counts()) # Counting the number of players (SN: Each player with 'Screen Name')
print("Total Number of Players: ", Total_Players_df) # Printing total number of players
```

    Total Number of Players:  573



```python
# *** Purchasing Analysis (Total) ***
```


```python
Unique_items_df = len(pymoli_df['Item Name'].value_counts()) # Here value_counts() calculate the unique value, count 
print("Number of Unique Items: ",Unique_items_df)
```

    Number of Unique Items:  179



```python
Avg_Purchase_Price = pymoli_df['Price'].mean() # Here mean() calculates the average of 'Price' column
print("Average Purchase Price: ", Avg_Purchase_Price)
```

    Average Purchase Price:  2.931192307692303



```python
Total_purchases = pymoli_df['Price'].count() # Here count() calculates the number of pruchases
print("Total Number of Purchases: ", Total_purchases)
```

    Total Number of Purchases:  780



```python
Total_revenue = pymoli_df['Price'].sum() # Here sum() calculates the sum of 'Price' column
print("Total Revenue: $",Total_revenue)
```

    Total Revenue: $ 2286.3299999999963



```python
# *** Gender Demographics ***
```


```python
Count_players = pymoli_df['Gender'].value_counts() # Unique value counts of each gender type
Count_male_players = Count_players[0] # Gives count of Male players
Per_male_players = Count_male_players/pymoli_df['Gender'].count()*100 # Percentage of Male players
print("Percentage and Count of Male players:", Per_male_players,"and", Count_male_players) # Printing the respective output
```

    Percentage and Count of Male players: 81.1538461538 and 633



```python
Count_female_players = Count_players[1] # Gives count of Female players
Per_female_players = Count_female_players/pymoli_df['Gender'].count()*100 # Percentage of Female players
print("Percentage and Count of Female players:", Per_female_players,"and", Count_female_players) # Printing the respective outpu
```

    Percentage and Count of Female players: 17.4358974359 and 136



```python
Count_other_players = Count_players[2] # Gives count of Other/Non-disclosed players
Per_other_players = Count_other_players/pymoli_df['Gender'].count()*100 # Percentage of Other/Non-disclosed players
print("Percentage and Count of Other/Non-disclosed players:", Per_other_players,"and", Count_other_players) # Printing the respective outpu
```

    Percentage and Count of Other/Non-disclosed players: 1.41025641026 and 11



```python
# *** Purchasing Analysis (Gender) ***
```


```python
Purchase_count_groupby = pymoli_df.groupby('Gender')
Purchase_count = Purchase_count_groupby['Price'].count()
ScreenName_count = Purchase_count_groupby['SN'].count()
Avg_purchase_price = Purchase_count_groupby['Price'].mean()
Total_purchase_value = Purchase_count_groupby['Price'].sum()
Normalized_total = Total_purchase_value/ScreenName_count

# Reding 'Data Series' as 'DataFrame'
Purchase_count_df = pd.DataFrame(Purchase_count)
Avg_purchase_Price_df = pd.DataFrame(Avg_purchase_price)
Total_purchase_value_df = pd.DataFrame(Total_purchase_value)
Normalized_total = pd.DataFrame(Normalized_total)

Purchase_count_df # Purchase Count
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
      <th>Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
Avg_purchase_Price_df  # Average Purchase Price
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
      <th>Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>2.815515</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2.950521</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>3.249091</td>
    </tr>
  </tbody>
</table>
</div>




```python
Total_purchase_value_df # Total Purchase Value
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
      <th>Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
Normalized_total # Normalized Totals
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
      <th>0</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>2.815515</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2.950521</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>3.249091</td>
    </tr>
  </tbody>
</table>
</div>




```python
# *** Age Demographics ***
```


```python
pymoli_df.head()
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
age_bins = [0, 9, 14, 19, 24, 29, 34, 39, 44] # Create bins in which to place values based upon 'Age'
group_labels_age = ["<10", "10 to 14", "15 to 19", "20 to 24",
                    "25 to 29", "30 to 34", "35 to 39", ">40"] # Create labels for these bins
Age_Demographics = pd.cut(pymoli_df['Age'], bins, labels=group_labels_age) # Slice the data and place it into bins
pymoli_df['Age_Demography'] = pd.cut(pymoli_df['Age'], bins, labels=group_labels_age) # Creating a new column to place bin values
pymoli_df.head()
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
      <th>Age_Demography</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>35 to 39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20 to 24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>30 to 34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20 to 24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20 to 24</td>
    </tr>
  </tbody>
</table>
</div>




```python
Purchase_count_groupby_Age = pymoli_df.groupby('Age_Demography') # Groupby based on 'Age'
```


```python
Purchase_count_Age = Purchase_count_groupby_Age['Price'].count() # Calculating 'Purchase Count' based on count()
ScreenName_count_Age = Purchase_count_groupby_Age['SN'].count() # Calculating 'Screen Name Count' based on count()
Avg_purchase_price_Age = Purchase_count_groupby_Age['Price'].mean() # Calculating 'Avg Purchase Price' based on mean()
Total_purchase_value_Age = Purchase_count_groupby_Age['Price'].sum() # Calculating 'Total Purchase Count' based on sum()
Normalized_total_Age = Total_purchase_value_Age/ScreenName_count_Age
```


```python
Purchase_count_Age_df = pd.DataFrame(Purchase_count_Age) # Reading 'Data Series' as a DataFrame
Purchase_count_Age_df.rename(columns = {'Price': 'Purchase count'}, inplace=True) # Renaming column name
Purchase_count_Age_df.head()
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
      <th>Purchase count</th>
    </tr>
    <tr>
      <th>Age_Demography</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>28</td>
    </tr>
    <tr>
      <th>10 to 14</th>
      <td>35</td>
    </tr>
    <tr>
      <th>15 to 19</th>
      <td>133</td>
    </tr>
    <tr>
      <th>20 to 24</th>
      <td>336</td>
    </tr>
    <tr>
      <th>25 to 29</th>
      <td>125</td>
    </tr>
  </tbody>
</table>
</div>




```python
Total_purchase_value_Age_df = pd.DataFrame(Total_purchase_value_Age) # Reading 'Data Series' as a DataFrame
Total_purchase_value_Age_df.rename(columns = {'Price': "Total Purchase Val"}, inplace=True) # Renaming column name
Total_purchase_value_Age_df.head()
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
      <th>Total Purchase Val</th>
    </tr>
    <tr>
      <th>Age_Demography</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>83.46</td>
    </tr>
    <tr>
      <th>10 to 14</th>
      <td>96.95</td>
    </tr>
    <tr>
      <th>15 to 19</th>
      <td>386.42</td>
    </tr>
    <tr>
      <th>20 to 24</th>
      <td>978.77</td>
    </tr>
    <tr>
      <th>25 to 29</th>
      <td>370.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge_df_Age1 = pd.merge(Purchase_count_Age_df, Total_purchase_value_Age_df, left_index=True, right_index=True) # Merging two DataFrames
merge_df_Age1.head()
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
      <th>Purchase count</th>
      <th>Total Purchase Val</th>
    </tr>
    <tr>
      <th>Age_Demography</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>28</td>
      <td>83.46</td>
    </tr>
    <tr>
      <th>10 to 14</th>
      <td>35</td>
      <td>96.95</td>
    </tr>
    <tr>
      <th>15 to 19</th>
      <td>133</td>
      <td>386.42</td>
    </tr>
    <tr>
      <th>20 to 24</th>
      <td>336</td>
      <td>978.77</td>
    </tr>
    <tr>
      <th>25 to 29</th>
      <td>125</td>
      <td>370.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
Avg_purchase_price_Age_df = pd.DataFrame(Avg_purchase_price_Age) # Reading 'Data Series' as DataFrame
Avg_purchase_price_Age_df.rename(columns = {'Price': 'Avg Purchase Price'}, inplace=True) # Renaming column name
Avg_purchase_price_Age_df.head()
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
      <th>Avg Purchase Price</th>
    </tr>
    <tr>
      <th>Age_Demography</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>2.980714</td>
    </tr>
    <tr>
      <th>10 to 14</th>
      <td>2.770000</td>
    </tr>
    <tr>
      <th>15 to 19</th>
      <td>2.905414</td>
    </tr>
    <tr>
      <th>20 to 24</th>
      <td>2.913006</td>
    </tr>
    <tr>
      <th>25 to 29</th>
      <td>2.962640</td>
    </tr>
  </tbody>
</table>
</div>




```python
Age_Demography_df = pd.merge(merge_df_Age1, Avg_purchase_price_Age_df, left_index=True, right_index=True) # Merging two DataFrames
Age_Demography_df.head()
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
      <th>Purchase count</th>
      <th>Total Purchase Val</th>
      <th>Avg Purchase Price</th>
    </tr>
    <tr>
      <th>Age_Demography</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>28</td>
      <td>83.46</td>
      <td>2.980714</td>
    </tr>
    <tr>
      <th>10 to 14</th>
      <td>35</td>
      <td>96.95</td>
      <td>2.770000</td>
    </tr>
    <tr>
      <th>15 to 19</th>
      <td>133</td>
      <td>386.42</td>
      <td>2.905414</td>
    </tr>
    <tr>
      <th>20 to 24</th>
      <td>336</td>
      <td>978.77</td>
      <td>2.913006</td>
    </tr>
    <tr>
      <th>25 to 29</th>
      <td>125</td>
      <td>370.33</td>
      <td>2.962640</td>
    </tr>
  </tbody>
</table>
</div>




```python
# *** Top Spenders ***
```


```python
Groupby_SN = pymoli_df.groupby('SN') # Groupby using 'SN'
```


```python
Groupby_SN_Total_Purchase_Val = Groupby_SN['Price'].sum() # Calculating total purchase value by using sum()
Total_Pur_df = pd.DataFrame(Groupby_SN_Total_Purchase_Val) # Converting Data series into DataFrame
Total_Pur_df.rename(columns = {'Price': 'Total Purchase Val'}, inplace=True) # Renaming Column Name
Total_Pur_df.head() # Printing top 5 rows of the DataFrame
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
      <th>Total Purchase Val</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>6.70</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>5.80</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
Groupby_SN_Purchase_Count = Groupby_SN['Price'].count() # Calculating Purchase count using count()
Pur_count_df = pd.DataFrame(Groupby_SN_Purchase_Count) # Converting Data series into DataFrame
Pur_count_df.rename(columns = {'Price': 'Purchase Count'}, inplace=True) # Renaming Column Name
Pur_count_df.head() # Printing top 5 rows of the DataFrame
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
      <th>Purchase Count</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
Groupby_SN_Avg_Pur_Price = Groupby_SN['Price'].mean() # Calculating Avg purchase price using mean()
Avg_Price_df = pd.DataFrame(Groupby_SN_Avg_Pur_Price) # Converting Data series into DataFrame
Avg_Price_df.rename(columns = {'Price': 'Avg Purchase Price'}, inplace=True) # Renaming Column Name
Avg_Price_df.head() # Printing top 5 rows of the DataFrame
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
      <th>Avg Purchase Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.270000</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge_df = pd.merge(Pur_count_df, Avg_Price_df, left_index=True, right_index=True) #Merging two (Pur_count_df & Avg_Price_df) data frames
```


```python
top_spenders_df = pd.merge(Total_Pur_df, merge_df, left_index=True, right_index=True) #Merging 3rd DataFrame with the above merged DataFrame
top_spenders_df.sort_values(by = ['Total Purchase Val'], ascending=False).head() #Sorting (descending) DataFrame values by 'Total Purchase Val' and listing top 5 rows. 
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
      <th>Total Purchase Val</th>
      <th>Purchase Count</th>
      <th>Avg Purchase Price</th>
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
      <th>Undirrala66</th>
      <td>17.06</td>
      <td>5</td>
      <td>3.412000</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>13.56</td>
      <td>4</td>
      <td>3.390000</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>12.74</td>
      <td>4</td>
      <td>3.185000</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>12.73</td>
      <td>3</td>
      <td>4.243333</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>11.58</td>
      <td>3</td>
      <td>3.860000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# *** Most Popular Items ***
```


```python
pymoli_df_unique_Item_ID = pymoli_df.drop_duplicates('Item ID') # Removing Duplicates of 'Item ID'
pymoli_df_sort_unique_Item_ID = pymoli_df_unique_Item_ID.sort_values(by = ['Item ID'], ascending=True) # Sorting in the order of 'ascending' for 'Item ID' 
final_iloc = pymoli_df_sort_unique_Item_ID.iloc[0:] # To get the list of all records using 'iloc'
Item_ID_Name_df = final_iloc.set_index('Item ID') # Setting the index of 'Item ID'
Item_ID_on_Index_df = pd.DataFrame(Item_ID_Name_df['Item Name']) # Reading 'Data Series' as 'Data Frame'
Item_ID_on_Index_df.head() # Listing top 5 records in the DataFrame
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
      <th>Item Name</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Splinter</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Crucifer</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Verdict</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Phantomlight</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bloodlord's Fetish</td>
    </tr>
  </tbody>
</table>
</div>




```python
Item_ID_Name_Series = pymoli_df.groupby('Item ID') # Performing 'groupby' using 'Item ID'
Item_ID_Name_Series_Purchase_count = Item_ID_Name_Series['Price'].count() # Calculating 'Purchase Count' using count()
Item_ID_Name_Purchase_count_df = pd.DataFrame(Item_ID_Name_Series_Purchase_count) # Reading 'Data Series' as 'Data Frame'
Item_ID_Name_Purchase_count_df.rename(columns = {'Price': 'Purchase Count'}, inplace=True) # Renaming the column name
Item_ID_Name_Purchase_count_df.head() # Listing top 5 records in the DataFrame
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
      <th>Purchase Count</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge_df_1 = pd.merge(Item_ID_on_Index_df, Item_ID_Name_Purchase_count_df, left_index=True, right_index=True) # Merging two DataFrames
merge_df_1.head()
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
      <th>Item Name</th>
      <th>Purchase Count</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Splinter</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Crucifer</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Verdict</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Phantomlight</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bloodlord's Fetish</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
Item_ID_Name_Total_purchase_val = Item_ID_Name_Series['Price'].sum() # Calculating 'Total Purchase Value' using sum()
Item_ID_Name_Total_Purchase_Val_df = pd.DataFrame(Item_ID_Name_Total_purchase_val) # Reading 'Data Series' as 'Data Frame'
Item_ID_Name_Total_Purchase_Val_df.rename(columns = {'Price': 'Total Purchase Val'}, inplace=True) # Renaming column name
Item_ID_Name_Total_Purchase_Val_df.head()
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
      <th>Total Purchase Val</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
Item_ID_Name_Avg_Purchase_Val = Item_ID_Name_Series['Price'].mean() # Calculating 'Average Purchase Val' using mean()
Item_ID_Name_Avg_Purchase_Val_df = pd.DataFrame(Item_ID_Name_Avg_Purchase_Val) # Reading 'Dara Series' as 'Data Frame'
Item_ID_Name_Avg_Purchase_Val_df.rename(columns = {'Price': 'Avg Purchase Val'}, inplace=True) # Renaming colum name
Item_ID_Name_Avg_Purchase_Val_df.head()
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
      <th>Avg Purchase Val</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge_df_2 = pd.merge(Item_ID_Name_Total_Purchase_Val_df, Item_ID_Name_Avg_Purchase_Val_df, left_index=True, right_index=True) # Merging two different DataFrames
merge_df_2.head()
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
      <th>Total Purchase Val</th>
      <th>Avg Purchase Val</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.82</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.12</td>
      <td>2.28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.40</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.79</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.28</td>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
Most_popular_items_df = pd.merge(merge_df_1, merge_df_2, left_index=True, right_index=True) # Final merging of all DataFrames
Most_popular_items_df.sort_values(by = ['Purchase Count'], ascending=False).head() # Sorting 'Purchase Count' values in descending order inorder to list most popular items 
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
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Total Purchase Val</th>
      <th>Avg Purchase Val</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>11</td>
      <td>25.85</td>
      <td>2.35</td>
    </tr>
    <tr>
      <th>84</th>
      <td>Arcane Gem</td>
      <td>11</td>
      <td>24.53</td>
      <td>2.23</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Trickster</td>
      <td>9</td>
      <td>18.63</td>
      <td>2.07</td>
    </tr>
    <tr>
      <th>175</th>
      <td>Woeful Adamantite Claymore</td>
      <td>9</td>
      <td>11.16</td>
      <td>1.24</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Serenity</td>
      <td>9</td>
      <td>13.41</td>
      <td>1.49</td>
    </tr>
  </tbody>
</table>
</div>




```python
Item_ID_on_Index_df.loc[84] # Cross checking 'Item Name' corresponds to 'Item ID' using 'loc'
```




    Item Name    Arcane Gem
    Name: 84, dtype: object




```python
# *** Most Profitable Items ***
```


```python
Most_profitable_items_df = pd.merge(merge_df_1, merge_df_2, left_index=True, right_index=True) # Final merging of all DataFrames
Most_profitable_items_df.sort_values(by = ['Total Purchase Val'], ascending=False).head() # Sorting 'Total Purchase Val' in descending order inorder to list most profitable items 
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
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Total Purchase Val</th>
      <th>Avg Purchase Val</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>Retribution Axe</td>
      <td>9</td>
      <td>37.26</td>
      <td>4.14</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Spectral Diamond Doomblade</td>
      <td>7</td>
      <td>29.75</td>
      <td>4.25</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Orenmir</td>
      <td>6</td>
      <td>29.70</td>
      <td>4.95</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Singed Scalpel</td>
      <td>6</td>
      <td>29.22</td>
      <td>4.87</td>
    </tr>
    <tr>
      <th>107</th>
      <td>Splitter, Foe Of Subtlety</td>
      <td>8</td>
      <td>28.88</td>
      <td>3.61</td>
    </tr>
  </tbody>
</table>
</div>


