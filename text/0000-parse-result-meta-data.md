- Start Date: 2015-11-20
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

This RFC outlines ideas in adding meta data into into elements through the
means of meta links and adding link relations to the Parse Result namespace.

# Motivation

Parsing happens in multiple steps and information is added by different layers
in the stack in some situations. It would be helpful for end users to have meta
data to let the user know where data came from and which information was added
that did not exist in the original representation.

The idea with proposing meta links would be to provide a generic way to link to
out-of-band information to allow the user to explore more information in a
given context.

# Detailed design

The proposal is to add a `links` property to `meta` and propose two link
relations for the Parse Result namespace.

## Links Property in Meta

The property would be defined as the following the `meta` object of all
elements. This would be added in the Refract base spec.

- `links` (array)
    - (object)
        - `rel` - Link relation of the link
        - `href` - Resolvable URL for the link

The `rel` property MAY be any defined [link
relation](http://www.iana.org/assignments/link-relations/link-relations.xhtml)
or a resolvable URL to documentation on the link relation.

## Parse Result Link Relations

### `inferred`

The `inferred` link relation defines a link to documentation on how an element
was inferred. The presence of an `inferred` link tells the user that the
element was not in the original document, and should be considered as extra
information.

### `origin`

The `origin` link relation defines a link to documentation on the originating
system from which the parse result was generated. The `origin` link SHOULD be
applied to an element and all of its children elements.

# Drawbacks

* Generic way to solve this problem may be trying to think too much into this.
* This changes the base spec (alternative solution to change Parse Result
Namespace instead)

# Alternatives

To satisfy the requirements for the Parse Result namespace, we could propose a
simple `inferred` class that any element could use to tell the user the element
was inferred. While this works in the short term, it does not provide a way to
point the user to documentation about why or how something was inferred.

Additionally, if it is not desired to add `links` to the base spec of Refract,
the `links` property MAY be added to the attributes for all elements in the
Parse Result Namespace.

Lastly, we could add an `inferred` property to the `attributes` of all elements
in the Parse Result Namespace.

# Unresolved questions

* Whether this should be added to the base spec or Parse Result Namespace
* Whether to use hyperlinks or simple properties.
