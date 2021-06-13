# Beets

## Change MusicBrainz IDs of imported albums

First, change the ID metadata.
```
beet modify "<album name>" mb_albumid=<musicbrainz id>
```

Then, reimport using the `-c` flag to copy files in place and `-a` to use the
auto-tagger plugin.
```
beet import -ca "<path to album directory>"
```

## Import pre-tagged directories

```
beet import -C -A -W <dir>
```

For a set of directories, a for-loop like this will suffice:
```
for dir in *; do
  if [ -d "${dir}" ]; then
    pushd "${dir}"
    for album in *; do
      if [ -d "${dir}" ]; then
        beet import -C -A -W "${album}"
      fi
    done
    popd
  fi
done
```

## Edit all tags for an album

Use the 'edit' plugin to alter metadata via a text editor. Simply add 'edit' to
the plugins list in the Beets config files, and then run:

```
beet edit "<album>" --all
```
