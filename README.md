# WeatherAPIAnalysis


```python
# Dependencies and Setup
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import requests
import time

# Import API key
import api_keys

# Incorporated citipy to determine city based on latitude and longitude
from citipy import citipy

# Output File (CSV)
output_data_file = "output_data/cities.csv"

# Range of latitudes and longitudes
lat_range = (-90, 90)
lng_range = (-180, 180)
```

## Generate Cities List


```python
# List for holding lat_lngs and cities
lat_lngs = []
cities = []

# Create a set of random lat and lng combinations
lats = np.random.uniform(low=-90.000, high=90.000, size=1500)
lngs = np.random.uniform(low=-180.000, high=180.000, size=1500)
lat_lngs = zip(lats, lngs)

# Identify nearest city for each lat, lng combination
for lat_lng in lat_lngs:
    city = citipy.nearest_city(lat_lng[0], lat_lng[1]).city_name
    
    # If the city is unique, then add it to a our cities list
    if city not in cities:
        cities.append(city)

# Print the city count to confirm sufficient count
num_cities = len(cities)

```


```python
num_cities
```




    610




```python
city_df = pd.DataFrame({
    'cities':cities
                       })
#uq = city_df.cities.unique
city_df['Lat'] = ""
city_df['Temperature'] = ""
city_df['Humidity'] = ""
city_df['Cloudiness (%)'] = ""
city_df['Wind Speed (mph)'] = ""


city_df
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
      <th>cities</th>
      <th>Lat</th>
      <th>Temperature</th>
      <th>Humidity</th>
      <th>Cloudiness (%)</th>
      <th>Wind Speed (mph)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>carutapera</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>1</th>
      <td>belushya guba</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>hamilton</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>3</th>
      <td>saleaula</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>shimoda</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>5</th>
      <td>wattegama</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>6</th>
      <td>salalah</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>7</th>
      <td>iqaluit</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>8</th>
      <td>ardahan</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>9</th>
      <td>rikitea</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>10</th>
      <td>louisbourg</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>11</th>
      <td>kargil</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>12</th>
      <td>puerto ayora</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>13</th>
      <td>ushuaia</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>14</th>
      <td>chuy</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>15</th>
      <td>dikson</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>16</th>
      <td>cape town</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>17</th>
      <td>nikolskoye</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>18</th>
      <td>olafsvik</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>19</th>
      <td>qaanaaq</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>20</th>
      <td>banfora</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>21</th>
      <td>saskylakh</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>22</th>
      <td>mayumba</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>23</th>
      <td>kaitangata</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>24</th>
      <td>hasaki</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>25</th>
      <td>torbay</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>26</th>
      <td>jamestown</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>27</th>
      <td>mahebourg</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>28</th>
      <td>kinsale</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>29</th>
      <td>albany</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>580</th>
      <td>saint-georges</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>581</th>
      <td>rudnogorsk</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>582</th>
      <td>bubaque</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>583</th>
      <td>manokwari</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>584</th>
      <td>rettikhovka</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>585</th>
      <td>karmaskaly</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>586</th>
      <td>lethem</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>587</th>
      <td>uruguaiana</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>588</th>
      <td>montecristo</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>589</th>
      <td>wellington</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>590</th>
      <td>lorengau</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>591</th>
      <td>rondonopolis</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>592</th>
      <td>samarai</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>593</th>
      <td>hay river</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>594</th>
      <td>kieta</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>595</th>
      <td>awjilah</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>596</th>
      <td>zonguldak</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>597</th>
      <td>susaki</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>598</th>
      <td>baikunthpur</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>599</th>
      <td>sabancuy</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>600</th>
      <td>revda</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>601</th>
      <td>north bend</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>602</th>
      <td>barbar</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>603</th>
      <td>lodja</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>604</th>
      <td>acuna</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>605</th>
      <td>utiroa</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>606</th>
      <td>wainwright</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>607</th>
      <td>nisia floresta</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>608</th>
      <td>khapa</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>609</th>
      <td>karpathos</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>
<p>610 rows × 6 columns</p>
</div>




```python


```

## Perform API Calls


```python
# OpenWeatherMap API Key
import json
miss_count=0
api_key = api_keys.api_key
# Starting URL for Weather Map API Call
for index,row in city_df.iterrows():
    city = row['cities']
    url = "http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=" + api_key + "&q=" + city
    response = requests.get(url).json()
    #print(json.dumps(response,indent=4,sort_keys=True))
    print("Now retrieving city #%s: %s" % (index + 1, city_df.loc[index,"cities"]))
    print(url)
    
    try:
        city_df.loc[index,'Lat']=response['coord']['lat']
        city_df.loc[index,'Temperature']=response['main']['temp']
        city_df.loc[index,'Humidity']=response['main']['humidity']
        city_df.loc[index,'Cloudiness (%)']=response['clouds']['all']
        city_df.loc[index,'Wind Speed (mph)']=response['wind']['speed']
    except(KeyError):
        
        print("Missing details... skip.")
        miss_count += 1
        if num_cities-miss_count < 500:
            break
    
    

