# Audio

## Split lossless audio using a CUE file

For example, to split a FLAC file:

```bash
shnsplit -f <file>.cue -t "%n - %t" -o <codec> <file>.flac
```

`<codec>` can be left as `flac`.

`shntool` supports a variety of audio data formats, such as FLAC, ALAC, and
WAVE.
