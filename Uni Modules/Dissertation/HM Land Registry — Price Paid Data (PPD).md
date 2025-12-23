- every residential property sale in England and Wales since 1995
- CSV file (monthly updates)
## Format
- transaction unique identifier (long string)
- price ("70000")
- date of transfer (`YYYY-MM-DD HH:MM`)
- postcode 
- property type
	- D = detached
	- S = semi-detached
	- T = terraced
	- F = flat/Maisonette
	- O = other
- Old/New
	- Y = newly built
	- N = existing
- Duration
	- F = Freehold
	- L = Leasehold
- PAON (Primary addressable object name)
	- house number of house name
- SAON (Secondary Addressable Object Name)
	- flat identifier or secondary name (often empty)
- Street
- Locality
	- optional locality - smaller area identifier within town
- Town/City
- District
- County
- PPD Category Type
	- A = Standard residential sale
	- B = Additional price paid entry (e.g. repossessions, buy-to-lets)
- Record Status
	- A - Added
	- C - Changed
	- D - Deleted

### Example of format of first row
```python
"{F887F88E-…}"
"70000"
"1995-07-07 00:00"
"MK15 9HP"
"D"
"N"
"F"
"31"
""
"ALDRICH DRIVE"
"WILLEN"
"MILTON KEYNES"
"MILTON KEYNES"
"MILTON KEYNES"
"A"
```