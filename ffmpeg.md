# FFmpeg

Should the available information be lacking, look at the [FFmpeg
wiki](https://trac.ffmpeg.org/wiki) first. It's much more useful than
StackOverflow.


## Display the streams in a container

To view the streams present in a file, use:
```
ffprobe -v error -show_entries stream=index,codec_name,codec_type <input>
```


## Hardcode subtitles

See the [FFmpeg subtitle
docs](https://trac.ffmpeg.org/wiki/HowToBurnSubtitlesIntoVideo) for complete
documentation.

### Text-based subtitles (ass, srt, etc.)

If you want to hardcode soft subtitles in a video, run:
```
ffmpeg -i <input> -vf subtitles=<input> <output>
```

In this example, `<input>` contains a single subtitle stream that FFmpeg will
automatically pick up through `subtitles=<input>`. If using an external
subtitle file, use `subtitles=<external subfile>` instead.

Note that this will only work with text based (ass, srt) subtitles, not image
based ones, which are usually found in DVD/Blu-ray rips.

### Picture-based subtitles (sup, etc.)

For picture-based subtitles, instead run:
```
ffmpeg -i <input> -filter_complex "[0:v][0:s]overlay[v]" -map "[v]" -map 0:a <output>
```

This will burn the first subtitle stream into the first video stream.


## Extract streams into separate files

To split all the streams in a video container into separate files, run:
```
ffmpeg -i <input> -map 0:v -c copy <video output> \
       -map 0:a -c copy <audio output> -map 0:s -c copy <subtitle output>
```

The `-map 0:v` tells FFmpeg to take the first video stream. Similarly, `-map
0:a` and `-map 0:s` refer to the first audio and subtitle streams,
respectively. 

If there is more than one stream for video/audio/etc., you can specify one with
`map 0:a:x`, where `x` represents the number (starting from 0) of the stream in
the input file.

The example above uses `-c copy`, which simply copies the codec found in the
file. This is quickest, as `ffmpeg` will not have to reencode anything.
However, if you wish to specify a different format, replace `copy` with your
preference.

Note that when specifying the output file extension, you should take care that
it is compatibly with the stream, otherwise `ffmpeg` will exit with an error
(e.g., when converting sup subtitles to srt) or will start reencoding
automatically.


## Cut clips from a larger video file

(It may be easier to just write a script that handles this...)

To cut a bit out of a video:
```
ffmpeg -i <input> -ss <mm:ss.x> -t <s> <output>
```

The `-ss <mm:ss.x>` option is for specifying the timestamp for when you want
the clip to start, formatted minutes:seconds.decimal (e.g. '-ss 14:23.5'). The
`-t` flag is for setting the length of the clip in seconds, so setting, for
example, `-t 10.4` would make the clip last 10.4 seconds.

If you want to set specific streams in the video, you can add the `-map`
options described above. For example, to take the first video, audio, and
subtitle streams, run:
```
ffmpeg -i <input> -map 0:v -c:v copy -map 0:a:0 -c:a copy -map 0:s:0 -c copy \
       -ss <mm:ss.x> -t <s> <output>
```


## Join streams into a single file

To join separate streams into a single container, run:
```
ffmpeg -i <video> -i <audio> -i <subtitle> \
       -c:v copy -c:a copy -c:s copy <output>
```

The above example will splice a video, audio, and subtitle stream into one
video. Useful for foreign releases where audio tracks are supplied in separate
files.

It's also possible to do more complicated stuff, like using the same stream
more than once and reencoding each duplicate differently (see the [map
documentation](https://trac.ffmpeg.org/wiki/Map)).


## Show subtitles by default in a video

When setting subtitle streams, you can specify that they be showed by default
by adding `disposition:s:0 default` to the `ffmpeg` options. This will set the
first subtitle stream as the default. To set the (n+1)th stream as default
instead, use `dispostition:s:n default` instead.

To unset a stream as default, use `disposition:s:n 0`.


## Concatenate videos

See the [FFmpeg concatenation docs](https://trac.ffmpeg.org/wiki/Concatenate).


## Extract subtitles

```
ffmpeg -i <video>.<extension> <video>.srt
```
