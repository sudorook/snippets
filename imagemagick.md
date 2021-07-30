# ImageMagick

## Compress JPG/PNG images

Using `magick` instead of `convert`, run:
```
magick <input> -strip -interlace Plane -gaussian-blur 0.05 -quality 95% <output>
```

`-strip` removes comments and metadata, `-gaussian-blur` reduces noise (and finer
detail), and `-quality` sets the compression level.

Alternatively, one can forgo Gaussian blur and adjust sampling factors:
```
magick <input> -strip -interlace Plane -sampling-factor 4:2:0 -quality 95% <output>
```


## Rotate images

To rotate an image:
```
magick <input> -rotate <angle> <output>
```

Some images have built-in rotation metadata and will be oriented properly in
most image viewers.
