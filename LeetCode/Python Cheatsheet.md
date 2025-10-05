## 2D array
```python
w, h = 8, 5
Matrix = [[0 for x in range(w)] for y in range(h)] 
```
## Hash Set
```python
hs = {1,2,3,4,5}
hs.add(8)
hs.remove(2) # raises error if doesn't exist
hs.discard(5) # doesn't raise error
check = 2 in hs # true
```
## Dictionary
```python
dict = {
	"a": 1,
	"b": 2,
	"c": "check"
}
print(dict.get("a"))
del dict["a"] # removes item by key
```
## Queue
```python
queue = []
queue.append("a")
queue.pop(0)
```
## Stack
```python
stack = []
stack.append("a")
stack.pop()
isEmpty = not bool(stack)
```