# NetCDF To Excel Convertion Data

## Library
import required libraries :
* netCDF4
> from netCDF4 import Dataset
    
    incase you doesn't have netCDF4 :
> python -m pip install netcdf4
* pandas
> import pandas as pd
* numpy
> import numpy as np
* os 
> import os
* datetime
> from datetime import datetime

## See Type and Dimention of Data
To see the data type, when 
> data.variables.keys()

in the console section, parameter information related to netcdf data will appear

Example output : 
> dict_keys(['longitude', 'latitude', 'time', 'd2m', 't2m', 'skt'])

To view the dimensions of a variable, type :
> variable_name.dimensions

Example output :
> ('time', 'latitude', 'longitude')

## Storing coordinate of study area
for the prototype we use 3 coordinate case districs areas in Bali Indonesia:
1. Kab. Tabanan  -8.5511, 115.1216
2. Kab. Gianyar  -8.4667, 115.2833
3. Kab. Bangli   -8.3361,115.1575

## Squared difference of coordinates
to find the distance between two coordinates we can use this formula: 
> sq_diff_lat = (lat_districts - lat_data)**2

>sq_diff_lon = (lon_districts - lon_data)**2

## Identifying the index of minimum value of coordinates
To find out the regional area of ​​the district, we need a minimum index of that area. then we use the formula :

> min_index_lat = sq_diff_lat.argmin()

> min_index_lon = sq_diff_lon.argmin()

## Creating a pandas dataframe
Making range Date Time Series with pd.data_range :
>idx = pd.date_range("YYYY-MM-DD", periods=lenght data, freq="H")

> ts = pd.Series(range(len(idx)), index=idx)

Specify which parameters you will enter into the data frame sorted by date and time (Date Time series) :
> df = pd.DataFrame(0, columns=['parameter'],index = idx)

### example of output : 
---
                        t2m

2020-01-01 00:00:00	300.684602

2020-01-01 01:00:00	299.671909

2020-01-01 02:00:00	299.961250

2020-01-01 03:00:00	300.316197

2020-01-01 04:00:00	300.027417

...	...

2021-02-28 20:00:00	297.118310


2021-02-28 21:00:00	296.994387

2021-02-28 22:00:00	297.001116

2021-02-28 23:00:00	297.204663

2021-03-01 00:00:00	0.000000

---

## Save with CSV format
with data frame save the data 
> df.to_csv("District.csv")

## Reference Data 
https://cds.climate.copernicus.eu/ : ERA5 hourly data on single levels from 1979 to present