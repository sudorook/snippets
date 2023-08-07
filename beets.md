# Beets

## Change MusicBrainz IDs of imported albums

First, change the ID metadata.

```sh
beet modify "<album name>" mb_albumid=<musicbrainz id>
```

Then, reimport using the `-c` flag to copy files in place and `-a` to use the
auto-tagger plugin.

```sh
beet import -ca "<path to album directory>"
```

## Import pre-tagged directories

```sh
beet import -C -A -W <dir>
```

For a set of directories, a for-loop like this will suffice:

```sh
for dir in *; do
  if [ -d "${dir}" ]; then
    pushd "${dir}"
    for album in *; do
      if [ -d "${album}" ]; then
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

```sh
beet edit "<album>" --all
```

## Replace embedded cover art

In cases where the cover art downloaded using the `fetchart` plugin is too
large, extract the file, compress it, and then re-embed it.

To extract cover art directly, run:

```sh
beet extractart "<album>"
```

The output messages will say where the cover image is located, likely as
cover.jpg in the album directory.

Then, compress the file using ImageMagick, e.g.:

```sh
magick cover.jpg -strip -interlace Plane -sampling-factor 4:2:0 -quality 95% cover-new.jpg
mv cover-new.jpg cover.jpg
```

Alternately, instead of using `extractart` and then `magick`, one can use
`ffmpeg` directly:

```sh
ffmpeg -i "<song file"> -map 0:v cover.jpg
```

In practice, though, the defaults FFmpeg will produce an overly-compressed file.
The above ImageMagick example is less aggressive.

A third option, of course, is to simply download a new cover art file to replace
the existing one.

With an appropriate cover art file, simply run:

```sh
beet embedart -f cover.jpg "<album>"
```

## Making exact queries

The QUERY string will match precisely if `<field>:<string>` is specified, and it
allows regexes with `<field>::<string>`. However, short strings, when used with
the `:` syntax, will nevertheless match many, many files as if a regex had been
specified. Therefore, for any specific query, use `^` and `$` in a regex:

```sh
beet <command> '<field>::^<string>$'
```

Doing so will guarantee that the patterns will be matched.

## Scan library for missing MusicBrainz tags

To scan the library and write missing tags to the Beets database, first enable
the `mbscan` plugin by adding it to the `plugins: <list>` field in the
`~/.config/beets/config.yaml` file. Then, run:

```sh
beet mbscan
```

Adjust the command by running: `beet mbscan <query>` to only update specific
files.

**NOTE:** This command will remove any changes (e.g. fixed
capitalization/spelling, additional metadata fields) to the files in the
library. Only run this when existing tags have been systematically corrupted.

## List all album Musicbrainz IDs

Use `beet list` and pass the `-a` (return albums) flag and use `-f` to format
the output:

```sh
beet list -af '$mb_albumid: $album'
```
