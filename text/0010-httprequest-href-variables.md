- Start Date: 2015-11-27
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

This RFC proposes we add a `hrefVariables` attribute to the `httpRequest` and
change `href` to become a `Templated Href` instead of a `Href`.

# Motivation

From the perspective of tools such as testing, mocking, proxy, routing and
validation it may be required that these tools have access to the unexpanded
URI template with variables.

# Detailed design

Currently the `httpRequest` element contains a `href` attribute as follows:

> - `href` (Href) - A concrete URI for the request. The href SHOULD be
>   inherited from a parent transition by expanding the href and
>   hrefVariables if unset.

These proposed changes would change the meaning of the `href` attribute
to become:

> - `href` (Templated Href) - URI Template for this HTTP request. The `href`
>   and `hrefVariables` SHOULD be inherited from a parent transition.
>   When `href` is set, you MAY also set `hrefVariables`.

While introducing a new `hrefVariables` attribute:

> - `hrefVariables` (Href Variables) - Definition of URI Template variables
>   used in the `href` property.

# Drawbacks

This is a backwards incompatible change and thus can break existing
implementations.

# Alternatives

As an alternative, we can keep `httpRequest` element as it is, however tooling
will not be able to make use of the unexpanded `href`.
