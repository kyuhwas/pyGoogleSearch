# pyGoogleSearch
Package for collecting and aggregating search results from various Google sources (Google Search, Google News, Google Scholar).

Python 3.x is required to run this package

Feedback is welcome at: mdgithub@gmail.com

## Exmaple:
```
from pyGoogleSearch import *

topic = 'hello world'

# COLLECT DATA FROM GOOGLE SEARCH

# outputs in json format
raw_web_data = Google(topic, pages=5).search()

# takes data from json, collects content from all urls and outputs to a list comprehension
output_web_data = DataHandler(raw_web_data).aggregate_data()
write_csv(output_web_data, 'web_data.csv')

# COLLECT DATA FROM GOOGLE NEWS SEARCH

# outputs in json format
raw_news_data = Google(topic, pages=5).search_news()

# takes data from json, collects content from all urls and outputs to a list comprehension
output_news_data = DataHandler(raw_news_data).aggregate_data()
write_csv(output_news_data, 'news_data.csv')

# COLLECT DATA FROM GOOGLE SCHOLAR SEARCH

# outputs in json format
raw_scholar_data = Google(topic, pages=5).search_scholar()

# takes data from json, collects content from all urls and outputs to a list comprehension
output_scholar_data = DataHandler(raw_scholar_data).aggregate_data()
write_csv(output_scholar_data, 'scholar_data.csv')

# Site specfic search and special characters in search query

topic = 'social emotional learning AND \"healthy school culture\"'
d = Google(topic, site='edutopia.org').search()
print json.dumps(d, indent=2)
```

## The DataHandler module
The module takes the json that is returned from the Google().search() functions and does two things:

* Scrapes all visible text from URLs that are returned from the search
* Formats data for outputting to CSV with the data points below


#### Data points returned for a web search:

* URL
* Link Text
* Link Info
* Ranking
* Content

#### Data points returned for a news search:

* URL
* Link Text
* Link Info
* Source
* Time
* Ranking
* Content

#### Data points for scholar search:

* URL
* Title
* Excerpt
* Citations
* Year
* Ranking
* Content


## The ImportExportFucntions module
Contains the following functions for importing and exporting data
```
write_csv(data, output_file)
write_json(data, output_file)
open_json(input_file)
```

#### Additionally, there are some flaws to be aware of: 

* The scholar function has a few flaws in how it collects data. Part of this is due to inconsistencies in how google renders their scholar results but regardless I need to revisit so that I can handle those inconsistencies better
* The function I’ve written to collect all the content from the search results cannot handle select websites and every so often returns nothing. Additionally, some websites will return a 404 error when you try to scrape it. The script does not break when this happens, it merely takes note and continues. It’s just important to know that because the function tries to grab all text from all the urls, it will inevitably miss on a few. Unfortunately, I believe that’s just the nature of the beast.

