# Graded Browser Support



| Tables        | Grade-A support | Grade-C support  |
| ------------- |:---------------:| ----------------:|
| Chrome        | latest stable   |                  |
| Edge          | latest stable   |                  |
| Firefox       | latest stable   |               $1 |
| IE            | 9, 10, 11       |               <9 |
| Opera         | latest stable   |              <10 |
| Safari        | latest stable, latest stable -1   |  <4.1 (desktop) |
| Webkit        | Android 4.&#8224; |  <3           |

## Graded Browser Support: What and Why

In the first 10 years of professional web development, back in the early '90s, browser support was binary: Do you - or don't you - support a given browser? When the answer was "No", user access to the site was often actively prevented. In the years following IE5's release in 1998, professional web designers and developers have become accustomed to asking at the outset of any new undertaking, "Do I have to support Netscape 4.x browsers for this project?"


By contrast, in modern web development we must support all browsers. Choosing to exclude a segment of users is inappropriate, and, with a "Graded Browser Support" strategy, unnecessary.

Graded Browser Support offers two fundamental ideas:

- A broader and more reasonable definition of "support."
- The notion of "grades" of support.

## What Does "Support" Mean?

Support does not mean that everybody gets the same thing. Expecting two users using different browser software to have an identical experience fails to embrace or acknowledge the heterogeneous essence of the Web. In fact, requiring the same experience for all users creates an artificial barrier to participation. Availability and accessibility of content should be our key priority.

Consider television. At the core: TV distributes information. A hand-cranked emergency radio is capable of receiving television audio transmissions. It would be counter-productive to prevent access to this content, even though it's a fringe experience.

Some viewers still have black-and-white televisions. Broadcasting only in black-and-white - the "lowest common denominator" approach - ensures a shared experience but benefits no one. Excluding the black-and-white television owners - the "you must be this tall to ride" approach - provides no benefit either.
An appropriate support strategy allows every user to consume as much visual and interactive richness as their environment can support. This approach-commonly referred to as progressive enhancement - builds a rich experience on top of an accessible core, without compromising that core.

## Progressive Enhancement vs. Graceful Degradation

The concepts of graceful degradation and progressive enhancement are often applied to describe browser support strategies. Indeed, they are closely related approaches to the engineering of "fault tolerance".

These two concepts influence decision-making about browser support. Because they reflect different priorities, they frame the support discussion differently. Graceful degradation prioritizes presentation, and permits less widely-used browsers to receive less (and give less to the user). Progressive enhancement puts content at the center, and allows most browsers to receive more (and show more to the user). While close in meaning, progressive enhancement is a healthier and more forward-looking approach. Progressive enhancement is a core concept of Graded Browser Support.


## What are Grades of Support?

While an inclusive definition of browser support is necessary, the support continuum does present design, development, and testing challenges. If anything goes, how do I know when the experience is broken? To address this question and return a sense of order to the system, we define grades of support. There are three grades: A-grade, C-grade, and X-grade support.

Before examining each grade, here are some characteristics useful for defining levels of support.
Identified vs. Unknown There are over 10,000 browser brands, versions, and configurations and that number is growing. It is possible to group known browsers together.

Capable vs. Incapable No two browsers have an identical implementation. However, it is possible to group browsers according to their support for most web standards.

Modern vs. Antiquated As newer browser versions are released, the relevancy of earlier versions decreases.
Common vs. Rare There are thousands of browsers in use, but only a few dozen are widely used.



## Three Grades of Support

### C-grade

C-grade is the base level of support, providing core content and functionality. It is sometimes called core support. Delivered via nothing more than semantic HTML, the content and experience is highly accessible, unenhanced by decoration or advanced functionality, and forward and backward compatible. Layers of style and behavior are omitted.

C-grade browsers should be identified on a blacklist.

Summary: C-grade browsers are identified, incapable, antiquated and rare.


### A-grade

A-grade support is the highest support level. By taking full advantage of the powerful capabilities of modern web standards, the A-grade experience provides advanced functionality and visual fidelity.

A-grade browsers should be identified on a whitelist. Approximately 96% of our audience enjoys an A-grade experience.

Summary: A-grade browsers are identified, capable, modern and common.


### X-grade

X-grade provides support for unknown, fringe or rare browsers as well as browsers on which development has ceased. Browsers receiving X-grade support are assumed to be capable. (If a browser is shown to be incapable - if it chokes on modern methodologies and its user would be better served without decoration or functionality - then it should considered a C-grade browser.)

X-grade browsers are all browsers not designated as any other grade.

Summary: X-grade browsers are assumed to be capable and modern.


### The Relationship Between A-grade and X-grade Support

Unlike the C-grade, which receives only HTML, the X-grade receives everything that A-grade does. Though a brand-new browser might be characterised initially as a X-grade browser, we give its users every chance to have the same experience as A-grade browsers.

## Conclusion

Graded Browser Support provides an inclusive definition of support and a framework for taming the ever-expanding world of browsers and frontend technologies.

Tim Berners-Lee, inventor of the World Wide Web and director of the W3C, has said it best:

> > "Anyone who slaps a 'this page is best viewed with Browser X' label on a Web page appears to be yearning for the bad old days, before the Web, when you had very little chance of reading a document written on another computer, another word processor, or another network."


- Reproduced from guidelines by [http://nate.koechley.com/](Nate Koechely)
