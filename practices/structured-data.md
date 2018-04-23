# Structured data

In the context of the web, structured data refers to information describing and classifying the content of a webpage. For example; on a scientific article page, who the author is, what the article title is, and so on. Structured data contributes towards the vision of the [Semantic Web](https://en.wikipedia.org/wiki/Semantic_Web#Semantic_Web_solutions) as well as providing SEO benefit.

There are 4 widely accepted ways to implement structured data:
- [JSON-LD](https://en.wikipedia.org/wiki/JSON-LD) (a W3C Recommendation)
- [RDFa](https://en.wikipedia.org/wiki/RDFa) (a W3C Recommendation)
- [Microdata](https://en.wikipedia.org/wiki/Microdata_(HTML))
- [Microformat](https://en.wikipedia.org/wiki/Microformat)


## How we implement structured data

We primarily use JSON-LD. Information is defined in JSON using the [RDF](https://en.wikipedia.org/wiki/Resource_Description_Framework) format. You can add these inside `<script>` elements on the page (multiple JSON-LD script elements on a page are perfectly valid) or you can externalise the data as a file on it's own URL. Here's an example:
```html
<!-- An article, fully linked to the issue, volume, and periodical in which it was published -->
<script type="application/ld+json">
{
  "@context": "http://schema.org",
  "@graph": [
    {
        "@id": "#issue",
        "@type": "PublicationIssue",
        "issueNumber": "5",
        "datePublished": "2012",
        "isPartOf": {
            "@id": "#periodical",
            "@type": [
                "PublicationVolume",
                "Periodical"
            ],
            "name": "Cataloging & Classification Quarterly",
            "issn": [
                "1544-4554",
                "0163-9374"
            ],
            "volumeNumber": "50",
            "publisher": "Taylor & Francis Group"
        }
    },
    {
        "@type": "ScholarlyArticle",
        "isPartOf": "#issue",
        "description": "The library catalog as a catalog of works was an infectious idea, which together with research led to reconceptualization in the form of the FRBR conceptual model. Two categories of lacunae emerge--the expression entity, and gaps in the model such as aggregates and dynamic documents. Evidence needed to extend the FRBR model is available in contemporary research on instantiation. The challenge for the bibliographic community is to begin to think of FRBR as a form of knowledge organization system, adding a final dimension to classification. The articles in the present special issue offer a compendium of the promise of the FRBR model.",
        "sameAs": "http://dx.doi.org/10.1080/01639374.2012.682254",
        "about": [
            "Works",
            "Catalog"
        ],
        "pageEnd": "368",
        "pageStart": "360",
        "name": "Be Careful What You Wish For: FRBR, Some Lacunae, A Review",
        "author": "Smiraglia, Richard P."
    }
  ]
}
</script>
```

## Why JSON-LD?
Using JSON-LD instead of marking up HTML with one of the other techniques has benefits:

- Separation of structured data and HTML. Provides information about the page without binding it to specific HTML elements. This improves the maintainability of both HTML and structured data.
- Generally speaking, it will be easier to generate from the backend. This is especially true for apps that already deal with JSON data as part of their implementation.
- Easier for client apps to consume if you consider that those apps no longer need to trawl through HTML to extract.
- JSON-LD is an official [W3C Recommendation](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium#W3C_recommendation_(REC)).
- Google [recommends](https://developers.google.com/search/docs/guides/intro-structured-data) JSON-LD for structured data.

## Vocabulary
A shared, standardised vocabulary ensures that structured data is interpreted consistently by people and machines. We use the vocabulary defined and maintained at [https://www.schema.org](https://www.schema.org). Since its creation in 2011 by Google, Bing, Yahoo! and Yandex this vocabulary has been widely adopted and is the most commonly implemented.

Tip - after adding a new JSON-LD script to your website, be sure to validate your use of vocabulary by using [Google’s structured data test tool](https://search.google.com/structured-data/testing-tool).
