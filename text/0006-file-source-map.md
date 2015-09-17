- Start Date: 2015-08-24
- RFC PR: https://github.com/refractproject/rfcs/pull/12
- Refract Issue: (leave this empty)

# Summary

Update to Parse Result namespace Source Map element so it MAY carry information
about the original source file.

# Motivation

Information about the original source file is needed in a situation where the
final refract document with source maps is a result of processing multiple
input files.

This covers the situation where the final refract tree is created by parsing
multiple API Blueprint files as described in
[this issue](https://github.com/apiaryio/api-blueprint/issues/8).

This RFC SHOULD be considered before implementing the Parser Result namespace
 as releasing it in its current form may lead into backward incompatible changes
in the future.

# Detailed design

I suggest to remove the following from the current Parser Result namespace
`Source Map` element:

> The Source Map element MAY be used in any other element attributes in its
normal ("unrefracted") form under the `sourceMap` property.

This change alone will allow us to store any additional information about the
source file in element's attributes.

Instead, we should add:

> Every refract element MAY include an `sourceMap` attribute. Its content SHOULD
be an array of `Source Map` elements. The Source Map elements represent the
location(s) in source file(s) from which the element was composed.

For clarity I suggest to add following:

> The Source Map element SHOULD NOT be used it its normal ("unrefracted") form
unless the particular application clearly implies what is the source file the
source map is pointing in.

I would suggest to leave the `content` of the `Source Map` element as is
(array of tuples).

The examples should be updated accordingly:

For example:

```json
{
    "element": "...",
    "attributes": {
        "sourceMap": [
            {
                "element": "sourceMap",
                "attributes": {},
                "content": [[4, 12], [20, 12]]
            }
        ]
    }
}
```

# Drawbacks

n/a

# Alternatives

Alternatively we can leave current `Source Map` element as is and introduce –
once needed – a "Source File" element. That element could be a descendant of
API Description namespace `Asset` element where its `href` will be used to refer
to the file.

For example:

```json
{
    "element": "...",
    "attributes": {
        "sourceFile": {
            "contentType": "text/vnd.apiblueprint+markdown",
            "href": "apiary.apib"
        },
        "sourceMap": [
            [4, 12],
            [20, 12]
        ]
    }
}
```

Note the actual content of the `sourceFile` hash or `Source File` element is
out of the scope of this RFC.

# Unresolved questions

It is still undecided how do we refer to the source file but this does not have
to be solved at this moment. The goal of this RFC is to propose a change so
in adding the information about the source file in future can be done in a
non-breaking way.
