# Success Criterion 3.1.1 Language of Page and Success Criterion 3.1.2 Language of Parts

The HTML `lang` attribute is used to give information about the primary and secondary languages of your pages. It must be present and correct. 

See [Understanding Language of Page](https://www.w3.org/WAI/WCAG22/Understanding/language-of-page.html) and [Understanding Language of Parts](https://www.w3.org/WAI/WCAG22/Understanding/language-of-parts.html) for further details. 

The issues and remediations listed in this file are not exhaustive. 

## The issues

- [Specified language is incorrect](#specified-language-is-incorrect)
- [Change in language not specified](#change-in-language-not-specified)

### Specified language is incorrect

#### What's the problem?

The language specified in the HTML `lang` attribute doesn't match the language used for the main page. 

#### Who's affected by the problem?

* Screen reader users

#### Why's it a problem?

Words are pronounced differently in different languages. Screen reader software is designed to respect these pronunciation differences when it encounters web pages that specify their main language. 

If the language specified doesn't match the actual language used, the screen reader software may mispronounce the text of the page. 

#### How do I fix it? 

Make sure the language specified in the `lang` attribute accurately reflects the language of the page. If you provide a translated version of a page, make sure you provide the correct `lang` attribute, too. 

We do this:
```html
<html lang="es">
  ...
  <title>Las razas estándar de gansos</title>


<html lang="en">
  ...
  <title>The Standard Breeds of Geese</title>
```

We _don't_ do this:
```html
<html lang="en">
  ...
  <title>Die Standardrassen von Gänsen</title>
```

### Change in language not specified

#### What's the problem?

An element on the page contains text in a different language to the rest of the page, but the change in language isn't signalled with a `lang` attribute. 

#### Who's affected by the problem?

* Screen reader users

#### Why's it a problem?

Words are pronounced differently in different languages. Screen reader software is designed to respect these pronunciation differences when it encounters components on web pages that specify a change in language. 

If a piece of text in a document is presented in a different language without programmatically indicating the change, the screen reader software may mispronounce the text. 

#### How do I fix it? 

If you have text on a web page that is in a different language to the rest of the page, include the appropriate `lang` attribute in its wrapping element. 

We do this:
```html
<html lang="es">
  ...
  <title>Las razas estándar de gansos</title>
  ...
  <p lang="fr">C'est un belle journee sur le village, et tu es un méchant oie.</p>
```

We _don't_ do this:
```html
<html lang="en">
  ...
  <title>The Standard Breeds of Geese</title>
  ... 
  <p>C'est un belle journee sur le village, et tu es un méchant oie.</p>
```