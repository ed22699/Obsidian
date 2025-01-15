---
tags:
  - web_scraping
---
- provide a portal for explicit data acquisition, and are generally less prone to the issues from HTML scraping as:
	- code is optimised for retrieval and not for visual layout/aesthetics
	- standard serialisation tools (e.g. JSON) are typically used
	- the core items of interest have been extracted (e.g. dates, URLs)
- [Examples of Web APIs](https://github.com/toddmotto/public-apis)
- web APIs, although similar in principle, will have very different schemas
- writing code for APIs is generally simpler than parsing HTML, requires less maintenance, are often documented, and results in faster overall code
## RESTful APIs
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
## Summary
- API-based querying is robust, reliable, well maintained and documented with a static schema
- information extraction is not based on fickle naming conventions of tag attributes
- since only content is acquired (not images, JavaScript or style files) the bandwidth spent to acquire data is reduced significantly. This lends itself to faster processing
- Since access is acquired through API keys, it is easy for the service provider to manage the bandwidth and throughput of its service as necessary
- The data structures being received from APIs are complex, and need specific serialisation tools to be built