```

    Now retrieving city #1: carutapera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=carutapera
    Now retrieving city #2: belushya guba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=belushya guba
    Missing details... skip.
    Now retrieving city #3: hamilton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hamilton
    Now retrieving city #4: saleaula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=saleaula
    Missing details... skip.
    Now retrieving city #5: shimoda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=shimoda
    Now retrieving city #6: wattegama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=wattegama
    Now retrieving city #7: salalah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=salalah
    Now retrieving city #8: iqaluit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=iqaluit
    Now retrieving city #9: ardahan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ardahan
    Missing details... skip.
    Now retrieving city #10: rikitea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rikitea
    Now retrieving city #11: louisbourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=louisbourg
    Missing details... skip.
    Now retrieving city #12: kargil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kargil
    Now retrieving city #13: puerto ayora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=puerto ayora
    Now retrieving city #14: ushuaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ushuaia
    Now retrieving city #15: chuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=chuy
    Now retrieving city #16: dikson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=dikson
    Now retrieving city #17: cape town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=cape town
    Now retrieving city #18: nikolskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nikolskoye
    Now retrieving city #19: olafsvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=olafsvik
    Missing details... skip.
    Now retrieving city #20: qaanaaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=qaanaaq
    Now retrieving city #21: banfora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=banfora
    Now retrieving city #22: saskylakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=saskylakh
    Now retrieving city #23: mayumba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mayumba
    Now retrieving city #24: kaitangata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kaitangata
    Now retrieving city #25: hasaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hasaki
    Now retrieving city #26: torbay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=torbay
    Now retrieving city #27: jamestown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=jamestown
    Now retrieving city #28: mahebourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mahebourg
    Now retrieving city #29: kinsale
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kinsale
    Now retrieving city #30: albany
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=albany
    Now retrieving city #31: hilo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hilo
    Now retrieving city #32: mataura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mataura
    Now retrieving city #33: champerico
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=champerico
    Now retrieving city #34: troitsko-pechorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=troitsko-pechorsk
    Now retrieving city #35: komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=komsomolskiy
    Now retrieving city #36: pacifica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pacifica
    Now retrieving city #37: hithadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hithadhoo
    Now retrieving city #38: nicoya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nicoya
    Now retrieving city #39: hofn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hofn
    Now retrieving city #40: upernavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=upernavik
    Now retrieving city #41: beringovskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=beringovskiy
    Now retrieving city #42: klaksvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=klaksvik
    Now retrieving city #43: aswan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=aswan
    Now retrieving city #44: karamay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=karamay
    Missing details... skip.
    Now retrieving city #45: thompson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=thompson
    Now retrieving city #46: flinders
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=flinders
    Now retrieving city #47: leningradskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=leningradskiy
    Now retrieving city #48: busselton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=busselton
    Now retrieving city #49: hambantota
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hambantota
    Now retrieving city #50: doctor pedro p. pena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=doctor pedro p. pena
    Missing details... skip.
    Now retrieving city #51: hobart
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hobart
    Now retrieving city #52: paamiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=paamiut
    Now retrieving city #53: luderitz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=luderitz
    Now retrieving city #54: hermanus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hermanus
    Now retrieving city #55: maine-soroa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=maine-soroa
    Now retrieving city #56: huejuquilla el alto
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=huejuquilla el alto
    Now retrieving city #57: barentsburg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=barentsburg
    Missing details... skip.
    Now retrieving city #58: vaini
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vaini
    Now retrieving city #59: lagoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lagoa
    Now retrieving city #60: souillac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=souillac
    Now retrieving city #61: avarua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=avarua
    Now retrieving city #62: taolanaro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=taolanaro
    Missing details... skip.
    Now retrieving city #63: adrar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=adrar
    Now retrieving city #64: lucea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lucea
    Now retrieving city #65: slyudyanka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=slyudyanka
    Now retrieving city #66: portland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=portland
    Now retrieving city #67: punta arenas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=punta arenas
    Now retrieving city #68: ahipara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ahipara
    Now retrieving city #69: longyearbyen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=longyearbyen
    Now retrieving city #70: ponta delgada
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ponta delgada
    Now retrieving city #71: andros town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=andros town
    Now retrieving city #72: illoqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=illoqqortoormiut
    Missing details... skip.
    Now retrieving city #73: yulara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=yulara
    Now retrieving city #74: linjiang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=linjiang
    Now retrieving city #75: kahului
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kahului
    Now retrieving city #76: cabo san lucas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=cabo san lucas
    Now retrieving city #77: vilcun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vilcun
    Now retrieving city #78: georgetown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=georgetown
    Now retrieving city #79: antofagasta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=antofagasta
    Now retrieving city #80: port lincoln
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=port lincoln
    Now retrieving city #81: maturin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=maturin
    Now retrieving city #82: rio grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rio grande
    Now retrieving city #83: ostrow mazowiecka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ostrow mazowiecka
    Now retrieving city #84: tezu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tezu
    Now retrieving city #85: opuwo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=opuwo
    Now retrieving city #86: new norfolk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=new norfolk
    Now retrieving city #87: bluff
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bluff
    Now retrieving city #88: comodoro rivadavia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=comodoro rivadavia
    Now retrieving city #89: ambilobe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ambilobe
    Now retrieving city #90: amderma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=amderma
    Missing details... skip.
    Now retrieving city #91: barrow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=barrow
    Now retrieving city #92: vera cruz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vera cruz
    Now retrieving city #93: betafo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=betafo
    Now retrieving city #94: chifeng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=chifeng
    Now retrieving city #95: otane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=otane
    Now retrieving city #96: kodiak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kodiak
    Now retrieving city #97: atuona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=atuona
    Now retrieving city #98: hobyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hobyo
    Now retrieving city #99: bowling green
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bowling green
    Now retrieving city #100: son la
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=son la
    Now retrieving city #101: bambous virieux
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bambous virieux
    Now retrieving city #102: faya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=faya
    Now retrieving city #103: aklavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=aklavik
    Now retrieving city #104: saint-leu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=saint-leu
    Now retrieving city #105: kumluca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kumluca
    Now retrieving city #106: klyuchi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=klyuchi
    Now retrieving city #107: markala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=markala
    Now retrieving city #108: ayan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ayan
    Now retrieving city #109: tsihombe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tsihombe
    Missing details... skip.
    Now retrieving city #110: cayambe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=cayambe
    Now retrieving city #111: sisimiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sisimiut
    Now retrieving city #112: lebu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lebu
    Now retrieving city #113: vaitupu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vaitupu
    Missing details... skip.
    Now retrieving city #114: skibbereen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=skibbereen
    Now retrieving city #115: sabzevar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sabzevar
    Now retrieving city #116: bilma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bilma
    Now retrieving city #117: faanui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=faanui
    Now retrieving city #118: asau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=asau
    Missing details... skip.
    Now retrieving city #119: marathon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=marathon
    Now retrieving city #120: tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tuktoyaktuk
    Now retrieving city #121: byron bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=byron bay
    Now retrieving city #122: poum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=poum
    Now retrieving city #123: kapaa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kapaa
    Now retrieving city #124: esperance
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=esperance
    Now retrieving city #125: sentyabrskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sentyabrskiy
    Missing details... skip.
    Now retrieving city #126: east london
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=east london
    Now retrieving city #127: altay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=altay
    Now retrieving city #128: fort nelson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=fort nelson
    Now retrieving city #129: belyy yar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=belyy yar
    Now retrieving city #130: vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vestmannaeyjar
    Now retrieving city #131: husavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=husavik
    Now retrieving city #132: chokurdakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=chokurdakh
    Now retrieving city #133: tumannyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tumannyy
    Missing details... skip.
    Now retrieving city #134: shwebo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=shwebo
    Now retrieving city #135: constitucion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=constitucion
    Now retrieving city #136: boa vista
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=boa vista
    Now retrieving city #137: romitan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=romitan
    Now retrieving city #138: jieshi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=jieshi
    Now retrieving city #139: verkhnevilyuysk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=verkhnevilyuysk
    Now retrieving city #140: chandrapur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=chandrapur
    Now retrieving city #141: berdigestyakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=berdigestyakh
    Now retrieving city #142: mount isa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mount isa
    Now retrieving city #143: sorong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sorong
    Now retrieving city #144: porto novo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=porto novo
    Now retrieving city #145: mayo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mayo
    Now retrieving city #146: naze
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=naze
    Now retrieving city #147: pevek
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pevek
    Now retrieving city #148: ginda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ginda
    Now retrieving city #149: tasiilaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tasiilaq
    Now retrieving city #150: briancon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=briancon
    Now retrieving city #151: yellowknife
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=yellowknife
    Now retrieving city #152: saint-augustin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=saint-augustin
    Now retrieving city #153: tiznit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tiznit
    Now retrieving city #154: coahuayana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=coahuayana
    Now retrieving city #155: nizwa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nizwa
    Now retrieving city #156: callaguip
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=callaguip
    Now retrieving city #157: stjordalshalsen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=stjordalshalsen
    Now retrieving city #158: geraldton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=geraldton
    Now retrieving city #159: aleppo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=aleppo
    Now retrieving city #160: bredasdorp
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bredasdorp
    Now retrieving city #161: petrolina de goias
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=petrolina de goias
    Now retrieving city #162: waycross
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=waycross
    Now retrieving city #163: erzin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=erzin
    Now retrieving city #164: quatre cocos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=quatre cocos
    Now retrieving city #165: bethel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bethel
    Now retrieving city #166: sinfra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sinfra
    Now retrieving city #167: havre-saint-pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=havre-saint-pierre
    Now retrieving city #168: kuche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kuche
    Missing details... skip.
    Now retrieving city #169: guane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=guane
    Now retrieving city #170: provideniya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=provideniya
    Now retrieving city #171: skalistyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=skalistyy
    Missing details... skip.
    Now retrieving city #172: ucluelet
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ucluelet
    Now retrieving city #173: soyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=soyo
    Now retrieving city #174: havelock
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=havelock
    Now retrieving city #175: kandrian
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kandrian
    Now retrieving city #176: russell
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=russell
    Now retrieving city #177: cidreira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=cidreira
    Now retrieving city #178: fairbanks
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=fairbanks
    Now retrieving city #179: san quintin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=san quintin
    Now retrieving city #180: alice springs
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=alice springs
    Now retrieving city #181: benghazi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=benghazi
    Now retrieving city #182: katsuura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=katsuura
    Now retrieving city #183: saint-philippe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=saint-philippe
    Now retrieving city #184: mar del plata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mar del plata
    Now retrieving city #185: samusu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=samusu
    Missing details... skip.
    Now retrieving city #186: kavaratti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kavaratti
    Now retrieving city #187: saint george
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=saint george
    Now retrieving city #188: cayenne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=cayenne
    Now retrieving city #189: cristalina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=cristalina
    Now retrieving city #190: butaritari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=butaritari
    Now retrieving city #191: belmonte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=belmonte
    Now retrieving city #192: sayat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sayat
    Now retrieving city #193: umm durman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=umm durman
    Missing details... skip.
    Now retrieving city #194: port alfred
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=port alfred
    Now retrieving city #195: port macquarie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=port macquarie
    Now retrieving city #196: vardo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vardo
    Now retrieving city #197: santo domingo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=santo domingo
    Now retrieving city #198: nizhneyansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nizhneyansk
    Missing details... skip.
    Now retrieving city #199: kalety
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kalety
    Now retrieving city #200: kiama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kiama
    Now retrieving city #201: khani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=khani
    Now retrieving city #202: kirakira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kirakira
    Now retrieving city #203: mattru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mattru
    Now retrieving city #204: kasama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kasama
    Now retrieving city #205: kenai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kenai
    Now retrieving city #206: fallon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=fallon
    Now retrieving city #207: pontes e lacerda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pontes e lacerda
    Now retrieving city #208: xunchang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=xunchang
    Now retrieving city #209: vostok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vostok
    Now retrieving city #210: vanavara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vanavara
    Now retrieving city #211: severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=severo-kurilsk
    Now retrieving city #212: grand river south east
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=grand river south east
    Missing details... skip.
    Now retrieving city #213: ilulissat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ilulissat
    Now retrieving city #214: ribeira grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ribeira grande
    Now retrieving city #215: castro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=castro
    Now retrieving city #216: khandyga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=khandyga
    Now retrieving city #217: saint-pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=saint-pierre
    Now retrieving city #218: palabuhanratu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=palabuhanratu
    Missing details... skip.
    Now retrieving city #219: marquette
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=marquette
    Now retrieving city #220: birin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=birin
    Now retrieving city #221: vasilkovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vasilkovo
    Missing details... skip.
    Now retrieving city #222: tuatapere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tuatapere
    Now retrieving city #223: trelew
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=trelew
    Now retrieving city #224: airai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=airai
    Now retrieving city #225: ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ostrovnoy
    Now retrieving city #226: srednekolymsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=srednekolymsk
    Now retrieving city #227: rocha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rocha
    Now retrieving city #228: vyazma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vyazma
    Now retrieving city #229: dwarahat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=dwarahat
    Now retrieving city #230: nuuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nuuk
    Now retrieving city #231: bacolod
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bacolod
    Now retrieving city #232: muswellbrook
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=muswellbrook
    Now retrieving city #233: likasi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=likasi
    Now retrieving city #234: baiao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=baiao
    Now retrieving city #235: muisne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=muisne
    Now retrieving city #236: cherskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=cherskiy
    Now retrieving city #237: victoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=victoria
    Now retrieving city #238: envira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=envira
    Missing details... skip.
    Now retrieving city #239: meru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=meru
    Now retrieving city #240: samalaeulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=samalaeulu
    Missing details... skip.
    Now retrieving city #241: tete
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tete
    Now retrieving city #242: sohag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sohag
    Now retrieving city #243: valparaiso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=valparaiso
    Now retrieving city #244: pochutla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pochutla
    Now retrieving city #245: san patricio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=san patricio
    Now retrieving city #246: pisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pisco
    Now retrieving city #247: rungata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rungata
    Missing details... skip.
    Now retrieving city #248: srivardhan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=srivardhan
    Now retrieving city #249: calabozo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=calabozo
    Now retrieving city #250: lavrentiya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lavrentiya
    Now retrieving city #251: tiksi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tiksi
    Now retrieving city #252: aktash
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=aktash
    Missing details... skip.
    Now retrieving city #253: mys shmidta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mys shmidta
    Missing details... skip.
    Now retrieving city #254: sambava
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sambava
    Now retrieving city #255: grand centre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=grand centre
    Missing details... skip.
    Now retrieving city #256: hihifo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hihifo
    Missing details... skip.
    Now retrieving city #257: teya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=teya
    Now retrieving city #258: gat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=gat
    Now retrieving city #259: sitka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sitka
    Now retrieving city #260: mingyue
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mingyue
    Now retrieving city #261: port elizabeth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=port elizabeth
    Now retrieving city #262: rapid city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rapid city
    Now retrieving city #263: vytegra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vytegra
    Now retrieving city #264: pacific grove
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pacific grove
    Now retrieving city #265: vila franca do campo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vila franca do campo
    Now retrieving city #266: nangong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nangong
    Now retrieving city #267: kalundborg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kalundborg
    Now retrieving city #268: zelenogorskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=zelenogorskiy
    Now retrieving city #269: fortuna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=fortuna
    Now retrieving city #270: sangmelima
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sangmelima
    Now retrieving city #271: narsaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=narsaq
    Now retrieving city #272: mandawar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mandawar
    Now retrieving city #273: concepcion del uruguay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=concepcion del uruguay
    Now retrieving city #274: avera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=avera
    Now retrieving city #275: forest grove
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=forest grove
    Now retrieving city #276: meulaboh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=meulaboh
    Now retrieving city #277: karkaralinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=karkaralinsk
    Missing details... skip.
    Now retrieving city #278: bloomfield
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bloomfield
    Now retrieving city #279: mehamn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mehamn
    Now retrieving city #280: tucuman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tucuman
    Now retrieving city #281: tabiauea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tabiauea
    Missing details... skip.
    Now retrieving city #282: okhotsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=okhotsk
    Now retrieving city #283: mirina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mirina
    Missing details... skip.
    Now retrieving city #284: karachi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=karachi
    Now retrieving city #285: ninghai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ninghai
    Now retrieving city #286: gizo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=gizo
    Now retrieving city #287: cockburn town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=cockburn town
    Now retrieving city #288: lima
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lima
    Now retrieving city #289: augustow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=augustow
    Now retrieving city #290: qandahar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=qandahar
    Missing details... skip.
    Now retrieving city #291: iquitos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=iquitos
    Now retrieving city #292: eskasem
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=eskasem
    Missing details... skip.
    Now retrieving city #293: maldonado
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=maldonado
    Now retrieving city #294: bitung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bitung
    Now retrieving city #295: itarema
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=itarema
    Now retrieving city #296: turukhansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=turukhansk
    Now retrieving city #297: nadym
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nadym
    Now retrieving city #298: xinqing
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=xinqing
    Now retrieving city #299: deputatskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=deputatskiy
    Now retrieving city #300: akdepe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=akdepe
    Now retrieving city #301: iracoubo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=iracoubo
    Now retrieving city #302: pyra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pyra
    Now retrieving city #303: meyungs
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=meyungs
    Missing details... skip.
    Now retrieving city #304: alta floresta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=alta floresta
    Now retrieving city #305: caucaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=caucaia
    Now retrieving city #306: malwan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=malwan
    Missing details... skip.
    Now retrieving city #307: gorontalo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=gorontalo
    Now retrieving city #308: tuggurt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tuggurt
    Missing details... skip.
    Now retrieving city #309: ancud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ancud
    Now retrieving city #310: lompoc
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lompoc
    Now retrieving city #311: burica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=burica
    Missing details... skip.
    Now retrieving city #312: sobolevo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sobolevo
    Now retrieving city #313: elko
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=elko
    Now retrieving city #314: gotsu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=gotsu
    Now retrieving city #315: vao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vao
    Now retrieving city #316: khatanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=khatanga
    Now retrieving city #317: calama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=calama
    Now retrieving city #318: gerash
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=gerash
    Now retrieving city #319: komsomolskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=komsomolskoye
    Now retrieving city #320: rorvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rorvik
    Now retrieving city #321: mizan teferi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mizan teferi
    Now retrieving city #322: hami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hami
    Now retrieving city #323: ixtapa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ixtapa
    Now retrieving city #324: rock sound
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rock sound
    Now retrieving city #325: ulaangom
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ulaangom
    Now retrieving city #326: gryazi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=gryazi
    Now retrieving city #327: concepcion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=concepcion
    Now retrieving city #328: grimari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=grimari
    Missing details... skip.
    Now retrieving city #329: bathsheba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bathsheba
    Now retrieving city #330: atar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=atar
    Now retrieving city #331: codrington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=codrington
    Now retrieving city #332: biak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=biak
    Now retrieving city #333: ossora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ossora
    Now retrieving city #334: catamarca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=catamarca
    Missing details... skip.
    Now retrieving city #335: haapiti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=haapiti
    Now retrieving city #336: tucumcari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tucumcari
    Now retrieving city #337: chulman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=chulman
    Now retrieving city #338: rio do sul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rio do sul
    Now retrieving city #339: tarakan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tarakan
    Now retrieving city #340: seoul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=seoul
    Now retrieving city #341: petropavlovsk-kamchatskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=petropavlovsk-kamchatskiy
    Now retrieving city #342: carnarvon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=carnarvon
    Now retrieving city #343: lannion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lannion
    Now retrieving city #344: vila
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vila
    Now retrieving city #345: ileza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ileza
    Now retrieving city #346: labuhan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=labuhan
    Now retrieving city #347: buqayq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=buqayq
    Missing details... skip.
    Now retrieving city #348: nanortalik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nanortalik
    Now retrieving city #349: ponnani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ponnani
    Now retrieving city #350: marsh harbour
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=marsh harbour
    Now retrieving city #351: naryan-mar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=naryan-mar
    Now retrieving city #352: beloha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=beloha
    Now retrieving city #353: laguna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=laguna
    Now retrieving city #354: teknaf
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=teknaf
    Now retrieving city #355: grindavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=grindavik
    Now retrieving city #356: college
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=college
    Now retrieving city #357: taoudenni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=taoudenni
    Now retrieving city #358: doha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=doha
    Now retrieving city #359: la ronge
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=la ronge
    Now retrieving city #360: karratha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=karratha
    Now retrieving city #361: fare
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=fare
    Now retrieving city #362: buariki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=buariki
    Missing details... skip.
    Now retrieving city #363: benguela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=benguela
    Now retrieving city #364: barawe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=barawe
    Missing details... skip.
    Now retrieving city #365: palmer
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=palmer
    Now retrieving city #366: vanimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vanimo
    Now retrieving city #367: kondagaon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kondagaon
    Now retrieving city #368: guerrero negro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=guerrero negro
    Now retrieving city #369: iskateley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=iskateley
    Now retrieving city #370: arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=arraial do cabo
    Now retrieving city #371: roma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=roma
    Now retrieving city #372: ambulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ambulu
    Now retrieving city #373: frederikshavn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=frederikshavn
    Now retrieving city #374: mount gambier
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mount gambier
    Now retrieving city #375: ndende
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ndende
    Missing details... skip.
    Now retrieving city #376: galveston
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=galveston
    Now retrieving city #377: yungkang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=yungkang
    Missing details... skip.
    Now retrieving city #378: sao filipe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sao filipe
    Now retrieving city #379: ojinaga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ojinaga
    Now retrieving city #380: diffa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=diffa
    Now retrieving city #381: cairns
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=cairns
    Now retrieving city #382: ust-kamchatsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ust-kamchatsk
    Missing details... skip.
    Now retrieving city #383: zhangye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=zhangye
    Now retrieving city #384: praia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=praia
    Now retrieving city #385: bereda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bereda
    Now retrieving city #386: te anau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=te anau
    Now retrieving city #387: tocopilla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tocopilla
    Now retrieving city #388: baniyas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=baniyas
    Now retrieving city #389: aquiraz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=aquiraz
    Now retrieving city #390: vryheid
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vryheid
    Now retrieving city #391: galgani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=galgani
    Missing details... skip.
    Now retrieving city #392: qidong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=qidong
    Now retrieving city #393: emerald
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=emerald
    Now retrieving city #394: yarmouth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=yarmouth
    Now retrieving city #395: ulaanbaatar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ulaanbaatar
    Now retrieving city #396: haflong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=haflong
    Now retrieving city #397: kulhudhuffushi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kulhudhuffushi
    Now retrieving city #398: praia da vitoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=praia da vitoria
    Now retrieving city #399: kazalinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kazalinsk
    Missing details... skip.
    Now retrieving city #400: port hardy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=port hardy
    Now retrieving city #401: micheweni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=micheweni
    Now retrieving city #402: egvekinot
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=egvekinot
    Now retrieving city #403: boras
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=boras
    Now retrieving city #404: norman wells
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=norman wells
    Now retrieving city #405: san borja
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=san borja
    Now retrieving city #406: tarudant
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tarudant
    Missing details... skip.
    Now retrieving city #407: vila velha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=vila velha
    Now retrieving city #408: pangnirtung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pangnirtung
    Now retrieving city #409: wanxian
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=wanxian
    Now retrieving city #410: mbanza-ngungu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mbanza-ngungu
    Now retrieving city #411: santa fe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=santa fe
    Now retrieving city #412: hualmay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hualmay
    Now retrieving city #413: ust-tsilma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ust-tsilma
    Now retrieving city #414: muros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=muros
    Now retrieving city #415: atherton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=atherton
    Now retrieving city #416: baykit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=baykit
    Now retrieving city #417: sovetskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sovetskiy
    Now retrieving city #418: berikulskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=berikulskiy
    Missing details... skip.
    Now retrieving city #419: mirnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mirnyy
    Now retrieving city #420: caravelas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=caravelas
    Now retrieving city #421: los llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=los llanos de aridane
    Now retrieving city #422: nabire
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nabire
    Now retrieving city #423: umm kaddadah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=umm kaddadah
    Now retrieving city #424: athabasca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=athabasca
    Now retrieving city #425: levelland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=levelland
    Now retrieving city #426: san pedro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=san pedro
    Now retrieving city #427: paducah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=paducah
    Now retrieving city #428: kodinar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kodinar
    Now retrieving city #429: jacareacanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=jacareacanga
    Now retrieving city #430: ouadda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ouadda
    Now retrieving city #431: boyolangu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=boyolangu
    Now retrieving city #432: port blair
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=port blair
    Now retrieving city #433: yenisea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=yenisea
    Missing details... skip.
    Now retrieving city #434: koumac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=koumac
    Now retrieving city #435: kavieng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kavieng
    Now retrieving city #436: malumfashi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=malumfashi
    Now retrieving city #437: jabiru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=jabiru
    Missing details... skip.
    Now retrieving city #438: san buenaventura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=san buenaventura
    Now retrieving city #439: shizunai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=shizunai
    Now retrieving city #440: port-gentil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=port-gentil
    Now retrieving city #441: taltal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=taltal
    Now retrieving city #442: kamenskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kamenskoye
    Missing details... skip.
    Now retrieving city #443: tignere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tignere
    Now retrieving city #444: esfarayen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=esfarayen
    Now retrieving city #445: moussoro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=moussoro
    Now retrieving city #446: arroyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=arroyo
    Now retrieving city #447: bukama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bukama
    Now retrieving city #448: marcona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=marcona
    Missing details... skip.
    Now retrieving city #449: ryomgard
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ryomgard
    Now retrieving city #450: berlevag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=berlevag
    Now retrieving city #451: praya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=praya
    Now retrieving city #452: gebze
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=gebze
    Now retrieving city #453: talnakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=talnakh
    Now retrieving city #454: la brea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=la brea
    Now retrieving city #455: chapais
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=chapais
    Now retrieving city #456: rudnya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rudnya
    Now retrieving city #457: nouadhibou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nouadhibou
    Now retrieving city #458: attawapiskat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=attawapiskat
    Missing details... skip.
    Now retrieving city #459: dabola
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=dabola
    Now retrieving city #460: mtambile
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mtambile
    Now retrieving city #461: nome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nome
    Now retrieving city #462: careiro da varzea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=careiro da varzea
    Now retrieving city #463: billings
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=billings
    Now retrieving city #464: higuey
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=higuey
    Missing details... skip.
    Now retrieving city #465: khorixas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=khorixas
    Now retrieving city #466: ha giang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ha giang
    Now retrieving city #467: kaspiyskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kaspiyskiy
    Now retrieving city #468: tanete
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tanete
    Now retrieving city #469: kayalpattinam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kayalpattinam
    Now retrieving city #470: san cristobal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=san cristobal
    Now retrieving city #471: coquimbo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=coquimbo
    Now retrieving city #472: ambon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ambon
    Now retrieving city #473: ust-nera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ust-nera
    Now retrieving city #474: atocha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=atocha
    Now retrieving city #475: entre rios
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=entre rios
    Now retrieving city #476: yanchukan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=yanchukan
    Missing details... skip.
    Now retrieving city #477: maykain
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=maykain
    Missing details... skip.
    Now retrieving city #478: lodwar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lodwar
    Now retrieving city #479: tervel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tervel
    Now retrieving city #480: bulgan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bulgan
    Now retrieving city #481: patacamaya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=patacamaya
    Now retrieving city #482: bengkulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bengkulu
    Missing details... skip.
    Now retrieving city #483: bethanien
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bethanien
    Now retrieving city #484: morgan city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=morgan city
    Now retrieving city #485: skelleftea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=skelleftea
    Now retrieving city #486: nizhnyaya tura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nizhnyaya tura
    Now retrieving city #487: clyde river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=clyde river
    Now retrieving city #488: svetlaya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=svetlaya
    Now retrieving city #489: isangel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=isangel
    Now retrieving city #490: abu samrah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=abu samrah
    Now retrieving city #491: reyes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=reyes
    Now retrieving city #492: jimenez
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=jimenez
    Now retrieving city #493: kawalu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kawalu
    Now retrieving city #494: mandal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mandal
    Now retrieving city #495: plettenberg bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=plettenberg bay
    Now retrieving city #496: maragogi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=maragogi
    Now retrieving city #497: mareeba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mareeba
    Now retrieving city #498: pandan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pandan
    Now retrieving city #499: goderich
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=goderich
    Now retrieving city #500: kem
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kem
    Now retrieving city #501: san francisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=san francisco
    Now retrieving city #502: temaraia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=temaraia
    Missing details... skip.
    Now retrieving city #503: villa altagracia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=villa altagracia
    Now retrieving city #504: eucaliptus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=eucaliptus
    Now retrieving city #505: bolungarvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bolungarvik
    Missing details... skip.
    Now retrieving city #506: isabela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=isabela
    Now retrieving city #507: umzimvubu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=umzimvubu
    Missing details... skip.
    Now retrieving city #508: ormara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ormara
    Now retrieving city #509: lolua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lolua
    Missing details... skip.
    Now retrieving city #510: caloundra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=caloundra
    Now retrieving city #511: henties bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=henties bay
    Now retrieving city #512: simao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=simao
    Now retrieving city #513: priekule
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=priekule
    Now retrieving city #514: padang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=padang
    Now retrieving city #515: esso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=esso
    Now retrieving city #516: viligili
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=viligili
    Missing details... skip.
    Now retrieving city #517: bonthe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bonthe
    Now retrieving city #518: davila
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=davila
    Now retrieving city #519: genthin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=genthin
    Now retrieving city #520: sidrolandia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sidrolandia
    Now retrieving city #521: esperantinopolis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=esperantinopolis
    Now retrieving city #522: lar gerd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lar gerd
    Missing details... skip.
    Now retrieving city #523: kaeo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kaeo
    Now retrieving city #524: kruisfontein
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kruisfontein
    Now retrieving city #525: garowe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=garowe
    Now retrieving city #526: kendari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kendari
    Now retrieving city #527: ahuimanu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ahuimanu
    Now retrieving city #528: kiunga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kiunga
    Now retrieving city #529: xining
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=xining
    Now retrieving city #530: tutoia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tutoia
    Now retrieving city #531: saint-francois
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=saint-francois
    Now retrieving city #532: popondetta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=popondetta
    Now retrieving city #533: bang ban
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bang ban
    Now retrieving city #534: kuala terengganu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kuala terengganu
    Now retrieving city #535: ponta do sol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ponta do sol
    Now retrieving city #536: jalingo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=jalingo
    Now retrieving city #537: asind
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=asind
    Now retrieving city #538: matara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=matara
    Now retrieving city #539: atambua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=atambua
    Now retrieving city #540: yar-sale
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=yar-sale
    Now retrieving city #541: domoni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=domoni
    Missing details... skip.
    Now retrieving city #542: belozerskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=belozerskoye
    Now retrieving city #543: xai-xai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=xai-xai
    Now retrieving city #544: lasa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lasa
    Now retrieving city #545: pontianak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pontianak
    Now retrieving city #546: natal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=natal
    Now retrieving city #547: the pas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=the pas
    Now retrieving city #548: papetoai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=papetoai
    Now retrieving city #549: namibe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=namibe
    Now retrieving city #550: heinola
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=heinola
    Now retrieving city #551: taunggyi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=taunggyi
    Now retrieving city #552: tarrega
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tarrega
    Now retrieving city #553: port moresby
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=port moresby
    Now retrieving city #554: kjollefjord
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kjollefjord
    Now retrieving city #555: tshikapa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=tshikapa
    Now retrieving city #556: anahuac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=anahuac
    Now retrieving city #557: bhatkal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bhatkal
    Now retrieving city #558: chaman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=chaman
    Now retrieving city #559: artyom
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=artyom
    Now retrieving city #560: kayerkan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kayerkan
    Now retrieving city #561: sabha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sabha
    Now retrieving city #562: senanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=senanga
    Now retrieving city #563: ugoofaaru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=ugoofaaru
    Now retrieving city #564: severo-yeniseyskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=severo-yeniseyskiy
    Now retrieving city #565: jambi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=jambi
    Now retrieving city #566: svetlyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=svetlyy
    Missing details... skip.
    Now retrieving city #567: nueva helvecia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nueva helvecia
    Now retrieving city #568: pomabamba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=pomabamba
    Now retrieving city #569: biltine
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=biltine
    Now retrieving city #570: trat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=trat
    Now retrieving city #571: arman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=arman
    Now retrieving city #572: namatanai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=namatanai
    Now retrieving city #573: mantua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=mantua
    Now retrieving city #574: bayan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bayan
    Now retrieving city #575: nancha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nancha
    Now retrieving city #576: belousovka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=belousovka
    Now retrieving city #577: berbera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=berbera
    Missing details... skip.
    Now retrieving city #578: belaya gora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=belaya gora
    Now retrieving city #579: san antonio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=san antonio
    Now retrieving city #580: shirokiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=shirokiy
    Now retrieving city #581: saint-georges
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=saint-georges
    Now retrieving city #582: rudnogorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rudnogorsk
    Now retrieving city #583: bubaque
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=bubaque
    Now retrieving city #584: manokwari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=manokwari
    Now retrieving city #585: rettikhovka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rettikhovka
    Now retrieving city #586: karmaskaly
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=karmaskaly
    Now retrieving city #587: lethem
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lethem
    Now retrieving city #588: uruguaiana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=uruguaiana
    Now retrieving city #589: montecristo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=montecristo
    Now retrieving city #590: wellington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=wellington
    Now retrieving city #591: lorengau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lorengau
    Now retrieving city #592: rondonopolis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=rondonopolis
    Now retrieving city #593: samarai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=samarai
    Now retrieving city #594: hay river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=hay river
    Now retrieving city #595: kieta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=kieta
    Now retrieving city #596: awjilah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=awjilah
    Now retrieving city #597: zonguldak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=zonguldak
    Now retrieving city #598: susaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=susaki
    Now retrieving city #599: baikunthpur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=baikunthpur
    Now retrieving city #600: sabancuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=sabancuy
    Now retrieving city #601: revda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=revda
    Now retrieving city #602: north bend
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=north bend
    Now retrieving city #603: barbar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=barbar
    Missing details... skip.
    Now retrieving city #604: lodja
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=lodja
    Now retrieving city #605: acuna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=acuna
    Missing details... skip.
    Now retrieving city #606: utiroa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=utiroa
    Missing details... skip.
    Now retrieving city #607: wainwright
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=wainwright
    Now retrieving city #608: nisia floresta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=nisia floresta
    Now retrieving city #609: khapa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=khapa
    Now retrieving city #610: karpathos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=66edd4468cab1021c4051f8c4f083177&q=karpathos
    


```python
print(miss_count)
city_df.head()
```

    73
    




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
      <th>cities</th>
      <th>Lat</th>
      <th>Temperature</th>
      <th>Humidity</th>
      <th>Cloudiness (%)</th>
      <th>Wind Speed (mph)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>carutapera</td>
      <td>-1.2</td>
      <td>77.93</td>
      <td>87</td>
      <td>0</td>
      <td>9.42</td>
    </tr>
    <tr>
      <th>1</th>
      <td>belushya guba</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>hamilton</td>
      <td>32.3</td>
      <td>78.8</td>
      <td>69</td>
      <td>40</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>3</th>
      <td>saleaula</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>shimoda</td>
      <td>34.7</td>
      <td>78.8</td>
      <td>74</td>
      <td>40</td>
      <td>14.99</td>
    </tr>
  </tbody>
</table>
</div>




```python
city_df['Lat'].replace('', np.nan, inplace=True)
city_df

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
      <th>cities</th>
      <th>Lat</th>
      <th>Temperature</th>
      <th>Humidity</th>
      <th>Cloudiness (%)</th>
      <th>Wind Speed (mph)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>carutapera</td>
      <td>-1.20</td>
      <td>77.93</td>
      <td>87</td>
      <td>0</td>
      <td>9.42</td>
    </tr>
    <tr>
      <th>1</th>
      <td>belushya guba</td>
      <td>NaN</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>hamilton</td>
      <td>32.30</td>
      <td>78.8</td>
      <td>69</td>
      <td>40</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>3</th>
      <td>saleaula</td>
      <td>NaN</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>shimoda</td>
      <td>34.70</td>
      <td>78.8</td>
      <td>74</td>
      <td>40</td>
      <td>14.99</td>
    </tr>
    <tr>
      <th>5</th>
      <td>wattegama</td>
      <td>7.35</td>
      <td>83.87</td>
      <td>66</td>
      <td>64</td>
      <td>7.18</td>
    </tr>
    <tr>
      <th>6</th>
      <td>salalah</td>
      <td>17.01</td>
      <td>78.8</td>
      <td>74</td>
      <td>75</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>7</th>
      <td>iqaluit</td>
      <td>63.75</td>
      <td>28.7</td>
      <td>100</td>
      <td>80</td>
      <td>8.63</td>
    </tr>
    <tr>
      <th>8</th>
      <td>ardahan</td>
      <td>NaN</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>9</th>
      <td>rikitea</td>
      <td>-23.12</td>
      <td>70.37</td>
      <td>100</td>
      <td>92</td>
      <td>7.4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>louisbourg</td>
      <td>NaN</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>11</th>
      <td>kargil</td>
      <td>34.56</td>
      <td>33.02</td>
      <td>94</td>
      <td>92</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>12</th>
      <td>puerto ayora</td>
      <td>-0.74</td>
      <td>68.48</td>
      <td>100</td>
      <td>0</td>
      <td>9.53</td>
    </tr>
    <tr>
      <th>13</th>
      <td>ushuaia</td>
      <td>-54.81</td>
      <td>32</td>
      <td>100</td>
      <td>90</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>14</th>
      <td>chuy</td>
      <td>-33.69</td>
      <td>65.24</td>
      <td>99</td>
      <td>92</td>
      <td>4.16</td>
    </tr>
    <tr>
      <th>15</th>
      <td>dikson</td>
      <td>73.51</td>
      <td>41.48</td>
      <td>91</td>
      <td>92</td>
      <td>8.52</td>
    </tr>
    <tr>
      <th>16</th>
      <td>cape town</td>
      <td>-33.93</td>
      <td>59</td>
      <td>67</td>
      <td>0</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>17</th>
      <td>nikolskoye</td>
      <td>59.70</td>
      <td>50</td>
      <td>87</td>
      <td>20</td>
      <td>15.66</td>
    </tr>
    <tr>
      <th>18</th>
      <td>olafsvik</td>
      <td>NaN</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>19</th>
      <td>qaanaaq</td>
      <td>77.48</td>
      <td>15.56</td>
      <td>100</td>
      <td>0</td>
      <td>9.86</td>
    </tr>
    <tr>
      <th>20</th>
      <td>banfora</td>
      <td>10.64</td>
      <td>71.36</td>
      <td>98</td>
      <td>76</td>
      <td>6.06</td>
    </tr>
    <tr>
      <th>21</th>
      <td>saskylakh</td>
      <td>71.97</td>
      <td>40.31</td>
      <td>91</td>
      <td>80</td>
      <td>5.17</td>
    </tr>
    <tr>
      <th>22</th>
      <td>mayumba</td>
      <td>-3.44</td>
      <td>75.23</td>
      <td>99</td>
      <td>68</td>
      <td>4.05</td>
    </tr>
    <tr>
      <th>23</th>
      <td>kaitangata</td>
      <td>-46.28</td>
      <td>45.08</td>
      <td>90</td>
      <td>92</td>
      <td>13.44</td>
    </tr>
    <tr>
      <th>24</th>
      <td>hasaki</td>
      <td>35.73</td>
      <td>79.65</td>
      <td>54</td>
      <td>40</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>25</th>
      <td>torbay</td>
      <td>47.66</td>
      <td>45.35</td>
      <td>100</td>
      <td>0</td>
      <td>12.55</td>
    </tr>
    <tr>
      <th>26</th>
      <td>jamestown</td>
      <td>-33.21</td>
      <td>69.2</td>
      <td>28</td>
      <td>20</td>
      <td>11.21</td>
    </tr>
    <tr>
      <th>27</th>
      <td>mahebourg</td>
      <td>-20.41</td>
      <td>78.8</td>
      <td>65</td>
      <td>40</td>
      <td>17.22</td>
    </tr>
    <tr>
      <th>28</th>
      <td>kinsale</td>
      <td>51.71</td>
      <td>44.6</td>
      <td>93</td>
      <td>40</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>29</th>
      <td>albany</td>
      <td>42.65</td>
      <td>46.98</td>
      <td>76</td>
      <td>90</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>580</th>
      <td>saint-georges</td>
      <td>46.12</td>
      <td>41.3</td>
      <td>81</td>
      <td>20</td>
      <td>5.06</td>
    </tr>
    <tr>
      <th>581</th>
      <td>rudnogorsk</td>
      <td>57.27</td>
      <td>57.23</td>
      <td>49</td>
      <td>0</td>
      <td>3.83</td>
    </tr>
    <tr>
      <th>582</th>
      <td>bubaque</td>
      <td>11.28</td>
      <td>80.27</td>
      <td>100</td>
      <td>48</td>
      <td>11.88</td>
    </tr>
    <tr>
      <th>583</th>
      <td>manokwari</td>
      <td>-0.87</td>
      <td>82.43</td>
      <td>100</td>
      <td>24</td>
      <td>3.38</td>
    </tr>
    <tr>
      <th>584</th>
      <td>rettikhovka</td>
      <td>44.17</td>
      <td>63.53</td>
      <td>76</td>
      <td>56</td>
      <td>7.18</td>
    </tr>
    <tr>
      <th>585</th>
      <td>karmaskaly</td>
      <td>54.37</td>
      <td>59</td>
      <td>100</td>
      <td>75</td>
      <td>2.24</td>
    </tr>
    <tr>
      <th>586</th>
      <td>lethem</td>
      <td>3.38</td>
      <td>81.35</td>
      <td>64</td>
      <td>8</td>
      <td>11.32</td>
    </tr>
    <tr>
      <th>587</th>
      <td>uruguaiana</td>
      <td>-29.77</td>
      <td>78.8</td>
      <td>83</td>
      <td>0</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>588</th>
      <td>montecristo</td>
      <td>8.30</td>
      <td>72.53</td>
      <td>100</td>
      <td>88</td>
      <td>2.15</td>
    </tr>
    <tr>
      <th>589</th>
      <td>wellington</td>
      <td>-41.29</td>
      <td>53.6</td>
      <td>76</td>
      <td>0</td>
      <td>21.92</td>
    </tr>
    <tr>
      <th>590</th>
      <td>lorengau</td>
      <td>-2.02</td>
      <td>84.41</td>
      <td>100</td>
      <td>64</td>
      <td>4.83</td>
    </tr>
    <tr>
      <th>591</th>
      <td>rondonopolis</td>
      <td>-16.46</td>
      <td>70.91</td>
      <td>85</td>
      <td>0</td>
      <td>2.59</td>
    </tr>
    <tr>
      <th>592</th>
      <td>samarai</td>
      <td>-10.62</td>
      <td>78.2</td>
      <td>99</td>
      <td>88</td>
      <td>18.03</td>
    </tr>
    <tr>
      <th>593</th>
      <td>hay river</td>
      <td>60.82</td>
      <td>35.6</td>
      <td>47</td>
      <td>20</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>594</th>
      <td>kieta</td>
      <td>-6.22</td>
      <td>78.92</td>
      <td>100</td>
      <td>92</td>
      <td>4.94</td>
    </tr>
    <tr>
      <th>595</th>
      <td>awjilah</td>
      <td>29.14</td>
      <td>71.99</td>
      <td>60</td>
      <td>0</td>
      <td>4.94</td>
    </tr>
    <tr>
      <th>596</th>
      <td>zonguldak</td>
      <td>41.25</td>
      <td>62.6</td>
      <td>82</td>
      <td>40</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>597</th>
      <td>susaki</td>
      <td>33.42</td>
      <td>80.6</td>
      <td>69</td>
      <td>40</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>598</th>
      <td>baikunthpur</td>
      <td>23.26</td>
      <td>84.23</td>
      <td>79</td>
      <td>0</td>
      <td>8.63</td>
    </tr>
    <tr>
      <th>599</th>
      <td>sabancuy</td>
      <td>18.97</td>
      <td>80.81</td>
      <td>100</td>
      <td>24</td>
      <td>7.96</td>
    </tr>
    <tr>
      <th>600</th>
      <td>revda</td>
      <td>67.94</td>
      <td>48.41</td>
      <td>78</td>
      <td>92</td>
      <td>11.77</td>
    </tr>
    <tr>
      <th>601</th>
      <td>north bend</td>
      <td>43.41</td>
      <td>53.96</td>
      <td>96</td>
      <td>1</td>
      <td>3.94</td>
    </tr>
    <tr>
      <th>602</th>
      <td>barbar</td>
      <td>NaN</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>603</th>
      <td>lodja</td>
      <td>-3.52</td>
      <td>76.67</td>
      <td>82</td>
      <td>8</td>
      <td>4.61</td>
    </tr>
    <tr>
      <th>604</th>
      <td>acuna</td>
      <td>NaN</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>605</th>
      <td>utiroa</td>
      <td>NaN</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>606</th>
      <td>wainwright</td>
      <td>52.84</td>
      <td>31.58</td>
      <td>89</td>
      <td>92</td>
      <td>10.54</td>
    </tr>
    <tr>
      <th>607</th>
      <td>nisia floresta</td>
      <td>-6.09</td>
      <td>71.6</td>
      <td>88</td>
      <td>20</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>608</th>
      <td>khapa</td>
      <td>21.42</td>
      <td>86</td>
      <td>70</td>
      <td>40</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>609</th>
      <td>karpathos</td>
      <td>35.51</td>
      <td>77</td>
      <td>69</td>
      <td>20</td>
      <td>23.04</td>
    </tr>
  </tbody>
