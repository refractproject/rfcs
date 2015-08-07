- Start Date: 2015-08-06
- RFC PR: https://github.com/refractproject/rfcs/pull/8
- Refract Issue: https://github.com/refractproject/refract-spec/pull/40

# Summary

This RFC proposes a backward-incompatible change of the `meta` property `class` to `classes`.

# Motivation

In many programming languages `class` is a reserved keyword. Sometimes it cannot be easily used as an attribute/property name (e.g. Python) and other times it clobbers useful existing information (e.g. Ruby). Changing to `classes` prevents both issues in most languages and also helps to explain that it is a list that can contain any number of class names.

See also: https://github.com/refractproject/refract-spec/issues/37

# Detailed design

The meta property `class` will need to be renamed to `classes` in the base Refract specification. Additionally, the API Description and Parse Result namespaces will need to be updated to reflect this change. All documentation around the property needs to be updated. A new version of the Refract specification should be released, and its changelog should describe the breaking change.

# Drawbacks

This is a backward incompatible change and will require client libraries which implement the refract specification to be updated.

# Alternatives

Language-specific implementers can provide their own workarounds, for example you could provide a `cls` property in Python/Ruby instead of `class`. This may lead to fracturing and could become a maintenance burden over time.

# Unresolved questions

None.
