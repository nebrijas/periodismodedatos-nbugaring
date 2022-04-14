# Actividad dirigida 4    


En esta practiva vamos a analizar la información de la url https://www.zaragoza.es/sede/servicio/transporte\ sobre los accidencentes de tráfico, con el objetivo de crear un mapa y añadirle marcadores.     

Primero importamos todas las librerias necesarias. Una vez hecho esto añadiremos a la variable url la dirección web de donde vamos a sacar los datos y en la variable coord las coordenadas que nosotros queremos.   

Con la función `folium.Map` creamos un mapa en las coordenadas que hemos añadido en la variable coord. Por otro lado con la función `pd.read_csv` leemos el csv que nos proporciona la url, delimitando su contenido con los ; que se encuentran dentro de ese fichero.   

El siguiente paso fue crear dos bucles, en los que el objetivo de ellos es conseguir dos arrays, uno para las longitudes y otro para las altitudes de los datos del DataFrame contenido en df. Los dos bucles tienen la siguiente forma:   
- for i in df['geometry']: - recorremos cada una de las filas del DataFrame
- longlat = i.split(',') - dividimos los datos de esa fila, teniendo en cuenta la como, es decir por una parte quedará lo que hay antes de ella y por otra lo que hay despues.
- longitudes += [float(longlat[0])] o latitudes += [float(longlat[1])] - añadimos al array lo que ha quedado delante de la coma o lo que hay despues de la coma, dependiendo si queremos las longitudes o las latitudes    

## AÑADIR MARCADOR EN EL MAPA   
Para añadir un marcador en el mapa, los pasos que vamos a seguir son los siguientes:
1. Añadimos a la variable coord las coordenadas que queremos
2. con la función folium.Map creamos el mapa, pasandole como paramatro las coordenadas anteriores y el tiles.
3. Creamos con la función folium.Marker, el marcador que nosotros queremos añadiendoles como parámetro el color del marcador
4. Añadimos con la función mapa.add_child() el marcador a nuestro mapa
5. Mostramos nuestro mapa    

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

## ENLACES ad4

[MAPA ITERATIVO HTML](https://nebrijas.github.io/periodismodedatos-nbugaring/tipo.html)   
[ENLACE JUPITER](https://github.com/nebrijas/periodismodedatos-nbugaring/blob/main/api-pandas-folium-raw.ipynb)   
