# Accessibility in PDFs

- [A warning](#a-warning)
- [Is PDF the right choice?](#is-pdf-the-right-choice)
- [Creating accessible PDF documents](#creating-accessible-pdf-documents)
- [Creation From a word processor (e.g. Microsoft Word or Google Docs with Grackle)](#creation-from-a-word-processor-eg-microsoft-word-or-google-docs-with-grackle)
  - [Headings](#headings)
  - [Alt text](#alt-text)
  - [Links](#links)
  - [Contrast](#contrast)
  - [Colour](#colour)
  - [Built-in structure and navigation](#built-in-structure-and-navigation)
  - [Tables](#tables)
  - [Rich media](#rich-media)
  - [Forms](#forms)
  - [Font Size](#font-size)
- [Further resources](#further-resources)

## A warning

If you’re concerned about the accessibility of your Portable Document Format (PDF) documents, then you should [consult a specialist like AbilityNet](https://www.abilitynet.org.uk/creating-accessible-pdfs) to review what you have, make expert recommendations, and potentially remediate issues for you. 

## Is PDF the right choice?

PDF is not the best document format for accessibility. It will always contain accessibility issues. PDF is a fixed dimension format intended for printing, and some user accessibility requirements --such as reflow, text resizing or changing text spacing-- are not supported in PDF format.

We recommend that you avoid using PDF if you can, and prioritise accessible alternatives instead, such as HTML or [EPUB](https://www.w3.org/publishing/epub32/). As a reference, please read [why UK Government content should be published in HTML and not PDF](https://gds.blog.gov.uk/2018/07/16/why-gov-uk-content-should-be-published-in-html-and-not-pdf/).

If you don’t have a choice, then you must purposefully build your PDFs to be accessible - **it doesn’t happen automatically**. 

## Creating accessible PDF documents

PDF is a destination format, created from a source document (e.g. Microsoft Word or Adobe InDesign). In order to create accessible PDFs, the source documents themselves must be accessible. For screen reader users, this means the document must be correctly formatted with headings and alternative text, among other requirements. A correctly-formatted document can be exported as a [tagged PDF](https://helpx.adobe.com/uk/acrobat/using/creating-accessible-pdfs.html#tag_the_pdf), which allows screen reader software to describe the meaning of different pieces of text. 

Some source document applications include an automated accessibility checker to help you identify basic accessibility issues.

Microsoft has an [accessibility checker](https://support.microsoft.com/en-us/topic/improve-accessibility-with-the-accessibility-checker-a16f6de0-2f39-4a2b-8bd8-5ad801426c7f) built into its tools. When you save a document as a PDF, make sure that the option to save tagged PDFs is checked.

[Grackle Docs](https://www.grackledocs.com/) is a Google Workspace addon that does the same thing for Google suite documents. You’ll need a [paid plan](https://www.grackledocs.com/features/create-tagged-pdf/) to export tagged PDFs from Grackle. 

## Creation From a word processor (e.g. Microsoft Word or Google Docs with Grackle)

### Headings

Make sure that all your heading text is formatted using the built-in heading styles. This way, those texts will be marked as headings both in the source document and in the PDF document. Don’t just use paragraph text with a bigger font size - these won’t be properly tagged in the final PDF document.

Screen reader users need headings to be arranged in a logical order, without skipping levels (first Heading 1, then same level or Heading 2, but not skipping to Heading 3). Don’t use the built-in heading levels to control the visual appearance of text in your document - use the font size and style settings for that. 

### Alt text

Visual content (pictures, graphics, charts etc) that convey meaning must include alternative text describing that meaning for screen reader users.

If the visual content is decorative (conveys no meaning) and the software provides the option to mark it as decorative, then it must be marked as decorative so that it can be ignored by screen readers.

The [Web Accessibility Initiative](https://www.w3.org/WAI/) has produced an alternative text decision tree to help you decide whether an image is decorative or meaningful: [An alt decision tree](https://www.w3.org/WAI/tutorials/images/decision-tree/)

### Links

Links must have concise, meaningful, descriptive text so that screen reader users can understand their purpose. Screen reader users don’t always read the whole page in context - they may jump from link to link without reading the surrounding text. 

Avoid link text that says “click here” or “more” - be more specific. Focus on where the link is going, and try to describe it as concisely as you usefully can. 

WebAIM has published guidance on [what good link text looks like](https://webaim.org/techniques/hypertext/link_text) (the final section on “hover and focus effects” is for websites only, and isn’t relevant to PDF documents).

### Contrast

Text must have enough contrast with the background colour in order to be visible and readable by as many users as possible. Text contrast is measured in a ratio and at least a minimum 4.5:1 ratio must be achieved. Use a tool to check your contrast ratio, like the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).

### Colour

Don’t use colour as the only way of conveying information (for example colouring some text in red to indicate a problem, but having no other way of indicating that the problem exists). Blind or low vision user may not be able to see your colours well or at all, and some colourblind users may be unable to distinguish between certain colours. 

### Built-in structure and navigation 

Order lists with bullet points or numbers using the built-in list creation tools in your word processor. 

Include a table of contents, and add page numbers.

### Tables

Microsoft Word can only help to make basic tables accessible. You must manually tag these after the document has been created (see [Fixing non-accessible PDFs below](#how-to-fix-non-accessible-PDFS?)). 

Google documents do not have the ability to mark up tables correctly, but the Grackle Docs addon allows you to remediate tables once you’ve built them. 

### Rich media

If your PDF contains rich media files like audio or video, it must also include alternatives so that users who can’t see or hear the media can still understand what it conveys. 

Depending on the rich media you use, this may involve [transcripts, closed captions, and/or audio description](https://www.w3.org/WAI/media/av/). 

### Forms

Consider whether you really need to use a PDF file for your purposes - can you achieve the same results with a webpage, or with a survey tool like Google Forms or SurveyMonkey? 

Forms created in your source document will not be accessible without further work. If you have no choice but to use a PDF, you’ll need to add your form fields manually with Adobe Acrobat Pro DC. See WebAIM’s guide to [Accessible Forms in Acrobat](https://webaim.org/techniques/acrobat/forms) for more details. 

### Font Size

PDF documents don’t let the user change the font size, so avoid small text sizes.

## Further resources

- [Microsoft: How to make your Word documents accessible to people with disabilities](https://support.microsoft.com/en-us/topic/make-your-word-documents-accessible-to-people-with-disabilities-d9bf3683-87ac-47ea-b91a-78dcacb3c66d)
- [Google: Make your document or presentation more accessible](https://support.google.com/docs/answer/6199477?hl=en-GB)

# How to fix non-accessible PDFs?

Fixing a non-accessible PDF requires using Adobe Acrobat Pro to manually tag the whole document. This could be a time consuming, tedious task, so it's best to create an accessible PDF from an accessible native document (e.g. Word, Google documents, or InDesign).

If you have no choice, follow the guidelines from Adobe on [Creating Accessible PDFs in Adobe Acrobat](https://helpx.adobe.com/acrobat/using/creating-accessible-pdfs.html), and remember that some issues (e.g. low contrast) may not be fixed with this method. 

A full explanation of tagging PDFs is out of scope for this document - if you need training or support to do this kind of remediation work, we recommend [contacting a specialist like AbilityNet](https://www.abilitynet.org.uk/creating-accessible-pdfs) to help you understand what needs to be done and how to do it. 

# References

- [PDF Accessibility Overview (Adobe)](https://www.adobe.com/accessibility/pdf/pdf-accessibility-overview.html)
- [Create and Verify PDF Accessibility (Adobe)](https://helpx.adobe.com/acrobat/using/create-verify-pdf-accessibility.html)
- [Creating Accessible PDFs (Adobe InDesign)](https://helpx.adobe.com/indesign/using/creating-accessible-pdfs.html)
- [Create Accessible PDFs (Microsoft)](https://support.microsoft.com/en-us/topic/create-accessible-pdfs-064625e0-56ea-4e16-ad71-3aa33bb4b7ed)
- [PDF Accessibility (WebAIM)](https://webaim.org/techniques/acrobat/)