</table>
<p>610 rows × 6 columns</p>
</div>




```python
city_dropped_df=city_df.dropna().reset_index(drop=True)
city_dropped_df
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
      <th>cities</th>
      <th>Lat</th>
      <th>Temperature</th>
      <th>Humidity</th>
      <th>Cloudiness (%)</th>
      <th>Wind Speed (mph)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>carutapera</td>
      <td>-1.20</td>
      <td>77.93</td>
      <td>87</td>
      <td>0</td>
      <td>9.42</td>
    </tr>
    <tr>
      <th>1</th>
      <td>hamilton</td>
      <td>32.30</td>
      <td>78.8</td>
      <td>69</td>
      <td>40</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>2</th>
      <td>shimoda</td>
      <td>34.70</td>
      <td>78.8</td>
      <td>74</td>
      <td>40</td>
      <td>14.99</td>
    </tr>
    <tr>
      <th>3</th>
      <td>wattegama</td>
      <td>7.35</td>
      <td>83.87</td>
      <td>66</td>
      <td>64</td>
      <td>7.18</td>
    </tr>
    <tr>
      <th>4</th>
      <td>salalah</td>
      <td>17.01</td>
      <td>78.8</td>
      <td>74</td>
      <td>75</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>5</th>
      <td>iqaluit</td>
      <td>63.75</td>
      <td>28.7</td>
      <td>100</td>
      <td>80</td>
      <td>8.63</td>
    </tr>
    <tr>
      <th>6</th>
      <td>rikitea</td>
      <td>-23.12</td>
      <td>70.37</td>
      <td>100</td>
      <td>92</td>
      <td>7.4</td>
    </tr>
    <tr>
      <th>7</th>
      <td>kargil</td>
      <td>34.56</td>
      <td>33.02</td>
      <td>94</td>
      <td>92</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>puerto ayora</td>
      <td>-0.74</td>
      <td>68.48</td>
      <td>100</td>
      <td>0</td>
      <td>9.53</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ushuaia</td>
      <td>-54.81</td>
      <td>32</td>
      <td>100</td>
      <td>90</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>10</th>
      <td>chuy</td>
      <td>-33.69</td>
      <td>65.24</td>
      <td>99</td>
      <td>92</td>
      <td>4.16</td>
    </tr>
    <tr>
      <th>11</th>
      <td>dikson</td>
      <td>73.51</td>
      <td>41.48</td>
      <td>91</td>
      <td>92</td>
      <td>8.52</td>
    </tr>
    <tr>
      <th>12</th>
      <td>cape town</td>
      <td>-33.93</td>
      <td>59</td>
      <td>67</td>
      <td>0</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>13</th>
      <td>nikolskoye</td>
      <td>59.70</td>
      <td>50</td>
      <td>87</td>
      <td>20</td>
      <td>15.66</td>
    </tr>
    <tr>
      <th>14</th>
      <td>qaanaaq</td>
      <td>77.48</td>
      <td>15.56</td>
      <td>100</td>
      <td>0</td>
      <td>9.86</td>
    </tr>
    <tr>
      <th>15</th>
      <td>banfora</td>
      <td>10.64</td>
      <td>71.36</td>
      <td>98</td>
      <td>76</td>
      <td>6.06</td>
    </tr>
    <tr>
      <th>16</th>
      <td>saskylakh</td>
      <td>71.97</td>
      <td>40.31</td>
      <td>91</td>
      <td>80</td>
      <td>5.17</td>
    </tr>
    <tr>
      <th>17</th>
      <td>mayumba</td>
      <td>-3.44</td>
      <td>75.23</td>
      <td>99</td>
      <td>68</td>
      <td>4.05</td>
    </tr>
    <tr>
      <th>18</th>
      <td>kaitangata</td>
      <td>-46.28</td>
      <td>45.08</td>
      <td>90</td>
      <td>92</td>
      <td>13.44</td>
    </tr>
    <tr>
      <th>19</th>
      <td>hasaki</td>
      <td>35.73</td>
      <td>79.65</td>
      <td>54</td>
      <td>40</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>20</th>
      <td>torbay</td>
      <td>47.66</td>
      <td>45.35</td>
      <td>100</td>
      <td>0</td>
      <td>12.55</td>
    </tr>
    <tr>
      <th>21</th>
      <td>jamestown</td>
      <td>-33.21</td>
      <td>69.2</td>
      <td>28</td>
      <td>20</td>
      <td>11.21</td>
    </tr>
    <tr>
      <th>22</th>
      <td>mahebourg</td>
      <td>-20.41</td>
      <td>78.8</td>
      <td>65</td>
      <td>40</td>
      <td>17.22</td>
    </tr>
    <tr>
      <th>23</th>
      <td>kinsale</td>
      <td>51.71</td>
      <td>44.6</td>
      <td>93</td>
      <td>40</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>24</th>
      <td>albany</td>
      <td>42.65</td>
      <td>46.98</td>
      <td>76</td>
      <td>90</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>25</th>
      <td>hilo</td>
      <td>19.71</td>
      <td>75.92</td>
      <td>79</td>
      <td>75</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>26</th>
      <td>mataura</td>
      <td>-46.19</td>
      <td>46.07</td>
      <td>82</td>
      <td>76</td>
      <td>12.44</td>
    </tr>
    <tr>
      <th>27</th>
      <td>champerico</td>
      <td>16.38</td>
      <td>70.91</td>
      <td>87</td>
      <td>64</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>28</th>
      <td>troitsko-pechorsk</td>
      <td>62.71</td>
      <td>56.87</td>
      <td>91</td>
      <td>92</td>
      <td>6.06</td>
    </tr>
    <tr>
      <th>29</th>
      <td>komsomolskiy</td>
      <td>67.55</td>
      <td>54.71</td>
      <td>97</td>
      <td>92</td>
      <td>15.35</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>507</th>
      <td>belaya gora</td>
      <td>68.54</td>
      <td>38.42</td>
      <td>82</td>
      <td>80</td>
      <td>4.61</td>
    </tr>
    <tr>
      <th>508</th>
      <td>san antonio</td>
      <td>-33.58</td>
      <td>51.8</td>
      <td>100</td>
      <td>75</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>509</th>
      <td>shirokiy</td>
      <td>53.87</td>
      <td>66.23</td>
      <td>48</td>
      <td>80</td>
      <td>8.3</td>
    </tr>
    <tr>
      <th>510</th>
      <td>saint-georges</td>
      <td>46.12</td>
      <td>41.3</td>
      <td>81</td>
      <td>20</td>
      <td>5.06</td>
    </tr>
    <tr>
      <th>511</th>
      <td>rudnogorsk</td>
      <td>57.27</td>
      <td>57.23</td>
      <td>49</td>
      <td>0</td>
      <td>3.83</td>
    </tr>
    <tr>
      <th>512</th>
      <td>bubaque</td>
      <td>11.28</td>
      <td>80.27</td>
      <td>100</td>
      <td>48</td>
      <td>11.88</td>
    </tr>
    <tr>
      <th>513</th>
      <td>manokwari</td>
      <td>-0.87</td>
      <td>82.43</td>
      <td>100</td>
      <td>24</td>
      <td>3.38</td>
    </tr>
    <tr>
      <th>514</th>
      <td>rettikhovka</td>
      <td>44.17</td>
      <td>63.53</td>
      <td>76</td>
      <td>56</td>
      <td>7.18</td>
    </tr>
    <tr>
      <th>515</th>
      <td>karmaskaly</td>
      <td>54.37</td>
      <td>59</td>
      <td>100</td>
      <td>75</td>
      <td>2.24</td>
    </tr>
    <tr>
      <th>516</th>
      <td>lethem</td>
      <td>3.38</td>
      <td>81.35</td>
      <td>64</td>
      <td>8</td>
      <td>11.32</td>
    </tr>
    <tr>
      <th>517</th>
      <td>uruguaiana</td>
      <td>-29.77</td>
      <td>78.8</td>
      <td>83</td>
      <td>0</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>518</th>
      <td>montecristo</td>
      <td>8.30</td>
      <td>72.53</td>
      <td>100</td>
      <td>88</td>
      <td>2.15</td>
    </tr>
    <tr>
      <th>519</th>
      <td>wellington</td>
      <td>-41.29</td>
      <td>53.6</td>
      <td>76</td>
      <td>0</td>
      <td>21.92</td>
    </tr>
    <tr>
      <th>520</th>
      <td>lorengau</td>
      <td>-2.02</td>
      <td>84.41</td>
      <td>100</td>
      <td>64</td>
      <td>4.83</td>
    </tr>
    <tr>
      <th>521</th>
      <td>rondonopolis</td>
      <td>-16.46</td>
      <td>70.91</td>
      <td>85</td>
      <td>0</td>
      <td>2.59</td>
    </tr>
    <tr>
      <th>522</th>
      <td>samarai</td>
      <td>-10.62</td>
      <td>78.2</td>
      <td>99</td>
      <td>88</td>
      <td>18.03</td>
    </tr>
    <tr>
      <th>523</th>
      <td>hay river</td>
      <td>60.82</td>
      <td>35.6</td>
      <td>47</td>
      <td>20</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>524</th>
      <td>kieta</td>
      <td>-6.22</td>
      <td>78.92</td>
      <td>100</td>
      <td>92</td>
      <td>4.94</td>
    </tr>
    <tr>
      <th>525</th>
      <td>awjilah</td>
      <td>29.14</td>
      <td>71.99</td>
      <td>60</td>
      <td>0</td>
      <td>4.94</td>
    </tr>
    <tr>
      <th>526</th>
      <td>zonguldak</td>
      <td>41.25</td>
      <td>62.6</td>
      <td>82</td>
      <td>40</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>527</th>
      <td>susaki</td>
      <td>33.42</td>
      <td>80.6</td>
      <td>69</td>
      <td>40</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>528</th>
      <td>baikunthpur</td>
      <td>23.26</td>
      <td>84.23</td>
      <td>79</td>
      <td>0</td>
      <td>8.63</td>
    </tr>
    <tr>
      <th>529</th>
      <td>sabancuy</td>
      <td>18.97</td>
      <td>80.81</td>
      <td>100</td>
      <td>24</td>
      <td>7.96</td>
    </tr>
    <tr>
      <th>530</th>
      <td>revda</td>
      <td>67.94</td>
      <td>48.41</td>
      <td>78</td>
      <td>92</td>
      <td>11.77</td>
    </tr>
    <tr>
      <th>531</th>
      <td>north bend</td>
      <td>43.41</td>
      <td>53.96</td>
      <td>96</td>
      <td>1</td>
      <td>3.94</td>
    </tr>
    <tr>
      <th>532</th>
      <td>lodja</td>
      <td>-3.52</td>
      <td>76.67</td>
      <td>82</td>
      <td>8</td>
      <td>4.61</td>
    </tr>
    <tr>
      <th>533</th>
      <td>wainwright</td>
      <td>52.84</td>
      <td>31.58</td>
      <td>89</td>
      <td>92</td>
      <td>10.54</td>
    </tr>
    <tr>
      <th>534</th>
      <td>nisia floresta</td>
      <td>-6.09</td>
      <td>71.6</td>
      <td>88</td>
      <td>20</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>535</th>
      <td>khapa</td>
      <td>21.42</td>
      <td>86</td>
      <td>70</td>
      <td>40</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>536</th>
      <td>karpathos</td>
      <td>35.51</td>
      <td>77</td>
      <td>69</td>
      <td>20</td>
      <td>23.04</td>
    </tr>
  </tbody>
</table>
<p>537 rows × 6 columns</p>
</div>




```python
city_dropped_df.loc[:,'Lat':'Wind Speed (mph)'] = city_dropped_df.loc[:,'Lat':'Wind Speed (mph)'].astype(float)

