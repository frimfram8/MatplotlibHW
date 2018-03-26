

```python
#Pyber
```


```python
# Dependencies and Setup
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
```


```python
# Import our data into pandas from CSV
city = 'raw_data/city_data.csv'
city_data_df = pd.read_csv(city)

city_data_df.head(10)


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
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>5</th>
      <td>South Josephville</td>
      <td>4</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>6</th>
      <td>West Sydneyhaven</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Travisville</td>
      <td>37</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Torresshire</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Lisaville</td>
      <td>66</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
#there is a duplicate city, so we need to do a groupby on city, and then .sum the driver count and .first the type
city_data_clean = pd.DataFrame({'type': city_data_df.groupby('city').first()['type'],
                                'driver_count': city_data_df.groupby('city').sum()['driver_count']}).reset_index()
city_data_clean.head(10)

#set index to city to we can merbge later
#city_data_clean = city_data_clean.set_index("city")
#city_data_clean
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
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>16</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>49</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Arnoldview</td>
      <td>41</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Campbellport</td>
      <td>26</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Carrollbury</td>
      <td>4</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Carrollfort</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Clarkstad</td>
      <td>21</td>
      <td>Suburban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Import our data into pandas from CSV
ride = 'raw_data/ride_data.csv'
ride_data_df = pd.read_csv(ride)

ride_data_df.head(10)
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
    <tr>
      <th>5</th>
      <td>New Jeffrey</td>
      <td>2016-02-22 18:36:25</td>
      <td>36.01</td>
      <td>9757888452346</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Port Johnstad</td>
      <td>2016-06-07 02:39:58</td>
      <td>17.15</td>
      <td>4352278259335</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Jacobfort</td>
      <td>2016-09-20 20:58:37</td>
      <td>22.98</td>
      <td>1500221409082</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Travisville</td>
      <td>2016-01-15 17:32:02</td>
      <td>27.39</td>
      <td>850152768361</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Sandymouth</td>
      <td>2016-11-16 07:27:00</td>
      <td>21.61</td>
      <td>2389035050524</td>
    </tr>
  </tbody>
</table>
</div>




```python
#in the ride_data_df, find avg fare per city, and total no of rides per city
#create groupby by city
group_by_city = ride_data_df.groupby("city")
avg_fares_per_city = group_by_city.mean()["fare"]
avg_fares_per_city.head(10)

```




    city
    Alvarezhaven    23.928710
    Alyssaberg      20.609615
    Anitamouth      37.315556
    Antoniomouth    23.625000
    Aprilchester    21.981579
    Arnoldview      25.106452
    Campbellport    33.711333
    Carrollbury     36.606000
    Carrollfort     25.395517
    Clarkstad       31.051667
    Name: fare, dtype: float64




```python
total_rides_per_city = group_by_city.count()["ride_id"]
total_rides_per_city.head(10)
```




    city
    Alvarezhaven    31
    Alyssaberg      26
    Anitamouth       9
    Antoniomouth    22
    Aprilchester    19
    Arnoldview      31
    Campbellport    15
    Carrollbury     10
    Carrollfort     29
    Clarkstad       12
    Name: ride_id, dtype: int64




```python
#use city groupby to sum total rides per city
group_by_city = ride_data_df.groupby("city")
total_fares_per_city = group_by_city.sum()["fare"]
total_fares_per_city.head(10)
```




    city
    Alvarezhaven    741.79
    Alyssaberg      535.85
    Anitamouth      335.84
    Antoniomouth    519.75
    Aprilchester    417.65
    Arnoldview      778.30
    Campbellport    505.67
    Carrollbury     366.06
    Carrollfort     736.47
    Clarkstad       372.62
    Name: fare, dtype: float64




```python
rides_summary = pd.DataFrame({"avg fare per city":avg_fares_per_city,"total fares per city":total_fares_per_city,
                              "total rides per city":total_rides_per_city})
rides_summary.head()

rides_summary.reset_index(inplace=True)
rides_summary.head(10)
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
      <th>city</th>
      <th>avg fare per city</th>
      <th>total fares per city</th>
      <th>total rides per city</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>23.928710</td>
      <td>741.79</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>20.609615</td>
      <td>535.85</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>37.315556</td>
      <td>335.84</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>23.625000</td>
      <td>519.75</td>
      <td>22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>21.981579</td>
      <td>417.65</td>
      <td>19</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Arnoldview</td>
      <td>25.106452</td>
      <td>778.30</td>
      <td>31</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Campbellport</td>
      <td>33.711333</td>
      <td>505.67</td>
      <td>15</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Carrollbury</td>
      <td>36.606000</td>
      <td>366.06</td>
      <td>10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Carrollfort</td>
      <td>25.395517</td>
      <td>736.47</td>
      <td>29</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Clarkstad</td>
      <td>31.051667</td>
      <td>372.62</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
