# News scraper
##### Versión en español [aquí](https://github.com/margarcuae/news_scraper/blob/main/README(es).md)

This  scraper  extracts news from different online/digital newspapers and stores them in CSV files. It is currently configured to extract news from the newspapers [El universal](http://www.eluniversal.com.mx) and [El País](https://elpais.com). But it works for others too; just add the variables in the `config.yaml` file. 


## Requirements
* Python 

  * beautiful soup 4
  * requests 
  * yaml

You can install them like this:
* With pip

```
pip3 install bs4
pip3 install request
pip3 install yaml
```
* With conda:
```
conda create --name news_scraper beautifulsoup4 request yaml
```

## Execution

With this command the news of the newspaper El Universal specified in the  📂 file `config.yaml` will be extracted.

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
## Settings

More newspaper can be added in the `config.yaml` file, this file needs the following data
* NAME = newspaper's name
* LINK = Link to newspaper page
* QUERY_1 = query to get the link to the articles
* QUERY_2 = query to get the title
* QUERY_3 = query to get the content

> QUERIES must be specified in the `bs4` query syntax. You can find its documentation [here](https://beautiful-soup-4.readthedocs.io/en/latest/).

You must follow the following configuration:
```
NAME:
  url: LINK
  queries:
    homepage_article_links: 'QUERY_1'
    article_tirle: 'QUERY_2
    article_body: 'QUERY3
```