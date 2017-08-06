# Image Crop

Bulk crop images based on CSV input.

## Installation

Required Python version: 3.3 or higher.

Required packages:

- [GraphicsMagic](http://www.graphicsmagick.org/)

Required Python packages:

```
pip install click
```

## Usage

Image Crop takes a space-separated CSV file as its input in the following format:

```
<FILE_PATH> <OFFSET_LEFT_PX> <OFFSET_TOP_PX> <WIDTH_PX> <HEIGHT_PX>
<FILE_PATH> <OFFSET_LEFT_PX> <OFFSET_TOP_PX> <WIDTH_PX> <HEIGHT_PX>
...
```

The CSV is then read from the standard input (stdin).

Internally, Image Crop will run GraphicsMagic in the following format:

```
gm convert "<FILE_PATH>" -crop <WIDTH_PX>x<HEIGHT_PX>+<OFFSET_LEFT>+<OFFSET_TOP> "<FILE_BASENAME>__crop.<FILE_EXT>"
```

## Example

```
echo '"My Images/DSC-123.JPG" 5 10 600 350' | ./image_crop
```

Resulting GraphicsMagic call:

```
gm convert "My Images/DSC-123.JPG" -crop 600x350+5+10 "My Images/DSC-123__crop.JPG"
```

## More options

__--suffix, -s__: File name suffix, defaults to "__crop"

__--resize-width, -rw__: Resize the resulting image to exactly this width, optional.

__--resize-height, -rh__: Resize the resulting image to exactly this height, optional.

If only one of __--resize-width__ or __--resize-height__ options are passed, then the
other dimension will be calculated in such a way, that the original image aspect ratio
is preserved.

### Example

```
echo '"My Images/DSC-123.JPG" 5 10 600 350' | ./image_crop --suffix "-mod" -rw 1080
```

Resulting GraphicsMagic call:

```
gm convert "My Images/DSC-123.JPG" -crop 600x350+5+10 -resize 1080x "My Images/DSC-123-mod.JPG"
```

## Help

```
./image_crop --help
```

## Contributing

__Feel free to remix this piece of software.__ See [NOTICE](./NOTICE) and [LICENSE](./LICENSE) for license information.
