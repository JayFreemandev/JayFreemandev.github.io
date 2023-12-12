---
layout  : wiki
title   : Best practice of HTTP API architecture
date    : 2023-10-24 20:44:40 +0900
updated : 2023-10-24 20:44:40 +0900
resource: A7/953B01-621E-4081-B40C-2BCDA2ECBBC3
toc     : true
public  : true
parent  : [[2023]]
latex   : true
---
* TOC
  {:toc}
  Carpenters At Work Building Two Houses is a photograph by Everett which was uploaded on December 5th, 2011.

I referred to the Heroku HTTP API Design Guide.

### HTTP Design

**Background and Requirements**

- **Architecture familiar to the client side**, or **Learning curve should be manageable**.
- There should be no room for delays in the development schedule.

**Selections**

- HTTP API
- REST API
- GraphQL

GraphQL must consider the running curve and it is really difficult to satisfy REST's 'self-descriptive' and 'HATEOAS' principles to keep the complete REST API.

### Serialization Format

- XML
- JSON
- YAML

Let's use JSON

Although representing the same data, JSON is **better lighter** and **readable** is also good.

The tree structure of 'XML' was judged to be **not an effective format for expressing resources**.(Difficult to express Array)

'YAML' is not commonly used as a serialization format.** The speed of de-serialization is slow, and there is no particular advantage of using YAML.

'JSON' stands for **JavaScript Object Notation**. There is no structure **as comfortable as JSON for front-end users who will be logic-processing with JavaScript or their brothers (such as TypeScript), and most front-end engineers, including mobile apps and the web, are already familiar with JSON.**

### Simple description of JSON by [Koray Tugay](https://stackoverflow.com/questions/383692/what-is-json-and-what-is-it-used-for/383699#383699)
**What is JSON? – How I explained it to my wife**

**Me:** “It’s basically a way of communicating with someone in writing....but with very specific rules.

**Wife:** yeah....?

**Me:** In prosaic English, the rules are pretty loose: just like with cage fighting. Not so with JSON. There are many ways of describing something:

- Example 1: Our family has 4 people: You, me and 2 kids.
- Example 2: Our family: you, me, kid1 and kid2.
- Example 3: Family: [ you, me, kid1, kid2]
- Example 4: we got 4 people in our family: mum, dad, kid1 and kid2.

**Wife:** Why don’t they just use plain English instead?

**Me:** They would, but remember we’re dealing with computers. A computer is stupid and is not going to be able to understand sentences. So we gotta be really specific when computers are involved otherwise they get confused. Furthermore, JSON is a fairly efficient way of communicating, so most of the irrelevant stuff is cut out, which is pretty hand. If you wanted to communicate our family, to a computer, one way you could do so is like this:

```
{
    "Family": ["Me", "Wife", "Kid1", "Kid2"]
}

```

……and that is basically JSON. But remember, you MUST obey the JSON grammar rules. If you break those rules, then a computer simply will not understand (i.e. parse) what you are writing.

**Wife:** So how do I write in Json?

A good way would be to use a json serialiser - which is a library which does the heavy lifting for you.

**Summary**

> JSON is basically a way of communicating data to someone, with very, very specific rules. Using Key Value Pairs and Arrays. This is the concept explained, at this point it is worth reading the specific rules above.
>

### Check List
- [Return appropriate status codes](https://github.com/yoondo/http-api-design#return-appropriate-status-codes)
- [Provide full resources where available](https://github.com/yoondo/http-api-design#provide-full-resources-where-available)
- [Accept serialized JSON in request bodies](https://github.com/yoondo/http-api-design#accept-serialized-json-in-request-bodies)
- [Provide resource (UU)IDs](https://github.com/yoondo/http-api-design#provide-resource-uuids)
- [Provide standard timestamps](https://github.com/yoondo/http-api-design#provide-standard-timestamps)
- [Use UTC times formatted in ISO8601](https://github.com/yoondo/http-api-design#use-utc-times-formatted-in-iso8601)
- [Use consistent path formats](https://github.com/yoondo/http-api-design#use-consistent-path-formats)
- [Downcase paths and attributes](https://github.com/yoondo/http-api-design#downcase-paths-and-attributes)
- [Nest foreign key relations](https://github.com/yoondo/http-api-design#nest-foreign-key-relations)
- [Support non-id dereferencing for convenience](https://github.com/yoondo/http-api-design#support-non-id-dereferencing-for-convenience)
- [Generate structured errors](https://github.com/yoondo/http-api-design#generate-structured-errors)
- [Support caching with Etags](https://github.com/yoondo/http-api-design#support-caching-with-etags)
- [Trace requests with Request-Ids](https://github.com/yoondo/http-api-design#trace-requests-with-request-ids)
- [Paginate with ranges](https://github.com/yoondo/http-api-design#paginate-with-ranges)
- [Show rate limit status](https://github.com/yoondo/http-api-design#show-rate-limit-status)
- [Version with Accepts header](https://github.com/yoondo/http-api-design#version-with-accepts-header)
- [Provide machine-readable JSON schema](https://github.com/yoondo/http-api-design#provide-machine-readable-json-schema)
- [Provide human-readable docs](https://github.com/yoondo/http-api-design#provide-human-readable-docs)
- [Provide executable examples](https://github.com/yoondo/http-api-design#provide-executable-examples)
- [Describe stability](https://github.com/yoondo/http-api-design#describe-stability)
- [Require TLS](https://github.com/yoondo/http-api-design#require-tls)
- [Pretty-print JSON by default](https://github.com/yoondo/http-api-design#pretty-print-json-by-default)


**reference**  
https://stackoverflow.com/questions/383692/what-is-json-and-what-is-it-used-for/383699#383699