```


```python
city_dropped_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 537 entries, 0 to 536
    Data columns (total 6 columns):
    cities              537 non-null object
    Lat                 537 non-null float64
    Temperature         537 non-null float64
    Humidity            537 non-null float64
    Cloudiness (%)      537 non-null float64
    Wind Speed (mph)    537 non-null float64
    dtypes: float64(5), object(1)
    memory usage: 25.2+ KB
    


```python
city_dropped_df
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
      <th>cities</th>
      <th>Lat</th>
      <th>Temperature</th>
      <th>Humidity</th>
      <th>Cloudiness (%)</th>
      <th>Wind Speed (mph)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>carutapera</td>
      <td>-1.20</td>
      <td>77.93</td>
      <td>87.0</td>
      <td>0.0</td>
      <td>9.42</td>
    </tr>
    <tr>
      <th>1</th>
      <td>hamilton</td>
      <td>32.30</td>
      <td>78.80</td>
      <td>69.0</td>
      <td>40.0</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>2</th>
      <td>shimoda</td>
      <td>34.70</td>
      <td>78.80</td>
      <td>74.0</td>
      <td>40.0</td>
      <td>14.99</td>
    </tr>
    <tr>
      <th>3</th>
      <td>wattegama</td>
      <td>7.35</td>
      <td>83.87</td>
      <td>66.0</td>
      <td>64.0</td>
      <td>7.18</td>
    </tr>
    <tr>
      <th>4</th>
      <td>salalah</td>
      <td>17.01</td>
      <td>78.80</td>
      <td>74.0</td>
      <td>75.0</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>5</th>
      <td>iqaluit</td>
      <td>63.75</td>
      <td>28.70</td>
      <td>100.0</td>
      <td>80.0</td>
      <td>8.63</td>
    </tr>
    <tr>
      <th>6</th>
      <td>rikitea</td>
      <td>-23.12</td>
      <td>70.37</td>
      <td>100.0</td>
      <td>92.0</td>
      <td>7.40</td>
    </tr>
    <tr>
      <th>7</th>
      <td>kargil</td>
      <td>34.56</td>
      <td>33.02</td>
      <td>94.0</td>
      <td>92.0</td>
      <td>1.70</td>
    </tr>
    <tr>
      <th>8</th>
      <td>puerto ayora</td>
      <td>-0.74</td>
      <td>68.48</td>
      <td>100.0</td>
      <td>0.0</td>
      <td>9.53</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ushuaia</td>
      <td>-54.81</td>
      <td>32.00</td>
      <td>100.0</td>
      <td>90.0</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>10</th>
      <td>chuy</td>
      <td>-33.69</td>
      <td>65.24</td>
      <td>99.0</td>
      <td>92.0</td>
      <td>4.16</td>
    </tr>
    <tr>
      <th>11</th>
      <td>dikson</td>
      <td>73.51</td>
      <td>41.48</td>
      <td>91.0</td>
      <td>92.0</td>
      <td>8.52</td>
    </tr>
    <tr>
      <th>12</th>
      <td>cape town</td>
      <td>-33.93</td>
      <td>59.00</td>
      <td>67.0</td>
      <td>0.0</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>13</th>
      <td>nikolskoye</td>
      <td>59.70</td>
      <td>50.00</td>
      <td>87.0</td>
      <td>20.0</td>
      <td>15.66</td>
    </tr>
    <tr>
      <th>14</th>
      <td>qaanaaq</td>
      <td>77.48</td>
      <td>15.56</td>
      <td>100.0</td>
      <td>0.0</td>
      <td>9.86</td>
    </tr>
    <tr>
      <th>15</th>
      <td>banfora</td>
      <td>10.64</td>
      <td>71.36</td>
      <td>98.0</td>
      <td>76.0</td>
      <td>6.06</td>
    </tr>
    <tr>
      <th>16</th>
      <td>saskylakh</td>
      <td>71.97</td>
      <td>40.31</td>
      <td>91.0</td>
      <td>80.0</td>
      <td>5.17</td>
    </tr>
    <tr>
      <th>17</th>
      <td>mayumba</td>
      <td>-3.44</td>
      <td>75.23</td>
      <td>99.0</td>
      <td>68.0</td>
      <td>4.05</td>
    </tr>
    <tr>
      <th>18</th>
      <td>kaitangata</td>
      <td>-46.28</td>
      <td>45.08</td>
      <td>90.0</td>
      <td>92.0</td>
      <td>13.44</td>
    </tr>
    <tr>
      <th>19</th>
      <td>hasaki</td>
      <td>35.73</td>
      <td>79.65</td>
      <td>54.0</td>
      <td>40.0</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>20</th>
      <td>torbay</td>
      <td>47.66</td>
      <td>45.35</td>
      <td>100.0</td>
      <td>0.0</td>
      <td>12.55</td>
    </tr>
    <tr>
      <th>21</th>
      <td>jamestown</td>
      <td>-33.21</td>
      <td>69.20</td>
      <td>28.0</td>
      <td>20.0</td>
      <td>11.21</td>
    </tr>
    <tr>
      <th>22</th>
      <td>mahebourg</td>
      <td>-20.41</td>
      <td>78.80</td>
      <td>65.0</td>
      <td>40.0</td>
      <td>17.22</td>
    </tr>
    <tr>
      <th>23</th>
      <td>kinsale</td>
      <td>51.71</td>
      <td>44.60</td>
      <td>93.0</td>
      <td>40.0</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>24</th>
      <td>albany</td>
      <td>42.65</td>
      <td>46.98</td>
      <td>76.0</td>
      <td>90.0</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>25</th>
      <td>hilo</td>
      <td>19.71</td>
      <td>75.92</td>
      <td>79.0</td>
      <td>75.0</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>26</th>
      <td>mataura</td>
      <td>-46.19</td>
      <td>46.07</td>
      <td>82.0</td>
      <td>76.0</td>
      <td>12.44</td>
    </tr>
    <tr>
      <th>27</th>
      <td>champerico</td>
      <td>16.38</td>
      <td>70.91</td>
      <td>87.0</td>
      <td>64.0</td>
      <td>1.70</td>
    </tr>
    <tr>
      <th>28</th>
      <td>troitsko-pechorsk</td>
      <td>62.71</td>
      <td>56.87</td>
      <td>91.0</td>
      <td>92.0</td>
      <td>6.06</td>
    </tr>
    <tr>
      <th>29</th>
      <td>komsomolskiy</td>
      <td>67.55</td>
      <td>54.71</td>
      <td>97.0</td>
      <td>92.0</td>
      <td>15.35</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>507</th>
      <td>belaya gora</td>
      <td>68.54</td>
      <td>38.42</td>
      <td>82.0</td>
      <td>80.0</td>
      <td>4.61</td>
    </tr>
    <tr>
      <th>508</th>
      <td>san antonio</td>
      <td>-33.58</td>
      <td>51.80</td>
      <td>100.0</td>
      <td>75.0</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>509</th>
      <td>shirokiy</td>
      <td>53.87</td>
      <td>66.23</td>
      <td>48.0</td>
      <td>80.0</td>
      <td>8.30</td>
    </tr>
    <tr>
      <th>510</th>
      <td>saint-georges</td>
      <td>46.12</td>
      <td>41.30</td>
      <td>81.0</td>
      <td>20.0</td>
      <td>5.06</td>
    </tr>
    <tr>
      <th>511</th>
      <td>rudnogorsk</td>
      <td>57.27</td>
      <td>57.23</td>
      <td>49.0</td>
      <td>0.0</td>
      <td>3.83</td>
    </tr>
    <tr>
      <th>512</th>
      <td>bubaque</td>
      <td>11.28</td>
      <td>80.27</td>
      <td>100.0</td>
      <td>48.0</td>
      <td>11.88</td>
    </tr>
    <tr>
      <th>513</th>
      <td>manokwari</td>
      <td>-0.87</td>
      <td>82.43</td>
      <td>100.0</td>
      <td>24.0</td>
      <td>3.38</td>
    </tr>
    <tr>
      <th>514</th>
      <td>rettikhovka</td>
      <td>44.17</td>
      <td>63.53</td>
      <td>76.0</td>
      <td>56.0</td>
      <td>7.18</td>
    </tr>
    <tr>
      <th>515</th>
      <td>karmaskaly</td>
      <td>54.37</td>
      <td>59.00</td>
      <td>100.0</td>
      <td>75.0</td>
      <td>2.24</td>
    </tr>
    <tr>
      <th>516</th>
      <td>lethem</td>
      <td>3.38</td>
      <td>81.35</td>
      <td>64.0</td>
      <td>8.0</td>
      <td>11.32</td>
    </tr>
    <tr>
      <th>517</th>
      <td>uruguaiana</td>
      <td>-29.77</td>
      <td>78.80</td>
      <td>83.0</td>
      <td>0.0</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>518</th>
      <td>montecristo</td>
      <td>8.30</td>
      <td>72.53</td>
      <td>100.0</td>
      <td>88.0</td>
      <td>2.15</td>
    </tr>
    <tr>
      <th>519</th>
      <td>wellington</td>
      <td>-41.29</td>
      <td>53.60</td>
      <td>76.0</td>
      <td>0.0</td>
      <td>21.92</td>
    </tr>
    <tr>
      <th>520</th>
      <td>lorengau</td>
      <td>-2.02</td>
      <td>84.41</td>
      <td>100.0</td>
      <td>64.0</td>
      <td>4.83</td>
    </tr>
    <tr>
      <th>521</th>
      <td>rondonopolis</td>
      <td>-16.46</td>
      <td>70.91</td>
      <td>85.0</td>
      <td>0.0</td>
      <td>2.59</td>
    </tr>
    <tr>
      <th>522</th>
      <td>samarai</td>
      <td>-10.62</td>
      <td>78.20</td>
      <td>99.0</td>
      <td>88.0</td>
      <td>18.03</td>
    </tr>
    <tr>
      <th>523</th>
      <td>hay river</td>
      <td>60.82</td>
      <td>35.60</td>
      <td>47.0</td>
      <td>20.0</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>524</th>
      <td>kieta</td>
      <td>-6.22</td>
      <td>78.92</td>
      <td>100.0</td>
      <td>92.0</td>
      <td>4.94</td>
    </tr>
    <tr>
      <th>525</th>
      <td>awjilah</td>
      <td>29.14</td>
      <td>71.99</td>
      <td>60.0</td>
      <td>0.0</td>
      <td>4.94</td>
    </tr>
    <tr>
      <th>526</th>
      <td>zonguldak</td>
      <td>41.25</td>
      <td>62.60</td>
      <td>82.0</td>
      <td>40.0</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>527</th>
      <td>susaki</td>
      <td>33.42</td>
      <td>80.60</td>
      <td>69.0</td>
      <td>40.0</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>528</th>
      <td>baikunthpur</td>
      <td>23.26</td>
      <td>84.23</td>
      <td>79.0</td>
      <td>0.0</td>
      <td>8.63</td>
    </tr>
    <tr>
      <th>529</th>
      <td>sabancuy</td>
      <td>18.97</td>
      <td>80.81</td>
      <td>100.0</td>
      <td>24.0</td>
      <td>7.96</td>
    </tr>
    <tr>
      <th>530</th>
      <td>revda</td>
      <td>67.94</td>
      <td>48.41</td>
      <td>78.0</td>
      <td>92.0</td>
      <td>11.77</td>
    </tr>
    <tr>
      <th>531</th>
      <td>north bend</td>
      <td>43.41</td>
      <td>53.96</td>
      <td>96.0</td>
      <td>1.0</td>
      <td>3.94</td>
    </tr>
    <tr>
      <th>532</th>
      <td>lodja</td>
      <td>-3.52</td>
      <td>76.67</td>
      <td>82.0</td>
      <td>8.0</td>
      <td>4.61</td>
    </tr>
    <tr>
      <th>533</th>
      <td>wainwright</td>
      <td>52.84</td>
      <td>31.58</td>
      <td>89.0</td>
      <td>92.0</td>
      <td>10.54</td>
    </tr>
    <tr>
      <th>534</th>
      <td>nisia floresta</td>
      <td>-6.09</td>
      <td>71.60</td>
      <td>88.0</td>
      <td>20.0</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>535</th>
      <td>khapa</td>
      <td>21.42</td>
      <td>86.00</td>
      <td>70.0</td>
      <td>40.0</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>536</th>
      <td>karpathos</td>
      <td>35.51</td>
      <td>77.00</td>
      <td>69.0</td>
      <td>20.0</td>
      <td>23.04</td>
    </tr>
  </tbody>
</table>
<p>537 rows × 6 columns</p>
</div>




```python
def scatter_plot(x,y,info):
    plt.figure(figsize=(10,7))
    #plt.scatter(city_dropped_df["Lat"], city_dropped_df["Temperature"])
    plt.scatter(x, y)
    plt.title(info[0], fontsize=20)
    plt.ylabel(info[1], fontsize=14)
    plt.xlabel(info[2], fontsize=14)
    plt.ylim(-10, 1.2*max(y))
    plt.xlim(-100, 100)
    pic_name = ''.join(list(info[1])[0:4])+"_vs_Lat.png"
    print(pic_name)
    plt.savefig(pic_name)
    plt.show()
