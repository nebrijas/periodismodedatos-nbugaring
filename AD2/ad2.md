#ACTIVIDAD DIRIGIDA 2


##COMENTARIO PROCESO


##CÓDIGO BRUTO


```
import requests
from bs4 import BeautifulSoup

URL = "https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"
req = requests.get(URL)
if (req.status_code != 200):
    raise Exception("No se puede hacer Web Scraping en"+ URL)
if (req.status_code == 200):
    print("Vamos a por ello")

html = BeautifulSoup(req.text, "html.parser")
paises = html.find_all("th",{"class":"pais"})
oros = html.find_all("td",{"class":"m_oro"})
platas = html.find_all("td",{"class":"m_plata"})
bronces = html.find_all("td",{"class":"m_bronce"})
totales = html.find_all("td",{"class":"m_total"})

respuesta=input('¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?\n \n Si tu respuesta es Sí, presiona "s" \n')
if(respuesta == 's'):
    print('Vale, vamos a ello')
    print('\nRESULTADOS DE LOS DATOS DE LOS JUEGOS OLÍMPICOS 2020\n')
    print ('PAÍSES')
    print(paises)
    for i in range (20):
    # Con el método "getText()" no nos devuelve el HTML
        print("%d. %s \nOro: %s Plata: %s Bronce: %s \n Total: %s \n " % (i+1, paises[i+1].text.strip(),oros[i].text.strip(),platas[i].text.strip(),bronces[i].text.strip(), totales[i].text.strip()))
    else:
        print('Qué lástima, y...')    
```
