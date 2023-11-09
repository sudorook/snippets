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
