# News scraper

##### English versión [here](https://github.com/margarcuae/news_scraper)


Este es un scraper que  extrae las 📰 noticias de diferentes periódicos online/digitales y los almacena en archivos CSV. Actualmente se encuentra configurado para extraer las noticias de los periódicos [El universal](http://www.eluniversal.com.mx) y [El País](https://elpais.com). Pero también funciona para otros, basta con añadir las variables en el archivo `config.yaml`. 


## Requisitos
* Python 

  * beautiful soup 4
  * requests 
  * yaml

Puedes instalarlos así:
* Con pip

```
pip3 install bs4
pip3 install requests
pip3 install yaml
```
* Con conda:
```
conda create --name scraper_news pandas requests beautifulsoup4 yaml
```

## Ejecución

Con este comando se extraerá las noticias del diario El Universal especificado en el 📂 archivo `config.yaml`

```
python main.py eluniversal
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


