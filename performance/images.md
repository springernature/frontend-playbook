# Images

- [Introduction](#introduction)
- [Picking the right image format](#picking-the-right-image-format)
- [Image formats](#image-formats)
  - [SVG images](#svg-images)
  - [JPEG images](#jpeg-images)
  - [PNG images](#png-images)
- [Optimisation of images](#optimisation-of-images)
- [Serving images](#serving-images)
- [Comparing the quality of images](#comparing-the-quality-of-images)

This document describes best practices for the use of images on the web at Springer Nature.

## Introduction

In a frontend workflow we typically deal with two different categories of images:

* **User interface images**. These include icons, logos, buttons, and any other image that is part of the user. Usually managed by the frontend, these are stored with other client-side resources such as templates, CSS and JS. Like those resources, they may be shared between many different pages.

* **Content images**. These are unique to a page, or a handful of pages. They will usually be provided from a database or a content management system.

Most best practices described in this document apply to both categories unless otherwise indicated.

## Picking the right image format

* Use [SVG](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics) for icons, logos, and other images with sharply defined edges.
* Use [JPEG](https://en.wikipedia.org/wiki/JPEG) for still images, photographs, and in any other cases where using a PNG would result in an image too large to be delivered over the network effectively.
* Use [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) for illustrations, graphs, flat-colour graphics, images containing transparency (which JPEG doesn't support), and images containing text.
* Use [MP4](https://en.wikipedia.org/wiki/MPEG-4_Part_14) for any kind of animated images.
* Do not use [GIFs](https://en.wikipedia.org/wiki/GIF). The file size of animated GIF images is usually an order of magnitude bigger than MP4s of similar quality. They can be a barrier that prevents users from accessing our content, especially in markets where slower connections and low performing devices are more common. For static images with transparency, an 8-bit PNG can be used to deliver an indexed colour image, with binary transparency, [at a smaller size than a GIF](https://helpx.adobe.com/photoshop-elements/using/optimizing-images-gif-or-png.html).

A number of more modern image formats can also be used to deliver images:

* [WebP](https://en.wikipedia.org/wiki/WebP) is a replacement for JPEG, PNG, and GIFs, but improvements to encoders like [mozjpeg](https://github.com/mozilla/mozjpeg) means that [WEBP file sizes are only marginally smaller than JPEG](https://siipo.la/blog/is-webp-really-better-than-jpeg). It's supported by almost all major browsers ([Safari supports it partially](https://caniuse.com/webp)) and must be used only as an enhancement to another better supported format.
* [AVIF](https://en.wikipedia.org/wiki/AVIF) is suitable for static and animated images, and supports both lossy and lossless compression with better compression efficiency and better detail preservation than other formats. It's [supported by Chrome and Firefox](https://caniuse.com/avif), and can be used only as an enhancement to another better supported format. Compression (encoding) of images can be significantly slower than with other formats.
* [JPEG-XL](https://en.wikipedia.org/wiki/JPEG_XL) supports both lossy and lossless compression. It's [more efficient than other formats while being usually faster](https://cloudinary.com/blog/how_jpeg_xl_compares_to_other_image_codecs) both when compressing and decompressing than JPEG. Unfortunately, as of November 2022 [no browser officially supports it](https://caniuse.com/jpegxl) and [Google has announced that it's removing preliminary support from Chrome](https://www.theregister.com/2022/10/31/jpeg_xl_axed_chrome/), in favour of AVIF.

## Image formats

### SVG images

Always minify your SVGs using [SVGO](https://github.com/svg/svgo) or a similar tool.

### JPEG images

When encoding JPEG images:

* Use progressive encoding. [Progressive JPEGs provide a better user experience and, most of the time, are smaller than baseline](https://github.com/yeoman/yeoman/issues/810).
* Use [4:2:0](https://en.wikipedia.org/wiki/Chroma_subsampling#4:2:0) [chroma subsampling](https://en.wikipedia.org/wiki/Chroma_subsampling) whenever possible. This encodes the colour information at half the resolution of the luma, usually generating smaller images. It may however result in a perceptible loss of colour accuracy, so we suggest to create both 4:4:4 and 4:2:0 versions of an image and compare them for any quality loss. See [Comparing the quality of images](#comparing-the-quality-of-images) below for tools that can help you with this.
* Use encoders like [Mozilla's mozjpeg](https://github.com/mozilla/mozjpeg) that can create images with the same visual quality as other encoders but a much smaller file size.

### PNG images

Always use the maximum compression level (9).

## Optimisation of images

Images can contribute significantly to the size of a page, so it's important to optimise them before they are delivered to the user. This helps ensure that our sites stay performant and we're not preventing anyone from accessing them due to increased page weight. Common optimisations include:

* Making sure that you save images using an [sRGB](https://en.wikipedia.org/wiki/SRGB) ICC profile. Although modern browsers support images with ICCv2 profiles like [Adobe RGB](https://en.wikipedia.org/wiki/Adobe_RGB_color_space) and even [ProPhoto RGB](https://en.wikipedia.org/wiki/ProPhoto_RGB_color_space), colour space issues are extremely difficult to debug. Saving the images as sRGB and removing the colour profile is encouraged.
* Stripping the metadata from the image. This includes things like EXIF data, Copyright information (unless required), GPS data, colour profiles, thumbnails (in JPEGs), comments, and others.
* [Setting appropriate cache headers for the images](#serving-images).

For images that are going to be included in a repository, tools like [ImageOptim](https://imageoptim.com/mac) can be used to optimise them and strip the metadata before committing them to your codebase. There's also an [ImageOptim-CLI](https://github.com/JamieMason/ImageOptim-CLI) that can be integrated with CI systems.

If an image is still too big after following all these optimisations, other options can be used that will require editing the image. These can be used to generate images with a much smaller size than otherwise would be possible:

* Reducing or completely eliminating noise and other complexity from the image, which makes it easier to compress.
* Blurring unimportant areas will also make the image easier to compress.
* Finally, decreasing the export quality may be required if the image is still too big.

## Serving images

We work under the assumption that images are encoded only once but decoded many times. Therefore, increased encoding times, while undesirable, are usually secondary to other concerns like making the image easier to decompress, or having a smaller file size.

When optimising non-content images that are going to be committed to a repo, make sure you always use the maximum settings if you're using lossless optimisations.

For content images, we encourage using an on-premise or cloud-based image server in order to:

* Ensure that all images are optimised automatically.
* Ensure that the appropriate cache headers are always set.

As an additional benefit, changes to these tools may result in improvements to the images being served automatically, without the images having to be manually re-encoded.

## Comparing the quality of images

When comparing the output of two different image compression formats, algorithms, or quality settings, [tools that calculate the similarity between images](https://github.com/kornelski/dssim) with algorithms like [SSIM](http://en.wikipedia.org/wiki/Structural_similarity) and [DSSIM](https://github.com/kornelski/dssim) can be used to get an objective idea of the trade-off between quality and byte size.
