# Language style guide

* [Writing style](#writing-style)
  * [Tone of voice](#tone-of-voice)
  * [Plain English](#plain-english)
  * [Technical writing](#technical-writing)
* [Frontend or front-end](#frontend-or-front-end)

## Writing style

We don't enforce strict standards on writing style as we want you to use your own words to express your own personality. That said, we have three general sets of guidelines - tone of voice, plain English, and technical writing.

### Tone of voice

For a general audience, you should write like a human. Be professional, but conversational - we want our contributors and readers to feel comfortable joining in at any time.

Be thankful to contributors and those who log issues. They're giving up their time to make our playbook better. Make sure they know we're grateful to them.

Maintain the same friendly and professional standards across the entire repository - in documentation, issues, pull requests, and comments.

Always use [inclusive language](inclusive-language.md).

### Plain English

Follow Plain English guidelines to help safeguard the accessibility of your written content. All relevant guidelines for [writing well][writing-well] apply. You might find tools like [Hemingway App](http://www.hemingwayapp.com/) helpful when editing. In particular:

* Be concise
  * Check any sentences with more than 25 words to see if you can split them to make them clearer.
  * Ideally no more than 1-2 points per sentence.
  * Use contractions (e.g. "can't", "it's").
  * Go straight to the point.
  * Avoid unnecessary words (e.g. There is, It is, very, really, pretty, just, actually). 
* Be specific
  - Prefer the active voice to the passive voice<sup>[\[1\]][active-passive]</sup> (e.g. "NPM will install the dependencies" instead of "the dependencies will be installed").
  * Address the reader as "you" where possible.
  * Avoid referring to "things" or "stuff".
  * Be direct. Avoid metaphor, simile, and slang.
* Be informative
  * Consider your audience. General information may not look the same as information aimed at a technical audience.
  * Be as precise as you can usefully be - consider linking to high quality external resources where relevant.

### Technical writing

When expressing technical concepts, you'll need to use technical language. This may be complex, contain jargon, or seem formal. That's ok! Technical writing isn't for a general audience. Your priorities must be clarity, brevity, and accuracy. If you think your reader may need additional context to understand a concept, link out to external resources. 

All of the advice in the [plain English](#plain-english) section applies. Additionally:

* Expand acronyms the first time you use them, and limit their use thereafter e.g. "Avoid the use of TLAs (Three Letter Acronyms)".
* When defining technical requirements, you may use the keywords defined in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt) for those requirement levels, e.g. "MUST", "SHOULD", "OPTIONAL", etc.

## Frontend or front-end

Always use `frontend` regardless of the context. It's less confusing and error prone, and ensures consistency across all our documentation and portfolio of products.

[writing-well]: http://writersdiet.com/?page_id=16
[active-passive]: https://oxfordediting.com/the-active-verb-form-makes-academic-writing-more-readable/
