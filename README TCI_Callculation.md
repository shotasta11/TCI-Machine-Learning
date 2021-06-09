# TCI CALCULATION

## Library python
import required libraries :
> * pandas
> * numpy

## Read The Excel Data 
using pandas read the excel file of weather data
> df = pd.read_excel('ERA5_Tabanan.xlsx')

Do the same thing to Tabanan and Gianyar City

## Average the data to be in days
Average each parameter into data in day time 
> avg_perhari = df.groupby(np.arange(len(df))//24).mean()


## Calculate TCI and Making Data Frame 
with :
> df_TCI = avg_perhari.assign(TCI = avg_perhari.t2m[:60]*4 + avg_perhari.d2m[:60] + avg_perhari.windspeed_km_h[:60] + avg_perhari.tp_mm[:60]*2)

### TCI Formula
TCI = 4 CId + CIa + W + 2 R 
Annotation:
* TCI : Tourism Climate Index
* CId : Daytime Comfort Index, consisting of maximum air temperature (ᵒC) and the mean maximum relative humidity (%)
* CIa : Daily Comfort Index, consisting of mean air temperature (ᵒC) and the mean relative humidity (%)
* R : Rainfall, precipitation (mm)
* W : Wind, mean wind speed (m/s)

## Remove Parameters Except TCI
deleted all parameter except TCO Columns with a Pandas DataFrame by their index
 > pd.DataFrame.drop(labels=None, axis=1, inplace=True)

for our case :
>df_TCI.drop(df_TCI.columns[0:7], axis=1, inplace=True) 

this will leave only the TCI parameters.

## Save with CSV format
with data frame save the data 
> df_TCI.to_csv("Bangli.csv")