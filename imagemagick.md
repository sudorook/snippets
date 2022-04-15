# ImageMagick

## Strip image metadata but preserve embedded color profiles

The `-strip` flag will delete everything, including the color profiles. To
remove metadata but preserve them, use `-thumbnail` instead. Be sure to specify
the output dimensions, which in the case of mimicking `strip`, will be the
input dimensions.
```
magick <input> -thumbnail <heightxwidth> <output>
```


## Compress JPG/PNG images

Using `magick` instead of `convert`, run:
```
magick <input> -strip -interlace Plane -quality 95% <output>
```

`-strip` removes comments and metadata and `-quality` sets the compression
level.

Additional levels of compression can be achieved at the price of visible loss
of image quality. For example, use `-gaussian-blur` to reduce noise and finer
detail:
```
magick <input> -strip -interlace Plane -gaussian-blur 0.05 -quality 95% <output>
```

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
