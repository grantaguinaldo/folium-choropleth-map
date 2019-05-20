

I'm new to folium and am having trouble plotting the zip code boundaries from a json file that contains a total of 1,769 zip codes.

My desired output is to have all of the zip code boundaries in California rendered on a map object, and the code that I am working with is below.

I feel that the problem area with my code is either [1] `geo_data=ca_json.json()['features']` or maybe the json object `ca_json`.

```
#Python 3.7.3
#folium==0.9.0

import folium 
import requests as r 
import json
from IPython.display import HTML

ca_json = r.get('https://raw.githubusercontent.com/OpenDataDE/State-zip-code-GeoJSON/master/ca_california_zip_codes_geo.min.json')
print(ca_json)

cali_map = folium.Map(location=[33.895847, -118.220070], zoom_start=12)
folium.Choropleth(geo_data=ca_json.json()['features'][512], 
                     fill_color='OrRd',
                     fill_opacity=0.2,
                     line_opacity=0.5,
                     key_on='feature.properties.ZCTA5CE10').add_to(cali_map)

cali_map.save('plot_data_2.html')
HTML('<iframe src=plot_data_2.html width=800 height=500></iframe>')
```

Using this code block, I can generate the map using **one** zip code (i.e, using element 512 of the json via `geo_data=ca_json.json()['features'][512]`), however, when I try to plot all of the zip codes in the json file (using `geo_data=ca_json.json()['features']`), I get the following error.

`ValueError: Cannot render objects with any missing geometries:` and the error continues to return entries from the json. 

From the error message, I understand that there is an error with the json file where one or more of the entries are incorrect, but I don't know how to correct the error. 

I've spent a few hours trying to figure this out and I am at a loss as to what to do next since I don't understand all of the inner workings of folium.

**Can someone help me understand why I can't plot all of the zip boundaries in the json file on my map object?**

