# Structured data

In the context of the web, structured data refers to information describing and classifying the content of a webpage. For example; on a scientific article page, who the author is, what the article title is, and so on. Structured data contributes towards the vision of the [Semantic Web](https://en.wikipedia.org/wiki/Semantic_Web#Semantic_Web_solutions) as well as providing SEO benefit. There are 4 widely accepted ways to implement structured data:
- [JSON-LD](https://en.wikipedia.org/wiki/JSON-LD) (a W3C Recommendation)
- [RDFa](https://en.wikipedia.org/wiki/RDFa) (a W3C Recommendation)
- [Microdata](https://en.wikipedia.org/wiki/Microdata_(HTML))
- [Microformat](https://en.wikipedia.org/wiki/Microformat)


## How we implement structured data

Our primary method of implementation is JSON-LD. This involves defining information in JSON, adhering to the [RDF](https://en.wikipedia.org/wiki/Resource_Description_Framework) format. Here's an example:
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