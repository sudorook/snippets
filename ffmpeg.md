# FFmpeg

Should the available information be lacking, look at the
[FFmpeg wiki](https://trac.ffmpeg.org/wiki) first. It's much more useful than
StackOverflow.

## Change output verbosity

Copied from
[this thread](https://ffmpeg.org/pipermail/ffmpeg-user/2013-December/018834.html).

| key | function                                             |
| --- | ---------------------------------------------------- |
| ?   | show this help                                       |
| +   | increase verbosity                                   |
| -   | decrease verbosity                                   |
| c   | send command to first matching filter supporting it  |
| C   | send/Que command to all matching filters             |
| D   | cycle through available debug modes                  |
| h   | dump packets/hex press to cycle through the 3 states |
| q   | quit                                                 |
| s   | show QP histogram                                    |

The left arrow key sends the escape sequence `^[[D` to ffmpeg, and ffmpeg
ignores all keys until it matches something usable:

- Up: `^[[A`
- Down: `^[[B`
- Right: `^[[C` (matches Send/Que command to all matching filters)
- Left: `^[[D` (matches cycle through available debug modes)

## Display the streams in a container

To view the streams present in a file, use:

```sh
ffprobe -v error -show_entries stream=index,codec_name,codec_type <input>
```

(Or, simply run `ffprobe` without the extra arguments above.)

## Hard-code subtitles

See the
[FFmpeg subtitle docs](https://trac.ffmpeg.org/wiki/HowToBurnSubtitlesIntoVideo)
for complete documentation.

### Text-based subtitles (ass, srt, etc.)

If you want to hard-code text subtitles in a video, run:

```sh
ffmpeg -i <input> -vf subtitles=<input> <output>
```

In this example, `<input>` contains a single subtitle stream that FFmpeg will
automatically pick up through `subtitles=<input>`. If using an external subtitle
file, use `subtitles=<external subfile>` instead.

Subtitles can additionally use custom fonts, etc. Pass additional values to the
`subtitles` video format filter.

```sh
ffmpeg -i <input> \
  -filter:v "subtitles=<subtitle>:force_style='FontName=<fontname>,Fontsize=<size>'" \
  <output>
```

`fontname` is the font family, including style (e.g. 'Bold' or 'Italic'), and
`size` is the font size.

Note that this will only work with text based (ass, srt) subtitles, not image
based ones, which are usually found in DVD/Blu-ray rips.

### Picture-based subtitles (sup, etc.)

For picture-based subtitles, instead run:

```sh
ffmpeg -i <input> -filter_complex "[0:v][0:s]overlay[v]" -map "[v]" -map 0:a <output>
```

This will burn the first subtitle stream into the first video stream.

## Offset subtitle times

To shift all the timings for subtitles, run:

```sh
ffmpeg -itsoffset <mm:ss.x> -i <input> -map 0:s:<stream> -c:s copy <output>
```

It is important to specify the `itsoffset` flag _before_ the input. The output
format will be inferred by the file extension. It can also be specified by `-f`.

## Crop Video

Run:

```sh
ffmpeg -i <input> -filter:v 'crop=<width>:<height>:<x>:<y>' -codec:a copy <output>
```

Parameters `width` and `height` are width and height of the cropped video, and
`x` and `y` are the coordinates relative to the original video for where the
top-left corner is located.

To estimate the appropriate values for the crop filter, one can use the
`cropdetect` feature. Run:

```sh
ffmpeg -i <input> -filter:v cropdetect -codec:a copy -f null -
```

The output stream will show a moving estimate for the best crop setting.

To avoid scanning the entire video stream, add the `-t <duration>` flag to the
above command to specify the duration to scan.

[See also](https://ffmpeg.org/ffmpeg-filters.html#crop)

## Extract streams into separate files

To split all the streams in a video container into separate files, run:

```sh
ffmpeg -i <input> -map 0:v -c copy <video output> \
       -map 0:a -c copy <audio output> -map 0:s -c copy <subtitle output>
```

The `-map 0:v` tells FFmpeg to take the first video stream. Similarly,
`-map 0:a` and `-map 0:s` refer to the first audio and subtitle streams,
respectively.

If there is more than one stream for video/audio/etc., you can specify one with
`map 0:a:x`, where `x` represents the number (starting from 0) of the stream in
the input file.

The example above uses `-c copy`, which simply copies the codec found in the
file. This is quickest, as `ffmpeg` will not have to re-encode anything.
However, if you wish to specify a different format, replace `copy` with your
preference.

Note that when specifying the output file extension, you should take care that
it is compatibly with the stream, otherwise `ffmpeg` will exit with an error
(e.g., when converting sup subtitles to srt) or will start reencoding
automatically.

## Cut clips from a larger video file

(It may be easier to just write a script that handles this...)

To cut a bit out of a video:

```sh
ffmpeg -i <input> -ss <mm:ss.x> -t <s> <output>
```

The `-ss <mm:ss.x>` option is for specifying the timestamp for when you want the
clip to start, formatted minutes:seconds.decimal (e.g. '-ss 14:23.5'). The `-t`
flag is for setting the length of the clip in seconds, so setting, for example,
`-t 10.4` would make the clip last 10.4 seconds.

If you want to set specific streams in the video, you can add the `-map` options
described above. For example, to take the first video, audio, and subtitle
streams, run:

```sh
ffmpeg -i <input> -map 0:v -c:v copy -map 0:a:0 -c:a copy -map 0:s:0 -c copy \
       -ss <mm:ss.x> -t <s> <output>
```

# Down-mix audio streams

To combine many streams into a simpler layout, use `pan` to re-map audio
streams. For example, the following will map the front left and front right
streams to the left and right stereo:

```sh
ffmpeg -i <input> -af "pan=stereo|c0=FL|c1=FR" <output>
```

In the case where streams are to be down-mixed to stereo, simply use the `-ac`
flag:

```sh
ffmpeg -i <input> -ac 2 <output>
```

Note that the above shorthand will drop the low frequency (LFE) stream.

## Join streams into a single file

To join separate streams into a single container, run:

```sh
ffmpeg -i <video> -i <audio> -i <subtitle> \
       -c:v copy -c:a copy -c:s copy <output>
```

The above example will splice a video, audio, and subtitle stream into one
video. Useful for foreign releases where audio tracks are supplied in separate
files.

It's also possible to do more complicated stuff, like using the same stream more
than once and re-encoding each duplicate differently (see the
[map documentation](https://trac.ffmpeg.org/wiki/Map)).

## Copy chapters/metadata from one file to another

The following copies all the data streams from `input1` and merges them with the
metadata from `input0`:

```sh
ffmpeg -i <input0> -i <input1> -map 1 -map_metadata 0 -c copy <output>
```

Note that this only copies metadata, not fonts or other attachments.

To copy chapter data, instead run:

```sh
ffmpeg -i <input0> -i <input1> -map 1 -map_chapters 0 -c copy <output>
```

## Copy embedded fonts from one file to another

The following copies the metadata from `input1` to `input0`:

```sh
ffmpeg -i <input0> -i <input1> -map_chapters 1 \
  -map 0:v -map 0:a -c copy -map 0:s -map 1:s -map 0:t -map 1:t <output>
```

## Append fonts to a Matroska container

To attach an opentype font file to a container, run:

```sh
ffmpeg -i <input.mkv> -map 0 -c copy \
  -attach <font.otf> -metadata:s:t mimetype=application/vnd.ms-opentype \
  <output.mkv>
```

For attaching a truetype font, instead run:

```sh
ffmpeg -i <input.mkv> -map 0 -c copy \
  -attach <font.ttf> -metadata:s:t mimetype=application/x-truetype-font \
  <output.mkv>
```

Multiple fonts can be attached to a single stream by adding multiple `-attach`
lines. The font streams will be added and numbered at the end of the list.

## Dump all attachments in a video container

To dump all the attached files in the current working directory, run:

```sh
ffmpeg -dump_attachment:t "" -i <input>
```

## Change default streams

To change the default video/audio/subtitle stream in containers with multiple,
use the `disposition` flag. Set the new default stream by
`-disposition:x:n default` --- where `x` is the type of stream and `n` the index
number in the container --- and unset the remaining ones with
`-disposition:y:m none`. Remember that streams are indexed from 0.

For example, to switch the default audio stream from the first to the second in
a Matroska container with two audio streams (while keeping everything else
intact), run:

```sh
ffmpeg -i <input> -map 0 -disposition:a:1 default -disposition:a:0 none -c copy <output>
```

Be sure to specify the disposition before the codec. Also, for Matroska output
containers, also specify `-default_mode infer_no_subs` with the disposition
parameter.

For another example, to disable showing any subtitle stream by default, use the
`-disposition:s -default` flag.

## Concatenate videos

See the [FFmpeg concatenation docs](https://trac.ffmpeg.org/wiki/Concatenate)
for full documentation.

To simply concatenate two files, create a text file (e.g. files.lst) containing
a list of files to be combined. Format is as follows:

```text
file 'path/to/file1'
file 'path/to/file2'
```

The files paths need to be encapsulated in single quotes, so avoid file names
with single quotes in them.

Then, pass the text file to FFmpeg with the `concat` flag:

```sh
ffmpeg -safe 0 -f concat -i files.lst -c copy -scodec copy output.mkv
```

The `-safe 0` flag may be necessary to bypass warnings about unsafe file names,
such as those with spaces.

## Extract subtitles

To extract an SRT text stream:

```sh
ffmpeg -i <video>.<extension> <video>.srt
```

For DVDSUB streams, extract into a Matroska container:

```sh
ffmpeg -i <video> -map 0:s:0 -c:s dvdsub -f matroska subtitles.mkv
```

The stream can be added to a video later via:

```sh
ffmpeg -i <video> -i subtitles.mkv -c copy -c:s dvd_subtitle <new video>
```

## Increase probe size for codec detection

When warnings appear and suggest increasing the 'analyzeduration' and
'probesize' options (for example when reading PGS subtitle format), alter the
`ffmpeg` command:

```sh
ffmpeg -analyzeduration 50M -probesize 50M ...
```

Increase the size until the warning disappears.

## Convert FLAC to MP3

```sh
ffmpeg -i "<FLAC input>" -b:a 320k "<MP3 output>"
```

The above uses the maximum MP3 bitrate of 320k for conversion. To reduce file
size, reduce this value.

## Strip all metadata

To remove attachments, subtitles, fonts, etc. from a container, run:

```sh
ffmpeg -i <input> -map_metadata -1 -c:v copy -c:a copy <output>
```

To strip chapter metadata instead, run:

```sh
ffmpeg -i <input> -map_chapters -1 -c:v copy -c:a copy <output>
```

Combine `-map_metadata -1` and `-map_chapters -1` to remove both.

## Extract metadata to file

To dump existing metadata to a file, run:

```sh
ffmpeg -i <input> -f ffmetadata <output>
```

To load metadata, (e.g. after edits), run:

```sh
ffmpeg -i <input> -i <ffmetadatafile> -map_metadata 1 ...
```

The `<ffmetadatafile>` is the data produced by the first command.

## Merge streams

To merge streams from two files, (e.g. add an audio stream to a video), run:

```sh
ffmpeg -i <input 0> -i <input 1> -map 0 -map 1 -c copy <output>
```

If some streams are to be omitted when merging, adjust the above command as
needed. For example, to combine the video stream in one file with the audio of
another, run:

```sh
ffmpeg -i <input 0> -i <input 1> -map 0:v -map 1:a -c copy <output>
```

## Shift audio-video synchronization

To delay audio by 3 seconds:

```sh
ffmpeg -i <input> -itsoffset 3 -i <input> -map 0:v -map 1:a -codec:a copy -codec:v copy <output>
```

To delay video by 3 seconds (i.e. advance audio by 3 seconds):

```sh
ffmpeg -i <input> -itsoffset 3 -i <input> -map 1:v -map 0:a -codec:a copy -codec:v copy <output>
```

The second `-i` flag must come _immediately after_ the `-itsoffset` flag.

## Change the frame rate

To change the frame rate, pass the `fps` flag to the video filter:

```sh
ffmpeg -i <input> -filter:v 'fps=fps=<VAL>' -codec:a copy <output>
```

where `<VAL>` is the new frames-per-second value.

[See also](https://trac.ffmpeg.org/wiki/ChangingFrameRate)
