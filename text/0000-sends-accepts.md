- Start Date: 2015-12-3
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

This proposes adding `sends` and `accepts` attributes to the `Category` element
and `Transaction` element in the API Description format.

# Motivation

This accommodates the ability to capture what mime types an API or Transaction
will send or accept. This will provide hints to the clients and server
developers into what mime types are supported.

# Detailed design

This is the definition of these two attributes:

- `sends` (array[string]) - Defines what MAY be used in the `Content-Type` header
- `accepts` (array[string]) - Defines what MAY be used in the `Accepts` header

When either of these are not present, these values are determined by those in
the HTTP Request and HTTP Response element. These values do not dictate what
mime types a Transaction MUST use, but rather acts as hints.

These attributes should be added to `Category` and `Transaction` elements.

# Drawbacks

This is adding information that is only for hinting, and may not actually
include example Transactions or implementations. We would need to encourage
users to always provide examples when these attributes are used.

# Alternatives

When supporting API Description formats that use this, we could create
additional transaction for each mime type that does not produce an example.
This would mean that we can not add this and rely on `inferred` elements to
provide additional fake examples.

The downside of this is that we are inferring data and creating bloat.

# Unresolved questions

None at this point.
