---
tags:
  - web_scraping
---
## Content
- provide a portal for explicit data acquisition, and are generally less prone to the issues from HTML scraping as:
	- code is optimised for retrieval and not for visual layout/aesthetics
	- standard serialisation tools (e.g. JSON) are typically used
	- the core items of interest have been extracted (e.g. dates, URLs)
- [Examples of Web APIs](https://github.com/toddmotto/public-apis)
- web APIs, although similar in principle, will have very different schemas
- writing code for APIs is generally simpler than parsing HTML, requires less maintenance, are often documented, and results in faster overall code
### RESTful APIs
- representational state transfer (REST) or RESTful Web services are one way of providing interoperability between computer systems on the internet
- in most circumstances API keys are required before data can be accessed
```python
# Specify the arguments 
args = {
		"section": "technology",
		"order-by": "newest", 
		"api-key": "test",
		"page-size": "100"
}

# Construct the URL
base_url = create_guardian_url(args)

# Make the request and extract the source
response = json.loads(requests.get(url).text)
...
...
# Print the data that is available
print(response.keys())
# ["currentPage", "orderBy", "pageSize", "pages", "results", "startIndex", "status", "total", "userTier"]
```
### Summary
- API-based querying is robust, reliable, well maintained and documented with a static schema
- information extraction is not based on fickle naming conventions of tag attributes
- since only content is acquired (not images, JavaScript or style files) the bandwidth spent to acquire data is reduced significantly. This lends itself to faster processing
- Since access is acquired through API keys, it is easy for the service provider to manage the bandwidth and throughput of its service as necessary
- The data structures being received from APIs are complex, and need specific serialisation tools to be built
## Examples
```python
from __future__ import print_function

import requests
import json
from configparser import ConfigParser

# Get key from config file
parser = ConfigParser()
parser.read('./myconfig.cfg')

myapikey = parser.get('guardian', 'api-key-2024')

# Inspect all sections
url = 'https://content.guardianapis.com/sections?api-key=' + myapikey
req = requests.get(url)
src = req.text

sections = json.loads(src)['response']
print(sections.keys())
# dict_keys(['status', 'userTier', 'total', 'results'])
print(json.dumps(sections['results'][0], indent=2, sort_keys=True))
# Find just technology based sections
for result in sections['results']:
	if 'tech' in result['id'].lower():
		print(result['webTitle'], result['apiUrl'])
```
- Hard coding a secret such as a password or a key in a code file is a security risk. Instead you should *store your api-key in a config file*
	```cfg
	[guardian]
	api-key=alkruio-xxxx-xxxx-xxxx-sdhl3489
	```
### Manual query on whole API
```python
# Specify the arguments 
args = {
		"section": "technology",
		"order-by": "newest", 
		"api-key": myapikey,
		"page-size": "100"
}

# Construct the URL
base_url = 'http://content.guardianapis.com/search'
url = '{}?{}'.format(
	base_url,
	'&'.join(["{}={}".format(kk, vv) for kk, vv in args.items()])
)

# Make the request and extract the source
req = requests.get(url)
src = req.text
print('Number of byes received:', len(src))
```
### Parsing the JSON
```python
response = json.loads(src)['response']
print('The following are available:\n ', sorted(respinse.keys()))
# impoirtant to verify that the status message is `ok` before continuing, if it isn't no real data will have been received
assert response['status'] == 'ok'

# List results
print(json.dumps(response['results'][0], indent=2, sort_keys=True))

print('Total news stories:', response['total']) 
print('Pages:', response['pages'])
print('Page size:', response['pageSize'])
- [ ] ```
### Finding all tech stories that talk about AI and OpenAI but not ChatGPT
```python
args = {
    'section': 'technology', 
    'order-by': 'newest', 
    'api-key': myapikey, 
    'page-size': '10',
    'q' : 'AI%20AND%20OpenAI%20AND%20NOT%20(ChatGPT)'
}    

# Construct the URL
base_url = 'http://content.guardianapis.com/search'
url = '{}?{}'.format(
    base_url, 
    '&'.join(["{}={}".format(kk, vv) for kk, vv in args.items()])
)

# Make the request and extract the source
req = requests.get(url) 
src = req.text

print('Number of byes received:', len(src))

# Parsing JSON
response = json.loads(src)['response']
print('The following are available:\n ', sorted(response.keys()))

# Verifying the status code
assert response['status'] == 'ok'

# Listing the results
print(json.dumps(response['results'][0], indent=2, sort_keys=True))

# Response statistics
print('Total news stories:', response['total']) 
print('Pages:', response['pages'])
print('Page size:', response['pageSize'])
```
### Request Specific Content from the API
#### Fetching the $i^{th}$ result
```python
i = 0
api_url = response['results'][i]['apiUrl']
api_id = response['results'][i]['id']

print(api_url)
print(api_id)
```
#### Fetching the headline and body text of the news story with id
```python
# Construct url
base_url = "https://content.guardianapis.com/search?"
search_string = "ids=%s&api-key=%s&show-fields=headline,body" %(api_id, myapikey)

url = base_url + search_string
print(url)

# Request url
req = requests.get(url) 
src = req.text

# Get and check response
response = json.loads(src)['response']
assert response['status'] == 'ok'

# Print headline
print(response['results'][0]['fields']['headline'])

# Print body of story
body = response['results'][0]['fields']['body']
print(body)
```
### Text Processing: Word count and store in data frame
```python
import pandas as pd
import re

# First, we need to clean that data -- remove HTML tags. 
# Here is a "not so good" way to do it. You could consider BeautifulSoup here!

words = body.replace('<p>','').replace('</p>','').split()
print(len(words))
unique_words = list(set(words))
print(len(unique_words))
# count_dictionary = {word: count for word, count in zip(words, [words.count(w) for w in words])}
count_dictionary = {'word': unique_words, 'count': [words.count(w) for w in unique_words]}

# Store in a dataframe
df = pd.DataFrame(count_dictionary)
df.sort_values(by='count', ascending=False)

# We could export the data frame in a CSV and observe the complete output
# df.to_csv('term-frequency.csv')

# Regex format the words to remove , e.g. Facebook, will be Facebook
words_wo_punctuation = re.sub(r'[^\w\s]','',body.replace('<p>','').replace('</p>','')).split() 
unique_words = list(set(words_wo_punctuation))
print(len(unique_words))
count_dictionary = {'word': unique_words, 'count': [words_wo_punctuation.count(w) for w in unique_words]}

df = pd.DataFrame(count_dictionary)
df.sort_values(by='count', ascending=False)

# We could export the data frame in a CSV and observe the complete output
# df.to_csv('term-frequency-regex.csv')
# Open the CSV in a text editor or a spread sheet and analyse the output

df.sort_values(by='count', ascending=False).to_csv('term-frequency-regex.csv')
```