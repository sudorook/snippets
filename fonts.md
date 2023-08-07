# Fonts

## Rebuild font cache

The font cache should automatically rebuild when fonts are added and removed,
but to force-rebuild, run:

```sh
fc-cache -f
```

Also pass `-v` to enable verbose output.

## View font hierarchy

Use `fc-match` to view the sequence of fonts that best match a query:

```sh
fc-match -s <FONT>
```

`FONT` can be string corresponding to a font exactly, or any string (e.g.
'monospace'). Fonts are printed in the sequence programs will search when
rendering fonts.

## Get the exact font name

Often the font name will not match the file. To view the exact file name, parse
the output from `fc-list`. The output is of the format:

```
<font file absolute path>: <font name>:style=<variant>
```

Look for the `<font name>` component of the output.

Alternately, open the font file in FontForge or another font-editing programs.
