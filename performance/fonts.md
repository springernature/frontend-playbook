# Fonts

## Formats

- Use a variable font if available. Always compress to .woff2. A [command line tool](https://github.com/google/woff2) from Google can be used for this task. 
- Also include a non-variable .woff file for Internet Explorer 11.  

## FOUT and FOIT

### `font-display`

Make use of `font-display`. For typefaces that are undistinctive and have a nice fallback websafe font consider using the value of `optional`. 

For distinctive and brand-critical fonts, use a value of `swap` or `fallback`. 

For typefaces that are important to the content such as fonts for displaying mathematical equations, use only `font-display: block;`. 

### Preloading

Consider preloading the regular Roman (non-italic, non-bold) version of your primary font. This can prevent FOUT and FOIT. Italic and bold variants can load later on.  