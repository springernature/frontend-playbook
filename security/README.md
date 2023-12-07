# Security

This document intends to provide frontend developers with a basic primer in security issues; relating both to client-side technologies, and technologies serve client-side code.

## Risk

It is a common misconception that "hackers are not interested in my product". **This is not true.**  If you have a web server connected to the internet, you have resources someone will want to abuse.

All public web applications are under constant automated attack; from those looking to steal server resources to conduct blackhat SEO, mine cryptocurrencies, distribute malware, send spam, etc.

Additionally organisations with ecommerce sites are under increased risk from those looking to steal payment information.

Your site *is* at risk.

Another common misconception is that security doesn't matter much for frontend technologies, and that security is a job just for backend developers and network people. **This is not true.**

Client-side technologies can be misused to:
 - distribute malware.
 - steal sessions and impersonate users.
 - steal payment information.
 - deface pages causing reputational and SEO harm.
 - act as viruses/worms to DDoS victim servers, DDoS other servers...
 - exploit a security hole in one web site to attack a different web site under the same main domain.
 - automate form submissions.
 - crash users browsers.
 - "and more"

### This is terrible! What can we do?

Yes, yes this *is* terrible. The internet was originally designed to be robust, not secure; but web standards have evolved to meet increasing security threats, and we will look at some of these standards.

The good news is, by following some basic principles and using some standardised technologies we can go a long way towards making our web sites safer for our users and our organisation.

## Basic principles

### Never trust the client

People can use scripts as well as browsers to access your site, and use techologies to tamper with requests or the DOM, or perhaps the attack originates from an innocent user infected with malware. In any case, we must **never trust the client**. Any and all information from the client can be tampered with, including:

  - URL query parameters
  - URL fragment identifiers
  - browser `localStorage` etc.
  - anything in the DOM
  - any HTTP header, notably:
    - cookie names
    - cookie values
    - `User-Agent` string
    - `Referer`

A little paranoia can be healthy.

### Sanitise all user input

As web developers we have to process information that browsers send us, so what can we do?

The process of "cleaning" incoming data to make sure it's suitable for use in your application is known as "sanitisation".  Obviously this includes things like search terms typed into a text box, but now we have learned to **never trust the client**, we know we must sanitise *all* data the browser sends us.

How do we do that?

#### Program defensively

#### Don't do it yourself

Security is hard. But security is also a problem the industry shares. So the good news is, people much smarter than you or I have already thought about these problems, and written software we can use to do the hard stuff.

We will talk about some of this software later, but here's some more general principles on this topic:

 - Never try to write your own crypto. It's harder than you think.
 - Never try to write your own authentication/login systems. It's harder than you think, and many open-source offerings are immature and of questionable quality.
 - Avoid reimplementing browser features. The smart thing to do is leverage the security and development expertise of browser vendors, who have been working on these problems for decades.

#### Onion-skin defense


## Useful standardised technologies

* [Secure markup](secure-markup.md)

[Main table of contents](../README.md#table-of-contents)
