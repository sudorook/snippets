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


## Resize images

Use the `-resize` flag to resize images. Run:
```
magick <input> -resize <width>x<height> <output>
```

To break the aspect ratio when resizing, use a `!` on one of the dimensions.
See below:
```
magick <input> -resize <width>x<height>! <output>
```

Because `!` is a command in many shells, be sure to escape it (`\!`) in
practice.


## Crop images

To crop images, use the `-crop` flag. Format is as follows:
```
magick <input> -crop <width>x<height>+<x offset>+<y offset> <output>
```

Coordinates start (0,0) at top left.
