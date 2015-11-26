- Start Date: 2015-11-24
- RFC PR: https://github.com/refractproject/rfcs/pull/23
- Refract Issue:

# Summary

This proposes link relations for use with the [Parse Result Namespace](https://github.com/refractproject/refract-spec/blob/master/namespaces/parse-result-namespace.md). This is dependent on [PR 22](https://github.com/refractproject/rfcs/pull/22).

# Motivation

The motivation for this RFC is to provide custom link relations to be used with parse results to tell the client where things like annotations originated and which elements were inferred.

# Detailed design

This proposal is to add two link relations: the `origin` and `inferred` links.

## Origin Link Relation

The `origin` link relation defines a link to documentation on the originating system from which the parse result was generated. The `origin` link SHOULD be applied to an element and all of its children elements.

An `origin` link is useful for tying a specific element (namely annotations) to some specific functionality. Instead of saying in the parse results that a particular element used a specific function in the code, the `origin` link can link to documentation on how that functionality actually works and why it was used. Additionally, the URL itself can be used by the client to know what functionality was used. This all prevents coupling client and server code.

## Inferred Link Relation

The `inferred` link relation defines a link to documentation on how an element was inferred. The presence of an `inferred` link tells the user that the element was not in the original document, and should be considered as extra information. Conversely, the absence of the link tells the client the element was not inferred.

In addition to expressing the nature of the element, it also provides a link to documentation on why and how the element was inferred. This can be useful to client developers in understanding the reason behind inferring.

# Drawbacks

The drawbacks would be from the RFC for adding hyperlinking to Refract.

# Alternatives

None.

# Unresolved questions

None.
