- Start Date: 2015-12-03
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

This proposes we reserve the keyword `element` for all objects in a Refract
tree.

# Motivation

This allows us to not worry about domain-specific knowledge when parsing a
Refract tree. Right now, we have to rely on something out of band to tell us
when something MAY be refracted, but if we rely on the reserved keyword
`element`, we can know if an object is a normal object or a Refract Object.

Note: we are already doing this in Minim.

# Design

This RFC proposes to reserve `element` in the entire tree. This means that
anywhere the `element` keyword is found, a parser SHOULD treat the object as a
Refract Object.

## Secondary Proposal

This allows for us to know when an object is a Refract Object or not. It also
allows for us only refract things that need to be refracted when serializing.
In this situation, for example, the `key` property of a `Member Element` would
not need to refracted if it is a string.

We can then follow this proposed rule when serializing: if an element is a
primitive element and has no attributes or meta data, the element MAY be left
as a primitive value.

# Drawbacks

This means that no user can ever use the keyword `element`. We could provide
ways to get around this with some identifier, like `_isRefract: false`, but this
just makes it more confusing.

# Alternatives

We can provide a special `meta` property that tells you if something is
Refract or not. This way, we could look for `obj.meta.isRefracted` to know if
it is Refracted. This feels very forced.

So as to not pollute the entire tree with reserving `element` everywhere, we
could only reserve it in `meta` and `attributes`. This creates a special
parsing rule, though, and may provide more headaches than it prevents.


# Unresolved questions

None at the moment.
