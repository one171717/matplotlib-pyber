
Pyber Ride Sharing Analysis:

   -Though the average fare is far greater in rural areas, urban areas take home a much larger portion of total fares(income), indicating that volume of rides is more important than fare pricing. Or it could indicate that needing to travel longer distances, which therefore results in larger fares, does not nearly make up for more ride volume in more urban areas, where the fare would be cheaper. 
   -Services like Pyber definitely see more business in urban areas, as seen by urban areas controlling more than 50% of the total in all areas.
   -All of the data supports the idea that a larger population denotes a greater need for a service like Pyber. Urban areas tend to have a larger population than suburban ones, then rural, and each chart reflects that. 
   -Rural areas support the smallest portion of this business, meaning fewer people are able to become drivers. This could be because of fewer people needing rides in rural areas, but it also indicates that rural areas are much less forgiving for people who need to travel this way. 
   


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```


```python
#import csv files
city_path = "raw_data/city_data.csv"
ride_path = "raw_data/ride_data.csv"
city_df = pd.read_csv(city_path)
ride_df = pd.read_csv(ride_path)

```


```python
#Take a look at the data
ride_df.head()
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-14 10:14:22</td>
      <td>13.83</td>
      <td>5739410935873</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Michelleport</td>
      <td>2018-03-04 18:24:09</td>
      <td>30.24</td>
      <td>2343912425577</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Samanthamouth</td>
      <td>2018-02-24 04:29:00</td>
      <td>33.44</td>
      <td>2005065760003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rodneyfort</td>
      <td>2018-02-10 23:22:03</td>
      <td>23.44</td>
      <td>5149245426178</td>
    </tr>
    <tr>
      <th>4</th>
      <td>South Jack</td>
      <td>2018-03-06 04:28:35</td>
      <td>34.58</td>
      <td>3908451377344</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Take a look at the data
city_df.head()
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
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Williamsstad</td>
      <td>59</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Angela</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rodneyfort</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>West Robert</td>
      <td>39</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Merge the two data sets on 'city'
merged_city_df = pd.merge(city_df,ride_df, on="city")
merged_city_df.head()
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
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-24 08:40:38</td>
      <td>13.93</td>
      <td>5628545007794</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-13 12:46:07</td>
      <td>14.00</td>
      <td>910050116494</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-16 13:52:19</td>
      <td>17.92</td>
      <td>820639054416</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-02-01 20:18:28</td>
      <td>10.26</td>
      <td>9554935945413</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
      <td>2018-04-17 02:26:37</td>
      <td>23.00</td>
      <td>720020655850</td>
    </tr>
  </tbody>
</table>
</div>




```python
#organize data into variables for graphing
city_org = merged_city_df.groupby("city")
avg_fare = city_org.mean()["fare"]
total_rides = city_org["ride_id"].count()
drivers = city_org.mean()["driver_count"]
type_of_city = city_df.set_index("city")["type"]
# Check that all variable work
# city_org
# avg_fare
# total_rides
# drivers
# type_of_city
```


```python
#Create a new dataframe with new variables
org_city_info = pd.DataFrame({
    "Average Fare": avg_fare,
    "Total Rides": total_rides,
    "Number of Drivers": drivers,
    "City Type": type_of_city
})
org_city_info.head()
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
      <th>Average Fare</th>
      <th>City Type</th>
      <th>Number of Drivers</th>
      <th>Total Rides</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Amandaburgh</th>
      <td>24.641667</td>
      <td>Urban</td>
      <td>12.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Barajasview</th>
      <td>25.332273</td>
      <td>Urban</td>
      <td>26.0</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Barronchester</th>
      <td>36.422500</td>
      <td>Suburban</td>
      <td>11.0</td>
      <td>16</td>
    </tr>
    <tr>
      <th>Bethanyland</th>
      <td>32.956111</td>
      <td>Suburban</td>
      <td>22.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Bradshawfurt</th>
      <td>40.064000</td>
      <td>Rural</td>
      <td>7.0</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Create city type variables
rural = org_city_info.loc[org_city_info["City Type"]== "Rural"]
urban = org_city_info.loc[org_city_info["City Type"]== "Urban"]
suburban = org_city_info.loc[org_city_info["City Type"]== "Suburban"]
# #Check to make sure variable work
# rural.head()
# urban.head()
# suburban.head()
```


