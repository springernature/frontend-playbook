# Fonts

## Formats

- Use a variable font if available. Always compress to .woff2. [Google's command line compression tool](https://github.com/google/woff2) can be used for this task. 
- Also include a non-variable .woff file for Internet Explorer 11.  

## Flash of Unstyled Text (FOUT) and Flash of Invisible Text (FOIT)

### `font-display`

Make use of `font-display`. For typefaces that are undistinctive and have a nice fallback websafe font consider using the value of `optional`. If the custom font offers only a slight design/readability improvement, using a websafe fallback font is superior to FOIT and FOUT. 

For distinctive and brand-critical fonts, use a value of `swap` or `fallback`. For these fonts brand consistency is more important than avoiding FOUT and FOIT.  

For typefaces that are important to the content such as fonts for displaying mathematical equations, use only `font-display: block;`. It is better for these fonts to load late than to not load at all, seeing as they are critical for the correct rendering of content.

### Preloading

Consider preloading the regular Roman (non-italic, non-bold) version of your primary font. This can prevent FOUT and FOIT. Italic and bold variants can load later on without adversely affecting user perception. 

e.g.: 

`<link rel="preload" href="/static/fonts/Lora-Regular.woff2" type="font/woff2" as="font" crossorigin>`