# Vim

## Increment numbers at the start of a line by 1

```
s/^\d\+/\=(submatch(0)+1)/
```

To increment anywhere within lines:
```
s/^filler text \zs\(\d\+\)/\=(submatch(0)+1)/
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

## Enable truecolor support

By default, vim will default to a 256-color palette. To enable more colors, add
the following to your vimrc:
```
set termguicolors
```

## Disable MiniBufferExplorer

If you don't find MiniBufferExplorer useful and want to disable it, add to your
vimrc:
```
let g:miniBufExplAutoStart=0
```

If all you want is to disable the addon from showing by default in diffs, you
can instead add:
```
let g:miniBufExplHideWhenDiff=0
```

## Convert spaces to newlines

To break a list of space- or otherwise-delimited items into a list with one
item on each line, run:
```
%s/ /\r/g
```

## Select a paragraph/function in visual mode

To select a whole paragraph or function, move the cursor to within the block of
interest and type:
```
vip
```

The section is demarcated by empty lines above and below.
