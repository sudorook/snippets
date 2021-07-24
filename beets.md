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

## Replace embedded cover art

In cases where the cover art downloaded using the `fetchart` plugin is too
large, extract the file, compress it, and then re-embed it.

To extract cover art directly, run:
```
beet extractart "<album>"
```

The output messages will say where the cover image is located, likely as
cover.jpg in the album directory.

Then, compress the file using ImageMagick, e.g.:
```
magick cover.jpg -strip -interlace Plane -sampling-factor 4:2:0 -quality 95% cover-new.jpg
mv cover-new.jpg cover.jpg
```

Alternately, instead of using `extractart` and then `magick`, one can use
`ffmpeg` directly:
```
ffmpeg -i "<song file"> -map 0:v cover.jpg
```

In practice, though, the defaults FFmpeg will produce an overly-compressed
file. The above ImageMagick example is less aggressive.

A third option, of course, is to simply download a new cover art file to
replace the existing one.

With an appropriate cover art file, simply run:
```
beet embedart -f cover.jpg "<album>"
```