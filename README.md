# Stereogram

A bash script to process 3D MPO JPEG files. Turning MPOs into other types of stereo image can be tedious and a lot of manual work. This script wraps exiftool and ImageMagick to automate the process.

## Prequisites

* exiftool
* ImageMagick

On macOS (Homebrew):

```bash
brew install exiftool imagemagick
```
## Compatibility

Tested on macOS Mojave. Should work on other Linux or BSD distros.

## Usage

To create 'triples' from MPOs in the current working directory:

```bash
stereogram
```

## Options

```bash
-i /path/to/mpos
```

```bash
-i /path/to/mpo/file.mpo
```

Specify an input file or directory. If the path is a directory, all MPOs will be processed. Default: Current working directory.

```bash
-o /path/to/mpos
```

```bash
-o /path/to/mpo/file.mpo
```

Specify an output file or directory. Default: Current working directory.

```bash
-s anaglyph
```

Specify the type of stereo image to create. Default is 'triple'. See 'Stereo types' for available values.


```bash
-w /path/to/dir
```

By default the input directory is also used as the working directory where split (left and right) files are placed. This switch overrides that value.

```bash
-e
```

If specified, an attempt is made to auto-enhance the image using ImageMagick before further processing. Does not affect the original image.

```bash
-k
```

Keep split files. If omitted the left and right images are deleted after processing. Combine with `-s none` to just split MPO files.

```bash
-n
```

Do not overwrite existing L/R split files. This can be useful for manual image enhancement. Run `stereogram -k -s none` to just create the split files, then do the enhancement work on the L and R images then run `stereogram -n` to create stereos from those files.

## Stereo Types

The following types of 3D image can be generated using the `-s` switch:

**triple**

The default mode. Creates a side-by-side image in the format LEFT-RIGHT-LEFT making the image suitable for cross-eye (left 2) and parallel (right 2) viewing.

**crosseye**

Side-by-side image in the form L R

**parallel**

Side-by-side image in the form R L

**anaglyph**

Classic red-blue greyscale image

**all**

Creates one of each of the above image types.

**none**

Do not create a stereo image. Handy if you just want to split the files into left and right images.

## Note on File Names

Example: `DSC12345.MPO`

When the MPO is split into it's left and right parts:

`DSC12345_L.jpg` and `DSC12345_R.jpg`

Stereo types:

`DSC12345_triple.jpg`

`DSC12345_crosseye.jpg`

`DSC12345_parallel.jpg`

`DSC12345_anaglyph.jpg`