#looking for var:
#Average Fare ($) Per City 
#Total Number of Rides Per City
#Total Number of Drivers Per City
#City Type (Urban, Suburban, Rural)
```


```python
#merge cleaned city df with rides_summary df
merge_table = pd.merge(city_data_clean, rides_summary, on="city", how="outer")
merge_table.head(10)
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
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>avg fare per city</th>
      <th>total fares per city</th>
      <th>total rides per city</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>21</td>
      <td>Urban</td>
      <td>23.928710</td>
      <td>741.79</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>67</td>
      <td>Urban</td>
      <td>20.609615</td>
      <td>535.85</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>16</td>
      <td>Suburban</td>
      <td>37.315556</td>
      <td>335.84</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>21</td>
      <td>Urban</td>
      <td>23.625000</td>
      <td>519.75</td>
      <td>22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>49</td>
      <td>Urban</td>
      <td>21.981579</td>
      <td>417.65</td>
      <td>19</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Arnoldview</td>
      <td>41</td>
      <td>Urban</td>
      <td>25.106452</td>
      <td>778.30</td>
      <td>31</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Campbellport</td>
      <td>26</td>
      <td>Suburban</td>
      <td>33.711333</td>
      <td>505.67</td>
      <td>15</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Carrollbury</td>
      <td>4</td>
      <td>Suburban</td>
      <td>36.606000</td>
      <td>366.06</td>
      <td>10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Carrollfort</td>
      <td>55</td>
      <td>Urban</td>
      <td>25.395517</td>
      <td>736.47</td>
      <td>29</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Clarkstad</td>
      <td>21</td>
      <td>Suburban</td>
      <td>31.051667</td>
      <td>372.62</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
# make x and y var for each plot (urban, suburban, rural). x is total rides per city, y is avg fare per city. 
#s=size of dot (use driver count)


x_rural = merge_table.loc[merge_table["type"]=="Rural"]['total rides per city']
y_rural = merge_table.loc[merge_table["type"]=="Rural"]['avg fare per city']
s_rural = merge_table.loc[merge_table["type"]=="Rural"]["driver_count"]*10

x_suburban = merge_table.loc[merge_table["type"]=="Suburban"]['total rides per city']
y_suburban = merge_table.loc[merge_table["type"]=="Suburban"]['avg fare per city']
s_suburban = merge_table.loc[merge_table["type"]=="Suburban"]["driver_count"]*10

x_urban = merge_table.loc[merge_table["type"]=="Urban"]['total rides per city']
y_urban = merge_table.loc[merge_table["type"]=="Urban"]['avg fare per city']
s_urban = merge_table.loc[merge_table["type"]=="Urban"]["driver_count"]*10

# plot and style the data
plt.scatter(x_rural, y_rural, s=s_rural, marker="o",
                   c="gold", alpha=.7, linewidths=.7, edgecolors="black", label="Rural")
plt.scatter(x_suburban, y_suburban, s=s_suburban, marker="o",
                    c="lightskyblue", alpha=.7, linewidths=.7, edgecolors="black", label="Suburban")
plt.scatter(x_urban, y_urban, s=s_urban, marker="o",
                    c="lightcoral", alpha=.7, linewidths=.7, edgecolors="black", label="Urban")

# #create title, x and y labels, x and y limits
plt.title("Pyber Ride Sharing Data 2016")
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")
plt.xlim(0, 40)
plt.ylim(15, 55)

#make a legend, grid, change background color to lightgrey, add a note
plt.legend(labels=["Rural","Suburban","Urban"])
plt.gca().set_axisbelow(True)
plt.grid(True, c='white')
plt.gca().set_facecolor('lightgrey')
plt.gcf().text(1, .75,("Note: Circle size correlates with driver count per city"), fontsize=12)
                                        

# Show the chart
plt.show()

```


![png](Pyber1copy_files/Pyber1copy_11_0.png)



```python
#make piecharts:
# % of Total Fares by City Type

