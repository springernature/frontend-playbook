# Inclusive language

* [Non-discriminatory language](#non-discriminatory-language)
  * [Unacceptable language](#unacceptable-language)
  * [Language that excludes](#language-that-excludes)
  * [Gendered language](#gendered-language)
  * [Disability and accessibility](#disability-and-accessibility)

## Non-discriminatory language

[Discrimination](https://en.wikipedia.org/wiki/Discrimination) is prohibited under law in the UK and many other countries.

Language is our main form of communication and it plays a powerful role both in contributing to and in eliminating discrimination.

Language influences thinking. For example, Hebrew uses gender markers, whereas Finnish doesn’t mark gender at all. A study done in the 1980s<sup>[\[1\]][wiley]</sup> found that kids who spoke Hebrew knew their own genders a year earlier than those who grew up speaking Finnish.

Inclusive language is language that is free from words, phrases or tones that reflect prejudiced, stereotyped or discriminatory views of particular people or groups. It is also language that doesn't deliberately or inadvertently exclude people from being seen as part of a group<sup>[\[2\]][govau]</sup>.

We're committed to using inclusive, non-discriminatory language in every written or verbal communication.

### Unacceptable language

Inappropriate or unacceptable language highlights perceived or actual differences between people. The use of insensitive and inappropriate language can create a hostile environment for people who have protected characteristics, as outlined in the [Equality Act 2010](http://www.legislation.gov.uk/ukpga/2010/15/contents).

Stereotyping means presuming a range of things about people based on their personal characteristics. These may include their appearance, apparent intelligence, personality or character, or their gender, sexual orientation, race, ethnicity, age, location, socioeconomic status or disability. We don't use language that reinforces stereotypes.

### Language that excludes

Language matters. It remains a common practice in IT to use terminology like slave/master or blacklist/whitelist that reference slavery or segregation.

There's always a better way to label the relationship between two entities. In the case of databases, choosing more descriptive terms like replica/primary, secondary/primary, follower/leader or standby/active instead of slave/master not only removes the reference to slavery, but also makes it easier to understand as it [avoids metaphor](https://github.com/springernature/frontend-playbook/blob/main/writing/house-style.md#plain-english).

Similarly, in the case of blacklist/whitelist there are alternatives that better show their purpose to people not familiar with the terminology, like denylist/allowlist, blocklist/allowlist or block/permit. Choose a term that is appropriate and descriptive for your particular app or feature.

["Treat problematic terminology as technical debt. When you learn that you have it in your projects, make it a priority to remove it."](https://blog.carbonfive.com/problematic-terminology-in-open-source/)

The [IETF has published a document (ietf.org)](https://tools.ietf.org/html/draft-knodel-terminology-01) that further describes the reasoning for avoiding this kind of language alongside further alternatives.

### Gendered language

In most cases your writing will address the reader directly as "you", but if you do need to write about people in the abstract, avoid language that centers the male identity as the default. Try recasting your sentences as plural to make them more inclusive and concise. You can also use the [singular _they_](https://www.poynter.org/reporting-editing/2015/the-washington-post-will-allow-singular-they/) as per the Washington Post.

Avoid "bro" language, even in verbal communication.

We _don't_ say this:
> Each student must complete his or her homework.

> Server: Hello.
>
> Client: Hey _bro_, I have a message for you.

> Hey guys!

We say this:
> All students must complete their homework

> Server: Hello.
>
> Client: Hey server, I have a message for you.

> Hey people!  
> Hey team!

### Disability and accessibility

Using inclusive language is critical when writing about accessibility. Avoid references that dehumanise or 'other' people, or that cast them as helpless victims. Never use collective nouns like "the disabled" or "the blind" - these words are descriptors, not group labels.

Use positive language that emphasises abilities rather than limitations. Consider whether you need to refer to a disability at all - for example, instead of writing about "users who are unable to use a mouse", perhaps you can be more precise with "keyboard users", or "users of alternative input devices".

We _don't_ say this:

> The disabled.  
> Dyslexics.  
> Susan is a victim of blindness.  
> People suffering from deafness.  
> Users who cannot see a screen.  

We say this:

> Disabled people.  
> Dyslexic people.  
> Susan is blind.  
> Deaf people.  
> Screenreader users / blind users. [where relevant]

The Special Interest Group on Accessible Computing (SIGACCESS) has published a [comprehensive guide to writing about disability](http://www.sigaccess.org/welcome-to-sigaccess/resources/accessible-writing-guide/) within the context of science and technology.

You may also find the more general [gov.uk inclusive language guidance](https://www.gov.uk/government/publications/inclusive-communication/inclusive-language-words-to-use-and-avoid-when-writing-about-disability) helpful.

[govau]: https://www.education.tas.gov.au/documentcentre/Documents/Guidelines-for-Inclusive-Language.pdf "Guidelines for Inclusive Language"
[hemingway]: http://www.hemingwayapp.com/
[wiley]: http://onlinelibrary.wiley.com/doi/10.1111/j.1467-1770.1982.tb00973.x/abstract "Language environment and gender identity attainment"
