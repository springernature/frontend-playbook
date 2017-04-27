# Images

This document describes best practices for the use of images on the web at Springer Nature.

In a front-end workflow we typically deal with two kinds of image:

* **User interface images**, including icons, logos, and buttons. Usually managed by the frontend, these are stored with other client-side resources such as templates, CSS and JS. Like those resources, they may be shared between many different pages.

* **Content images**. These are unique to a page (or a handful of pages). They will usually be provided from a database or a content management system.

Most best practices are common to both categories.

## Formats

### Which format to use

* Use SVG for an icon, logo, or other image with sharply defined edges.
* Use JPEG for a still image, photograph, or in any other case where a PNG would be too large to be delivered over the network.
* Use PNG for an illustration, graph, flat-colour graphic, image containing transparency (which JPEG doesn't support), or an image containing text. An 8-bit PNG will usually also allow the delivery of an indexed colour image, with binary transparency, [at a smaller size than a GIF](https://helpx.adobe.com/photoshop-elements/using/optimizing-images-gif-or-png.html).

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

When optimising non-content images that are going to be committed to a repo, make sure you always use the maximum settings if you're using lossless optimisations.

For content images, we encourage using an image server like [Immagine](https://github.com/springernature/immagine) or an image service like [Kraken.io](https://kraken.io/) in order to:

* Ensure that images are optimised automatically.
* Ensure that appropriate cache headers are set.

Also, future improvements to these tools will automatically be reflected in all of the images being served, instead of them having to be re-encoded.

## Comparing the quality of images

Besides visual inspection, if you need to compare the quality of two different image compression formats, algorithms or quality settings, you may want to use something like the [SSIM index](http://en.wikipedia.org/wiki/Structural_similarity) to get an objective idea of the trade-off between quality and byte size.
