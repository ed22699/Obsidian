---
tags:
  - Lesson
  - data_ingress
---
# What is it
- The process of collecting and acquiring data from various sources
- directly impacts the quality of analysis and insights
# Data structures
- can use `list`, `set`, `dict` and `np.array` 
- `pandas.DataFrame` pandas dataframe is a powerful data structure that can also be used
	- will look like a spreadsheet 
# Object persistence
## Serialisation/Deserialisation
### Serialisation
![[Serialisation#^204a95]]
### Deserialisation
![[Deserialisation#^910654]]
### Problems with bespoke serialisation/deserialisation
- very specific use case
- format not standardised
- example code is not robust in its current state
- needs to be tested against many test cases
- no object metadata encoded (e.g. data type, length)
- every data structure (e.g. matrices, dictionaries, list of strings) requires a (de)serialisation method

- should be fine if using it in well-controlled situations
## Comma-separated values (CSV)
![[Comma-separated values]]

# Data Types
| Data types                 | Data characteristics             |
| -------------------------- | -------------------------------- |
| dense data                 | CSV should be fine               |
| sparse data                | don't store in dense format      |
| text data                  | how to store efficiently         |
| structured/relational data | handle relationships             |
| categorical/ordinal        | handling categorical constraints |
| date/time                  | retrieving time zone             |
| lat/lon                    | retrieving location              |
- good format for sparse data e.g. $\begin{pmatrix} - & - & 1 \\ - & - & - \\ - & 2 & - \end{pmatrix}$ is with a coordinate system e.g $(x, y, n)$ so $(0, 2, 1)$
# Serialising generic objects
## JSON (JavaScript Object Notation)
![[JSON (JavaScript Object Notation)]]
## HDF5 (Hierarchical Data Format)
![[HDF5 (Hierarchical Data Format)]]
# Data Collection Methods:
- **Web Scraping**: extracting data from websites using automated tools
- **APIs**: Accessing data programmatically through APIs provided by various services
- **Databases**: Queering a database to extract relevant data
- **Sensors**: Collecting data from sensors and other devices
- **Surveys and questionnaires**: Gathering directly from individuals
- **Publicly available datasets**: Accessing datasets from government agencies, research institutions and other organisations