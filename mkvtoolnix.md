# mkvtoolnix

## Editing title and other tag metadata from MKV containers

### Remove/modify container title tags

To rename the title tag, run:
```
mkvpropedit -e info -s title="<TITLE>" <VIDEO>
```

To instead delete the title tag from the video container, run:
```
mkvpropedit -e info -d title <VIDEO>
```


### Remove/modify stream title tags

Each stream may have title tags associated with it. To delete, run:
```
mkvpropedit -e track:<ID> -d name <VIDEO>
```

The `ID` can be a number (starting from 1) or labelled by type of stream (e.g.
`v1` for video stream 1 and `s2` for subtitle stream 2).

If instead, one wants to rename the field, use:

```
mkvpropedit -e track:<ID> -s name="<NAME>" <VIDEO>
```


## Modify chapter metadata

First, extract the metadata into an XML file:
```
mkvextract <INPUT> chapters > <XML>
```

Edit this file as needed, and when ready to re-import into the original file, run:
```
mkvpropedit <INPUT> --chapters <XML>
```


## Change default tracks

To change the default audio, subtitle, etc. track for a MKV container, use the
`--edit` flag to change the `flag-default` setting. For example, to switch from
the first audio track to the second, run:
```
mkvpropedit <INPUT> --edit track:a1 --set flag-default=0 --edit track:a2 --set flag-default=1
```
