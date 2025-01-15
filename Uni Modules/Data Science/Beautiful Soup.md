---
tags:
  - web_scraping
---
## Concepts
- powerful library for parsing XML/HTML documents
	- can create information extraction engines that can run autonomously
- HTML scraping comes with many serious problems:
	- selecting the 'correct' link to follow is a strong function of the ability to identify the link of interest based only on its HTML tags. Can be difficult for *poorly designed websites*
	- if the layout or formatting of information on a webpage changes, it will become necessary to reconfigure the web scraping mechanism from scratch
- test for format changes should be defined
## Functions
- `soup.prettify()` corrects the HTML source
- `soup.find_all("head")` finds all instances within and including the head tag
	- `soup.find_all("div", attrs=("class": "col-sm-2"))` finds all instances within and including the div tag whee it has that class attribute
- `soup.find("head")` finds the first instance of content within and including the head tag
- `soup.find("title").text` gets the text within the title tag
```python
url = 'https://www.theguardian.com/books/2023/jan/18/ts-eliot-prize-winner-anthony-joseph-how-poetry-helped-me-love-my-absent-father'
req = requests.get(url)
source = req.text
soup = BeautifulSoup(source, 'html.parser')
print(source)
# To view the complete HTML source of a web page in a web browser, right click on the page, and click "View Page Source."
```