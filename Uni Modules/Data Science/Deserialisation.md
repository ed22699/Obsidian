---
tags:
  - data_ingress
---
Deserialisation is the inverse process; translating data structures that have been stored in a particular format to memory ^910654
# Manual creation
- Bespoke serialisation and deserialisation methods can be crafted manually
```Python
# Instantiate list
v = []

# Read the file
f = open("d.ivec", "r")
for l in f.readlines():
	v.append(int(l))
f.close()

# Print features of the data
print(v)
# [1, 2, 3, 4, 5]
print(len(v)) # 5
print(v[2])   # 3

# Alternatively
with open("d.ivec", "r") as f:
	v = map(int, f.readlines())
```