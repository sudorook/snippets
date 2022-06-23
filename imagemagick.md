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
magick <input> -strip -quality 95% <output>
```

`-strip` removes comments and metadata and `-quality` sets the compression
level.

One also can adjust the sampling factor:
```
magick <input> -strip -sampling-factor 4:2:0 -quality 95% <output>
```


## Rotate images

To rotate an image:
```
magick <input> -rotate <angle> <output>
```

Some images have built-in rotation metadata and will be oriented properly in
most image viewers.