```python
#create the scatter plots
plt.scatter(rural["Total Rides"],rural["Average Fare"], s = rural["Number of Drivers"]*10, color="gold", edgecolors="black", lw = 0.75, alpha = 0.75, label="Rural")
plt.scatter(urban["Total Rides"],urban["Average Fare"], s = urban["Number of Drivers"]*10, color="lightcoral",edgecolors="black", lw = 0.75, alpha = 0.75, label="Urban")
plt.scatter(suburban["Total Rides"],suburban["Average Fare"], s = suburban["Number of Drivers"]*10, color="lightskyblue",edgecolors="black", lw = 0.75, alpha = 0.75, label="Suburban")

#Create aesthetics
plt.suptitle("Pyber Ride Sharing Information")
plt.title("Note: Circle size corresponds to number of drivers")
plt.xlabel("Total Number of Rides by City")
plt.ylabel("Average Fare by City")
plt.legend(loc="best")
plt.grid(lw = 0.5)
plt.show()

```


![png](output_9_0.png)



```python
#Create groupby for first pie chart
fare_pie = merged_city_df.groupby(["type"])["fare"].sum()
fare_pie
```




    type
    Rural        4327.93
    Suburban    19356.33
    Urban       39854.38
    Name: fare, dtype: float64




```python
fare_pie.index
```




    Index(['Rural', 'Suburban', 'Urban'], dtype='object', name='type')




```python
#Create the pie chart
explode = [0,0,0.1]
colors = ["gold", "lightskyblue", "lightcoral"]
plt.pie(fare_pie, labels = fare_pie.index, explode = explode, colors = colors, autopct="%1.1f%%", startangle = 110, shadow = True)
plt.axis("equal")
plt.title("Percent of Total Fares by City Type")
plt.show()
```


![png](output_12_0.png)



```python
#Create groupby for second pie chart
ride_pie = merged_city_df.groupby(["type"])["ride_id"].count()
ride_pie
```




    type
    Rural        125
    Suburban     625
    Urban       1625
    Name: ride_id, dtype: int64




```python
ride_pie.index
```




    Index(['Rural', 'Suburban', 'Urban'], dtype='object', name='type')




```python
#Create the pie chart
explode = [0,0,0.1]
colors = ["gold", "lightskyblue", "lightcoral"]
plt.pie(ride_pie, labels = ride_pie.index, explode = explode, colors = colors, autopct="%1.1f%%", startangle = 140, shadow = True)
plt.axis("equal")
plt.title("Percent of Total Rides by City")
plt.show()
```


![png](output_15_0.png)



```python
#Save the image
plt.savefig("Images/pyber_pie_rides.png")
```


    <matplotlib.figure.Figure at 0x11d65f588>



```python
#Create groupby for third pie chart
rider_pie = merged_city_df.groupby(["type"])["driver_count"].sum()
rider_pie
```




    type
    Rural         537
    Suburban     8570
    Urban       59602
    Name: driver_count, dtype: int64




```python
rider_pie.index
```




    Index(['Rural', 'Suburban', 'Urban'], dtype='object', name='type')




```python
#Create third pie chart
explode = [0,0,0.2]
colors = ["gold", "lightskyblue", "lightcoral"]
plt.pie(rider_pie, labels = rider_pie.index, explode = explode, colors = colors, autopct="%1.1f%%", startangle = 140, shadow = True)
plt.axis("equal")
plt.title("Percent of Total Drivers by City Type")
plt.show()
```


![png](output_19_0.png)

