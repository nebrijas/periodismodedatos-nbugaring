# Actividad dirigida 3

En la AD3 vamos a aprender a usar bases de datos y procesar gráficas. Para ello, leeremos de la URL: https://api.covid19api.com/countries los datos de los países España, Colombia y Argentina. Para leer estos datos usaremos la función de Panda que se llama ´read_json´. Estos datos se guardarán en diferente variables llamadas df_es, df_co y df_arg, siendo del tipo DataFrame.


Una vez tengamos estos datos, primero mostraremos en una gráfica los datos de España, para ello usaremos la función ´set_index´ para coger solo las columnas que nos interesan (date y cases) y a continuación con la función ´plot´ mostraremos dicha gráfica.


Para el siguiente apartado mostraremos en una gráfica los datos de covid en España y en Colombia correspondientes al mismo periodo de tiempo. Para ello, usaremos la función ´set_index´ para guardar los datos que nos interesan, tanto de España como de Colombia. A continuación, juntaremos las tablas de los datos anteriores obteniendo como resultado una tabla en la cual la primera columna corresponde a la fecha, la segunda a los datos de Covid19 en España y la tercera en Colombia. Una vez tengamos esto, con la función ´plot´ mostraremos la gráfica donde se observan los datos de ambos países.

El resultado lo podemos ver en la siguiente imagen:   
![Grafico covid](https://nebrijas.github.io/periodismodedatos-nbugaring/api-covid19-pandas-plot.png)


Por último, haremos el proceso anterior pero incorporando los datos de un país más, en este caso Argentina. El resultado de esto es un plot donde se muestra los casos de Covid19 en los tres países.


## CÓDIGO BRUTO


```
!pip install pandas
import pandas as pd
url = 'https://api.covid19api.com/countries'
df = pd.read_json(url)
df.head()
df.tail()
df.info()
df['Country']
df['Country'][200]
url_live = 'https://api.covid19api.com/country/spain/status/confirmed/live'
df_es = pd.read_json(url_live)
df_es
df_es.info()
df_es.set_index('Date')
df_es.set_index('Date')['Cases']
df_es.set_index('Date')['Cases'].plot(title="Casos de Covid19 en España")
url_co = 'https://api.covid19api.com/country/colombia/status/confirmed/live'
df_co = pd.read_json(url_co)
df_co.set_index('Date')['Cases'].plot(title="Datos de Covid19 en Colombia")
casos_es = df_es.set_index('Date')['Cases']
casos_co = df_co.set_index('Date')['Cases']
pd.concat([casos_es,casos_co],axis=1)
vs = pd.concat([casos_es,casos_co],axis=1)
vs.columns = ['España','Colombia']
vs.plot(title="España Vs Colombia", kind='area')
url_arg = 'https://api.covid19api.com/country/argentina/status/confirmed/live'
df_arg = pd.read_json(url_arg)
df_arg.set_index('Date')['Cases'].plot(title="Datos de Covid19 en Argentina")
casos_es = df_es.set_index('Date')['Cases']
casos_co = df_co.set_index('Date')['Cases']
casos_arg = df_arg.set_index('Date')['Cases']
pd.concat([casos_es,casos_co,casos_arg],axis=1)
vs1 = pd.concat([casos_es,casos_co,casos_arg],axis=1)
vs1.columns = ['España','Colombia','Argentina']
vs1.plot(title="España, Colombia y Argentina")
df_es.set_index('Date')[['Cases','Lon']]
vs.to_csv('vs.csv')
grafico = vs.plot()
fig = grafico.get_figure()
fig.savefig("vs.png")

```


## ENLACES ad3

[DATOS CSV](https://github.com/nebrijas/periodismodedatos-nbugaring/blob/main/api-covid19-pandas-plot.csv)   
[DATOS HTML](https://nebrijas.github.io/periodismodedatos-nbugaring/api-covid19-pandas-plot.html)   
[ENLACE JUPITER](https://github.com/nebrijas/periodismodedatos-nbugaring/blob/main/api-covid19-pandas-plot.html.ipynb)   
