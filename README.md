![GitHub license](https://img.shields.io/github/license/jordanparker6/newsreader)

```
    _   __                                      __             ________    ____
   / | / /__ _      _______________  ____ _____/ /__  _____   / ____/ /   /  _/
  /  |/ / _ \ | /| / / ___/ ___/ _ \/ __ `/ __  / _ \/ ___/  / /   / /    / /  
 / /|  /  __/ |/ |/ (__  ) /  /  __/ /_/ / /_/ /  __/ /     / /___/ /____/ /   
/_/ |_/\___/|__/|__/____/_/   \___/\__,_/\__,_/\___/_/      \____/_____/___/   
                                                                               

Welcome to Newsreader CLI
```

# newsreader
A web-scraper, sentiment and entity analysis tool for market research.

This library includes the following features:
- A multi-threaded web-scraper implentation with an extendable interface.
- A collection of web-scrapers for building up a market research corpus.
- An NLP pipeline for Named Entity Recognition, Entity Linking with Wikidata and Sentiment Analysis.
- Feature extraction from Wikidata for linked entities.
- A relational data store for storing scraped articles, named entities and sentiment.
- A streamlit dashboard for interactive analysis and visualization.

### Quick Start

To install `newsreader` run the following command, `pip3 install https://github.com/jordanparker6/newsreader`.

After `newsreader` has been installed, run the CLI with `newsreader`.

Please note that the default setting will save the analyzed news articles to a sqlite database in your current directory.

### Contribute

Pull requests to add additional scrapers to the CLI are welcomed. To add a scraper, implement the `ScraperBase` interface defined at `newsreader/scrapers/base.py` within `newsreader/scrapers/all.py`. For reference, the `ScraperBase` interface is displayed below:

```python
ScraperBase(ABC)
    @abstractmethod
    def _find_documents(self, to: dt.datetime) -> Generator[Dict]:
        """
        Collect news records up to period 'to'. 

        Yield:
            Dict: Dictionary of article names, date and href.
        """
        raise NotImplementedError
    
    @abstractmethod
    def _scrape_document(self, href: str) -> str:
        """
        Collect text from the href of a collected news record.

        Return:
            str: The content of the article.
        """
        raise NotImplementedError
```

#### To do list:
- possible migration to spaCy for NLP and integration of entity linking with https://github.com/UB-Mannheim/spacyopentapioca
- add database migration utility
- add steamlit interface for summary analytics
- add better handling of errors in NLP pipeline
