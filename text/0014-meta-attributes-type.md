- Start Date: 2017-03-27
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Meta/Attributes Value Type

## Summary

Currently meta and attributes value may be either an object or an array of
member values. This PR suggestions forcing the value to be a specific type to
simplify Refract and any implementations.

## Motivation

There are multiple forms of values supported in meta/attributes and this means
that any implementations MUST support every form which leads to additional
complexity. In experiences with current Refract implementations, some forms are
not supported and this subsequently ties tooling to specific serialisations of
Refract which can lead to fragile implementations that MAY break when a
serialisation rule is changed such as if a meta or attribute key would include
a meta or attribute itself.

At the time of writing this RFC, there are no Refract name-spaces that make use
of storing meta or attributes on a meta or attribute member or key. Therefore
it does not make sense to continue supporting this given it increases the
complexity of Refract.

The outcome of these changes would simplify the Refract specification, and any
implementations to reduce complexity when handling meta and attributes.

## Detailed design

All meta and attributes MUST be treated as hashes where the key is a string and
the value is a Refract element. The value of meta or attributes MUST no longer
be an array of member elements.

## Drawbacks

It will not be possible for elements declared in name spaces to allow
meta/attributes to be stored on a member or member key. This would not effect
any existing name-spaces however it may have impact in the future.

Although this may impose a limitation, it is clearer to consumers of Refract.

## Alternatives

An alternative design was considered in
https://github.com/refractproject/rfcs/pull/35 where we would use an array of
member elements, however it would increase the complexity and at given time
there would be no use to store meta or attributes in this way.
