# yt-dlp

## Extract audio from and store as MP3

To extract audio, use `-x`, and to store in MP3 format, use
`--audio-format mp3`.

```sh
yt-dlp -x --audio-format mp3 ...
```

Additionally, use `--audio-quality 0` to use the best quality audio stream.

## Download playlist

To download a playlist while keeping the files numbered by playlist order, use
`-o` and format the output as:

```sh
yt-dlp -o "%(playlist_index)s %(title)s.%(ext)s" <playlist>
```

## Use browser cookies for downloading streams

First, extract cookies from a web browser. The
[cookies.txt](https://addons.mozilla.org/en-US/firefox/addon/cookies-txt/)
Firefox addon can output them in a Netscape Cookie format text file.

Note, a properly formatted Netscape HTTP Cookie file is tab-delimited and
contains the header:

```txt
# Netscape HTTP Cookie File
```

Next, format the `yt-dlp` command:

```sh
yt-dlp --cookies=<cookie file> <url>
```

## Exclude VP9 (or other) codec from downloader

To prevent downloading VP9 streams, adjust the format string as follows:

```
-f "bestvideo[vcodec!~='vp0?9']"

```

VP9 codecs can often be reported as `vp9` or `vp09`, so use an optional `0` to
catch both cases.

**Note:** The format string must be quoted for this to work.
