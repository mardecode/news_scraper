# News scraper
##### Versión en español [aquí](https://github.com/margarcuae/news_scraper/blob/main/README(es).md)


## Description

This scraper extracts the 📰 news from different online/digital newspapers and cleans the data to save it in a database.

It is currently configured to extract news from the newspapers [El universal](http://www.eluniversal.com.mx) and [El País](https://elpais.com). But it works for others too; just add the variables in the `config.yaml` file. 

## Requirements
* Python 

  * beautiful soup 4
  * requests 
  * yaml
  * pandas
  * nltk 
  * sqlalchemy

The specific requirements are in the `news_scraper.yml` file, which you can clone with conda

```
conda env create --file news_scraper.yml
conda activate scraper_news
```

## Execution

The `pipeline.py` file will run the following task:
* **Extraction:** Scraper of the news in a CSV file.
* **Transformation:** Data cleaning.
* **Load:** Storage of the data to an SQLite database.

To execute: 
```
python pipeline.py
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

Additionally, you must add `NAME` in the pipeline.py file

```
news_sites_uids = ['eluniversal', 'elpais',NAME]

```
