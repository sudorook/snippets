# ImageMagick

## Strip image metadata but preserve embedded color profiles

The `-strip` flag will delete everything, including the color profiles. To
remove metadata but preserve them, use `-thumbnail` instead. Be sure to specify
the output dimensions, which in the case of mimicking `strip`, will be the input
dimensions.

```sh
magick <input> -thumbnail <heightxwidth> <output>
```

## Compress JPG/PNG images

Using `magick` instead of `convert`, run:

```sh
magick <input> -strip -quality 95% <output>
```

`-strip` removes comments and metadata and `-quality` sets the compression
level.

One also can adjust the sampling factor:

```sh
magick <input> -strip -sampling-factor 4:2:0 -quality 95% <output>
```

## Rotate images

To rotate an image:

```sh
magick <input> -rotate <angle> <output>
```

Some images have built-in rotation metadata and will be oriented properly in
most image viewers.

## Resize images

Use the `-resize` flag to resize images. Run:

```sh
magick <input> -resize <width>x<height> <output>
```

To break the aspect ratio when resizing, use a `!` on one of the dimensions. See
below:

```sh
magick <input> -resize <width>x<height>! <output>
```

Because `!` is a command in many shells, be sure to escape it (`\!`) in
practice.

## Crop images

To crop images, use the `-crop` flag. Format is as follows:

```sh
magick <input> -crop <width>x<height>+<x offset>+<y offset> <output>
```

Coordinates start (0,0) at top left.

## Split an image into separate images

To split an image into two equal halves along the vertical axis, run:

```sh
magick <image> -crop 50%x100% +repage <output>
```

Adjust the first percentage for width and the second for height. Using the same
name for `<image>` and `<output>` will result in a sequence of files with
`<input>-%d.<ext>`, where `%d` is an integer and `<ext>` is the extension of the
input file.

## Combine images

To append a sequence of images along a single axis, run either:

```sh
magick -append <image1> <image2> ... <output>
```

or,

```sh
magick +append <image1> <image2> ... <output>
```

Using `-append` appends images vertically, and `+append` does so horizontally.
