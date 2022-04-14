# Actividad dirigida 4


## CÓDIGO BRUTO


```
!pip install pandas folium
import pandas as pd
import folium
url = 'https://www.zaragoza.es/sede/servicio/transporte\
/accidentalidad-trafico/accidente.csv?rows=20'
coord = [41.64,-0.88]
mapa = folium.Map(location=coord)
df = pd.read_csv(url,delimiter=';')
longitudes = []
for i in df['geometry']:
    longlat = i.split(',')
    longitudes += [float(longlat[0])]
latitudes = []
for i in df['geometry']:
    longlat = i.split(',')
    latitudes += [float(longlat[1])]
df_coord = pd.DataFrame({'long':longitudes,\
                         'lat':latitudes})
df_tipo = pd.concat([df['type'],df_coord],axis=1)
for index, fila in df_tipo.iterrows():
    marcador = folium.Marker([fila['lat'], fila['long']],\
                            popup=fila['type'])
    mapa.add_child(marcador)
mapa
coord = [40.535564,-3.6475137]
mapa = folium.Map(location=coord, tiles='Stamen Terrain')
marcador = folium.Marker (coord, icon=folium.Icon(color="green"))
mapa =mapa.add_child(marcador)
mapa
mapa.save('./tipo.html')
```
