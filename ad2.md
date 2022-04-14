# Actividad dirigida 2


## COMENTARIO PROCESO


En esta actividad explicaremos paso a paso el código de la AD2

### LIBRERÍAS

Importaremos la librería request y BeautifuSoup que nos facilitarán el trabajo a lo largo del proceso.

- La librería request nos facilitará el trabajo con peticiones HTTP
- La librería BeautifulSoup nos permitirá traducir el código a html

### VARIABLES

Las variables nos permitirán asociar datos concretos a un valor. Esto nos facilitará referirnos a él en diferentes partes del código. Podemos ver un ejemplo de ello es: URL = "https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"

### SOLICITUD

Solicitaremos a la web de El País los datos acerca del medallero de los juegos olímpicos a través de un request, asociandolo a la variable req. En este caso, si el status code no es 200, esta acción no podrá ejecutarse.

### VARIABLES DE DATOS

Definimos las variables paises, oros, etc para asociar la información encontrada en el fichero teniendo en cuenta los filtros que hemos establecido a la función find_all del código.

### LA PREGUNTA

Le preguntamos al usuario si quiere conocer los resultados que hemos solicitado previamente a la web de El País donde se muestran los resultados del medallero de los JJOO. La respuesta s por parte de los usuarios significará que quieren tener acceso a los 20 primeros países del medallero.

### OBTENCIÓN DE DATOS

A partir del resultado afirmativo por parte de los usuarios se procederá a la muestra de los datos. Aparecerá en pantalla un mensaje con los resultados ofrecidos por El País.

## CÓDIGO BRUTO


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


ENLACE SCRAPING: https://github.com/nebrijas/periodismodedatos-nbugaring/blob/main/scraping.ipynb
