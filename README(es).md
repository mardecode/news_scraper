# News scraper

##### English version [here](https://github.com/margarcuae/news_scraper)

## Descripción

Este es un scraper que  extrae las 📰 noticias de diferentes periódicos online/digitales, limpia y corrige los datos  para finalmente guardarlo en una base de datos. 

Actualmente se encuentra configurado para extraer las noticias de los periódicos [El universal](http://www.eluniversal.com.mx) y [El País](https://elpais.com). Pero también funciona para otros, basta con añadir las variables en el archivo `config.yaml`. 


## Requisitos
* Python 

  * beautiful soup 4
  * requests 
  * yaml
  * pandas
  * nltk 
  * sqlalchemy

Los requisitos específicos se encuentran en el archivo `news_scraper.yml` , el cual puedes clonarlo con conda 

```
conda env create --file news_scraper.yml
conda activate scraper_news
```

## Ejecución
El archivo `pipeline.py` realizará las siguientes tareas:
* **Extracción:** Scraper de las noticias en un archivo csv.
* **Transformación:**  Limpieza de los datos.
* **Carga:** Almacenamiento de los datos a una dase datos SQLite.

Para ejecutar: 
```
python pipeline.py
```

## Configuración

Se puede añadir más diarios en el 📂 archivo `config.yaml`, este archivo necesita los siguientes datos
* NAME = nombre del diario
* LINK = enlace a la página del diario 
* QUERY_1 = query para obtener el link de los artículos 
* QUERY_2 = query para obtener el titulo
* QUERY_3 = query para obtener el contenido

> Las QUERIES deben ser especificadas en la sintaxis de consulta de `bs4`. Puedes encontrar su documentación [aquí](https://beautiful-soup-4.readthedocs.io/en/latest/)

Se debe seguir la siguiente configuración
```
NAME:
  url: LINK
  queries:
    homepage_article_links: 'QUERY_1'
    article_tirle: 'QUERY_2
    article_body: 'QUERY3
```


config.yaml
```
news_sites:
  eluniversal:
    url: http://www.eluniversal.com.mx
    queries:
      homepage_article_links : '.bsg-Macrogaleria_Titulo a, .titulo a'
      article_title: '.Encabezado-Articulo h1, .ceh-Opinion_Titulo'
      article_body: '.field-name-body'
  elpais:
    url: https://elpais.com
    queries:
      homepage_article_links : 'header h2.c_t a'
      article_title: '.a_e_txt h1.a_t'
      article_body: '.a_c'

```

Adicionalmente se debe añadir `NAME` en el archivo pipeline.py 

```
news_sites_uids = ['eluniversal', 'elpais',NAME]

```