- Start Date: 2015-12-03
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

This proposes we move `extend`, `select`, and `option` from the base
specification to its own profile.

Note that I'm calling this a "profile" versus a "namespace." This is pending
this [RFC](https://github.com/refractproject/rfcs/pull/30). If we do not go the
route proposed there, we can refer to this as a Utility Namespace.

# Motivation

The main motivation is to make the base specification as simple as possible. In
ever implementation we've created for consuming Refract, such as from the Parse
Result or API Description results, we have not needed to use any of these
elements.

In light of simplifying, this keeps the base specification concerned with
primitive, meta elements, and addressability.

# Detailed design

This proposal is to move `extend`, `select`, and `option` to its own
profile/namespace. Once there, the Data Structure namespace would then
reference that specification as a dependency.

# Drawbacks

This removes functionality from the base specification, and therefore limits it
in some way. The original argument was that these elements were important to
have for all other namespaces, but this has proven to not be true.

# Alternatives

The alternative is to of course not implement this RFC.

# Unresolved questions

None at this moment.
