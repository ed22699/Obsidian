---
tags:
  - data_ingress
---
- Serialisation is the process of translating data structures or objects from memory into a format that can be stored ^204a95
# Manual creation
- Bespoke serialisation and deserialisation methods can be crafted manually
```Python
# Create list
v = [1, 2, 3, 4, 5]
# Write it to file
f = open("d.ivec", "w")
for el in v:
	f.write("%d\n" % el)
f.close 

# Alternatively
with open("d.ivec", "w") as f:
f.write("\n".join(map(str, v)))
```