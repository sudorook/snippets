1. Increment numbers at the start of a line by 1:

```
s/^\d\+/\=(submatch(0)+1)/
```
