# Actividad dirigida 3




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
