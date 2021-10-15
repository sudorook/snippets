# Fonts

## View font hierarchy

Use `fc-match` to view the sequence of fonts that best match a query:
```
fc-match -s <FONT>
```

`FONT` can be string corresponding to a font exactly, or any string (e.g.
'monospace'). Fonts are printed in the sequence programs will search when
rendering fonts. 
