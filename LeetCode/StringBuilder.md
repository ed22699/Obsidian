used for altering strings
```java
public void appendNtimesUsingStringBuilder(char c, int n) {
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < n; i++) {
        sb.append(c);   // O(1)
    }
    return sb.toString();
}
```

## Methods
- `charAt(i)` returns the character at position i
- `delete(start, end)` deletes the substring from the StringBuilder
- `indexOf(char)` returns the index of the first instance of that character
- `length()` returns the length of the StringBuilder
- `reverse()` reverses the StringBuilder sequence 
- `setCharAt(pos, char)` replaces char at pos
- `subSequence(start, end)` returns the subSequence
- `toString()` converts StringBuilder to string