temp = ["Temperature (F) vs. City Latitude","Temperature (F)","Latitude"]
scatter_plot(city_dropped_df["Lat"],city_dropped_df["Temperature"],temp)
```

    Temp_vs_Lat.png
    


![png](WeatherPy_files/WeatherPy_14_1.png)



```python
humid = ["Humidity vs. City Latitude","Humidity","Latitude"]
scatter_plot(city_dropped_df["Lat"],city_dropped_df["Humidity"],humid)
```

    Humi_vs_Lat.png
    


![png](WeatherPy_files/WeatherPy_15_1.png)



```python
cloud = ["Cloudiness vs. City Latitude","Cloudiness(%)","Latitude"]
scatter_plot(city_dropped_df["Lat"],city_dropped_df["Cloudiness (%)"],cloud)
```

    Clou_vs_Lat.png
    


![png](WeatherPy_files/WeatherPy_16_1.png)



```python
wind = ["Wind Speed vs. City Latitude","Wind Speed (mph)","Latitude"]
scatter_plot(city_dropped_df["Lat"],city_dropped_df["Wind Speed (mph)"],wind)
```

    Wind_vs_Lat.png
    


![png](WeatherPy_files/WeatherPy_17_1.png)



```python
city_dropped_df.to_csv("WeatherPy.csv")

```
