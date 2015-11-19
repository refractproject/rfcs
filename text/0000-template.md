- Start Date: 2015-11-18
- RFC PR:
- Refract Issue:

# Summary

Provide media types for each namespace.

# Motivation

Users of the namespaces should all use the same media types when exchanging documents so that it can be adequately conveyed what namespace is being used. If a generic media type is used for all Refract, the document should convey the namespace used within the document. Using a namespace-specific media type provides a way to convey that outside of the document.

# Detailed design

The following media types are proposed for each respective namespace.

- [API Description Namespace](https://github.com/refractproject/refract-spec/blob/master/namespaces/api-description-namespace.md) - `application/vnd.refract.api-description`
- [Data Structure](https://github.com/refractproject/refract-spec/blob/master/namespaces/data-structure-namespace.md) - `application/vnd.refract.data-structure`
- [Parse Result](https://github.com/refractproject/refract-spec/blob/master/namespaces/parse-result-namespace.md) - `application/vnd.refract.parse-result`

In each case, the format used MUST be added as a suffix. For example, when exchanging the JSON format of a parse result representation, you would use:

```
application/vnd.refract.parse-result+json
```

All suffixes MUST conform to the [structured syntax registry](http://www.iana.org/assignments/media-type-structured-suffix/media-type-structured-suffix.xhtml). YAML formats MUST use `+yaml`.

The full refract version MUST be used with all representations prefixed with `application/vnd.refract`.

Additionally, we SHOULD register all media types we use with the [IANA media type registry](http://www.iana.org/assignments/media-types/media-types.xhtml).

# Drawbacks

The only drawback would be media type explosion.

# Alternatives

As said, we can convey inside the document the namespace(s) used and use a Refract-generic media type.

# Unresolved questions

None.
