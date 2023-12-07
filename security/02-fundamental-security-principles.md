# Fundamental security principles

## Never trust the client

When building [client-server](https://www.britannica.com/technology/client-server-architecture) 
 web applications, be aware that people can use scripts as well as browsers to access your site, and use techologies to tamper with [HTTP requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Session) 
 or the [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction). 
 It's also likely your attacker is an innocent user infected with malware.

In any case, we must **never trust the client**. Any and all information from the client can be tampered with, including:

  - URL query parameters.
  - URL fragment identifiers.
  - browser `localStorage` etc.
  - any HTTP header, notably:
    - cookie names.
    - cookie values.
    - `User-Agent` string.
    - `Referer` field.
  - anything in the DOM, that might be read by your JavaScript, e.g:
    - form fields, whether `hidden` or `disabled` or not.
    - `class` & `id` values, other HTML element attributes...

A little paranoia can be healthy.

## Sanitise all user input and output

As web developers we have to process information that browsers send us, so how can we do this safely?

The process of "cleaning" incoming data to make sure it's suitable for use in your application is known as "sanitisation".  Obviously this includes things like search terms typed into a text box, but now we have learned to **never trust the client**, we know we must sanitise *all* data the browser sends us.

But this is difficult, because HTTP allows input to be encoded in many different ways and 
[something as "simple" as a URL can be surprisingly tricky](https://url.spec.whatwg.org/). 
Data that might not be problematic to one part of the system might create a big problem once it hits another part of the system.

Another idea is to be lax with incoming data, and instead sanitise data when it is being sent to the client. An interesting idea; except when the incoming data is destroying your databases, or storing information on your servers you _really_ don't want to be there, or gets transmitted to systems owned by other companies via analytics and marketing products. This can cause legal as well as security problems! So we can't rely on that alone.

So how do we sanitise data?

### Defensive programming

[Defensive programming](https://en.wikipedia.org/wiki/Defensive_programming) 
 is a topic in itself. The WikiPedia page linked describes it as "[ensuring] the continuing function of a piece of software under unforeseen circumstances".

This principle has many applications, and is commonly used in functions where we should:
1. Be very strict about what data we accept as an input.
1. Define what data we expect ("allow-list") which is known, not the data we do not want ("deny-list") which we can never fully know.
1. Fail early, and fail safely.

The same principle applies to web application architectures, and should be considered in all interactions between the user, client and server.

We will look at some examples later.

## Don't do it yourself

Security is hard. But security is also a problem the industry shares. So the good news is, people much smarter than you or I have already thought about these problems, and written software we can use to do the hard stuff.

We will talk about some of this software later, but here's some more general principles on this topic:

 - Never try to write your own crypto. It's harder than you think.
 - Never try to write your own authentication/login systems. It's harder than you think.
 - Avoid reimplementing browser features. The smart thing to do is leverage the security and development expertise of browser vendors, who have been working on these problems for decades.

## Defense in-depth
TBD

 - Next: [Frontend security examples](./03-frontend-security-examples.md)
 - Previous: [Frontend security risk](./01-frontend-security-risk.md) 
 - or back to [main table of contents](../README.md#table-of-contents)
