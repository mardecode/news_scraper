# News scraper

##### English version [here](https://github.com/margarcuae/news_scraper)

## Descripci贸n

Este es un scraper que  extrae las 馃摪 noticias de diferentes peri贸dicos online/digitales, limpia y corrige los datos  para finalmente guardarlo en una base de datos. 

Actualmente se encuentra configurado para extraer las noticias de los peri贸dicos [El universal](http://www.eluniversal.com.mx) y [El Pa铆s](https://elpais.com). Pero tambi茅n funciona para otros, basta con a帽adir las variables en el archivo `config.yaml`. 


## Requisitos
* Python 

  * beautiful soup 4
  * requests 
  * yaml
  * pandas
  * nltk 
  * sqlalchemy

Los requisitos espec铆ficos se encuentran en el archivo `news_scraper.yml` , el cual puedes clonarlo con conda 

```
conda env create --file news_scraper.yml
conda activate scraper_news
```

## Ejecuci贸n
El archivo `pipeline.py` realizar谩 las siguientes tareas:
* **Extracci贸n:** Scraper de las noticias en un archivo csv.
* **Transformaci贸n:**  Limpieza de los datos.
* **Carga:** Almacenamiento de los datos a una dase datos SQLite.

Para ejecutar: 
```
python pipeline.py
```

## Configuraci贸n

Se puede a帽adir m谩s diarios en el 馃搨 archivo `config.yaml`, este archivo necesita los siguientes datos
* NAME = nombre del diario
* LINK = enlace a la p谩gina del diario 
* QUERY_1 = query para obtener el link de los art铆culos 
* QUERY_2 = query para obtener el titulo
* QUERY_3 = query para obtener el contenido

> Las QUERIES deben ser especificadas en la sintaxis de consulta de `bs4`. Puedes encontrar su documentaci贸n [aqu铆](https://beautiful-soup-4.readthedocs.io/en/latest/)

Se debe seguir la siguiente configuraci贸n
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

Adicionalmente se debe a帽adir `NAME` en el archivo pipeline.py 

```
news_sites_uids = ['eluniversal', 'elpais',NAME]

```