urban_fares = merge_table.loc[merge_table["type"]=="Urban"]["total fares per city"].sum()
#print(urban_fares)
suburban_fares = merge_table.loc[merge_table["type"]=="Suburban"]["total fares per city"].sum()
rural_fares = merge_table.loc[merge_table["type"]=="Rural"]["total fares per city"].sum()

# Labels for the sections of our pie chart
labels = ["Urban", "Suburban", "Rural"]

# The values of each section of the pie chart
fares = [urban_fares, suburban_fares, rural_fares]

# The colors of each section of the pie chart
colors = ["lightcoral", "lightskyblue", "gold"]

# Tells matplotlib to seperate the suburban & rural sections from the others
explode = (0, 0.1, 0.1)

# Tell matplotlib to create a bar chart based upon the above data
plt.pie(fares, explode=explode, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)

# Create axes which are equal so we have a perfect circle
plt.axis("equal")

#title
plt.title("% of Total Fares by City Type")

# Save an image of our chart and print the final product to the screen
plt.savefig("PyFares.png")
plt.show()




```


![png](Pyber1copy_files/Pyber1copy_12_0.png)



```python
# % of Total Rides by City Type
urban_rides = merge_table.loc[merge_table["type"]=="Urban"]["total rides per city"].sum()
#print(urban_rides)
suburban_rides = merge_table.loc[merge_table["type"]=="Suburban"]["total rides per city"].sum()
#print(suburban_rides)
rural_rides = merge_table.loc[merge_table["type"]=="Rural"]["total rides per city"].sum()
#print(rural_rides)

# Labels for the sections of our pie chart
labels = ["Urban", "Suburban", "Rural"]

# The values of each section of the pie chart
rides = [urban_rides, suburban_rides, rural_rides]

# The colors of each section of the pie chart
colors = ["lightcoral", "lightskyblue", "gold"]

# Tells matplotlib to seperate the suburban & rural sections from the others
explode = (0, 0.1, 0.1)

# Tell matplotlib to create a bar chart based upon the above data
plt.pie(rides, explode=explode, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)

# Create axes which are equal so we have a perfect circle
plt.axis("equal")

#title
plt.title("% of Total Rides by City Type")

# Save an image of our chart and print the final product to the screen
plt.savefig("PyRides.png")
plt.show()
```


![png](Pyber1copy_files/Pyber1copy_13_0.png)



```python
# % of Total Drivers by City Type

urban_drivers = merge_table.loc[merge_table["type"]=="Urban"]["driver_count"].sum()
#print(urban_drivers)
suburban_drivers = merge_table.loc[merge_table["type"]=="Suburban"]["driver_count"].sum()
#print(suburban_drivers)
rural_drivers = merge_table.loc[merge_table["type"]=="Rural"]["driver_count"].sum()
#print(rural_drivers)

# Labels for the sections of our pie chart
labels = ["Urban", "Suburban", "Rural"]

# The values of each section of the pie chart
drivers = [urban_drivers, suburban_drivers, rural_drivers]

# The colors of each section of the pie chart
colors = ["lightcoral", "lightskyblue", "gold"]

# Tells matplotlib to seperate the suburban & rural sections from the others
explode = (0, 0.1, 0.1)

# Tell matplotlib to create a bar chart based upon the above data
plt.pie(drivers, explode=explode, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)

# Create axes which are equal so we have a perfect circle
plt.axis("equal")

#title
plt.title("% of Total Drivers by City Type")

# Save an image of our chart and print the final product to the screen
plt.savefig("PyDrivers.png")
plt.show()
```


![png](Pyber1copy_files/Pyber1copy_14_0.png)



```python
#Analysis:
#Observation One:
#The data correlates heavily by city type. Urban has more rides, drivers, and fares overall, followed by suburban, 
#followed by rural. To be expected given the service.

#Observation Two:
#There is a much larger spread in the average fares of rural cities. Most urban fares are between $20-30, but with 
#rural fares, there is no such trend. They range from about $22-50, with the average fares from all rural cities 
#spread out in between.

#Observation Three:
#There is also a wider spread in the total number of rides amongst suburban cities than in either urban or rural. Some 
#suburban cities have fewer than 10 rides, while one has over 30. Most suburban cities had a ride total in the teens.

#Observation Four:
#Urban drivers occupy almost 78% of the total drivers, and yet they are competing for 68% of rides and 
#63% of fares, so competition amongst this driver group is higher. In contrast, 19% of the drivers are suburban 
#but they are commanding 30% of the total fares.
```
