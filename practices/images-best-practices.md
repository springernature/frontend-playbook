# Best practices when dealing with images for the Web

This document describes the use of image at Springer Nature.

In a front-end workflow we typically deal with two kinds of images:

* **Icons, logos, buttons and other graphical elements** that are part of the User Interface of the page. These are usually managed by the frontend, and so they are stored with the rest of the resources (templates, CSS, JS). Like those resources, they may be shared between many different pages.

* **Content images**. These are unique to a page (or a handful of pages). They will be usually provided from a database or a content management system.

Most best practices are common to both categories.

## Formats

### What format to use

* Use SVGs for icons, logos, and other images with sharply defined edges, as long as you have access to the original image in a vector format (i.e. Adobe Illustrator). Don't convert vector to raster images, or raster images to SVG.
* Use JPEGs for still images, photography, or in any other case where using a PNG will generate an image that is too big to be delivered over the network.
* Use PNGs for illustrations, graphs, flat colour graphics, and other images with text. Also for images that require transparency, as JPEG doesn't support it.

### SVG images

Always minify your SVGs using [SVGO](https://github.com/svg/svgo) or a similar tool.

### JPEG images

When encoding JPEG images:

* Use progressive encoding. Progressive JPEGs provide a better user experience and, most of the time, are smaller than baseline. See this [yeoman issue](https://github.com/yeoman/yeoman/issues/810) for further details.
* Use [4:2:0](https://en.wikipedia.org/wiki/Chroma_subsampling#4:2:0) [chroma subsampling](https://en.wikipedia.org/wiki/Chroma_subsampling) whenever possible. This encodes the colour information at half the resolution of the luma, which may result in a perceptible loss of colour accuracy. This will usually generate much smaller images, so we suggest to create both of them and compare them for any loss of quality. For tools that can help you with this, see: [Comparing the quality of images](#comparing-the-quality-of-images), below.
* Use encoders like [Mozilla's mozjpeg](https://github.com/mozilla/mozjpeg) that can create smaller JPEGs with the same quality.

### PNG images

Always use the maximum compression level (9).

## Optimisation

* Make sure that you save images using an [sRGB](https://en.wikipedia.org/wiki/SRGB) ICC profile. Although modern browsers support images with ICCv2 profiles like [Adobe RGB](https://en.wikipedia.org/wiki/Adobe_RGB_color_space) and even [ProPhoto RGB](https://en.wikipedia.org/wiki/ProPhoto_RGB_color_space), colour space issues are extremely difficult to debug. Saving the images as sRGB and removing the colour profile is encouraged.
* Strip the metadata from the image. This includes:
    * EXIF data
    * Copyright information (unless required)
    * GPS data
    * Colour profiles
    * Thumbnails in JPEGs
    * Comments
    * Etc.
* Set appropriate cache headers for the images. (See [Serving images](#serving-images), below.)

For images that are going to be included in a repo, you can use tools like [ImageOptim](https://imageoptim.com/mac) to optimise them and strip the metadata before committing them.

There's also an [ImageOptim-CLI](https://github.com/JamieMason/ImageOptim-CLI) that can be integrated with CI systems.

## Serving images

We work under the assumption that images are encoded only once but decoded many times. Therefore, encoding times are usually secondary to the savings in e.g. file size.

When optimising non-content images that are going to be commited to a repo, make sure you always use the maximum settings if you're using lossless optimisations.

For content images, we encourage using an image server like [Immagine](https://github.com/springernature/immagine) or an image service like [Kraken.io](https://kraken.io/) in order to:

* Ensure that images are optimised automatically.
* Ensure that appropriate cache headers are set.

Also, future improvements to these tools will automatically be reflected in all of our images being served, instead of them having to be re-encoded.

## Comparing the quality of images

Besides visual inspection, if you need to compare the quality of two different image compression formats, algorithms or quality settings, you may want to use something like the [SSIM index](http://en.wikipedia.org/wiki/Structural_similarity) to get an objective idea of the trade-off between quality and byte size.
