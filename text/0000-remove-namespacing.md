- Start Date: 2015-12-03
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

This RFC proposes we remove all namespacing in the Refract base specification
while proposing we use `profile` links in its place.

Note: this is not to be confused with the actual namespace documents we have
put together, such as the API Description or Data Structure namespaces. These
should continue to exist.

# Motivation

Namespacing is currently not used anywhere, and is quite complex in its design.
In removing it, we can move to a more hypermedia-based approach, which is more
flexible and simpler.

# Detailed design

In moving away from using the concept of a namespace, this allows for us to
make the following changes to the base specification.

- Remove `prefix` from the `meta` object
- Remove `namespaces` from the `meta` object
- Refer to a "namespace" as a "profile" instead
- Remove the ability to prefix namespaces
- Remove namespacing from the `Element Pointer` section
- Remove `Namespacing` section in specification

In its place, we will provide instructions for using the `profile` link
relation for defining where the semantic definition for elements MAY be found.
This `profile` link SHOULD conform to [RFC
6906](https://www.ietf.org/rfc/rfc6906.txt).

# Drawbacks

Namespacing provides a very detailed way to extend documents and elements.
While this is very powerful, it is quite complex, and is currently not part of
any implementation we have done. The drawback here then is that we lose this
ability.

# Alternatives

None proposed here.

# Unresolved questions

None at this moment.
