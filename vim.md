# Vim

## Increment numbers at the start of a line by 1

```
s/^\d\+/\=(submatch(0)+1)/
```

## Wrap lines around 80-characters

In visual mode, highlight the text and enter:
```
gq
```

## Combine lines into one

In visual mode, highlight the text and enter:
```
%j
```
